# Warren's Notes for Sublime Text Power User (Online Course / Book)
v.20171220\
https://courses.wesbos.com/

---
## Table of Contents
* [Module 01: Sublime Text Settings]()
* [Module 02: Bookmarking]()
* [Module 03: The Command Palette]()
* [Module 04: Mastering Goto Anything]()
* [Module 05: Predictive Filename Typing]()
* [Module 06: Code Folding]()
* [Module 07: Creating and Using Snippets]()
* [Module 08: Moving, Jumping, Selecting and Inserting]()
* [Module 09: Finding, Selecting and Replacing]()
* [Module 10: Emmet - HTML]()
* [Module 11: Emmet - Tag Wrapping]()
* [Module 12: Emmet - CSS]()
* [Module 13: Emmet - Value Bumping]()
* [Module 14: Emmet - Filters]()
* [Module 15: Line Bubbling or Swapping]()
* [Module 16: Introduction to Panes and Groups]()
* [Module 17: Mastering Panes and Groups with Origami]()
* [Module 18: Working with Multiple Carets]()
* [Module 19: JavaScript Code Quality with JSHint]()
* [Module 20: Lint Any Language with Sublime Linter]()
---

## Module 01: Sublime Text Settings
* Review Sublime Setttings and override them below
* Sublime User Settings found here: `C:\Users\<username>\AppData\Roaming\Sublime Text 3\Packages\User\Preferences.sublime-settings`
* There are specific language settings files, e.g. `C:\Users\<username>\AppData\Roaming\Sublime Text 3\Packages\User\Markdown.sublime-settings`

## Module 02: Bookmarking
* `CTRL + F2` to set a bookmark, `F2` and `SHIFT+F2` to traverse bookmarks
* To select all bookmarks, use the `Goto` menu
* `CTRL + SHIFT + F2` clears all bookmarks

## Module 03: The Command Palette
* `CTRL + SHIFT + P` to open
* To set syntax colors: type `ssx`
* Can set up Build tasks
* `file` to delete/rename

## Module 04: Mastering Goto Anything
* `CTRL + P` to open
* "fuzzy matching" used
* `:` to go to a line number
* `@` to search a symbol

## Module 05: Predictive Filename Typing
* Package is called "AutoFileName" to suggest file names
* Settings can add file properties, if needed

## Module 06: Code Folding
* Click the arrow in the gutter to fold the code OR
* `CTRL + SHIFT + [` to fold
* `CTRL + SHIFT + ]` to unfold
* `CTRL + K + J` to unfold all at once
* `CTRL + K + T` to keep the tag name but hide attributes

## Module 07: Creating and Using Snippets
* Reuable code that you can create a "tab trigger" for
* `CTRL + SHIFT + P` and call your snippet
* To create a snippet, go to "Tools" > "Developer" > "New Snippet"
* Put code in line 3 to ?. You can add "Tab Trigger" in the XML.
* Need to save as `.sublime-snippet` file and needs to go into `snippets`
* Helpful note: But a `.` infront of all of your tab triggers so that it doesn't conflict with Emmet

## Module 08: Moving, Jumping, Selecting and Inserting
* Hold `Shift` and use arrows to jump around
* `CTRL + L` will select the line
* `CTRL + Enter` will create a line underneath your existing link

## Module 09: Finding, Selecting and Replacing
* Find Options: RegEx, Case Sensitive, Whole Word, Wrap (probably want this on), In Selection, Highlight matches
* `F3` and `SHIFT + F3` to traverse finds, `ESC` to edit
* To iterate through and select only items you want, `CTRL + D` to select, and `CTRL + K` to skip

## Module 10: Emmet - HTML
* Cheat sheet: https://docs.emmet.io/cheat-sheet/
* `img[src="dog$.jpg"]*5` =
```html
<img src="dog1.jpg" alt="">
<img src="dog2.jpg" alt="">
<img src="dog3.jpg" alt="">
<img src="dog4.jpg" alt="">
<img src="dog5.jpg" alt="">
```
* `img[src="dog$$.jpg"]*5` =
```html
<img src="dog01.jpg" alt="">
<img src="dog02.jpg" alt="">
<img src="dog03.jpg" alt="">
<img src="dog04.jpg" alt="">
<img src="dog05.jpg" alt="">
```

## Module 11: Emmet - Tag Wrapping
* Emmet wrapping feature is more flexible
* Select the copy, `CTRL + SHIFT + G`

## Module 12: Emmet - CSS
* Uses fuzzy search
* You can use `-` to mean `:`
* can use `-` at the start of the value to do all the vendor prefixes
* `@kf` to do keyframes

## Module 13: Emmet - Value Bumping
* `CTRL + ↑` + `CTRL + ↓` to bump
* `CTRL + SHIFT + ↑` + `CTRL + SHIFT + ↓` to bump by larger margin

## Module 14: Emmet - Filters
* `|c` at the end to create closing comments
* `|jade` at the end to create jade code, rather than default
* `|e` to escape code into html entities
* `|s` to single line it

## Module 15: Line Bubbling or Swapping
* `CTRL + SHIFT + ↑` and `CTRL + SHIFT + ↓` to move lines up and down

## Module 16: Introduction to Panes and Groups

## Module 17: Mastering Panes and Groups with Origami
* Install `Origami` Package
* Create/destroy panes however you'd like
* `Clone` to create same file on different pane
* `CTRL + K` to start, `← ↑ → ↓` to focus
* `CTRL + K` to start, `CTRL + ← ↑ → ↓` to create
* `CTRL + K` to start, `CTRL + SHIFT + ← ↑ → ↓` to delete

## Module 18: Working with Multiple Carets
* `CTRL + mouse click` creates multiple carets
* `CTRL + middle click` helps create multile carets quickly

## Module 19: JavaScript Code Quality with JSHint
* Install `JSHint Gutter` and `jshint` in bash via `npm install jshint -g`

## Module 20: Lint Any Language with Sublime Linter
* Sublime Linter base
* Install various SublimeLinters, e.g. `jshint`, `csshint`, etc.
* Read the Sublime Linter docs