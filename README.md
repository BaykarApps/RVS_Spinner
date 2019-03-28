![Spinner Icon](icon.png)

RVS_Spinner Control
==========
This is a special control class that implements a "pop-up spinner" control.

You can associate an array of values with a Spinner, and they will be presented to the user when they tap the center of the control.

The control will pop up either a "fan" of values that can be scrolled like a knob, or a UIPickerView.

It is completely self-contained. You only need to instantiate the control, give it a place in the view (just like any other control), and associate a set of values with it.

The values should be accompanied by images.

The operation and appearance of the Spinner are highly customizable, either at runtime, or through IB Inspectable properties.

The Spinner is presented as a Swift-only shared dynamic framework, supporting iOS 11.0 and above.

OPERATION
=========
RADIAL SPINNER
---------------------
The way it works, is that the "quiescent" control is small. By default, it is an oval or circle; possibly with an image or text in it.

![The Spinner When Closed](doc-images/Closed.png)
Figure 1: The Spinner, When Closed.

Tapping on the circle "pops up" a surrounding ring of images, which can be rotated about the center, like a prize wheel or a knob.

This popup is a UIView that is opened in the superview of the center, so the superview must be able to support having a larger view added.

![The Spinner Open](doc-images/OpenLargeDaisy.png)
Figure 2: The Spinner When Open

![The Spinner Open](doc-images/OpenLargeNonDaisy.png)
Figure 3: The Spinner When Open (No "Daisy" Effect)

You can prescribe the radius of the popup or UIPickerView at runtime, or in the Interface Builder/Storyboard Editor. The sizes of the images will adjust to fit the circle.

![The Spinner Open](doc-images/OpenSmallDaisy.png)
Figure 4: The Spinner When Open With Many Values (Many Radial "Spokes").

![The Spinner Open](doc-images/OpenSmallNonDaisy.png)
Figure 5: The Spinner When Open With Many Values (Many Radial "Spokes"); with no cropping ("Daisy") Effect.

You can control the open Spinner with gestures. It was designed to be thumb-controlled; including a "prize wheel" spinner, where you can send the control spinning in a decelerating rotation. The top (most visible) value is the one that will be selected.

PICKER VIEW VARIANT
---------------------------
You can also have a standard UIPickerView come up, which may be better for larger numbers of values, or for developers that prefer a more standard Apple User Experience.

![The Spinner When Open, Using A UIPickerView](doc-images/OpenPicker.png)
Figure 6: The Spinner, Open, Using a UIPickerView.

IMPLEMENTATION
==============
To use Spinner, import the framework into your Swift 4.0 or above project. The main Spinner class is called "RVS_Spinner," and you can use this class in storyboards.

Unlike the UIPickerView, the Spinner is self-contained. You supply it an Array of RVS_Spinner.RVS_SpinnerDataItem instances, which contain, at minimum, and icon (a UIImage), and a title (a String). These are displayed by the Spinner when it is opened.

The Spinner has a  RVS_Spinner.selectedIndex property that denotes which Array element is the selected value.

In order to use this in Interface Builder/Storyboard Editor, you need to drag in a UIView, then make it an instance of RVS_Spinner. The module will be RVS_Spinner.

![Adding The Spinner, Using the Interface Builder/Storyboard Editor](doc-images/StoryboardEditor.png)
Figure 11: Adding the Spinner, Using the Storyboard Editor.

INTERFACE BUILDER/STORYBOARD EDITOR OPTIONS
-----------------------------------------------------------------
Once you assign the RVS_Spinner class to the UIView, a number of options will appear in the Attributes Inspector for the Spinner:

![The Spinner Attributes Inspector Options](doc-images/SpinnerOptions.png)
Figure 12: The Spinner Attribute Inspector Options in the Storyboard Editor.

1. **Play Sounds**
This specifies whether or not the Spinner will give subtle audio feedback (faint "clicks") when opening, closing, or selecting values.

2. **Play Haptics**
This specifies whether or not to use haptic feedback (on devices that can play haptics).

3. **Spinner Threshold**
This is an integer, from 0 to whatever value you wish, that represents the point at which an Array of values switches from the radial spinner to the picker. This only applies when the **Spinner Mode** option is set o 0 (*both*).

4. **Spinner Mode**
This is an integer, with 3 values:
    -1 Use only the radial spinner (ignore the **Spinner Threshold** value).
    0  Switch between radial spinner and the picker (based on the **Spinner Threshold** value).
    1  Use only the picker (ignore the **Spinner Threshold** value).

5. **Radius of Open Spinner in Display Units**
This is a floating-point number that specifies the *radius* (not the diameter) of the "open" radial spinner. In the case of the Picker, it specifes the height, above the center, of the open picker.

6. **Closed Icon**
This is an image (UIImage) that is displayed in the center. Default is no specific image, but the one representing the selected value. If a specific image is selected, then that will always be shown in the center, regardless of the value.

7. **Open Background Color**
This is a color to display behind the open radial spinner or picker. By default, it is clear.

8. **Border Color**
This is the color to use for borders and text. By default, it is unspecified. If unspecified, then the tint of the UIView is used.

9. **Picker Row Background Color**
This applies to each line in the UIPickerView. It also applies to the background color of the value circles in "**Daisy** mode."

10. **Daisy**
This is a mode that applies only to the radial spinner. When open, the icons will be displayed, surreounded (and clipped) by a circle, the border color of which is specified by either the tint, or the **Border Color** option.

11. **Show Icon In Center**
If on (default), then an image (either the one set in the **Closed Icon** option or the one representing the currently selected value) will be displayed in the closed control. If off, then no image will be displayed there.

12. **Show Center Background**
This is a boolean (default is on), specifying that the center circle will be filled with a background color. This color is the one specified as the UIView background color. If off, then the background will be clear.

13. **Show Center Border**
This is a boolean (default is on), specifying that the center circle/oval will be surrounded by a border, the color of which will be specified by either the **Border Color** option, or the tint.

These values are mirrored by runtime class instance properties.
