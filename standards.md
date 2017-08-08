# standards

## UI

* Every component must be stateless.
* Use the stateless function syntax.
* Each custom component must go in its own file.
* Composition over inheritence. Use hocs to achieve this.
* Use recompose to set the static properties. Put these enhacements in the enhance function.

### Dumb Components

In general most components should be a dumb component. A dumb component refers to a component having no understanding of the store's state, or its structure. All of its props are purely passed in from its parent.

* Exports a minimum of 3 items: `enhance`, `PureX`, and `X` (default). Where X is the name of the component.
* Be supplied a prop called `classNamespace`. The root element (if it is not an html element) must use this prop to allow for easier debugging. This className can be stripped out at build time.
* Must not handle actions. Instead all callbacks must be provided `onEvent` callbacks.
* If any callbacks require a form identification then a `pin` prop must be provided.
* Lifecyle methods should be avoided.
* Must be pure. Therefore given the same input will result in the same output.

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

In some cases it is near impossible to achieve inline css. Some of these cases are:

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

#### Forms (ReduxForm)
* Any and all form components should use the reduxForm hoc within its `enhance`.
* The form props should be namespaced to `form` using reduxForm's `propNamespace` config option.

### Smart Components

* A smart component must be called `ConnectedX`.
* It does not have any render function. Instead it uses `react-redux`'s `connect` hoc.
* If any actions need to be performed upon lifecycle methods then use `lifecyle` from recompose.
* All callback methods defined in the child dumb components must be handled by `withHandlers` from recompose.
* All actions must be pre-bound, and supplied into an actions object.

### Assets

* SVGs are the preferred choice for imagery.

#### SVGs

* Use Inline SVG.

#### Images

#### Fonts

## State Management

* All data, state. and ui state, must be stored in the global state.
* The entire state tree must be a plain object or array.
* Avoid storing any data that can be "easily" derived.

### Reducers

* A reducer must return a completely new object. Aka, the state must not be mutated.
* Use `redux-create-reducer` where possible.
* Each module must export a root reducer (if it uses reducers).

### Selectors

* Any data that needs to be retreived from state must be obtained via a selector.
* Use selectors to derive data.

## Business Logic

Business logic must avoid components at all costs. A component must not be coupled to how things are done. Instead a component should render the state of the application and dispatch user intents.

This logic can be decoupled and achieved in several ways such as thunks, sagas, and epics. Our standard is to use `redux-most` (epics).

### Epics

* Whilst epics can be written to be pure, they are often used in impure way (performing ajax requests). Therefore any operation that performs impure actions must be supplied to the epic via partial application.
* Functional style is preferred to the fluent style.
* Each module must export a root epic (if it uses epics).
* Must use most.js to handle streams.
* Should try and break down epics into smaller streams.
* If 2 operations needs to be achieved which do not have anything to do with each other but use the same action, then split them into 2 different epics.
* Put as much core logic into services. Use epics as a means of wiring up services and dispatching actions.

### Streams

* Avoid using promising, opting instead to use cold promises.

## Actions

All actions can be split into 2 different types. Signals and messages. A signal denotes an intent to do something; they are written as current tense. Such as `S_DO_THING`, `S_LOAD_DATA`. A reducer must not react to signals.

In contrast messages denote events have occured in the system. They are written as past tense. Such as `M_DATA_LOADED`. A message must describe what has happened in the system, and avoid names such as `UPDATED`, `SET`, `CHANGED`.

Each action can have 4 keys: `type`, `payload`, `meta`, and `error`. Payload, meta, and error are optional. When the payload / action is an error the error flag must be set to `true`.

Meta is useful data / functions that do not affect the reducer. For example the resolve and reject functions needed to work with `redux-form` in an epic.

Use `redux-actions` to create actions.

