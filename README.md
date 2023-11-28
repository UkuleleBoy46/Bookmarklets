# Bookmarklets
This is a collection of useful bookmarklets. If you find this helpful, consider starring it. If you know someone who may benefit from it, share it with them! If you want to add a bookmarklet or contribute in some way, please see [CONTRIBUTING.md](CONTRIBUTING.md).
## Table of Contents
  - [Disclaimer](#disclaimer)
  - [What are bookmarklets?](#what-are-bookmarklets)
  - [How to Use](#how-to-use-bookmarklets)
  - [YouTube Standard Page/Embed Toggle](#youtube-standard-pageembed-toggle)
  - [YouTube Video Speed Adjuster](#youtube-video-speed-adjuster)
  - [YouTube Share Link Generator](#youtube-share-link-generator)
  - [QR Code Generator](#qr-code-generator)
  - [Discord Messenger](#discord-messenger)
  - [Discord Messenger v2](#discord-messenger-v2) 🔥
  - [Drag and Drop Website Editor](#drag-and-drop-website-editor)
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
| #youtube #utility | v1.0.0 | [⬆](#table-of-contents) |
| --- | --- | --- |

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
| #youtube #utility | v1.0.2 | [⬆](#table-of-contents) |
| --- | --- | --- |

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
| #youtube #utility | v1.0.0 |[⬆](#table-of-contents) |
| --- | --- | --- |

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
| #utility | v1.0.0 | [⬆](#table-of-contents) |
| --- | --- | --- |

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
## Discord Messenger
| #discord #message #utility #performance | v1.0.3 | [⬆](#table-of-contents) |
| --- | --- | --- |

With this bookmarklet, you can send messages to people without booting up Discord (which is slow sometimes). There are two setup steps to get this working.
1. Put your token into the area in the below code marked "PUT.YOUR_DISCORD.TOKEN_HERE" (leave the quotation marks). You can find out how to get your Discord token [here](https://www.androidauthority.com/get-discord-token-3149920/).
> **WARNING: Never share your token with anyone or paste it into applications, websites, or bookmarklets you don't trust (you can see from that this one is completely harmless and only uses it for accessing Discord API)!**

> Tip: You can also use a bot's token to send a message as a bot, just add "Bot" before the token (example: "Bot xadafdfda.vcnm65cv_awaeou").
2. Edit the if condition. First, [turn on developer mode](https://www.partitionwizard.com/partitionmagic/discord-developer-mode.html). Then duplicate one of the "else if"s or edit an existing one. Change all the text within quotes containing "Change this to username or channel name" to a username you want it to use (it doesn't have to be the exact username or channel name, you can shorten it to make it easier to type/remember). Then copy the channel ID (Not to be confused with a user ID. Even when DMing people, you have to use the DM's channel ID.) and put in it the second area containing "channel-id-change-this". Repeat the process as many times, for each person or channel you want to be able to quickly message.
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
	alert("Error: User not found!");
	throw new Error("User not found!");
}
var message = prompt("Enter message:");
sendMessage();
async function sendMessage() {
	const response = await fetch(`https://discord.com/api/v9/channels/${channelID}/messages`, {
		method: 'post',
		body: JSON.stringify({
			content: message
		}),
		headers: {
			"Content-Type": "application/json",
			"Authorization": token
		}
	});
	const data = await response.json();
	if (response.status !== 200) {
		alert(`An error has occured! Error: ${response.status}`)
	} else {
		alert("Message sent!")
	};
}
```
## Discord Messenger v2
| #discord #message #utility #performance | v2.0.0 | [⬆](#table-of-contents) |
| --- | --- | --- |

With this bookmarklet, you can send messages to people without booting up Discord (which is slow sometimes). There are two setup steps to get this working.
1. Put your token into the area in the below code marked "PUT.YOUR_DISCORD.TOKEN_HERE" (leave the quotation marks). You can find out how to get your Discord token [here](https://www.androidauthority.com/get-discord-token-3149920/).
> **WARNING: Never share your token with anyone or paste it into applications, websites, or bookmarklets you don't trust (you can see from that this one is completely harmless and only uses it for accessing Discord API)!**

> Tip: You can also use a bot's token to send a message as a bot, just add "Bot" before the token (example: "Bot xadafdfda.vcnm65cv_awaeou").
2. Edit the if condition. First, [turn on developer mode](https://www.partitionwizard.com/partitionmagic/discord-developer-mode.html). Change all the text within quotes containing "Change this to a username or channel name" to a username or channel name you want to contact. Then copy the channel ID (Not to be confused with a user ID. Even when DMing people, you have to use the DM's channel ID.) and put in it the second area containing "it's-id-here". Make as many name-ID pairs as you want for all the people or channels you want to quickly contact via this bookmarklet.
> Make sure to also change the default channel. Its format is slightly different, so make sure you only change the things marked "Choose Your Default Channel" and "default-id-here". Repeat it in the standard format, too.

<details>
  <summary>Code in expandable area</summary>
	
  ```javascript
  javascript: (function (a) {
	const users = `{ "Default":{"Name":"Choose Your Default Channel","ID":"default-id-here"}, "Change this to a username or channel name": "it's-id-here", "Change this to a username or channel name": "it's-id-here-which-is-a-snowflake-number", "Change this to a username or channel name": "it's-id-here" }`;
	const usersParsed = JSON.parse(users);
	const token = "PUT.YOUR_DISCORD.TOKEN_HERE";
	a = document.createElement('div');
	a.style.position =
		'fixed';
	a.style.left = a.style.right = '30%';
	a.style.top = a.style.bottom = '10%';
	a.style.zIndex = '100000';
	a.style.background = '#313338';
	a.id = 'discord-messager';
	a.innerHTML =
		`<style>
		.header {
		  width: 100%;
		  height: 48px;
		  padding: 8px;
		  box-sizing: border-box;
		  justify-content: center;
		  box-shadow: 0px 3px 2px -2px #1d1d1d;
		}
	  
		.main-text {
		  font-size: 16px;
		  color: #f2f3f5;
		  text-align: left;
		  padding: 10px;
		  margin: 0;
		  display: inline;
		  font-weight: 600;
		  font-family: 'Noto Sans', 'Helvetica Neue', 'Helvetica', 'Arial', 'sans-serif';
		  line-height: 20px;
		}
	  
		.msg-area {
		  border-radius: 5px;
		  position: absolute;
		  bottom: 11px;
		  width: 98%;
		  left: 1%;
		  background-color: #383a40;
		  overflow-wrap: break-word;
		  padding-bottom: 11px;
		  padding-top: 11px;
		  white-space: break-spaces !important;
		  text-align: left;
		  height: 32px;
		}
	  
		.msg-input {
		  width: 100%;
		  display: block;
		  box-sizing: padding-box;
		  padding: 10px;
		  font-size: 14px;
		  margin: 50px auto;
		  border-radius: 6px;
		  border: 0;
		  outline: 0;
		  font-family: "gg sans", "Noto Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
		  font-weight: 400;
		  z-index: 1000;
		  bottom: -51px;
		  position: absolute;
		  background-color: #383a40;
		  color: #dbdee1;
		}
	  </style>
	  <div class="header">
		<svg padding="10px" width="24" height="24" viewBox="0 0 24 24" x="0" y="0" aria-hidden="true" role="img">
		  <path fill="#80848e" fill-rule="evenodd" clip-rule="evenodd" d="M5.88657 21C5.57547 21 5.3399 20.7189 5.39427 20.4126L6.00001 17H2.59511C2.28449 17 2.04905 16.7198 2.10259 16.4138L2.27759 15.4138C2.31946 15.1746 2.52722 15 2.77011 15H6.35001L7.41001 9H4.00511C3.69449 9 3.45905 8.71977 3.51259 8.41381L3.68759 7.41381C3.72946 7.17456 3.93722 7 4.18011 7H7.76001L8.39677 3.41262C8.43914 3.17391 8.64664 3 8.88907 3H9.87344C10.1845 3 10.4201 3.28107 10.3657 3.58738L9.76001 7H15.76L16.3968 3.41262C16.4391 3.17391 16.6466 3 16.8891 3H17.8734C18.1845 3 18.4201 3.28107 18.3657 3.58738L17.76 7H21.1649C21.4755 7 21.711 7.28023 21.6574 7.58619L21.4824 8.58619C21.4406 8.82544 21.2328 9 20.9899 9H17.41L16.35 15H19.7549C20.0655 15 20.301 15.2802 20.2474 15.5862L20.0724 16.5862C20.0306 16.8254 19.8228 17 19.5799 17H16L15.3632 20.5874C15.3209 20.8261 15.1134 21 14.8709 21H13.8866C13.5755 21 13.3399 20.7189 13.3943 20.4126L14 17H8.00001L7.36325 20.5874C7.32088 20.8261 7.11337 21 6.87094 21H5.88657ZM9.41045 9L8.35045 15H14.3504L15.4104 9H9.41045Z"></path>
		</svg>
		<h1 id="container" class="main-text">${usersParsed.Default.Name}</h1>
		<svg style="right:2%;position:absolute;" aria-hidden="true" role="img" width="24" height="24" viewBox="0 0 14 14">
		  <path class="close-button" id="close-button" fill="#b5bac1" d="M7.02799 0.333252C3.346 0.333252 0.361328 3.31792 0.361328 6.99992C0.361328 10.6819 3.346 13.6666 7.02799 13.6666C10.71 13.6666 13.6947 10.6819 13.6947 6.99992C13.6947 3.31792 10.7093 0.333252 7.02799 0.333252ZM10.166 9.19525L9.22333 10.1379L7.02799 7.94325L4.83266 10.1379L3.89 9.19525L6.08466 6.99992L3.88933 4.80459L4.832 3.86259L7.02733 6.05792L9.22266 3.86259L10.1653 4.80459L7.97066 6.99992L10.166 9.19525Z"></path>
		</svg>
		<div class="msg-area">
		  <textarea class='msg-input auto-expand' rows='1' data-min-rows='1' style="overflow:hidden;" id="msg-input" placeholder='Message #general' autofocus></textarea>
		</div>`;
	document.body.appendChild(a);
	function getScrollHeight(elm) {
		var savedValue = elm.value;
		elm.value = '';
		elm._baseScrollHeight = elm.scrollHeight;
		elm.value = savedValue;
	}
	function onExpandableTextareaInput({ target: elm }) {
		if (!elm.classList.contains('auto-expand') || !elm.nodeName == 'TEXTAREA') return;

		var minRows = elm.getAttribute('data-min-rows') | 0, rows;
		!elm._baseScrollHeight && getScrollHeight(elm);

		elm.rows = minRows;
		rows = Math.ceil((elm.scrollHeight - elm._baseScrollHeight) / 16);
		if (minRows + rows < 5) {
			elm.rows = minRows + rows;
			elm.style.overflow = "hidden";
		} else if (minRows + rows === 5) {
			elm.rows = 5;
			elm.rows = 5;
			elm.style.overflow = "hidden";
		} else {
			elm.rows = 5;
			elm.style.overflow = "auto";
		}
	}

	const textArea = document.getElementById('msg-input');

	textArea.addEventListener('keydown', async (event) => {
		if (event.key === 'Enter') {
			if (event.shiftKey) {
				const start = textArea.selectionStart;
				const end = textArea.selectionEnd;
				const value = textArea.value;
				textArea.value = value.substring(0, start) + '\n' + value.substring(end);
				textArea.selectionStart = textArea.selectionEnd = start + 1;
				event.preventDefault();
			} else {
				event.preventDefault();
				const message = textArea.value;
				try {
					const response = await fetch(`https://discord.com/api/v9/channels/${targetID}/messages`, {
						method: 'post',
						body: JSON.stringify({
							content: message
						}),
						headers: {
							"Content-Type": "application/json",
							"Authorization": token
						}
					});
					const data = await response.json();
					console.log(data);
					textArea.value = '';
				} catch (error) {
					console.error(error);
				}
			}
		}
	});
	function close() {
		document.getElementById('discord-messager').remove();
	}
	function buttonhover() {
		document.getElementById('close-button').fill = "#00000";
	}
	function buttonunhover() {
		document.getElementById('close-button').fill = "#fffff";
	};
	const container = document.getElementById('container');
	let targetID = usersParsed.Default.ID;

	container.addEventListener('click', (event) => {
		if (event.target === container) {
			for (const [key, value] of Object.entries(usersParsed).slice(1)) {
				const div = document.createElement('div');
				div.id = value;
				div.className = 'my-class';
				div.innerHTML = key;
				div.addEventListener('click', () => {
					targetID = div.id;
					let targetName = div.innerHTML;
					container.innerHTML = targetName;
					document.querySelectorAll('.my-class').forEach(e => e.remove());
				});
				container.appendChild(div);
			}
		} else {
			document.querySelectorAll('.user-option').forEach(e => e.remove());
		}
	});


	document.addEventListener('input', onExpandableTextareaInput);
	document.getElementById('close-button').addEventListener('click', close);
	document.getElementById('close-button').addEventListener('onmouseover', buttonhover);
	document.getElementById('close-button').addEventListener('onmouseleave', buttonunhover);
})();
  ```
</details>

## Drag and Drop Website Editor
| #dev #utility #editor | v1.0.0 | [⬆](#table-of-contents) |
| --- | --- | --- |

You can move any element you want around the web page! Really useful for web developers!
```javascript
javascript: var b = X = Y = T = L = 0;
document.addEventListener("click", function(a) {
	a.preventDefault()
}, !0);
document.addEventListener("mousedown", c);
document.addEventListener("touchstart", c);

function c(a) {
	a.preventDefault();
	a.target !== document.documentElement && a.target !== document.body && (b = Date.now(), a.target.setAttribute("data-drag", b), a.target.style.position = "relative", T = a.target.style.top.split("px")[0] || 0, L = a.target.style.left.split("px")[0] || 0);
	X = a.clientX || a.touches[0].clientX;
	Y = a.clientY || a.touches[0].clientY
}
document.addEventListener("mousemove", d);
document.addEventListener("touchmove", d);

function d(a) {
	if ("" !== b) {
		var e = document.querySelector('[data-drag="' + b + '"]');
		e.style.top = parseInt(T) + parseInt((a.clientY || a.touches[0].clientY) - Y) + "px";
		e.style.left = parseInt(L) + parseInt((a.clientX || a.touches[0].clientX) - X) + "px"
	}
}
document.addEventListener("mouseup", f);
document.addEventListener("touchend", f);

function f() {
	b = ""
}
document.addEventListener("mouseover", g);

function g(a) {
	a.target.style.cursor = "move";
	a.target.style.boxShadow = "inset lime 0 0 1px,lime 0 0 1px"
}
document.addEventListener("mouseout", h);

function h(a) {
	a.target.style.cursor = a.target.style.boxShadow = ""
};
```
