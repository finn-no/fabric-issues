# RFC: Fabric Elements API

## Background

When building our Web Component library (Fabric Elements) it's good to think of the overall picture of how the API should be structured. 
With the right conventions, it would be easier to maintain consistency when adding new components, which should result in the library being easy to work with for both authors and users.

This RFC attempts to start a discussion on how to structure the Fabric Elements API in a way that aims to minimise confusion and complexity of various components.

## Concepts/Principles to discuss

### Customization of components

To what degree should web components be customized with respective attributes if they return just one main HTML element,
e.g. when `<f-textarea>` returns `<textarea>`, `<f-button>` returns `<button>` or `<f-textfield>` returns `<input>`? 
Should we bind all possible attributes to respective WC properties in case the user wants to change these?
If we render multiple components on a page, each binding all possible attributes + being placed within shadow DOM, 
would that affect page performance much?

### Naming of component attributes

In most web component libraries the component attributes are called the same as native element attributes, e.g. `disabled`, `target`, `aria-label`.
Given Fabric Elements can contain both small and complex web components, what would be a good naming convention for the attributes?
Should we avoid native element attribute names like `href`, `target`, `value` in the API in case there were components with multiple elements to assign those attributes to?
Would it make sense to rename attributes even though they are clearly associated with the returned element,
like `<f-button focused>` instead of `<f-button autofocus>` or `<f-textfield input-type="number">` instead of `<f-textfield type="number">`

### One component, one responsibility

Let's take `Button` as an example. In some libraries ([Material components web](https://github.com/material-components/material-web), [Shoelace WC library](https://shoelace.style/), [Ionic](https://ionicframework.com/docs/api/button)) a `Button` component can return either a `button` element, or an `anchor`.
This however requires the component to handle attributes related to both elements. 
In addition, the `button` element is a form-associated element while the `a` element is not, so we'd need to figure out how to only form-associate the button.

With that in mind, maybe it would make sense to have a separate `Link/Anchor` component that can have the same design variants as `Button` and that handles attributes related to anchors (ref. [Vaadin WC library](https://vaadin.com/docs/latest/components/button/#related-components), [Microsoft's Fast WC library](https://github.com/microsoft/fast/tree/master/packages/web-components/fast-foundation))?


## Sources
* [Microsoft's Fast WC library](https://github.com/microsoft/fast/tree/master/packages/web-components/fast-foundation)
* [Shoelace WC library](https://shoelace.style/)
* [Material components web](https://github.com/material-components/material-web)
* [Ionic WC library](https://ionicframework.com/docs/api/button)
* [Vaadin WC library](https://vaadin.com/docs/latest/components/button/#related-components)
* [Best practices to build web components by Carlos Muñoz](https://medium.com/ing-blog/best-practices-to-build-web-components-6d517923fba4)
