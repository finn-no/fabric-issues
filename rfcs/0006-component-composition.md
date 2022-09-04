# Summary

Fabric needs guidance on how molecules should be handled; including when/how atoms should be modified, what support is created for molecules, and how molecules should be provided.

## Preface

For clarity, this document/discussion will make use of the _language_ established in [Atomic Design](https://bradfrost.com/blog/post/atomic-web-design).

This is *not* suggesting that Fabric follows Atomic Design principles, but it is useful to refer to core Fabric components as "atoms", and a composition of those components as a "molecule".

# Motivation (by example)

The concrete example of the "Card group" molecule will be used to highlight motivations.

An example in FINN is visible [here](https://pearofducks.com/fabric/rfc-card-group.png) in the "Størrelse på varen" area.

## Modifying atoms

The Card component currently sets `rounded-4` which cannot be overriden by `rounded-0`.

This means an implementation either needs support from the component, or to eject to pure CSS.

## Supporting molecules

Because the borders overlap, special CSS is needed for `hover` behavior.

Effectively:
- On hover, set `z-index: 1`
- When selected, set `z-index: 2 !important` - (`!important` so that hover behavior doesn't lower the element)

A working example can be seen [here](https://fabric-vue-card.surge.sh/).

## Providing molecules

The TJT team is currently packaging this molecule for use in their apps as a [standalone component](https://github.schibsted.io/finn/tjt-web/tree/main/common/components/packages/OptionCard).

# Implementation

TBD
