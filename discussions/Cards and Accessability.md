#Card

##What are card components?
Cards are typically square blocks of user interface, containing things like: a heading, a short chunk of 'teaser' text. Sometimes an  image, button or 'call to action'. Idealy this content should summarise the content of the resulting page. 

###A great Card component should:
* Be fully accessible to everyone
* Support usefull built in functionality like right clicking > context menu > open link in new tab
* Support copy/paste of the content(How important is this?)
* Look and feel like the card itself is interactive. 


##Dev approaches
There is a couple of common dev approaches used for cards and most of them have their issues. 

1. Wrapping the whole card in a link
2. Making the call to actions seperate links
3. Linking the main title, and stretching the clickarea of this to cover the whole card
4. handling the click action with js onClick or similar approach




###1. Wrapping the whole card in a link
Quite often Accessability issues arise from how they are built - commonly using a <code>a href=""</code> to wrap the whole component. This is an understandable approach because it achieves the objective of making the whole thing clickable but it ruins the screen reader experience. 

####Screenreader behavior
Screen reader will announse it is a link, then read out the full content as one long string with no structure.

Nesting links inside for other functionality like favorite button is even worse, in some cases the outer link might just break and not work at all. 

####CONS
* Breaks accessability, should never be implemented.


###2. Making the call to action(s) seperate links
Splitting up the link to wrap smaller logical pieces of the card. Typically one arround the image, one arround the title, and one arround the rating and so on. This is a quite common model. 
Example:  [amazon.com](amazon.com)

####Behavior 
When using keyboard navigation, you typically tab straight to each interactive element inside the card instead of the card itself. The card itself is mainly used as a visual grouping. Hovering the card typiccally is not showing any interaction either. 

####PROS
* Works
* Does not get in the way of Good semantics
* Uncomlicated 
* Easy to support lots of different interactive elements within each card.

####CONS
* Bit unsexy form a design pow(?)
* Looks like a card but is not really within the definition.
* The card itself shows no interactivity.
* Might be unclear(?) In this model the main link should in many cases be repeated arround the image and the title. Screenreader will repeat 'link' alot. 

###3. Linking the main title, and stretching the clickarea of this to cover the whole card

The main link for the card is commonly wrapped arround the title in the card, this can be stretched to the full size of the card either by using a pseudo element or by placing an element inside the link. These are stretched to the full size of the card. Other interactive elements inside the card might need to be handled with z-index to be on top of the main card link. 

####Behavior
The card itself looks fully interactive for the user. The card can be hovered/clicked anywhere within its border.

Keyboard navigation like TAB will first focus the card itself, the next tab will activate the Card AND the first interactive element inside the card, like a favorite icon. 

####PROS
* Built in browser functionality like right clicking for the context menu > open in new tab works great. 

####CONS
* Conflicts with marking text for copy/paste within the card.
* Not great if the card is supposed to have many other interactive elements.
* Not the most robust thing in the world, especially if the dev is not familiar with why it is set up as it is. This is a non-issue if a component is use since it hides the magic.

###4. Javascript handler on the card itself instead of relying on a link

####CONS
* Breaks Built in browser functionality like right clicking for the context menu > open in new tab.
