# Warren Shea's Notes for Design Systems Handbook by Invision (Book)
**Version**: 20210711 | **Status**: Complete

## Examples
* [Anna Debenham's Styleguide Resources](http://styleguides.io/)
* [Google's Material Design System](https://material.io/design)
* [Shopify's Polaris Design System](https://polaris.shopify.com/)
* [Salesforce's Lightning Design System](https://www.lightningdesignsystem.com/)
* [Mina Markham's Pantsuit Design System](https://medium.com/git-out-the-vote/pantsuit-the-hillary-clinton-ui-pattern-library-238e9bf06b54)
* [Pivotal UI's Design System](https://styleguide.pivotal.io/)
* [IBM's Design System](https://www.ibm.com/design/language/)
* [U.S. Web Design Systems](https://designsystem.digital.gov/)
* [Lonely Planet](https://rizzo.lonelyplanet.com/)
* [Morning Star Design System](https://designsystem.morningstar.com/)
* [Gitub's Design System](https://primer.style/)

## To watch/read:
* [Donna Chan & Isaak Hayes: Building Empowering Style Guides with Practical Research](https://www.clarityconf.com/session/building-empowering-style-guides-with-practical-research)
* [Programming Design Systems](https://programmingdesignsystems.com/)
* [Modular Scale](https://type-scale.com/)
* [Brad Frost's Atomic Design](https://atomicdesign.bradfrost.com/table-of-contents/)
* [Frontend Masters](https://frontendmasters.com/books/)
* [a11y by Addy Osmani](https://addyosmani.com/a11y/)

## Introduction
A design system unites product teams around a common visual language. It:
* Reduces design debt
* Accelerates the design process
* Builds bridges between teams working in concert to bring products to life


## 1 Introducing Design Systems: The power of scale

### Scaling design with systems thinking
* Standards
* Components

### The value of design systems
* Scale Design
* Manage your debt
* Design consistently
* Prototype faster
* Iterate more quickly
* Improve usability
* Build in accessibility

### Myths of design systems
* Too limiting
* Loss of creativity
* One and done


## 2 Designing your design system: Step by step

### Who should be involved
* Designers, Front-end Developers, a11y experts, content strategists, researches, performance experts, product managers, leaders
* Choosing the right team model: solitary (overlord), centralized (dedicated team), federated (various team members join)
* Creating a visual inventory:
  * Conducting a visual audit
* Creating a visual design language
  * Design Tokens: subatomic, name & value pairs stored as data
  * Colors
    * Interactive items should be the same color background color to help the user
  * Typography (size, leading (line spacing), typefaces)
    * Leading is usually 1.5 for a11y reasons, 1.25/1.125 for headings.
  * Spacing (margins, paddings, position coordinates, border spacing)
  * Images (icons, illustrations)
  * Visual form (depth, elevation, shadows, rounded corners, textures)
  * Motion
  * Sound
* Creating a user interface library
  * Elements (basics/atoms)
  * Components (molecules/modules)
  * Regions (zones/organisms)
  * Layouts


## 3 Building your design system: A strong foundation

**Your technical approach doesn't matter as much as creating a living, breathing system that's flexible, maintainable, stable, scalable, and successful in the long-term**

## Foundations

* Consistent - use configuration settings for IDEs,
* Self-contained - Design System should be separate from main codebase
* Reusable
* Accessible
* Robust - Unit (Mocha, Jasmine, Jest), Functional (Nightwatch, Protractor, Casper), Visual Regression (Wraith, Gemini, Backstop, Percy), Automated (Paypal AATT, aXe)

## Common Challenges

* Keeping documentation up-to-date (automate it)
* Handling breaking changes (wrong: duplication, right: versioning - semver: Major 1.0.0, Minor 0.1.0, Patches 0.0.1)
* Avoid performance degradations


## 4 Putting your design system into practice: Better together

### Large-scale redesigns

Criteria for good candidates for design system projects:
* Potential for common components
* Potential for common patterns
* High-value elements
* Technical feasibility
* Available champion
* Scope
* Technical independence
* Marketing poteential

### Incremental redesigns

### General Notes
* Documentation is key "If it's not documented, it doesn't exist"
* "Waiting room" for components before moving to codebase
* Need to prioritize Navigation and Search/findability

## 5 Expanding your design system: More than the sum of its parts

Vision Statement: to help everyone know where you're going and why
Design Principles
Process
Voice and Tone

## 6 The future of design systems: To infinity and beyond
