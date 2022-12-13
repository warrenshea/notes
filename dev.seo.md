# Warren Shea's Notes for SEO (Search Engine Optimization)
v20221211

* 301 Redirect = permanent redirect
* 302 Redirect = temporary redirect
* `aria-label`s don't affect SEO
* Canonical URLs should exactly match their intended URL - don't use canonical urls that 301/302 redirect]
* A SEO Friendly show-for-sr class:
```html
<span class="show-for-sr-seo" sronly="dagger"></span>
```
```css
show-for-sr-seo:before {
  content: attr(sronly);
  display:inline;
  position: absolute;
  left: -9999px
  width: 1px
  height: 1px
}
```