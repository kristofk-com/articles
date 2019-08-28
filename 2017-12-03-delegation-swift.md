---
layout: article
title: Delegation in Swift
tags: SwiftDevelopment
---

This post is a beginners guide to delegation in Swift. I’ll be showing off why is delegation useful, where can it be used and how to use it.

Delegation is a very common pattern in swift used by almost everything. The idea is that objects can delegate or give away some of their tasks to other objects. This allows loose coupling between objects which leads to a more generic and flexible code base.

Delegation might be hard to grasp at the beginning but it doesn’t introduce any crazy new logic, just a creative way to use theme hence it is a design pattern.

In this post, I’ll be using a dice game as an example to custom delegation. The rules of the dice game are as follows:

*   The number of rounds and players are specified before the game
*   Every round each player rolls one dice once
*   After every round, there is a round-winner
*   After the game (past all rounds) for each player, a total is calculated based on their throws in the rounds
*   After the game based on the totals, a game winner is named

## Setting up the game class

### Init

Now, with all that out of the way, let’s start coding the bases of the game. There is going to be a DiceGame class that is going to be the basis of everything. In this Dice game class we are going to declare some stored properties:

*   the number of rounds in the game
*   the players
*   player rolls to store the rolls from each round for all the players
*   results for the total of each player at the end of the game

Then we need to create an init method for the class. The arguments for this method are the number of rounds and the players. So far the code should look something like this:

```
class DiceGame {
	let numOfRound: Int
	var players: [String]
	var playerRolls = [String: [Int]]()
	var results = [String: Int]()

	init(numOfRound: Int, players: String {
		self.numOfRounds = numOfRounds
		self.players = players
	}
}
```

Next up we need to define the stages of the game. These are going to be functions. There is a function for the setup, game start, roll and the end of the game.

### Setup

The setup is going to shuffle the players so that we cannot define who will start throwing and then the dictionaries will be set up.

In order for this function to work tough especially the shuffling part, we need to add some extensions to the project, these extensions are as follows.

```
extension MutableCollection {
    /// Shuffles the contents of this collection.
    mutating func shuffle() {
        let c = count
        guard c > 1 else { return }

        for (firstUnshuffled, unshuffledCount) in zip(indices, stride(from: c, to: 1, by: -1)) {
            let d: IndexDistance = numericCast(arc4random_uniform(numericCast(unshuffledCount)))
            let i = index(firstUnshuffled, offsetBy: d)
            swapAt(firstUnshuffled, i)
        }
    }
}

extension Sequence {
    /// Returns an array with the contents of this sequence, shuffled.
    func shuffled() -> [Element] {
        var result = Array(self)
        result.shuffle()
        return result
    }
}
```

Now we have the shuffle function available and we are ready to create the setup function.

```
func setup() {
	players.shuffle()
	for player in players {
		playerRolls.updateValue([], forKey: player)
	}
}
```

### Rolling the dice

Let’s create a function for rolling the dice for a player. This will take the player as an argument and it will add the result of the roll to the playerRolls dictionary. The function is also going to return the rolled result so that we can access it outside the function.

```
func rollFor(_ player: String) -> Int {
	let roll = Int(arc4random_uniform(6)) + 1
	playerRolls[player]?.append(roll)
	return Int
}
```

### Ending the game

This function is going to be called after all the rounds have passed and the game is ready to conclude. We are going to print out the result of each round and we are going to calculate the sum of the throws for each player and assign the results to results.

```
func gameEnd() {
	print(playerRolls)
	var results = [String: Int]()
	for player in players {
		var rollSum = 0
		for roll in playerRolls[player]! {
			rollSum += roll
		}
		results.updateValue(rollSum, forKey: player)
	}
	print(results)
}
```

### Game start

This function is going to be called to start the game and to manage it until the end. By the time this function has concluded the results are going to be in already. This function is going to call the setup and gameEnd function and it is going to roll the dice each turn.

```
func gameEnd() {
	print(playerRolls)
	var results = [String: Int]()
	for player in players {
		var rollSum = 0
		for roll in playerRolls[player]! {
			rollSum += roll
		}
		results.updateValue(rollSum, forKey: player)
	}
	print(results)
}
```

