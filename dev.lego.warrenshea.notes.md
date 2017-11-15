# Warren's Lego CMS Notes
v.20171113

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
* Styleguide
  * Colors
* Component Library
  * Requires Design and Development to be created
  * Theme based
  * All components have a component id
  * Each components has
    - 1 node (in the first position) called "component-properties", containing properties of that component such as "id", "component-id", "classes", the other component properties
    "component-id": 1,
    - 0+ (in the second+ positions) nodes, for the hotspots of that component
* Sites
* Content Management System
* Product API
* Page API

---

# Product API Example
https://lego.warrenshea.com/api/bmo/bank-accounts/<br>
https://lego.warrenshea.com/api/bmo/credit-cards/cashback<br>
https://lego.warrenshea.com/api/bmo/credit-cards/spc-cashback<br>
https://lego.warrenshea.com/api/bmo/credit-cards/cashback-world<br>
https://lego.warrenshea.com/api/bmo/credit-cards/cashback-world-elite<br>
https://lego.warrenshea.com/api/bmo/credit-cards/air-miles<br>
https://lego.warrenshea.com/api/bmo/credit-cards/spc-airmiles<br>
https://lego.warrenshea.com/api/bmo/credit-cards/air-miles-world-elite<br>
https://lego.warrenshea.com/api/bmo/credit-cards/air-miles-world<br>
https://lego.warrenshea.com/api/bmo/credit-cards/world-elite<br>
https://lego.warrenshea.com/api/bmo/credit-cards/preferred-rate<br>
https://lego.warrenshea.com/api/bmo/credit-cards/rewards<br>
https://lego.warrenshea.com/api/bmo/credit-cards/usd<br>
https://lego.warrenshea.com/api/bmo/credit-cards/prepaid<br>
https://lego.warrenshea.com/api/bmo/mortgages/rates<br>
https://lego.warrenshea.com/api/bmo/investments/progressive-gics<br>
https://lego.warrenshea.com/api/bmoharris/* ?

# Page API Example
https://lego.warrenshea.com/api/bmo.com/main/personal/mortgages
```json
"page-details" = {
  "properties" : {
    "id": 163723,
    "component-id": 1,
    "lang": "en",
    "site": "bmo.com",
    "url": "/main/personal/mortgages/",
  },
  "page-architecture": {
    "properties": {
      "id": 1763458435,
      "component-id": 2,
      "title": "Mortgages | BMO",
      "keywords": "Mortages, Rates, First Time Home Buyer",
      "description": "Discover competitive mortgage rates, tools and articles to help you become a successful homeowner whether you’re a first time buyer or a seasoned owner."
      "canonical": "canonical",
    },
    "hotspot-1" : {
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
      },
    },
    "hotspot-2" : {
      "body" : {
        "properties": {
        },
        "hotspot-1"" {
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
}
```

# Component Library

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

