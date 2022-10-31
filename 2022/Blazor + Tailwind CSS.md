# Blazor + Tailwind CSS

The amazing notes:

* Tailwind uses _Atomic style classes:_ "Atomic CSS is the approach to CSS architecture that favors small, single-purpose classes with names based on visual function.". See [here](https://css-tricks.com/lets-define-exactly-atomic-css/)
* _Utility-based_ means that when implementing designs, you use predefined classes to set font sizes, padding, margins, colors, etc on each individual item to create a custom element from the available options. This is the case for Tailwind CSS. See [here](https://littlelines.com/blog/2019/04/30/component-vs-utility-based-css-design-systems).
* Sometimes repetitive layouts can be best implemented with components: reusable, segmented blocks of predefined elements. For example Bootstrap. See [here](https://littlelines.com/blog/2019/04/30/component-vs-utility-based-css-design-systems).

What do you get with Tailwind:

* A color pallet like bg-gray-100.
* A spacing pallet like w-40 or h-20.
* A variants pallet like hover:bg-reg-800.
* All these options are configurable.

How to implement it:

* Using a CDN, but that's not really production friendly.
* CLI commands with NPM/NPX.
* Implement central pieces in the app.css file and use blazor for components.

Dark mode:

* Top-level dark class will enable dark mode.
* This can be stored in the local storage.
* Adding a MSBuild target instead of CI/CD pipeline for deployment.
