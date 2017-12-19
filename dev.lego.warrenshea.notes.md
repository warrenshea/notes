# Warren's Lego CMS Notes
v.20171119

---

# Keys aspects to this solution

1. Website Data and Content (APIs) separated from Presentation (HTML/CSS) and Logic (JavaScript)
2. Website Data and Content (APIs) agnostic to code bases*
*This is partially bad if you need to maintain many components across codebases*
3. Copy, Design, Layout can be done by separate individuals
4. Copy can be edited in the "Copy" section of the page
5. Design (padding, margin, border, background color, border radius) can be edited in the "Design" section of the page
6. Layout (components dragged into hotspots) can be edited in the "Layout" section of the page

---

# Sections
* Product API
* Page API
* Content Management System
* Codebase ([Lego Themes](https://en.wikipedia.org/wiki/List_of_Lego_themes))
  - Styleguide
    - Colors
    - Font Sizes and Line Heights
    - Margin
    - Padding
    - Border Radius
    - Helper Classes
  - Component Library
    - Requires Design and Development to be created
    - Theme based
    - All components have a component id
    - Each components has
      + 1 node (in the first position) called "component-properties", containing properties of that component such as "id", "component-id", "classes", the other component properties
      "component-id": 1,
      + 0+ (in the second+ positions) nodes, for the hotspots of that component
    - A component cannot be placed within the exact same component, or you get infinite loops
* Database
  - Sitemap: Contains unique page id, the site and pathname, the language of the page, and the id for the page architecture component
  - Components: Contains unique component id, component name, component id, the component properties and the hotspot locations

---

# Product API Example
https://lego.warrenshea.com/api/product/bmo/bank-accounts/<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/cashback<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/spc-cashback<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/cashback-world<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/cashback-world-elite<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/air-miles<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/spc-airmiles<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/air-miles-world-elite<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/air-miles-world<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/world-elite<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/preferred-rate<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/rewards<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/usd<br>
https://lego.warrenshea.com/api/product/bmo/credit-cards/prepaid<br>
https://lego.warrenshea.com/api/product/bmo/mortgages/rates<br>
https://lego.warrenshea.com/api/product/bmo/investments/progressive-gics<br>
https://lego.warrenshea.com/api/product/bmoharris/* ?

# Page API Example
https://lego.warrenshea.com/api/site/bmo.com/main/personal/mortgages
```json
"page-architecture": {
  "properties": {
    "id": 1763458435,
    "component-id": 1,
    "html-lang": "en",
    "head-title": "Mortgages | BMO",
    "head-keywords": "Mortages, Rates, First Time Home Buyer",
    "head-description": "Discover competitive mortgage rates, tools and articles to help you become a successful homeowner whether you’re a first time buyer or a seasoned owner.",
    "head-robots": "index,follow,noodp",
    "head-canonical": "https://www.bmo.com/main/personal/mortgages/",
    "head-alternate-en": "https://www.bmo.com/main/personal/mortgages/",
    "head-alternate-fr": "https://www.bmo.com/principal/particuliers/prets-hypothecaires/",
    "head-alternate-x-default": "https://www.bmo.com/main/personal/mortgages/",
    "codebase": "batman",
    "body-data-site": "bmo.com",
    "body-data-section": "mortgages",
  },
  "hotspot-0" : {
    "meta-charset" : {
      "properties" : {
        "id": 1274535,
        "component-id": 3,
        "charset": "utf-8"
      }
    },
    "meta-data-alternate-lang" : {
      "properties": {
        "id": 12445,
        "component-id": 4,
      }
    }
  },
  "hotspot-1" : {
    "body" : {
      "properties": {
      },
      "hotspot-0": {
        "header": {
        },
        "main": {
        },
        "footer": {
        }
      }
    }
  }
}
```

# Component Library Structure

All Components follow this format:

```json
"component-name": {
  "properties": {
  },
  "hotspot-#": {
  },
}
```
Where # can be as many hotspots for that component as you want
OR
```json
"component-name": {
  "properties": {
  },
}
```
Which is a "Leaf Node" component - no component can go inside this.
A link/A button/An image are good examples of this type of component.

# Component Library

## Component 1: Page Architecture (page-architecture)

```php
<!doctype html>
<html lang={{properties.html-lang}}>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width,initial-scale=1">
        <meta content="IE=EDGE" http-equiv="X-UA-Compatible">
        <meta name="last-modified" content={{properties.head-last-modified}}>
        <title>{{properties.head-title}}</title>
        <meta name="description" content={{properties.head-description}}>
        <meta name="keywords" content={{properties.head-keywords}}>
        <meta name="theme-color" content="#0079c1">
<?php
  if (properties.canonical) {
?>
        <link rel="canonical" href={{properties.head-canonical}}>
<?php
  }
  if (properties.alternate-en) {
?>
        <link rel="alternate" hreflang="en" href={{properties.head-alternate-en}}>
<?php
  }
  if (properties.alternate-fr) {
?>
        <link rel="alternate" hreflang="fr" href={{properties.head-alternate-fr}}>
<?php
  }
?>
        <link rel="alternate" hreflang="x-default" href={{properties.head-canonical}}>
        <meta name="robots" content={{head-robots}}>

      <div data-hotspot="0">
        </div>
    </head>
    <body class="{{codebase}}" data-site="{{body-data-site}}" data-section="{{body-data-section}}">

      <div data-hotspot="1">
      </div>
    </body>
</html>
```

```json
"page-architecture": {
  "properties": {
    "id": 0,
    "component-id": 1,
    "html-lang": "en",
    "head-title": "",
    "head-keywords": "",
    "head-description": "",
    "head-robots": "index,follow,noodp",
    "head-canonical": "",
    "head-alternate-en": "",
    "head-alternate-fr": "",
    "head-alternate-x-default": "",
    "codebase": "batman",
    "body-data-site": "bmo.com/bmoharris.com",
    "body-data-section": "bank-accounts/credit-cards/mortgages/investments/self-directed/nesbitt-burns/smartfolio",
  },
  "hotspot-0" : {
  },
  "hotspot-1" : {
  }
}
```

## Component 2: BMO & BMO Harris Header (header)
```php
<header>

</header>
```

```json
"header": {
  "properties": {
  },
  "hotspot-0": {
  },
  "hotspot-1": {
  }
  "hotspot-2": {
  }
  "hotspot-3": {
  }
}
```

## Component 3: BMO & BMO Harris Popup Header (header--popup)

## Component 4: BMO & BMO Harris Main (main)
```php
<main>
  <span class="show-for-sr">{{properties.navigation-skipped-copy}}</span>
    <div data-hotspot="0">
  </div>
</main>
```

```json
"main": {
  "properties": {
    navigation-skipped-copy: "Navigation skipped";
  },
  "hotspot-0": {
  },
}
```

## Component 5: BMO & BMO Harris Footer (footer)
```php
<footer>
    <div data-hotspot="0">
  </div>
</footer>
```
```json
"header": {
  "properties": {
  },
  "hotspot-0": {
  }
}
```

# Databases
```text
sitemap
  id                            int
  site                          varchar(200)
  pathname                      varchar(200)
  lang                          varchar(5)
  componentsPageArchitectureId  int

components
  id            int
  componentName varchar(500)
  componentId   int
  properties    text
  hotspot0      int
  hotspot1      int
  hotspot2      int
  hotspot3      int
  hotspot4      int
  hotspot5      int
```