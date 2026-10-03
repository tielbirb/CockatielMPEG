![InShot GIF](./InShot_20261002_142918858.gif)
<p align="center">
  <img src="icon-512.png" width="128" alt="CockatielMPEG icon">
</p>

# 🦜 CockatielMPEG

FFmpeg for Android, with a GUI. Put text on a video with a few taps, or run your own FFmpeg commands and save them as presets.

**Version:** 0.0.0.2

## Two builds
| Build | Android | Look |
|---|---|---|
| `CockatielMPEG-0.0.0.2.apk` | 9+ | Command Prompt theme (black, gray and green) |
| `CockatielMPEG-0.0.0.2-legacy.apk` | 5+ (see note) | Old-style Holo dark UI |

You can install both side by side. On Android 5 and 5.1 the FFmpeg engine may fail to load, because its library officially needs Android 6+.

## Features
- **Simple mode:** upload a video or image, type text, and it's burned onto the video. Emoji, Arabic, Persian and Russian text work, and long text wraps. Images become 5-second videos.
- **FFmpeg command mode:** type your own arguments. Use `{input}` for the file you picked and `{output}` for the result. The app adds `-y` for you.
- **Presets:** create a preset (name, command, save folder), then pick it from **Select preset**. After a render, the video is saved into the preset's folder.
- **Dark progress bar** with a percentage, and a **Cancel** button
- **Live FFmpeg log** that ends with DONE, FAILED or CANCELLED
- **Built-in player** to watch the result, and a Save button (`Movies/CockatielMPEG`)
- **Languages:** English, Arabic, Russian, Persian and LOLCAT (pick in the app)
- **Credits** menu

## Example commands
Mirror a video:
```
-i {input} -vf hflip {output}
```
Make a test video without picking a file:
```
-f lavfi -i testsrc=duration=5:size=640x360:rate=25 -pix_fmt yuv420p {output}
```
Use `-c:v mpeg4` for video. The `libx264` encoder may not be included in these builds.

## Install
1. Open the **Actions** tab and open the latest green "Build APK" run.
2. Download the **CockatielMPEG-apks** artifact and unzip it.
3. Allow installs from unknown sources, then open the APK that matches your Android version.

## Build it yourself
**GitHub (easiest):** push this project to a repo. The workflow in `.github/workflows/build.yml` builds both APKs automatically.

**Android Studio:** open the folder, let Gradle sync, press Run.

**Command line:** with JDK 17, Android SDK and Gradle 8.7+:
```
gradle assembleDebug
```
The APKs land in `app/build/outputs/apk/debug/` and `legacy/build/outputs/apk/debug/`.

## Known bugs
- Output uses `mpeg4`, not `h264`, so files are bigger and lower quality.
- Image clips are fixed at 5 seconds, with no audio.
- The progress bar follows the input's length, so heavy commands (like audio stretching) can hit 100% early.
- Large videos can be slow or run out of memory.
- Rotating the screen may clear the log in the normal build.
- On Android 5 to 9, Save puts the video in the app's own Movies folder, not the public one.
- Translations are AI-made. Corrections welcome.

## Planned
- Built-in presets (GIF maker, audio extractor, compressor)
- Copy log button
- H.264 option
- Font, size, color and position options for text

## Credits
Made with Claude (Anthropic). Built with Kotlin, Jetpack Compose, Media3 ExoPlayer and FFmpegKit forks by moizhassankh and JamaisMagic. FFmpeg is licensed under the LGPL/GPL depending on the build.
