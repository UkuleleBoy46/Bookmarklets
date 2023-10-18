# Bookmarklets
This is a collection of useful bookmarklets.
## Table of Contents
  - [Disclaimer](#disclaimer)
  - [What are bookmarklets?](#what-are-bookmarklets)
  - [How to Use](#how-to-use-bookmarklets)
## Disclaimer
I don't endorse any of these bookmarklets. Some of them *may* be against some Terms of Service, and I am not responsible for if or how you use these, and you are accountable for your actions. Use at your own risk. No statements I make void this disclaimer.
## What Are Bookmarklets?
Bookmarklets are pieces of Javascript code you can put in a bookmark in a web browser that supports them. When clicked, the Javascript code will run, executing whatever the code does. Be wary of bookmarks you get from strangers, and read through them carefully. Be especially careful about external links in them, as your browser cookies (which may contain sensitive information such as passwords) and other information could be sent to them. **Don't worry, all bookmarklets on this page have been manually approved and are safe.**
## How to Use Bookmarklets
1. Create a bookmark in a browser that supports Javascript bookmarklets.
2. Copy the full code into the URL section, and give it a name (I often use short names or letter abbreviations so I can fit more into my bookmark bar).
3. Click the bookmarklet like you would with a regular bookmark. The bookmarklet should fire.
   > Tip: If it doesn't work, check the browser console for errors.
## YouTube Standard Page/Embed Toggle
If you are on a YouTube page such as https://www.youtube.com/watch?v=dQw4w9WgXcQ and click this bookmarklet, you will be taken to https://www.youtube.com/embed/dQw4w9WgXcQ. Inversely, if you are on https://www.youtube.com/embed/dQw4w9WgXcQ and click it, you will be taken to https://www.youtube.com/watch?v=dQw4w9WgXcQ. This is useful if I want to watch a video in a larger player but don't want to go full screen. It can also be used to bypass YouTube's "Disable your ad blocker" message, as it doesn't appear when viewing it from the embed URL.
```javascript
javascript: (function() {
	var url = window.location.href;
	var youtubeURL = "https://www.youtube.com";
	var embedURL = "/embed/";
	var watchURL = "/watch?v=";
	if (url.includes(watchURL)) {
		var vParam = new URLSearchParams(window.location.search).get("v");
		if (vParam) {
			window.location.href = youtubeURL + "/embed/" + vParam;
		} else {
			alert("Error: The current URL does not contain a 'v' parameter.");
		}
	} else if (url.includes(embedURL)) {
		var videoID = url.split(embedURL)[1];
		window.location.href = youtubeURL + "/watch?v=" + videoID;
	} else if (!url.includes(youtubeURL)) {
		alert("Error: The current URL is not a YouTube URL. If ");
	} else {
		alert("Error: The current URL is not a valid video.");
	}
})();
```
