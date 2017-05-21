# standards

## UI

## General

* Every component must be stateless.
* Use the stateless function syntax.
* Each custom component must go in its own file.
* Composition over inheritence. Use hocs to achieve this.
* Use recompose to set the static properties. Put these enhacements in the enhance function.

### Dumb Components

In general most components should be a dumb component. A dumb component refers to a component having no understanding of the store's state, or its structure. All of its props are purely passed in from its parent.

* Exports a minimum of 3 items: `enhance`, `PureX`, and `X` (default). Where X is the name of the component.
* Be supplied a prop called `classNamespace`. The root element (if it is not an html element) must use this prop to allow for easier debugging. This className can be stripped out at build time.

#### Styling

* Styles must be achieved via inline css*.
* To calculate styles for the component there should be 2 functions. `stylesheet(props: Object): Object` and `stylesheetToStyles(stylesheet: Object, props: Object): Object`.
* The `stylesheet` function is to return the same object syntax as `reactCSS`. Where each top level key is a modifier and each sub key is the element. The root element of the component in react must be called root in the stylesheet.
```js
{
  default: {
    root: {
      display: 'inline-block'
    }
    
    listItem: {
      float: 'left'
    }
  },
  
  block: {
    root: {
      display: 'block'
    }
  }
}
```
* The `stylesheetToStyles` function is to returned a fully computed styles object. Therefore requiring no more further computation in the render function. `reactCSS` is recommended for this.
* It is forbidden to allow styles to be passed down from a parent component, unless the component is for a general purpose library.
* The `PureComponent` is to be passed the final styles object.

##### Edge Cases

In some cases it is near impossible to ahcieve inline css. Some of these cases are:

* Input placeholders
* Raw html
* Psuedo classes
* Animations
* Fonts
*

#### Themeing

* All colours should be derived from the palette.
* Rounded corners must be derived from the curvature strength.
* Any text in the component must specify its font style.
* A theme object must be passed into the component as a prop. This object must never mutate as it goes through the render tree.
* All colours in the palette must have defined rules. For example `contrast` is a colour which can guaranteed to contrast against the `primary` colour.

#### Props / Modifiers

* Any and all modifications a component requires, including styling variations, must be handled via props.
* If a prop can have finite values those values must be handled via an enum. These enums should be exported in the component file.

#### i18n

* All text must either be provided by a backend service (which must localalise itself) or be provided via `react-intl`'s message bank.
* It is preferred to not have the text passed in whereas each component must supply a `intlNamespace`.
* Any child components should have their namespaces overwritten.

### Smart Components

### Assets

#### SVGs

#### Images

### 

## State Management

### Reducers

## Business Logic

### Epics

### Streams

## Actions

### Signals (Intent)

### Messages (Event)

