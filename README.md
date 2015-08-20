# Browser Bugs Building A Text Editing Surface Using contenteditable

When you build a text editing surface based on contenteditable which is designed for use on both iOS and desktop you run into a lot of browser bugs.  I've gathered a bunch of these bugs, samples, and workarounds here so it can be tracked in one place.

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

See extraClientRects.html

### Safari: autocapitalize doesn't work on contenteditable regions

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
