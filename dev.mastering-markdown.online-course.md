# Warren's Notes for Mastering Markdown (Online Course)
v.20171219\
https://courses.wesbos.com/

---
## Table of Contents
* [Module 01: Introduction to Markdown &amp; The Tooling](#module-01-introduction-to-markdown--the-tooling)
* [Module 02: Paragraphs and Text Decoration](#module-02-paragraphs-and-text-decoration)
* [Module 03: Headings in Markdown](#module-03-headings-in-markdown)
* [Module 04: Links in Markdown](#module-04-links-in-markdown)
* [Module 05: Markdown Images](#module-05-markdown-images)
* [Module 06: Lists — Ordered, Unorderd, Bullets and Nesting](#module-06-lists--ordered-unorderd-bullets-and-nesting)
* [Module 07: Line Breaks, Horizontal Rules and BlockQuotes](#module-07-line-breaks-horizontal-rules-and-blockquotes)
* [Module 08: Code Blocks](#module-08-code-blocks)
* [Module 09: Tables](#module-09-tables)
* [Module 10: Github Treats](#module-10-github-treats)
---

## Module 01: Introduction to Markdown & The Tooling
* For Sublime, Markdown Editing is the best package (https://github.com/SublimeText-Markdown/MarkdownEditing)
* GitHub uses Markdown GFM (GitHub Flavored Markdown)
* Specs and examples can be found here - https://github.github.com/gfm
* To change theme: `Sublime Text` > `Preferences` > `Package Settings` > `Markdown Editing` > `GFM Settings - User`
* `CTRL + B` inside Sublime will create an `.html` page

## Module 02: Paragraphs and Text Decoration
* Markdown needs a full line space between items to become a paragraph
* Strikethrough: surround with `~~`

## Module 03: Headings in Markdown

## Module 04: Links in Markdown
* Regular Link
  `<https://www.warrenshea.com>` = <https://www.warrenshea.com>

* Regular Link - Customize Link Text
  `[warrenshea.com](https://www.warrenshea.com)` = [warrenshea.com](https://www.warrenshea.com)

* Regular Link - Customize Link Text + Add Title Tag
  `[warrenshea.com](https://www.warrenshea.com "This is a title tag")` = [warrenshea.com](https://www.warrenshea.com "This is a title tag")

* Regular Link but use Pointer. Pointer is somewhere on the page. Recommended for readability or links that may change
  `[warrenshea.com][1]` + `[1]: https://www.warrenshea.com`
  `[warrenshea.com][ws]` + `[ws]: https://www.warrenshea.com`

## Module 05: Markdown Images
* Image with Alt Text and Tooltip
  `![ALT TEXT](IMG PATH "This is a tooltip")` = ![Mega Man GIF](http://www.v1.worldofwarren.com/common/megaman/ani_beat_rush_megaman.gif "This is a tooltip")

* Image with Alt Text and Pointer. Pointer is somewhere on the page. Recommended for readability or links that may change
  `![ALT TEXT][megaman]` + `[megaman]: http://www.v1.worldofwarren.com/common/megaman/ani_beat_rush_megaman.gif` = ![Mega Man GIF](http://www.v1.worldofwarren.com/common/megaman/ani_beat_rush_megaman.gif "This is a tooltip")

* Combining Hyperlink and Image
  `[![ALT TEXT](IMG PATH)](http://www.v1.worldofwarren.com)` = [![ALT TEXT](IMG PATH)](http://www.v1.worldofwarren.com)

## Module 06: Lists — Ordered, Unorderd, Bullets and Nesting
* Unordered List `*` or `-` or `+`
* Ordered List `1.` - just put a `1.` and the browser will automatically order it. Do not put `1.`, `2.`, `3.` as that leads to manual changes later
* Nest copy with indents

## Module 07: Line Breaks, Horizontal Rules and BlockQuotes
* Line Breaks: use `<br>` or `\`
* Horizontal Rules: `---` or `===` but put space between that and the item, or it becomes a header
* Block Quotes: `>`

## Module 08: Code Blocks
* 3 backticks: ` ``` ` and then the language, e.g. ````javascript`
* 1 backtick: ``code``
* Diff:
```diff
var x = 100;
+ var y = 200;
- var y = 100;
```

## Module 09: Tables
* `:---` = Left Aligned
* `---:` = Right Aligned
* `:--:` = Centered Aligned

## Module 10: Github Treats
* Checkboxes:
* [ ] Do dishes
* [ ] Bathe the dog
* [x] Take long, hibernating nap
```markdown
[ ] Do dishes
[ ] Bathe the dog
[x] Take long, hibernating nap
```