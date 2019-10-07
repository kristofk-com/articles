---
layout: article
title: Inline Documentation & Markdown in Xcode
tags: SwiftDevelopment
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1566802185/kristofk-com/posts/2018-01-13-swift-xcode-documentation/inline-doc-and-markdown-thumbanil.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1566802185/kristofk-com/posts/2018-01-13-swift-xcode-documentation/inline-doc-and-markdown-thumbanil.png
---

A clear, consistent and well-structured code is what signifies that you are dealing with a professional iOS Developer. Although comments in the code are ill-advised these special ones that I’m going to discuss here are quite the opposite. I’m going to write about inline documentation which can be especially useful if you are working on a library or framework but you can also use it in your personal project. The other type of comment that I’m going to discuss is the indicator comment that is highlighted in your code, these can give you subtitles in your code and they can also mark bugs and tasks inside your code. Use these wisely.

<div>{%- include extensions/youtube.html id='EaZypbkWIBY' -%}</div>

# Indicator comments

Back in the Obj-C days, this was #pragma but now in Swift, there are 3 distinct types.

1.  `// MARK: <text>`  
    MARK is good for marking sections in your code. With MARK you can give subtitles to different sections of your code. MARK is often used in with a dash (`// MARK: - <text>`) so that it creates a horizontal line too.
2.  `// TODO: <text>`  
    TODO is very similar to MARK, they have a very similar icon too. The only difference is the keyword and what you use it for. Obviously, you should use TODO to keep a reminder for yourself to implement something later. This is used a lot for error handling. You can use the dash (`// TODO: - <text>`) here as well for the same effect.
3.  `// FIXME: <text>`  
    FIXME has a yellow icon so that it stands out. If your code isn’t compiling then there is obviously no use for this but in case you notice that your code fails sometimes at a certain point or maybe the algorithm you are using isn’t as optimal as you taught then you can use this. You can use the dash (`// FIXME: - <text>`) here as well for the same effect yet again.

    // MARK: This is the standard marking
    // MARK: - This is mark with a line

    // TODO: This is the standard TODO
    // TODO: - This is TODO with a line

    // FIXME: This is the standard FIXME
    // FIXME: - This si FIXME witha a line

