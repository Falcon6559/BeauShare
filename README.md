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

## Install it (recommended)
Double-click **Install BeauShare.bat**. It installs Python and FFmpeg if you don't have them (using winget), builds the app,
puts it in `%LOCALAPPDATA%\Programs\BeauShare` with FFmpeg bundled, adds Desktop and Start menu shortcuts, and launches it.
The first run takes about 5-10 minutes. If it installs Python, it asks you to close the window and run it once more.
After that you can delete this folder. **Uninstall BeauShare.bat** removes the app but keeps your settings and recordings.

Windows SmartScreen may warn about an unsigned app the first time: choose More info, then Run anyway.

## Make a setup wizard to share
Double-click **Build Setup Wizard.bat**. It builds the app, installs the free Inno Setup tool if needed, and creates
`Output\BeauShareSetup.exe`: a normal installer with a wizard, Start menu and optional Desktop shortcuts, and an uninstaller
(which asks whether to also remove your settings). Send that single file to people. It bundles FFmpeg, so they need nothing else.
Edit `BeauShare.iss` to change the version number or wizard options.

## Run from source (for developers)
Double-click `run.bat`. Press the red button, or **Ctrl+Alt+R** from anywhere, to start and stop.

## How it records
- Desktop Duplication capture (FFmpeg `ddagrab`), falling back to `gdigrab` automatically.
- Hardware H.264 encoding (NVIDIA NVENC, AMD AMF, Intel Quick Sync), tested at startup; CPU x264 as fallback.
- Quality presets Balanced / High / Ultra, up to 120 fps, optional downscale to 2160p/1440p/1080p/720p.
- Records to .mkv (safe if the PC crashes), then converts to a web-ready .mp4 when you stop.
- BeauShare hides its own window from recordings.
- If the wrong display is captured, pick the other one in the Screen list.

## Push to talk
Under Sound, tick **Microphone**, then **Push to talk**. The mic is silent until you hold your key.
Click the key button to choose any keyboard key or mouse button (Esc cancels). The default is Right Ctrl.
A badge on the Record screen shows "Mic live" while the key is held. The mic stays open for 0.2 s after you let go so
word endings aren't cut off. Computer sound is never gated.

## Editor
Open a recording with **Edit** (Library or the Record screen) or **Open video** on the Editor tab.
- Drag the lilac handles on the timeline, or press **I** / **O** at the playhead, then **Add clip**.
- Add as many clips as you like, reorder them, and select a clip to adjust it, then **Update**.
- **Export**: separate files, or join all clips into one video. With no clips added, it exports the current selection.
- **Accurate** re-encodes with your chosen encoder for frame-exact cuts. **Fast** copies the video without re-encoding,
  but cuts snap to keyframes (about every 2 seconds).
- Exports are saved beside the original and copied to your extra destinations. You can upload straight to YouTube after.
- Keys: Space play/pause, I start, O end, Left/Right 1 s, Shift+Left/Right one frame.

## Sound
Pick "Computer sound" and/or "Microphone". Windows doesn't expose desktop audio to FFmpeg directly:
enable **Stereo Mix** (Settings > System > Sound > More sound settings > Recording > right-click > Show disabled devices),
or install a virtual audio cable and select it.

## Save destinations
Settings > choose the main folder and add any number of extra folders (external drive, OneDrive, NAS).
Every finished recording is copied to all of them.

## YouTube setup (one time)
1. Go to console.cloud.google.com, create a project, and enable **YouTube Data API v3**.
2. Configure the OAuth consent screen (External), and add your Google account as a test user.
3. Create credentials > **OAuth client ID** > type **Desktop app**. Download the JSON.
4. In BeauShare: Settings > YouTube > **Add client_secret.json**, then **Sign in**.
5. Upload from the Record screen or Library: set title, description, tags, and privacy.

Note: videos uploaded by API projects that haven't passed Google's audit are locked to *private*.
To publish publicly, request an audit at support.google.com/youtube/contact/yt_api_form, or change the video's
visibility in YouTube Studio after uploading. Default quota allows about 6 uploads per day.

