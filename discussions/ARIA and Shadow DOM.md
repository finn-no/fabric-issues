# ARIA and Shadow DOM on Collision Course

## TLDR
[ARIA relational attributes](https://www.w3.org/TR/wai-aria-1.2/#attrs_relationships) cannot penetrate Shadow DOM encapsulation.
How do we work around this limitation in future web component composites in Fabric where it is necessary to define relations across shadow roots?

## The issue in a nutshell
The whole point of [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM) is encapsulation.
However, it's still perfectly possible to create **visual** relationships across shadow roots in the viewport by styling and positioning the elements accordingly.
This is needed in composite components such as menus, grids, tabs, and comboboxes just to mention a few.
For screen readers, it is equally important that these relationships can be programmatically determined.
This is specified in [WCAG §1.3.1](https://www.w3.org/TR/WCAG21/#info-and-relationships), and this is where [relational attributes in ARIA](https://www.w3.org/TR/wai-aria-1.2/#attrs_relationships) come to the rescue.
There's just one problem. Shadow DOM effectively prevent this.


## Example combobox
The following is a stripped down HTML example of what a combobox component could look like with only the appropriate relational ARIA attributes included:

```html
<f-combobox>
  #shadow-root
    <f-textfield>
      #shadow-root
        <label for="f-input-text">What's your favorite fruit?</label>
        <input id="f-input-text" value="kiwi" aria-controls="f-popup" aria-activedescendant="f-li-2" />
    </f-textfield>
    <f-listbox id="f-popup">
      #shadow-root
        <f-listitem id="f-li-1">
          #shadow-root
            <span>Banana</span>
        </f-listitem>
        <f-listitem id="f-li-2">
          #shadow-root
            <span>Kiwifruit</span>
        </f-listitem>
    </f-listbox>
</f-combobox>
```

Obviously this will not work because the id references are not visible outside their closest shadow root.


## How do we work around this?
Here are two proposed options (in no particular order):

### Option 1: Use light DOM only
Light DOM allows full control across components, but provides no encapsulation by itself.
In a way, this would probably be the most consistent and well-proven approach, but it would be sad to say goodbye to all the benefits of shadow DOM just because of one little problem.

### Option 2: Mixed light DOM and shadow DOM
The idea here is that custom components that are designed to be part of other custom components would not include their own shadow root.
In the combobox example above, only the f-combobox component would use shadow root.
However, a mixed environment would come with a whole bag of challenges.
For example, how would we set default styling on components that don't have their own shadow DOM?


## Further reading

### AOM specification
At the time of this writing, the [Accessibility Object Model (AOM)](https://wicg.github.io/aom/explainer.html) is slowly making its way into web browsers.
It enables developers to define relations by setting ARIA mixins such as:

```javascript
inputElement.ariaLabelledByElements = [labelElement];
```

However, setting aside the fact that this is not production-ready yet, it won't solve the problem completely because it only allows relations that traverse up the ancestor chain.
The reason for this restriction is to prevent objects that are enclosed in a shadow DOM from being implicitly exposed outside their enclosure.

Consider the following line of code (in context of the combobox markup example above):

```javascript
inputElement.ariaActiveDescendantElement = listItemElements[1];
```

Now, anyone with access to inputElement would also implicitly have access to the second list item element, and from there they could traverse up to the root of the listbox element and gain access to that one as well.
This goes against the principle of shadow DOM encapsulation, and is therefore not permitted.

The key to understand the reasoning behind this restriction is implicit versus explicit.
Explicitly breaking encapsulation is not the same as implicitly/accidentally breaking it.
E.g. setting a custom property like inputElement.coolBeans would be like explicitly exposing whatever value you want to expose.
When setting an ARIA mixin on the other hand, the explicit action is to configure the ARIA feature, not to actually expose an object ref.

### Cross-root ARIA delegation
Another proposed specification that aims to solve this problem is [Cross-root ARIA delegation](https://github.com/leobalter/cross-root-aria-delegation).
However, in terms of a production-ready solution, this is even further away than [AOM](https://wicg.github.io/aom/explainer.html).
