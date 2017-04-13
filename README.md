# Browser Bugs Building A Text Editing Surface Using contenteditable

When you build a text editing surface based on contenteditable which is designed for use on both iOS and desktop you run into a lot of browser bugs.  I've gathered a bunch of these bugs, samples, and workarounds here so it can be tracked in one place.

### Safari: Changing text alignment can leave artifacts on fonts that spill outside of the bounding box

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=170801

See changingAlignmentArtifacts.html

### Chrome: Images of certain dimensions dont fully cover the background of elements that are 60x60

Chromium Bug: https://bugs.chromium.org/p/chromium/issues/detail?id=710342

See backgroundSizeCoverLeavesGap.html

### iOS Safari: Quicktype suggestions fail when text-transform is applied to an input

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=167770

See quickTypeUppercase.html

### Chrome: Caret is misaligned when using :before as a placeholder in contenteditable region

Chromium Bug: https://bugs.chromium.org/p/chromium/issues/detail?id=670995

See placeholderCaretAlign.html

### iOS10: mailto links don't work inside of frames

Webkit bug: https://bugs.webkit.org/show_bug.cgi?id=164378

### Chrome/Safari/Firefox: Bold text cannot be unbolded when it uses a font weight under 600

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=164149

See cannotUnboldTextWithLowerFontWeight.html

### IE: input event is not supported on contenteditable regions

See https://connect.microsoft.com/IE/feedbackdetail/view/794285

Not sure why it lists that as fixed in Edge because from what I can tell it is still broken there.

### IE: Ordered list items are all 1s when element between li and ol exists

See elementBetweenListAndItem.html

### Chrome/IE: Click event fires on parent when mousedown occurs on child

See clickDoesntFireOnParent.html

### iOS Safari: keydown event doesn't fire when arrow keys pressed on external keyboard

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=149054

See arrowKeysOnKeyDown.html

### OSX: File dialog doesn't restore Apple Photos location when choosing another photo

Filed at bugreport.apple.com (#22630757)

See fileDialog.html

### IE11: Removing all ranges sets focus

See removeAllRangesSetsFocus.html

### Firefox: Setting selection doesn't set focus

See setSelectionDoesntSetFocus.html

### Firefox: Calling queryCommandState can result in NS_ERROR_FAILURE when no contenteditable region is on the page

See queryCommandState.html

### IE11: Caret remains visible after blur() called within an iframe

See caretRemains.html

### IE11: Selection cannot be set on paste event handler

See setSelectionOnPaste.html

### IE11: anchorNode of a selection can be wrong after sending bold/italic commands to a contenteditable region

See plainTextIndices.html

### Webkit: Extra ClientRects in Selection Range at the start/end of lines

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=148532

See extraClientRects.html

### Safari: autocapitalize doesn't work on contenteditable regions

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=148503

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=148504

See autoCapitalize.html

### iOS8: Dictation fails when a text-transform is applied to an input

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=141163

A Regression in iOS8 that broke Siri input for dictation in contenteditable regions that have uppercase text-transforms.

See dictationUppercase.html

### Safari: Setting iframe src clears undo stack

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=140262

A UIWebView that communicates with a native app shell by changing the src of an iframe will have its undo stack cleared.  This is unfortunate when you often send events to the native shell (like save for example).  A possible workaround might be to switch to WKWebView which has a different native shell communication method.  

Looks like someone else ran into this too: http://stackoverflow.com/questions/10810246/iframe-load-clears-browser-undo-stack

### iOS8: custom keyboards don’t fire keydown, keypress events

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=137070

If your application relies on detecting keydown events (like intercepting ENTER/BACKSPACE for example) you may want to disable custom keyboards in the native shell app since custom keyboards aren't firing keydown/keypress events.

### iOS8: custom keyboards don’t always scroll the caret into view

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=148496

Steps to reproduce:

1. Using iPad Air with iOS8
2. Set a custom keyboard as your default keyboard
3. Go to disney.com
4. Scroll to the bottom of the page
5. Tap in the Search field
6. Notice the caret is hidden under the keyboard

The caret position is often hidden off screen when using custom keyboards.  If this is a dealbreaker you may want to consider disabling custom keyboards in your application.  I filed this bug at bugreport.apple.com on February 2, 2015.

### A contenteditable element puts the caret at left instead of center when it has a :before element with some content defined

Webkit Bug: https://bugs.webkit.org/show_bug.cgi?id=135914

Chrome Bug: https://code.google.com/p/chromium/issues/detail?id=403581&thanks=403581&ts=1407972699

See leftAlignedCaret.html

I've worked around this in the past by wrapping the text field in another div that was inline-block.

Ideally there would be better placeholder support on contenteditable regions so we don’t have to rely on hacking around :before to implement it.


### Safari: Spaces typed into a contenteditable region with text-align:right don’t show up until another non-space character is typed

Safari Bug: https://bugs.webkit.org/show_bug.cgi?id=136827

See rightAlignedSpaces.html


### Safari: Spacebar is sometimes ignored in a contenteditable region when the caret is against the right of the region

Safari Bug: https://bugs.webkit.org/show_bug.cgi?id=156657

See spacebarIgnored.html