Alright so now we have the base game ready. Now if we create an array of names, create an instance of the DiceGame class and we call the startGame function we should have the game start and finish and then print out the results of the turns and then the final result.

```
let players = ["Jack", "Chris", "Paul", "Eve"]
let game = DiceGame(numOfRounds: 3, players: players)
game.startGame()

// Printouts:
// ["Jack": [3, 2, 1], "Paul": [6, 6, 3], "Chris": [1, 4, 4], "Eve": [5, 2, 6]]
// ["Jack": 6, "Paul": 15, "Chris": 9, "Eve": 13]
```

## Setting up a manager

So now what if we want to listen in to what is happening inside this class? Well, of course, we can track the happenings by inserting print statements and whatever we would like. That would look like this:

```
func setup() {
      players.shuffle()
	print("Player order: ", separator: "", terminator: "")

      for player in players {
		print(player, separator: "", terminator: " ")
          playerRolls.updateValue([], forKey: player)
      }
	print()
  }

  func startGame() {
      setup()
      for round in 1...numOfRounds {
		print("ROUND \(round)")
          for player in players {
			let roll = rollFor(player)
			print("\t\(player) rolled \(roll)")
          }
      }
      gameEnd()
  }
```

Now, this is pretty bad. This looks like caveman debugging. If you want to change the print statement you have to go back to the class, look for the function and then edit the print statement. Not to mention, that if this was part of a [framework or library](https://old.kristofk.com//xcode-9-playground-frameworks/) then the poor fellow using the framework would have to go into your code to edit the printouts.  
One more drawback of this approach is that now is that no other objects have access to this data. What if you want to stream the game. Then you need to write the streaming class inside this one or call the streaming methods next to the print statements. Just for fun lets suppose that you have an antiCheating class that would also have to be called each time.  
As you can see this might get out of control real quick.

## Setting up a delegation

### Intersections

Alright, but what else could I do? Well, I’m glad you asked. This is where delegation comes into play. Let’s define intersections so to say where multiple objects may want to get information from within the Dice game class.  
These intersections would be the following:

```
init(numOfRounds: Int, players: [String]) {
      self.numOfRounds = numOfRounds
      self.players = players
	// PROVIDE THE NUMBER OF ROUNDS IN THE GAME AND THE PLAYERS
  }

  func setup() {
      players.shuffle()
	// PROVIDE THE SHUFFLED NAME ORDER
      for player in players {
          playerRolls.updateValue([], forKey: player)
      }
	print()
  }

  func startGame() {
      setup()
      for round in 1...numOfRounds {
          for player in players {
			let roll = rollFor(player)
			// PROVIDE THE ROLL FOR PLAYER IN A SPECIFIC ROUND
          }
      }
      gameEnd()
  }

func rollFor(_ player: String) -> Int {
	let roll = Int(arc4random_uniform(6)) + 1
	playerRolls[player]?.append(roll)
	return roll
}

  func gameEnd() {
      print(playerRolls)
      var results = [String: Int]()
      for player in players {
          var rollSum = 0
		for roll in playerRolls[player]! {
              rollSum += roll
          }
		results.updateValue(rollSum, forKey: player)
      }
	//PROVIDE THE ROLLS FROM EACH ROUND AND THE FINAL RESULT
	print(results)
  }
```

### Protocol

Now that we know what information we want to share and from where we can define a protocol with all the functions. This protocol can be taught of as the list of information accessible from outside of the class. The API Design Guidelines say that these protocols for delegates should include the “Delegate” keyword at the end.  
So the protocol for this class would look something like this:

```
protocol DiceGameDelegate {
	func gameStartWith(_ players: [String], _ rounds: Int)
	func setupWith(order: [String])
	func roll(_ rollResult: Int, for player: String, in round: Int)
	func gameConclusionWithResults(final: [String: Int], rounds: [String: [Int]])
}
```

These all the functions that the DiceGame class can execute for sure. So the delegate of the DiceGame class will have to conform to this protocol.

### Implementing the calls in the main class

Now we need to implement this protocol’s functions inside the DiceGame class. To do that we need to create a variable for delegate. This variable is an optional one so that if no delegate is defined that the function call is going to fail gracefully.  
Next up, let’s implement the functions from the delegate protocol to the places defined previously.

```
var delegate: DiceGameDelegate?

  init(numOfRounds: Int, players: [String]) {
      self.numOfRounds = numOfRounds
      self.players = players
	delegate?.gameStartWith(players, numOfRounds) // PROVIDE THE NUMBER OF ROUNDS IN THE GAME AND THE PLAYERS
  }

  func setup() {
      players.shuffle()
	delegate?.setupWith(order: players) // PROVIDE THE SHUFFLED NAME ORDER
      for player in players {
          playerRolls.updateValue([], forKey: player)
      }
  }

  func startGame() {
      setup()
      for round in 1...numOfRounds {
          for player in players {
			let roll = rollFor(player)
			delegate?.roll(roll, for: player, in: round) // PROVIDE THE ROLL FOR PLAYER IN A SPECIFIC ROUND
          }
      }
      gameEnd()
  }

func rollFor(_ player: String) -> Int {
	let roll = Int(arc4random_uniform(6)) + 1
	playerRolls[player]?.append(roll)
	return roll
}

  func gameEnd() {
      print(playerRolls)
      var results = [String: Int]()
      for player in players {
          var rollSum = 0
		for roll in playerRolls[player]! {
              rollSum += roll
          }
		results.updateValue(rollSum, forKey: player)
      }
	delegate?.gameConclusionWithResults(final: results, rounds: playerRolls) //PROVIDE THE ROLLS FROM EACH ROUND AND THE FINAL RESULT
	print(results)
  }
```

Alright so now with all the functions in their proper places we are ready to set up the class that will act as the delegate for the DiceGame class.

### Setting up the manager

With this class, we need to conform to the DiceGameProtocol and inside each function add our custom functionality.

```
class DiceGameManager: DiceGameDelegate {
	func gameStartWith(_ players: [String], _ rounds: Int) {
		print("This game has \(rounds) rounds and the players are:", separator: "", terminator: "")
		for player in players {
			print(player, separator: "", terminator: " ")
		}
		print()
	}

	func setupWith(order: [String]) {
		print("The order of the players is: ", separator: "", terminator: "")
		for player in players {
			print(player, separator: "", terminator: " ")
		}
		print()
	}

	func roll(_ rollResult: Int, for player: String, in round: Int) {
		print("In round \(round), \(player) rolled: \(rollResult)")
	}

	func gameConclusionWithResults(final: [String : Int], rounds: [String : [Int]]) {
		print("RESULT")
		for (key, value) in final {
			print("\(key) - \(value)")
		}
	}
}
```

The last thing needed is to establish the connection between the Manager and the Class.

```
let players = ["Jack", "Chris", "Paul", "Eve"]
let game = DiceGame(numOfRounds: 3, players: players)
game.delegate = DiceGameManager()
game.startGame()
```

And now we are finished! Now when the game runs the readout should be something like this:

```
The order of the players is: Jack Chris Paul Eve
In round 1, Paul rolled: 6
In round 1, Eve rolled: 4
In round 1, Jack rolled: 1
In round 1, Chris rolled: 5
In round 2, Paul rolled: 5
In round 2, Eve rolled: 6
In round 2, Jack rolled: 6
In round 2, Chris rolled: 6
In round 3, Paul rolled: 3
In round 3, Eve rolled: 4
In round 3, Jack rolled: 2
In round 3, Chris rolled: 5
["Jack": [1, 6, 2], "Paul": [6, 5, 3], "Chris": [5, 6, 5], "Eve": [4, 6, 4]]
RESULT
Jack - 9
Paul - 14
Chris - 16
Eve - 14
["Jack": 9, "Paul": 14, "Chris": 16, "Eve": 14]
```

Of course, I could do some cleaning so that the text is even prettier but I think this is just fine for this demonstration.

* * *

I hope this post offered some value to you. Feel free to leave your comments, suggestion and questions in the comments.
