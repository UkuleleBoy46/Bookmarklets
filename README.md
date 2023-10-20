# Bookmarklets
This is a collection of useful bookmarklets. If you find this helpful, consider starring it. If you know someone who may benefit from it, share it with them! If you want to add a bookmarklet or contribute in some way, please see [CONTRIBUTING.md](CONTRIBUTING.md)
  - [Disclaimer](#disclaimer)
  - [What are bookmarklets?](#what-are-bookmarklets)
  - [How to Use](#how-to-use-bookmarklets)
  - [YouTube Video Speed Adjuster](#youtube-video-speed-adjuster)
## Disclaimer
I don't endorse any of these bookmarklets. Some of them *may* be against some Terms of Service, and I am not responsible for if or how you use these, and you are accountable for your actions. Use at your own risk. No statements I make void this disclaimer.
## What Are Bookmarklets?
Bookmarklets are pieces of Javascript code you can put in a bookmark in a web browser that supports them. When clicked, the Javascript code will run, executing whatever the code does. Be wary of bookmarks you get from strangers, and read through them carefully. Be especially careful about external links in them, as your browser cookies (which may contain sensitive information such as passwords) and other information could be sent to them. **Don't worry, all bookmarklets on this page have been manually approved and are safe.**
> Tip: Most bookmarklets can be copied and pasted into your browser's console and run that way!
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
## YouTube Video Speed Adjuster
Use this bookmarklet to set your videos to a faster speed or a specific (e.g. 2.8) speed.
> Note: YouTube videos no longer play audio when the speed is higher than 4.

> Tip: This can be used with other video players, too! However, it will alter the first video on the page.
```javascript
javascript:speed = prompt('Select Playback Rate:');
document.querySelector('video').playbackRate = speed;
window.stop();
```
If you have a favorite speed to watch videos at, use the below bookmarklet and change the "2" to your desired speed. Upon clicking, it will set the video to the specified speed, skipping the pop-up prompt.
```javascript
javascript:document.querySelector('video').playbackRate = 2;
window.stop();
```
## QR Code Generator
This is a very useful bookmarklet for generating QR Codes of a website to then view on another device (with QR Code scanning abilities, of course). Credit goes to [Jarón Berends](https://codepen.io/jaronbarends) and you can view it [here on CodePen](https://codepen.io/jaronbarends/pen/nMpOZp).
> Help wanted! This bookmarklet seems complicated, and it can't run in the browser console (returns "[SyntaxError: missing variable name](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/No_variable_name)")
```javascript
javascript: (function() {
	var % 20 qrSrc = 'https://chart.googleapis.com/chart%3Fchs=250x250%26cht=qr%26chl=' + encodeURIComponent(document.location.href), overlay = document.createElement('div'), os = overlay.style, img = document.createElement('img');
	img.src = qrSrc;
	os.position = 'fixed';
	os.zIndex = 1000;
	os.width = '100%25';
	os.height = '100%25';
	os.top = 0;
	os.left = 0;
	os.textAlign = 'center';
	os.backgroundColor = 'rgba(0,0,0,0.9)';
	img.style.marginTop = '100px';
	overlay.appendChild(img);
	document.body.appendChild(overlay);
	overlay.addEventListener('click', function() {
		document.body.removeChild(overlay);
	})
})();
```
