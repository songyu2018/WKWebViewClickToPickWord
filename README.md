# WKWebViewClickToPickWord
## Motivation
In one of my iOS project, I was displaying a massive reading material stored in SQLite resource. The material shall be rendered in RTF and the view also needs to support tap-to-select-word. I was planning to convert the material to HTML and render it in a WKWebView. Unfortunately I did not find a way to accomplish tap-to-select-word in a WKWebView. I tried some JavaScript solution in the HTML header which worked perfectly with a browser like Safari but was blocked by WKWebView. And I regretfully gave up the HTML+WKWebView and turned to AttributedText+UITextView. Almost one year later, I happend to read an artical which completed answered my question.
## Implementation
* I choose SwiftUI to demonstrate this idea. By the time this sample is created, SwiftUI does not have a native WebView yet so I have to wrap up a WKWebView from UIKit, which is WrappedWKWebView.swift. For your future convenience to add this file to your Swift Package, all the types in WrappedWKWebView.swift are declared "public" when necessary.
* The key to the solution is a little tricky, achieved by several parts: (1) A jquery script in click_to_select.html header part to detect the click and post the message, (2) userContentController method in WrappedWKWebView.swift to list to the message posted and then call the delegate, and (3) SmartWebViewModel.swift, which is also the delegate to receive the event and update the view.
## Run
Tap a word on the sentence "Baa Baa Black Sheep" and the word you tapped will be shown on the topmost of the view.
