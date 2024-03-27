---
sidebar_position: 5
slug: /appearance-customization
---

# Appearance Customization

Under "Site settings > Appearance" you can override CSS variables and define your own custom CSS styles.

:::caution
Note that Astuto HTML classes and ids can change without notice, so try to keep CSS selectors simple and do not overuse this feature.
:::

## CSS variables

There are two main colors that can be customized through variables: `primary-color` and `background-color`. These variables are here to stay, so it is safe to override them. Just type the following CSS code in the editor, adjusting colors to your preferences:

```css
:root {
  --primary-color: rgb(0, 0, 0);
  --background-color: rgb(255, 255, 255);
}
```