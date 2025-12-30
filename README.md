# OBS Twitch stylized chat CSS

To use twitch chat window directly without any third-party software

Solution works for Twitch chat only.

Please follow instructions below to get transparent chat widget in your OBS translation without third party software:

1. Get your embedable chat window URL: 
  ```
  https://www.twitch.tv/embed/<channel>/chat?parent=<parent>
  ```
  where `<channel>` is your channel name, `<parent>` is "localhost". For me it is
  ```
  https://www.twitch.tv/embed/boggartmob/chat?parent=localhost
  ```
  [Twitch documentation](https://dev.twitch.tv/docs/embed/chat/)
  
2. Add "Browser" widget to your OBS scene for chat window, tune its size.
3. Use chat URL from (1.) for "Browser" widget "URL" property.
4. Use following CSS for "Browser" widget "Custom CSS" property:

```css
* {
	--text-color: white;
	--text-stroke-color: black;
	--text-stroke-size: 1px;
	--color-background-body: transparent;
	--color-background-base: transparent;
	--color-background-alt: transparent;
	--color-background-float: transparent;
	background: transparent;
	font-family: "Calibri" !important;
}
.tw-root--theme-light .chat-room {
	background: transparent;
}
.stream-chat-header, #chat-room-header-label, .chat-input {
	display: none !important;
}
.chat-scrollable-area__message-container {
	line-height: 1.5em;
}
.chat-line__message, .chat-line__moderation, .chat-line__status {
	padding: unset;
}
div[data-a-target="consent-banner"], div[data-a-target="chat-welcome-message"], div[data-a-target="moderation-action"], .chat-line__status, .chat-room__notifications, .community-highlight-stack__scroll-content--disable{
	display: none;
}

/* literally just  the : */
.chat-line__message {
	color: var(--text-color);
}

/*
	chat author styling
	effect i stole from https://stackoverflow.com/questions/76921116/how-can-i-give-text-a-rainbow-color-effect
*/
.chat-author__display-name{
	display: inline-block;
	background: linear-gradient(45deg,#ff7e5f,#feb47b,#ffed86,#9feb8f,#5fbfff,#9b8eff);
	background-size: 700% 700%;
	color: transparent;
	-webkit-background-clip: text;
	background-clip: text;
	-webkit-text-fill-color: transparent;
	animation: grad 3s linear infinite alternate;
}
@keyframes grad{
	0%{
		background-position:0% 50%}to{background-position:100% 50%
	}
}

/*
	message text styling
	effect i stole from https://prismic.io/blog/css-text-animations#8-neon-glow
*/
.text-fragment, .chat-line__message--emot {
	color: var(--text-color);
	text-shadow: 0 0 5px #ff005e, 0 0 10px #ff005e, 0 0 20px #ff005e, 0 0 40px #ff005e, 0 0 80px #ff005e;
	animation: glow 1.5s infinite alternate;
}
@keyframes glow {
	0% {
			text-shadow: 0 0 5px #ff005e, 0 0 10px #ff005e, 0 0 20px #ff005e, 0 0 40px #ff005e, 0 0 80px #ff005e;
	}
	100% {
			text-shadow: 0 0 10px #00d4ff, 0 0 20px #00d4ff, 0 0 40px #00d4ff, 0 0 80px #00d4ff, 0 0 160px #00d4ff;
	}
}

/*
	came to me in a weird dream
*/
button:has(img[alt="Broadcaster"])::before {
	content: "🐴";
}
button:has(img[alt="Moderator"])::before {
	content: "🦄";
}
button:has(img[alt="Chat Bot"])::before {
	content: "🤖";
}
button:has(img[alt="Prime"])::before {
	content: "🍎";
}
button:has(img[alt="Subscriber"])::before {
	content: "🥕";
}
img[alt="Broadcaster"], img[alt="Prime"], img[alt="Subscriber"], img[alt="Moderator"], img[alt="Chat Bot"] {
	display:none;
}
```

<img src="https://github.com/user-attachments/assets/6c8792e6-fec4-4870-9cab-f72b097218e9" width="75%"/>

5. Click OK and enjoy.

6. You can tune font style updating very first section of the CSS, following line:
```css
font-family: "Calibri" !important;
```

7. You can adjust font color changing following variable:
```css
--text-color: white;
```
Replace `white` with any color you want including hex notation like `--text-color: #FF00FF;`

8. Can use any CSS effects for the Chat Messages and Chat Author sections, as i'm using the "important" flag sparingly. 👀👆

9. I'm using emojis as replacements for the standard twitch icons, but I suspect It'tl work with base64 encoded images as well.

10. I would also reccomend using a 16px crop on the right+bottom to hide the scrollbar, and a stroke-glow filter for a text shadow.

#OBS #chat #widget #transparent #css #transparentchat #chatcss #obschatwidget
