# Summary

We need to explore theming in Fabric, and possibly add support for it in the future.

# Motivation

Fabric should become _reasonably_ themable. Meaning users can alter different aspects - likely with these being more painful to alter as they become less critical.

# Implementation

Easy to change:
- Adding the idea of a core color set, which will have 3 shades. Something like `--f-core-100`, `--f-core-200`, `--f-core-300`. In our case these would be primary blue, and then darker and darker for hover/active.
  - Core will be available on all color attributes: text, bg, border, etc.
  - Accent will also be available to support f.ex our secondary-blue
- Adding/expanding the idea of primary/secondary. Going to have primary, secondary, tertiary, success, warning, danger
  - A background-primary will probably be different than a text-primary - I don't think this is that confusing to work with, probably just something we need to ensure we're clear on
- Possibly introducing a patch-level change along with these color concept changes to border-radius, changing it to a "large" and "small" definition instead of 4 and 8. This would make it more themeable and so these are bashable in userland by a cssvar.

Medium-difficulty to change:
- In general, buttons and form-elements will be medium-difficult to change, and would be changed by bashing our CSS. This is less ideal since internal changes to our CSS could be breaking for someone else - but kinda comes with the "theming territory".
  - If a user wants to get rid of the border on buttons, they would use the cascade and overwrite our button class - e.g. `.button { border-width: 0; }`
  - Same with form-elements

Hard-mode:
- Changing anything (that doesn't inherit from the 'easy' changes) in the React/Vue/Web components would be quite difficult, since they use TW classes
  - Something clever for the component-classes use that we'll probably explore later, I really dig what Benja mentioned with having these get instanced and then we can just bash defaults with input from userland. But regardless this would almost definitely be major-breaking for the components.
  - Would we provide/inject the component-classes then instead of having them be imports? That way the components could take in this instanced set of classes?
