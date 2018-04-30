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



## 3. *Avoid Full-Screen Backgrounds*


Trying to create artwork for each and every resolution in use today is tedious and fragile, and also because new resolutions pop up every so often.
Hence, try to design your app to avoid some sort of full-screen background, where you are expecting the artwork to perfectly fit the screen.

• Use a background, but one that is designed to be cropped to fit and will look good in its cropped state :grinning:

• Use a background, but one that can naturally bleed into some solid fill to the edges (e.g., a starfield that simply lacks stars towards the edges), so you can “fill in” space around your background with that solid color to fill the screen :sunglasses:

• Dynamically draw the background (e.g., a starfield where you place the stars yourself at runtime using 2D graphics APIs)


## 4. *Fluid Designs*
Web designers need to deal with the fact that the user might resize their browser window.
*The approaches to deal with this are called fluid designs.*
Similarly, Android developers need to create fluid layouts for fragments, rows in a ListView, and so on, to deal with similar minor fluctuations in size.

Each of *The Big Three* container classes has its approach for dealing with this:

• Use android:layout_weight with *LinearLayout* to allocate extra space

• Use android:stretchColumns and android:shrinkColumns with *TableLayout* to determine which columns should absorb extra space and
which columns should be forcibly “shrunk” to yield space for other columns if we lack sufficient horizontal room

• Use appropriate rules on *RelativeLayout* to anchor widgets as needed to other widgets or the boundaries of the container, such that extra room flows naturally wherever the rules call for


## 5. *Considering Newer Densities*

tvdpi — around 213dpi — was added for Android TV, and is the density used for 720p Android TV devices. However, Google also elected to use -tvdpi for the Nexus7 tablet.
However, not even Google bothered to create many -tvdpi-specific resources, allowing the OS to downsample from the -hdpi edition. -xxhdpi was added in late 2012 and is for devices with a screen density around 480dpi.
While Android can up-sample an -xhdpi image for -xxhdpi, the results may
not be as crisp as you would like. Hence, you may wish to consider creating -xxhdpi as your *top tier* density, so other devices can downsample if needed.
About 15% of Play Store-equipped Android devices are -xxhdpi.-xxxhdpi is for devices with screens around 640dpi. Also, -xxxhdpi is not in significant use


## 6. *The SlidingPaneLayout* :yum:

The R13 update to the *Android Support package* introduced SlidingPaneLayout, a way of handling this sort of master-detail pattern. SlidingPaneLayout significantly reduces the level of effort for setting up master-detail, as it handles all
of the “dirty work” of showing the different fragments in different scenarios (normal screen, large screen, etc.)

SlidingPaneLayout will detect the screen size. If the screen size is big enough, SlidingPaneLayout will display its two *children side-by-side*. If the screen size is not big enough, *SlidingPaneLayout* will display one child at a time. However, by default, when the “master” child is visible, a thin strip on the right will allow the user to return to the “detail” child.

`These are in addition to any changes in context you might introduce based on UI operations (e.g., tapping on an element in a master ListView automatically switching to the detail child).`


## 7. *Drawables by Density*

Icons and related artwork are not necessarily going to be stretched at runtime, but they are still dependent upon screen density.

A 80x80 pixel image may look great on a Samsung Galaxy Nexus or other -xhdpi device, coming in at around a quarter-inch
on a side. However, when viewed on a -mdpi device, that same icon will be a half inch on a side, which may be entirely too large.
The best way is to create multiple renditions of the icon at different densities, putting each icon in the appropriate drawable resource directory (e.g., res/drawable-mdpi, res/drawable-hdpi).

This is what Android Asset Studio does, creating launcher icons from some supplied artwork for all four densities. Even better is to create icons tailored for each density — rather than just reducing the pixel count, take steps to draw an icon that will still make sense to the user at the lower pixel count.




