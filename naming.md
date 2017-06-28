# Naming

## Default
Unless specificially declared these are the rules:

* camelCase
* Camel case acroynms when they are over 2 characters. When they are 2 character uppercase
  * Example: `xmlParser` or `parseXml` vs `ioParser` or `parseIO`

## Components

* Pascal Case

## Epics

* Epic suffix
  * `rootEpic`

## Streams

* `$` suffix
  * `myStream$`

## Selectors

* get / is / has prefix
* @TODO: Define noun / filtering / adverb order


## Enums

* Namespace = Pascal Case
* Namespace = singular
* Keys = UNDERSCORE_CASE

**Example**

```js
const Color = {
 BLUE: 'BLUE',
 GREEN: 'GREEN',
};
```

## Files and Assets

* kebab-case

## Intl Messages

* Dot delimited

## Signals

### Action Type

* UNDERSCORE_CASED
* Prefixed with the module with @, using forward slash to separate (@MY_MODULE/S_MY_TYPE)
* Type prefixed with S_ (S_MY_TYPE)
* Present tense
* Verb noun

### Action Creator

* Verb noun

## Messages

### Action Type

* UNDERSCORE_CASED
* Prefixed with the module with @, using forward slash to separate (@MY_MODULE/M_MY_TYPE)
* Type prefixed with M_ (M_MY_TYPE)
* Past tense
* Noun verb

### Action Creator

* Noun verb
