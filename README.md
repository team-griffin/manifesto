# standards

## UI

## General

* Every component must be stateless.
* Use the stateless function syntax.
* Each custom component must go in its own file.

### Dumb Components
In general most components should be a dumb component. A dumb component refers to a component having no understanding of the store's state, or its structure. All of its props are purely passed in from its parent.

* Exports a minimum of 3 keys: `enhance`, `PureX`, and `X`. Where X is the name of the component.
* 

#### Styling

* Styles must be achieved via inline css*.
* To calculate styles for the component there should be 2 functions. `stylesheet(props: Object): Object` and `stylesheetToStyles(stylesheet: Object, props: Object): Object`.
* The `stylesheet` function is to return the same object syntax as `reactCSS`. Where each top level key is a modifier and each sub key is the element. The root element of the component in react must be called root in the stylesheet.
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

#### Modifiers

#### i18n

### Smart Components

### Assets



### 

## State Management

### Reducers

## Business Logic

### Epics

### Streams

## Actions

### Signals (Intent)

### Messages (Event)