![File Navigator](https://res.cloudinary.com/kristofk-com/image/upload/v1566802184/kristofk-com/posts/2018-01-13-swift-xcode-documentation/mark-todo-fixme-min.png)

# Inline Documentation & Markdown

Xcode has a feature that allows you to create inline documentation for your functions and types. The syntax has changed a lot from Obj-C so you could say that it is a completely new system.

## Declaration

Let’s start with the very basics. In Xcode, if you want to create a comment you either use`//` or `/*` ->`*/`. And if you want to create inline documentation then you need to add an extra`/` or`*` respectively like so: `///` and `/**` ->`*/`.

## Markdown Syntax

Inline documentation in Xcode uses standard markdown with some extra “Swift touch”.

### Text Types

You can create headings in Xcode by using hashtags (#). The number of hashtags you place in front of a line determines the level of the subheading (# = Heading 1, ## = Heading 2…).

You can use bold and italic characters in the text. You indicate italic like so: _*italic*_ and bold like so: ****bold****.

    /**

    # This is H1

    ## This is H2

    ## This is H3

    This is what *italic* and **bold** looks like.

    */

![Doc Window](https://res.cloudinary.com/kristofk-com/image/upload/v1566802184/kristofk-com/posts/2018-01-13-swift-xcode-documentation/text-types-cut-min.png)

### Lists

If you want to create an **Unordered List** than you can use either one of these characters: **–** / ***** / **+**. There is no need for tabs or spaces anywhere but between the symbol and the item itself.

For Ordered Lists, you will have to use Arabic numbers with a dot at the end (**1\.** / **2.**). The same spacing rule applies here as before.

If you want to create a gap between items in the list then you can change to list symbol (e.g. if you use * for each item then you switch to + and you will get a gap).

You can also create **sublists** by creating an indent (tab) in front of the item.

    /**

    Unordered list with a sublist and a gap:
    * Item 1
    * Item 2
    	* Item 2.2
    * Item 3
    + Item 4 with a gap

    Ordered List with a sublist:
    1\. Item 1
    2\. Item 3
    	1\. Item 3.1
    	2\. Item 3.2

    */

![Doc Window](https://res.cloudinary.com/kristofk-com/image/upload/v1566802385/kristofk-com/posts/2018-01-13-swift-xcode-documentation/lists-cut-min.png)

### Links

You can place links in your documentation. This is useful if you want to place references to documentation or maybe a link to the feature description within your company. **The syntax looks like this:`[title](http://kritsofk.com/)`**

    /**

    You can read more about Inline Documentation and Markdown on [NSHipster](http://nshipster.com/swift-documentation/) and [Apple's Documentation](https://developer.apple.com/library/content/documentation/Xcode/Reference/xcode_markup_formatting_ref/index.html#//apple_ref/doc/uid/TP40016497-CH2-SW1).

    */

![Doc Window](https://res.cloudinary.com/kristofk-com/image/upload/v1566802184/kristofk-com/posts/2018-01-13-swift-xcode-documentation/links-cut-min.png)

### Assets

You can, in theory, add images from the web to your documentation but I could not get this function to work. Regardless copied the example from Apple’s Documentation. **The syntax is as follows**:**`![title](link <optional: hover text>)`**

    /**

    An example of using *images* to display a web image

	    ![Xcode icon](http://devimages.apple.com.edgekey.net/assets/elements/icons/128x128/xcode.png "Some hover text")

    */

### Func specific Features

There are some features in the inline documentation that is specific to functions. This includes the description of the parameters, returns and the thrown errors. You can only implement these if your function actually includes theme so for example, if your function doesn’t return anything then you can’t create descriptions for the parameters. The syntaxes are the following:

*   For the parameters, you can write `- parameters:` and then with a sublist you can specify each one
*   Return value can have a description with `- returns:`
*   Thrown errors can be specified with `- throws:`

    /**

    This is an example function to show off **parameters**, **returns** and **throws**.

    - parameters:
    	- str: This is the string that is going to be printed.
    	- num: This is how many times the string is going to be printed.

    - throws: This function would throw someError but the code never reatcher that point.

    - returns: A Bool is returned that is always true for no real reason.

    */

![Doc Window](https://res.cloudinary.com/kristofk-com/image/upload/v1566802184/kristofk-com/posts/2018-01-13-swift-xcode-documentation/func-specific-features-cut-min.png)

### Code

You can indicate single line codes and even shorter, few word code snippets and even whole code blocks. This can be especially useful if you want to highlight some functionality or if you want to give an example for the implementation.

The syntax:

*   single line code / snippet: `
*   code block: “` before and after the code block

For the example, I have extended the previous one.

    /**

    This is an example function to show off **parameters**, **returns** and **throws**.

    - parameters:
    	- str: This is the string that is going to be printed.
    	- num: This is how many times the string is going to be printed.

    - throws: This function would throw someError but the code never reatcher that point.

    - returns: A Bool is returned that is always true for no real reason.

    * note: Since this function can throw you must implement some error handling. The following example is going to use `try?` and then it is going to capture the returned value.
    ```
    let aBool = try? printExample(str: "Hello, World!", num: 1)
    ```
    */

![Doc Window](https://res.cloudinary.com/kristofk-com/image/upload/v1566802184/kristofk-com/posts/2018-01-13-swift-xcode-documentation/code-cut-min.png)

### Other

There some other features in the Documentation that didn’t deserve its own section but they’ll receive an honourable mention:

*   Escape character  
    If you have some special character that you want to display put a backslash (`\`) in front of it. This character can also be used at the end of the line for a line break.
*   Callouts  
    There are some special keywords like`note` that I used in my previous example that will get highlighted. Some of these keywords are:`Author`,`Todo`,`Bug`…
*   Horizontal line  
    You can draw a horizontal line with the following character string: `***` or`---`.

* * *

**Further reading**

An older but still relevant article on the same topic: [Swift Documentation – NSHipster](http://nshipster.com/swift-documentation/)

Apple’s Official Documentation on the topic: [Apple Doc](https://developer.apple.com/library/content/documentation/Xcode/Reference/xcode_markup_formatting_ref/index.html#//apple_ref/doc/uid/TP40016497-CH2-SW1)

Next up, learn how to share your nicely documented code with others by learning about how to use [Xcode and GitHub](https://kristofk.com/posts/xcode-9-github).
