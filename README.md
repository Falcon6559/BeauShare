# BeauShare 2

High-quality screen recorder for Windows 11 with multiple save destinations and one-click YouTube upload.


## What's new in 2
**Stream to Twitch and YouTube** (Stream tab). Paste a stream key, press **Go live**. Both at once works too: BeauShare
encodes once and sends to every destination, so a dropped connection to one doesn't stop the other. Optionally it also saves
a full-quality recording at the same time (a separate encode, so your file isn't limited to stream bitrate).
Live bitrate, fps and dropped frames show under the button. Stream keys are stored in Windows Credential Manager and
are masked in any error messages.
- Twitch key: Twitch dashboard > Settings > Stream. YouTube key: YouTube Studio > Go live > Stream key.
- Settings that work well: 1080p at 30 fps and 6000 kbps (Twitch allows up to about 8000).

**Twitch chat in the app** (Stream tab). Type a channel and Connect to read chat with emotes, badges and sub alerts.
Pop it out into its own window. Signing in adds sending messages, fetching your stream key, setting your title and a viewer count.
One-time setup: go to dev.twitch.tv/console, register an application (Client Type **Public**, redirect URL
`http://localhost`), and paste its Client ID into BeauShare. Sign-in uses Twitch's device-code flow, so there is no secret to store.

**Custom stream panels** (Panels tab). Design on a 1920x1080 canvas with three panel types:
- **Text**: title and body with colours, size, alignment, rounded background. Tokens: `{uptime}` `{time}` `{date}` `{viewers}` `{title}`.
- **Chat**: live Twitch chat drawn on your stream, emotes included.
- **Image**: logos, frames, social badges (PNG with transparency works best).
Drag to move, drag the corner to resize, tick a panel to show it. Panels are composited into your stream, and into your
recordings if you leave "Also show panels in my recordings" on. **Export as Twitch panel image** saves any panel as a
320 px PNG for your channel's About section.

## Notes
- Panels cost a little CPU (the overlay is rendered 5 times a second). Disabled panels cost nothing.
- Only Twitch chat is built in. YouTube live chat isn't included.
- Creating a YouTube broadcast automatically isn't included. Use the stream key from Studio.


