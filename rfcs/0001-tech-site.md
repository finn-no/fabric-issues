# Summary

A single site that has documentation for developers spanning the frameworks Fabric supports.

# Motivation

Several key motivators:
- One page to refer to from design docs or userland
- A single experience for the user, and for the Fabric team to maintain
- Leaves the implementations to only worry about dev-playground sites instead of one/both
  - React currently has both a docsite and storybook
  - Vue has a combined approach

# Details

Loose example here: https://fabric-tech-poc.surge.sh/button/ - both Button and Pill have early pages

- Supported frameworks for a component should be clearly visible (via tabs, sidebar, whatever) - clearly indicating to the user that if the framework isn't there, it isn't supported (yet)
- Should be possible to view a minimal working example of the component
- Props should be able to be defined using JS so we can mixin/reuse descriptions [0]
- We should use a framework to handle markdown/prism/sidebar stuff, we should not be doing that setup/maintenance ourselves
  - Ideally also supporting components/logic

[0] Example of data for props

```js
  Pill: {
    required: [],
    props: [
      ['label', 'string', undefined, `The pill's label, complicated stuff`],
      ['canClose', 'boolean', false, 'If the pill should be removeable'],
      ['suggestion', 'boolean', false, `If the pill should have suggestion-styling`],
    ]
  },
  Button: {
    required: [],
    props: [
      ['label', 'string', undefined, 'Interchangable with the default slot for labelling'],
      ['href', 'string', undefined, 'When set, an anchor tag will be used instead of a button'],
      ['type', 'string', 'button', `Controls the button's type, unused when href is present`],
    ]
  },
  ButtonVariants: {
    titles: ['main', 'combinations'],
    rows: [
      ['primary', 'negative, small'],
      ['secondary', 'quiet, small'],
      ['negative', 'quiet, small'],
      ['link', 'small'],
      ['utility', 'small'],
      ['pill', undefined],
      ['loading', undefined],
    ]
  },
```
