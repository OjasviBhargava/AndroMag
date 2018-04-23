# AndroMag
General Android FAQs, Tips and Tricks, and some General Best Practices to Help You in your Android Career


## 1. *Does Everything Have To Be In a Fragment?*

`In a word, no.`

UI constructs that do not change based on screen size, configurations, and the like could simply be defined in the activity itself.
For example, the activity can add items to the action bar that should be there regardless of what fragments are shown.

## 2. *Dimensions and Units*

As a unit of measure, the `pixel (px)` is a poor choice, because its size varies by
density. Two phones might have very similar screen sizes but radically different densities. Anything specified in terms of pixels will be smaller on the higher-density device, and typically you would want them to be about the same size.

`For example, a Button should not magically shrink for a ~4" phone just because the phone happens
to have a much higher screen density than some other phone.`

The best answer is to avoid specifying concrete sizes where possible. This is why you tend to see containers, and some widgets, use match_parent and wrap_content for their size — those automatically adjust based upon device characteristics and using `dimens.xml`
