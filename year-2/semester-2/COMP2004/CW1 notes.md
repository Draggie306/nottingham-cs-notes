
### overall design
Heavy focus on using ios26 design principles and Apple's human interface guidelines.

- Shared anatomy with a consistent feel - the page title at the top, main contents hierarchically grouped, and persistent navigation at the bottom for optimal hand placement. All design decisions were made with hierarchy, harmony and consistency in mind, as defined in the HIG https://developer.apple.com/design/human-interface-guidelines
- Content is separated into clear top-level sections. Apples HI guide states that top tab bars are for global navigation and to reflect the app’s top-level content hierarchy. Additionally, they should be persistent, so in my animations and UX, I've tried to ensure they are kept the same and appear on harmoniously. https://developer.apple.com/br/videos/play/wwdc2022/10001/?time=540
- Hierarchy is communicated mostly through layout and the Gestalt principle of similarity with grouping. It also highlights bolder, left-aligned typography for natural Western legibility. https://developer.apple.com/videos/play/wwdc2025/356/ (5m 56)

- Primary icons like New are tinted to draw attention and make them stand out as a clear focal point: https://developer.apple.com/videos/play/wwdc2025/356/?time=596 (9m 56 in video)



## Homepage


Sequence of Use principle
- Page designed to be hierarchical, from the top left to the bottom. Users can scan from the large title, to the highlighted overview card, to the grouped appliance grid, and then to the persistent bottom navigation
- The "At a Glance" section shows anomalies, warnings, and current status. For example, if an appliance is off but is usually on, it will be positioned there. Due to hands not reaching, it automatically cycles through all information without the user needing to swipe.
- The middle energy usage section shows the electricity and gas usage, and can be set to \[1m/quarter/half-year/year]. Via the frequency of use principle
-  

### Utility usage
- Thinking about discrete vs continuous data, the information shows Sample data includes missing data, for example in the month view, it shows that it is not at the end of the month yet.
- In the settings, the user can toggle to show electricity consumption or cost, whichever is more important to them. Here is what it looks like with both selected.
- Chose to have the date selection at the top, which is an example of Apple's segmented controls https://developer.apple.com/design/human-interface-guidelines/segmented-controls that links closely-related functions. Felt it was important to have all options on the screen at once 


## Appliances

Designed around a metaphor: rooms. 
- Horizontal scrollable room carousels encourages the user to swipe to reveal it.
- Icons are simple, mostly monochrome, and concept-driven: home, chat bubble, settings, warning, etc. https://developer.apple.com/design/human-interface-guidelines/sf-symbols#Custom-symbols Some, such as the homepage warning icon and electricity/gas are designed to draw attention and be more appealing.  


- Switches, and visible objects have immediate feedback and direct reversible actions, which Shneiderman mentioned in his 1983 paper. "central ideas seemed to be be visibility of the object of interest; rapid, reversible, incremental actions; \[...] hence the term "direct manipulation."" Shneiderman, Direct Manipulation: A Step Beyond Programming Languages (1983)

## Chat
- Heavy use of Gestalt psychology. I used symmetry to divide the chat bubbles 
- Search field: https://developer.apple.com/design/human-interface-guidelines/search-fields



## Credits

- Electricity icon: https://thenounproject.com/browse/icons/term/electricity/
- Electricity usage design inspired by https://octopus.energy/blog/track-my-energy-use/
- Gas icon: https://www.flaticon.com/free-icon/natural-gas_4833029
- Appliances Icon: https://www.svgrepo.com/svg/490527/appliances
- Fridge: https://en.wikipedia.org/wiki/Refrigerator
- Kettle: https://islandinthenet.com/electric-kettle-vs-stovetop-kettle/
- User: https://www.vecteezy.com/vector-art/46010545-user-icon-simple-design
- James: https://stock.adobe.com/search?k=guy+face
- Female: https://www.pickpik.com/person-human-female-girl-long-hair-face-144885
- Note: https://freesvg.org/taking-notes-1625609238

## Features for video


![](../../../Images/Pasted%20image%2020260318214948.png)
Alignment of dates





![](../../../Images/Pasted%20image%2020260319110548.png)
Multiple form factors


![](../../../Images/Pasted%20image%2020260319113836.png)



![](../../../Images/Pasted%20image%2020260320114212.png)










