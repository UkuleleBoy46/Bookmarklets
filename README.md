# Bookmarklets
This is a collection of useful bookmarklets. If you find this helpful, consider starring it. If you know someone who may benefit from it, share it with them! If you want to add a bookmarklet or contribute in some way, please see [CONTRIBUTING.md](CONTRIBUTING.md)
## Table of Contents
  - [Disclaimer](#disclaimer)
  - [What are bookmarklets?](#what-are-bookmarklets)
  - [How to Use](#how-to-use-bookmarklets)
  - [YouTube Standard Page/Embed Toggle](#youtube-standard-pageembed-toggle)
  - [YouTube Video Speed Adjuster](#youtube-video-speed-adjuster)
  - [YouTube Share Link Generator](#youtube-share-link-generator)
  - [QR Code Generator](#qr-code-generator)
  - [Discord Messager](#discord-messager)
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
		var vidID = new URLSearchParams(window.location.search).get("v");
		if (vidID) {
			window.location.href = youtubeURL + "/embed/" + vidID;
		} else {
			alert("Error: Couldn't find the video's ID.");
		}
	} else if (url.includes(embedURL)) {
		var videoID = url.split(embedURL)[1];
		window.location.href = youtubeURL + "/watch?v=" + videoID;
	} else if (!url.includes(youtubeURL)) {
		alert("Error: The current URL is not a YouTube URL.");
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
## YouTube Share Link Generator
Copying YouTube short URLs (e.g. https://youtu.be/dQw4w9WgXcQ) has never been easy. You need to click on the Share button (sometimes nested within a 3 dots icon), let it load, and then click the copy button (and then click the X to exit out of the modal!). With this simple bookmarklet, you can simply click it and it'll copy the shortened youtu.be URL to your clipboard. 
> Tip: Change all or some of the "alert" actions to "console.log" if you want the process to be more seamless.
```javascript
javascript: var url = window.location.href;
if (url.includes("youtube.com")) {
	var vidID = new URLSearchParams(window.location.search).get("v");
	if (vidID) {
		navigator.clipboard.writeText("https://youtu.be/" + vidID);
		alert(`Successfully copied video shortlink. (https://youtu.be/${vidID})`);
	} else {
		alert("Error: Video ID not found.");
	}
} else {
	alert("Error: This is not a YouTube site.");
}
```
## QR Code Generator
This is a very useful bookmarklet for generating QR Codes of a website to then view on another device (with QR Code scanning abilities, of course). Credit goes to [Jarón Berends](https://codepen.io/jaronbarends) and you can view it [here on CodePen](https://codepen.io/jaronbarends/pen/nMpOZp).
> Help wanted! This bookmarklet seems complicated, and it can't run in the browser console (returns "[SyntaxError: missing variable name](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/No_variable_name)"). If you can simplify it, that would be appreciated (see [CONTRIBUTING.md](CONTRIBUTING.md)).
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
## Discord Messager
With this bookmarklet, you can send messages to people without booting up Discord (which is slow sometimes). There are two setup steps to get this working.
1. Put you token into the area in the below code marked "PUT.YOU_DISCORD.TOKEN_HERE" (leave the quotation marks). You can find out how to get your Discord token [here](https://www.androidauthority.com/get-discord-token-3149920/).
> **WARNING: Never share your token with anyone or paste it into applications, websites, or bookmarklets you don't trust (you can see from that this one is completely harmless and only uses it for accessing Discord API)!**

> Tip: You can also use a bot's token to send a message as a bot, just add "Bot" before the token (example: "Bot xadafdfda.vcnm65cv_awaeou").
2. Edit the if condition. First, [turn on developer mode](https://www.partitionwizard.com/partitionmagic/discord-developer-mode.html). Then duplicate one of the "else if"s or edit an existing one. Change all the text within quotes containing "Change this to username or channel name" to a username you want it to use (it doesn't have to be the exact username or channel name, user whatever you can remember the user or channel. Then copy the channel ID and put in it the second area containing "channel-id-change-this". Repeat the process as many times, for each person or channel you want to be able to quickly message.
```javascript
javascript: var token = "PUT.YOUR_DISCORD.TOKEN_HERE";
var username = prompt("Enter username or channel:");
var message = prompt("Enter message:");
if (username === "Change this to user or channel name") {
	var channelID = "2682632030152929-channel-id-change-this"
} else if (username === "paulbrown--Change this to username or channel name") {
	var channelID = "979796004217954394-channel-id-change-this"
} else if (username === "general--Change this to username or channel name") {
	var channelID = "97506846796530000-channel-id-change-this"
} else {
	alert("Error: User not found!")
};
fetch(`https://discord.com/api/v9/channels/${channelID}/messages`, {
	method: 'post',
	body: JSON.stringify({
		content: message
	}),
	headers: {
		"Content-Type": "application/json",
		"Authorization": token
	}
});
```
> Note: this bookmarklet will be updated soon, so check back later for a better version!
