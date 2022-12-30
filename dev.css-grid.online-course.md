# Warren Shea's Notes for CSS Grid (Online Course)
[https://courses.wesbos.com/](https://courses.wesbos.com/){:target="_blank"} | [https://cssgrid.io/](https://cssgrid.io/){:target="_blank"} | [https://github.com/wesbos/css-grid](https://github.com/wesbos/css-grid){:target="_blank"} \
**Version**: 20221226 | **Status**: Completed

---
## Table of Contents
* [Module 01: Welcome!](#module-01-welcome!)
* [Module 02: Starter Files and Tooling Setup](#module-02-starter-files-and-tooling-setup)
* [Module 03: CSS Grid Fundamentals](#module-03-css-grid-fundamentals)
* [Module 04: CSS Grid Dev Tools](#module-04-css-grid-dev-tools)
* [Module 05: CSS Grid Implicit vs Explicit Tracks](#module-05-css-grid-implicit-vs-explicit-tracks)
* [Module 06: CSS grid-auto-flow Explained](#module-06-css-grid-auto-flow-explained)
* [Module 07: Sizing tracks in CSS Grid](#module-07-sizing-tracks-in-css-grid)
* [Module 08: CSS Grid repeat function](#module-08-css-grid-repeat-function)
* [Module 09: Sizing Grid Items](#module-09-sizing-grid-items)
* [Module 10: Placing Grid Items](#module-10-placing-grid-items)
* [Module 11: Spanning and Placing Cardio](#module-11-spanning-and-placing-cardio)
* [Module 12: auto-fit and auto-fill](#module-12-auto-fit-and-auto-fill)
* [Module 13: Using minmax() for Responsive Grids](#module-13-using-minmax()-for-responsive-grids)
* [Module 14: Grid Template Areas](#module-14-grid-template-areas)
* [Module 15: Naming Lines in CSS Grid](#module-15-naming-lines-in-css-grid)
* [Module 16: grid-auto-flow dense Block Fitting](#module-16-grid-auto-flow-dense-block-fitting)
* [Module 17: CSS Grid Alignment + Centering](#module-17-css-grid-alignment-+-centering)
* [Module 18: Re-ordering Grid Items](#module-18-re-ordering-grid-items)
* [Module 19: Nesting Grid with Album Layouts](#module-19-nesting-grid-with-album-layouts)
* [Module 20: CSS Grid Image Gallery](#module-20-css-grid-image-gallery)
* [Module 21: Flexbox vs CSS Grid](#module-21-flexbox-vs-css-grid)
* [Module 22: Recreating Codepen](#module-22-recreating-codepen)
* [Module 23: Bootstrappy Grid with CSS Variables](#module-23-bootstrappy-grid-with-css-variables)
* [Module 24: Responsive Website](#module-24-responsive-website)
* [Module 25: Full Bleed Blog Layout](#module-25-full-bleed-blog-layout)

---

## Module 01: Welcome!

## Module 02: Starter Files and Tooling Setup

## Module 03: CSS Grid Fundamentals
* `display:grid` on container means everything inside is display:grid
* `grid-template-columns: 100px 100px 100px`: 3 columns, 100px each.
* `grid-template-rows: 20px 50px`: 2 columns, 20px, 50px each.
* `grid-gap`

## Module 04: CSS Grid Dev Tools

## Module 05: CSS Grid Implicit vs Explicit Tracks
* Explicit: Defined what columns will be (explicit) - solid black in Firefox Developer Dev tools
* Implicit: Defined what the rows is (implicit) -  dotted back in Firefox Developer Dev tools
* Implicit row: New row created outside explicit rules, outside the solid black line in dev tools
* `grid-auto-rows: 20px;` adds new 20px implicit rows

## Module 06: CSS grid-auto-flow Explained
* `grid-auto-flow: row (default) or column` - when new elements are added as rows or columns
* `grid-auto-columns: 20px;` BUT new items would go to columns

## Module 07: Sizing tracks in CSS Grid
* Don't use percentages for values, because it's doesn't factor in gap, so you can go over 100% if there are gaps (similar to how box-sizing:content-box is with width and padding)
* Use `fr`, fractional unit or ("free space") - the amount of space left after all the elements are laid out
* CSS will lay out the elements with explicit width, and then the `fr`
* `auto` will adjust to the max size of the content

## Module 08: CSS Grid repeat function
* instead of `1fr 1fr 1fr 1fr`, you can write `repeat(4, 1fr);`
* `100px repeat(2, 1fr auto) 200px repeat(2, 5fr)` = `100px 1fr auto 1fr auto 200px 5fr 5fr`

## Module 09: Sizing Grid Items
* `grid-column: span 2` still then make an item span 2 columns

## Module 10: Placing Grid Items
* `grid-column: span 2` is short for `grid-column-start: span 2` and `grid-column-end: auto`;
* `grid-column: span 2 / 5` is short for `grid-column-start: 3` and `grid-column-end: 5`;
* `grid-column: 1 / span 2` is short for `grid-column-start: 1` and `grid-column-end: 3`;
* `grid-column: 1 / -1` will span across the entire grid - like a width: 100%;

## Module 11: Spanning and Placing Cardio
Just some exercises on what has been learned so far

## Module 12: auto-fit and auto-fill
* `grid-template-columns: repeat(auto-fill, 150px)` adds items to the column if there's room
* `grid-template-columns: repeat(auto-fit, 150px)` ends explicit items at last item

## Module 13: Using minmax() for Responsive Grids
* `grid-template-columns: repeat(auto-fill, minmax(150px, 1fr))` which means a min of 150px, and doesn't fill the whole row
* `grid-template-columns: repeat(auto-fit, minmax(150px, 1fr))` which stretches the track to fit
* `grid-template-columns: auto 150px 150px 150px` will be auto size, then 3x 150px
* `grid-template-columns: fit-content(100px) 150px 150px 150px`

## Module 14: Grid Template Areas
* `grid-template-columns: 1fr 500px 1fr`
* `grid-template-row: 150px 150xpx 100px`
* `grid-template-area:
    "sidebar-1  content   sidebar-2"
    "sidebar-1  content   sidebar-2"
    "footer     footer    footer"`
* `.footer {grid-area: footer}`

## Module 15: Naming Lines in CSS Grid
* Lines inbetween columns
* `grid-template-columns: [site-left] 1fr [content-start] 500px [content-end] 1fr [site-right]`
* `grid-template-row: [content-top] repeat(10, auto) [content-bottom]`
* `grid-template` = `grid-template-columns / grid-template-row`
* For the item, \
```
grid-column: content-start;
grid-row: content-top / content-bottom
```

## Module 16: grid-auto-flow dense Block Fitting
* `grid-auto-flow:dense;` on the container fills in things more compactly, regardless of the size of the children

## Module 17: CSS Grid Alignment + Centering
* `justify-items` / `justify-content` / `justify-self` for x-axis/row-axis
* `align-items` / `align-content` / `align-self` for y-axis/column-axis
* `place-items` will do align-items, then justify items

### Resources:
* [https://css-tricks.com/snippets/css/complete-guide-grid/](https://css-tricks.com/snippets/css/complete-guide-grid/){:target="_blank"}

## Module 18: Re-ordering Grid Items
* Using order

## Module 19: Nesting Grid with Album Layouts
* Example: creating a grid layout

## Module 20: CSS Grid Image Gallery
* Example: image gallery of images at various dimensions between [1,1] and [4,4]

## Module 21: Flexbox vs CSS Grid
* Various examples of when to use Flexbox or Grid - some work better than others

## Module 22: Recreating Codepen

## Module 23: Bootstrappy Grid with CSS Variables
* 12 column grid system with CSS Grid
* `grid-template-columns: repeat(12, minmax(0, 1fr))` & `width:100%` on the item

## Module 24: Responsive Website

## Module 25: Full Bleed Blog Layout