---
title: SwiftUI - Displaying Web Content
date: 2022-05-01
author: johannes
---
SwiftUI was first released almost 3 years ago but it's still lacking some pretty fundamental functionality. I'm partial to the issue that you can't change the background color of list items in a list-style `Picker` or any layout specifics of that component to be honest. Admittedly this is a minor annoyance when you realise that there is no SwiftUI equivalent for `WKWebView`. Luckily the implementation of a simple UIKit wrapper is straight forward.

> ## Update
> 
> Although this method works great for opening links to external content inside an app I'd highly discourage you from using it for that purpose. Due to the excellent research by [Felix Krause](https://krausefx.com/blog/announcing-inappbrowsercom-see-what-javascript-commands-get-executed-in-an-in-app-browser) it became apparent that this is misused by a lot of companies to track users, attribute ads or personalize content. Developers should take this as a hint to switch to `SFSafariViewController` or open Safari outright. Felix goes into a lot more details so I **highly** encourage you to check out his work.
> 
> It's still completely fine to use this to show web content like HTML responses from your own servers, a Markdown preview screen for an editor or maybe a specific piece of UI was just easier to build using web technologies.

## Implementation

To get things started open a new file and import `WebKit`. We need this to have access to `WKWebView` which is Apples replacement for `UIWebView`.

```swift
import WebKit
```

Create a new struct called `WebView` which should conform to `UIViewRepresentable`.

```swift
import WebKit

struct WebView: UIViewRepresentable {
...
}
```

*Keeping with Apples naming conventions for SwiftUI it should just be called `Web` but that seemed a bit odd to me. It also confused me when I realised that Apple did **exactly** that when they called the SwiftUI equivalent for `MKMapView` just `Map`.*

Add a property called `url`. You can define this with `String` or `URL` as its type depending on where you want to implement the error handling in case the supplied URL is invalid.

{% highlight swift %}
import WebKit

struct WebView: UIViewRepresentable {

  let url: String
}
{% endhighlight %}

Now you're ready to implement the two methods required by the `UIViewRepresentable` protocol. Let's start with `makeUIView(context:)`.

{% highlight swift %}
import WebKit

struct WebView: UIViewRepresentable {

  ...

  func makeUIView(context: Context) -> WKWebView {
      WKWebView()
  }
}
{% endhighlight %}

Pretty straight forward, right? Now we just need to load the supplied URL and we're done. Continue by implementing the second required function like so.

{% highlight swift %}
import WebKit

struct WebView: UIViewRepresentable {

  ...

  func updateUIView(_ uiView: WKWebView, context: Context) {
      guard let url = URL(string: url) else {
          return
      }
      let request = URLRequest(url: url)
      uiView.load(request)
  }
}
{% endhighlight %}

This function tries to create a URL using the provided string. If it succeeds the newly created URL is passed to a `URLRequest` which is subsequently handed to the `load(_:)` function of our `WKWebView` instance.

That's all there is to it. Be aware that `WKWebView` is not equivalent to `SFSafariViewController` which basically embeds Safari into your application giving users access to Password Autofill for example.

## Conclusion

Wrapping `WKWebView` like this gives you a quick and easy way to show web content inside your application.

If you found this helpful, feel free to let me know. You can send me an E-Mail to <a href="mailto:{{ site.author.email }}">{{ site.author.email }}</a> or find me on Mastodon [@technocidal](https://mastodon.social/@technocidal).