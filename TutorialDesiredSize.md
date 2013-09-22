---
permalink: TutorialDesiredSize.html
layout: default
---

Next\: [Tutorial 8: Stretch](TutorialStretch.html)

Tutorial 7: Desired Size
==

<!-- TEMPLATE START -->

### Introduction

The _\[UIView sizeThatFits:(CGSize)size\]_ method returns the _desired size_ for any given view.  A view's _desired size_ reflects the "natural" size for its content.

![Layout Snapshot](images/snapshot-DA93EC7C-4F70-4ED7-BDBE-8A59653911FA-27667-0006BEA3B59FF297-0.png)

The _desired size_ of a non-wrapping _UILabel_ is determined by its text, font, etc.

![Layout Snapshot](images/snapshot-833C1973-01D5-46B5-B5D9-336ECFB27C2E-27936-0006BED475482CF7-0.png)

The _desired size_ of a UIImageView is the size of its image.

![Layout Snapshot](images/snapshot-D6C32D2A-FAD5-4C82-A0CB-B2EBDEC05D6A-24400-0006B8654F081079-0.png)

The _desired size_ of a WeView is the minimum size in which its subviews can be layed out properly, honoring its margins, spacing, etc.  

* If a WeView has _multiple layouts_, its minimum size is the max width or height needed by any of its layouts.

### Text Wrap, Flow Layouts, etc.

For some UIViews, their _desired size_ is context-dependent.  

![Layout Snapshot](images/snapshot-54DD17C9-F409-4FCB-AAAF-E3B24C309433-28210-0006BF4AD6A66AE5-0.png)
![Layout Snapshot](images/snapshot-54DD17C9-F409-4FCB-AAAF-E3B24C309433-28210-0006BF4AD6A66AE5-1.png)
![Layout Snapshot](images/snapshot-54DD17C9-F409-4FCB-AAAF-E3B24C309433-28210-0006BF4AD6A66AE5-2.png)
![Layout Snapshot](images/snapshot-54DD17C9-F409-4FCB-AAAF-E3B24C309433-28210-0006BF4AD6A66AE5-3.png)

A UILabel can _wrap_ its text (for example, if numberOfLines = 0 and lineBreakMode is NSLineBreakByWordWrapping).  For a wrapping UILabel, it's _desired size_ depends on the available space.  

The less horizontal space is available, the greater will be the UILabel's desired height.

![Layout Snapshot](images/snapshot-68DF0B1C-EB1C-4ABB-A1B8-D10AECD47082-29621-0006C114C564175B-0.png)
![Layout Snapshot](images/snapshot-68DF0B1C-EB1C-4ABB-A1B8-D10AECD47082-29621-0006C114C564175B-1.png)
![Layout Snapshot](images/snapshot-68DF0B1C-EB1C-4ABB-A1B8-D10AECD47082-29621-0006C114C564175B-2.png)

Similary, WeViews that use a _Flow Layout_ wrap their contents like text.

For this reason, the _\[UIView sizeThatFits:(CGSize)size\]_ method has a _size_ parameter that reflects the available space. The width and height of the _size_ parameter should be >= 0.

If _\[UIView sizeThatFits:(CGSize)size\]_ is called with a size of _CGSizeZero_ (ie. width = 0 and height = 0), a UIView should return its _ideal desired size_.  For a UILabel, this would be the _desired size_ without any text wrap.



### Manipulating Desired Sizes

WeViews offer a variety of ways to manipulate the _desired size_ of a subview.

	- (UIView *)setMinWidth:(CGFloat)value;
	- (UIView *)setMaxWidth:(CGFloat)value;
	- (UIView *)setMinHeight:(CGFloat)value;
	- (UIView *)setMaxHeight:(CGFloat)value;

These methods let you set a maximum or minimum desired width or height.

	// Sets both the minWidth and maxWidth properties.
	- (UIView *)setFixedWidth:(CGFloat)value;
	
	// Sets both the minHeight and maxHeight properties.
	- (UIView *)setFixedHeight:(CGFloat)value;
	
	// Sets all of the minWidth, minHeight, maxWidth and maxHeight properties.
	- (UIView *)setFixedSize:(CGSize)value;

These methods let you set more than one property at a time.


	// This adjustment can be used to manipulate the desired width of a view.
	- (UIView *)setDesiredWidthAdjustment:(CGFloat)value;
	
	// This adjustment can be used to manipulate the desired height of a view.
	- (UIView *)setDesiredHeightAdjustment:(CGFloat)value;
	
	// Sets both of the desiredWidthAdjustment and desiredHeightAdjustment properties.
	- (UIView *)setDesiredSizeAdjustment:(CGSize)value;

The _desired size adjustment_ properties let you add a fixed (positive or negative) adjustment to the desired width and/or height of the view.

For example, UIButtons have a useful _contentEdgeInsets_ property that functions like _padding_.  UILabels do not have a similar property, but by setting a _desired size adjustment_, we can add padding to a UILabel.

### Ignoring Desired Sizes

	- (UIView *)setIgnoreDesiredSize:(BOOL)value;
	
	// Equivalent to [UIVIew setIgnoreDesiredSize:YES].
	- (UIView *)setIgnoreDesiredSize;

If this property is set, the WeView layouts will treat the _desired size_ of this subview as _CGSizeZero_, ie. width = 0, height = 0.  We usually want to ignore the _desired size_ of a subview when the subview is set to _stretch_ horizontally and vertically.



<!-- TEMPLATE END -->

Next\: [Tutorial 8: Stretch](TutorialStretch.html)