# polaroid-obs-plugin
This a Polaroid plugin for OBS and StreamerBot, which let's users create polaroid pictures of the streamer and uploads them to Discord.

![](polaroid_sample.gif)

This plugin is heavily inspired from a free plugin previously developed by [Andilippy and StreamUP](https://streamup.tips/product/polaroid-picture). The Streamer.Bot code was developed on that plugins base. It was adapted in some major parts
 - stream lined code and OBS implementation
 - photo development effect
 - support for OBS 29+
 - new countdown effect with flash effect
 - pictures are ejected from a Polaroid camera
Feel free to check out there other plugins or to buy them a coffee via [Ko-Fi](https://ko-fi.com/streamup).

## Requirements
1. [OBS](https://obsproject.com/) (tested with version 29)
2. [StreamerBot](https://streamer.bot/) (tested with version 0.2.1)
3. [Exeldro's Source Clone plugin](https://obsproject.com/forum/resources/source-clone.1632/)
4. [Exeldro's Move Plugin](https://obsproject.com/forum/resources/move.913/)
5. [Exeldro's freeze filter plugin](https://obsproject.com/forum/resources/freeze-filter.950/)
6. [Exeldro's Scene Copy plugin](https://obsproject.com/forum/resources/source-copy.1261/)

## Installation
### Preperations
1. Download all files from the [obs](https://github.com/einfloh/polaroid-obs-plugin/tree/initial-release/obs), [StreamerBot](https://github.com/einfloh/polaroid-obs-plugin/tree/initial-release/streamerbot) and [resources](https://github.com/einfloh/polaroid-obs-plugin/tree/initial-release/resources) folders.
2. Move this files from your download folder to your prefert location on your PC. Remember this folder as you'll need it further down the line.
3. Download and install all programms listed under requirements, if not done already.

### OBS - Scene Import
1. Add the scene collection [obs-polaroid-plugin.json](https://github.com/einfloh/polaroid-obs-plugin/blob/initial-release/obs/obs-polaroid-plugin.json) to your OBS.
2. Select the newly imported scene collection named `obs-polaroid-plugin` under `Scene Collection`.
3. Go to `Tools > Source Copy > [O] Polaroid > Copy Scene`.
4. Go back to your normal scene collection and insert the previously copied scene via `Tools > Source Copy > Paste Scene`.
5. Go back to the scene collection named `obs-polaroid-plugin`.
6. Go to `Tools > Source Copy > [O] Polaroid-Picture > Copy Scene`.
7. Go back to your normal scene collection and insert the previously copied scene via `Tools > Source Copy > Paste Scene`.

### OBS - Scene Setup
1. Adapt under `[O] Polaroid` the source `[P] Polaroid-Countdown` to point to the file `countdown.webm` from `resources`.
2. Adapt under `[O] Polaroid` the source `[P] Polaroid-Camera` to point to the file `Camera.png` from `resources`.
    1. Both sources `[P] Polaroid-Camera` should point to the same file. The second camera is there so the `[O] Polaroid-Picture` is ejected from the photo slot of the `[P] Polaroid-Camera`.
3. Adapt under `[O] Polaroid-Picture` the source `[P] Polaroid-Frame` to point to the file `picture-frame.png` from `resources`.
4. Adapt under `[O] Polaroid-Picture` the source `[P] Camera` to point to your normal camera source.
    1. I recommened to use a camera helper scene. That makes it easier to work with other camera based plugins in the future. You can also just directly insert your normal camera source.
5. Add a `source clone` source pointing to `[O] Polaroid` to the scenes were you want to show the polaroid effect.

After this, you should be able to dry test the plugin. Try to enable the sources in `[O] Polaroid` and verify that the camera, countdown and picture are correctly shown as intended.

### Streamer.Bot - Setup
1. Open Streamer.Bot.
2. Import the content of the file `action.txt` from [streamerbot](https://github.com/einfloh/polaroid-obs-plugin/tree/initial-release/streamerbot/action.txt) into your Streamer.bot.
3. Adapt `pictureBasePath` in the `Take_Polaroid_Picture` action to point to a folder where the polaroid picture shall be outputed to.
4. Adapt `pictureName` in the `Take_Polaroid_Picture` action to your liking, but I would recommened you to leave it as it is.

### Discord - Setup
1. Go to your Discord server and add a new channel where the polaroid picture shall be posted to.
2. Go into your `Server Settings` under `Integrations > Webhooks` and add a new Webhook.
    1. Select channel previously added.
    2. Optional: Give your new Webhook a good name (the pictures will be posted under that name) and define a suitable picture.
3. Copy the Webhook URL, got to Streamer.Bot and insert the URL into the `Take_Polaroid_Picture` action under `discordWebhookURL`.

You don't need to setup the Discord integration if you don't want to. Just disable it in Streamer.Bot via `uploadToDiscord` set to `False`. You can also disable the rich text under the uploaded picture via `enableRichTextDiscord` so only the picture gets posted without any viewer information.

The plugin is now fully setup. To trigger the plugin via Streamer.Bot, you can either add a command under `Commands`, a `Channel Point Reward` under `Platforms > Twitch > Channel Point Rewards` or any other way suiting your use case.
