---
layout: page
title: Markdown
---

# Examples
```
It's very easy to make some words **bold** and other words *italic* with Markdown. You can even [link to Google!](http://google.com)
```
It's very easy to make some words **bold** and other words *italic* with Markdown. You can even [link to Google!](http://google.com)

# Syntax guide

## Headers
```
# This is an <h1> tag
## This is an <h2> tag
###### This is an <h6> tag
```

## Emphasis
```
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** combine them_
```

## Lists
```
Unordered
* Item 1
* Item 2
   * Item 2a
   * Item 2b
Ordered
1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b
```

## Images
```
![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)
```


## Links

```
http://github.com - automatic!
[GitHub](http://github.com)
```

## Blockquotes
```
As Kanye West said:

> We're living the future so
> the present is our past.
```

## Inline code
I think you should use an
`<addr>` element here instead.

## Footnote

Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here's one with multiple blocks.

    Subsequent paragraphs are indented to show that they
belong to the previous footnote.


Here is an inline note.^[Inlines notes are easier to write, since
you don't have to pick an identifier and move down to type the
note.]

[Footnote Syntax](http://pandoc.org/README.html#footnotes)

# Advantage

## KaTeX

Use the `katex` liquid tag for LaTeX math equations like so:

```
{ % katex % }
\Gamma(z) = \int_0^1\infty t^{z-1}e^{-t}dt\,.
{ % endkatex % }
```

{% katex %}
\Gamma(z) = \int_0^1\infty t^{z-1}e^{-t}dt\,.
{% endkatex %}

If you want the equation to be rendered in display mode (on its own line, centered, large symbols), just pass in the `display` parameter:

```
{ % katex display % }
\Gamma(z) = \int_0^1\infty t^{z-1}e^{-t}dt\,.
{ % endkatex % }
```

### More KaTeX examples
```
{ % katex % }
c = \pm\sqrt{a^2 + b^2}
{ % endkatex % }
```

{% katex %}
c = \pm\sqrt{a^2 + b^2}
{% endkatex %}

```
{ % katex display % }
c = \pm\sqrt{a^2 + b^2}
{ % endkatex % }
```

{% katex display %}
c = \pm\sqrt{a^2 + b^2}
{% endkatex %}


## UML diagram
```
```mermaid
sequenceDiagram
Alice ->> Bob: Hello Bob, how are you?
Bob-->>John: How about you John?
Bob--x Alice: I am good thanks!
Bob-x John: I am good thanks!
Note right of John: Bob thinks a long<br/>long time, so long<br/>that the text does<br/>not fit on a row.

Bob-->Alice: Checking with John...
Alice->John: Yes... John, how are you?
`` `
```

```mermaid
sequenceDiagram
Alice ->> Bob: Hello Bob, how are you?
Bob-->>John: How about you John?
Bob--x Alice: I am good thanks!
Bob-x John: I am good thanks!
Note right of John: Bob thinks a long<br/>long time, so long<br/>that the text does<br/>not fit on a row.

Bob-->Alice: Checking with John...
Alice->John: Yes... John, how are you?
```


## Flow chart

```
```mermaid
graph LR
A[Square Rect] -- Link text --> B((Circle))
A --> C(Round Rect)
B --> D{Rhombus}
C --> D
`` `
```


```mermaid
graph LR
A[Square Rect] -- Link text --> B((Circle))
A --> C(Round Rect)
B --> D{Rhombus}
C --> D
```

# GitHub Flavored Markdown
GitHub.com uses its own version of the Markdown syntax that provides an additional set of useful features, many of which make it easier to work with content on GitHub.com.

Note that some features of GitHub Flavored Markdown are only available in the descriptions and comments of Issues and Pull Requests. These include @mentions as well as references to SHA-1 hashes, Issues, and Pull Requests. Task Lists are also available in Gist comments and in Gist Markdown files.

## Syntax highlighting
Here’s an example of how you can use syntax highlighting with GitHub Flavored Markdown:
```
```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
`` `
```


You can also simply indent your code by four spaces:
```
    function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }
```

Here’s an example of Python code without syntax highlighting:

```
def foo():
    if not bar:
        return True
```


## Task Lists
```
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item
```


If you include a task list in the first comment of an Issue, you will get a handy progress indicator in your issue list. It also works in Pull Requests!

## Tables
You can create tables by assembling a list of words and dividing them with hyphens - (for the first row), and then separating each column with a pipe |:
```
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

## SHA references
Any reference to a commit’s SHA-1 hash will be automatically converted into a link to that commit on GitHub.
```
16c999e8c71134401a78d4d46435517b2271d6ac
mojombo@16c999e8c71134401a78d4d46435517b2271d6ac
mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac
```

## Issue references within a repository
Any number that refers to an Issue or Pull Request will be automatically converted into a link.
```
#1
mojombo#1
mojombo/github-flavored-markdown#1
```

## Username @mentions
Typing an `@` symbol, followed by a username, will notify that person to come and view the comment. This is called an `@mention`, because you’re mentioning the individual. You can also @mention teams within an organization.

## Automatic linking for URLs
Any URL (like http://www.github.com/) will be automatically converted into a clickable link.

## Strikethrough
Any word wrapped with two tildes (like `~~this~~` ~~this~~) will appear crossed out.

## Emoji
To see a list of every image we support, check out the [Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/).

# Resources
* https://mdp.tylingsoft.com/#fnref1
* https://support.typora.io/Draw-Diagrams-With-Markdown/
* http://flowchart.js.org/
---
