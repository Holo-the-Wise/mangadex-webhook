# Updated MangaDex discord webhook with Google Script
Inspired [GuilhermeFaga's version](https://github.com/GuilhermeFaga/MangaDex-discord-webhook-with-Google-Script/) but implemented in MangaDex's v5 API.

A simple `Google Script` to which can be set up in a few minutes (no downloads required). This allows for automatic chapter updates from MangaDex to be forwarded to Discord via Webhooks.

The output in Discord:

![Example](https://i.imgur.com/7vcPLyU.png)


# Installation
## Prerequisites
- MangaDex Account
- Google Account

## Steps
### Creating an MDList
- Log into your account and create a **public** [MDList](https://mangadex.org/create/list)

![MDList](https://i.imgur.com/TjE5SXW.png)


- Add manga to be tracked to the list through the `Add to MDList` on the manga page

![Add to MDList](https://i.imgur.com/6Hr2Ui2.png)

### Creating a Google Sheets

- Create a [Google Sheets](https://sheets.new/)
- Create three sheets `feeds` and `webhooks` and `accounts` (Case sensitive)

![Add sheet](https://i.imgur.com/nRAvByr.png)

- Copy the `id` of your list (from the url)

![id](https://i.imgur.com/M688YF2.png)

- In the `feeds` sheet, paste the `id` in the first column (multiple feeds can be pasted; also note, columns other than the first can have any text, useful for identifying which ID is which)

![sneed feed](https://i.imgur.com/OTAxrJb.png)

- Open App Script through `Extensions` -> `App Script`

![App Script](https://i.imgur.com/lXI4WbA.png)

- Paste in [`Code.gs`](./Code.gs)

![Code gs](https://i.imgur.com/go9D1FH.png)

- Create a new `Script` called helper.gs
- Paste in the code from [`helper.gs`](./helper.gs)
- Create a new `Trigger`

![Triggers](https://i.imgur.com/QrgAYY0.png)

- With the following settings: `function: main`, `event source: Time-driven`, `type of time: Minutes timer`, `Select minute interval: Every 10 minutes`

![settings](https://i.imgur.com/kp31kas.png)

## Account Integration
- You can link it with your account's following feed
- However you will need to get your account's access token

### Access Token
**USE AT YOUR OWN DISCRETION**
- Make a new script called `access_token.gs`
- Paste in [`access_token.gs`](./access_token.gs)
- Input `username` and `password` for MangaDex
- Run the script
- Your token will be output in the console
- Remove your credentials from the script file

![token](https://i.imgur.com/7JDblWm.png)

- Once you have it, simply add it into `accounts` sheet

![account token](https://i.imgur.com/Iqz3Klw.png)

### Creating a Discord WebHook
- Open server settings

![server settings](https://i.imgur.com/BWruWR8.png)

- Go to `Integrations -> Webhooks -> New Webhook` and copy its url

![new webhook](https://i.imgur.com/q0InJpm.png)

- The url should look like: https://discord.com/api/webhooks/954780574910939239/8kOKc413vL0CvxqsYtA8CUtZ0Hse8U3fTWiNqv42NWUymxV0k4_Rqya6oeGeA48JgYks

- Paste the link into the first column in the `webhooks` sheet

![webhooks sheets](https://i.imgur.com/UeKDpTF.png)


## Customisation
- At the moment only the `Trigger Interval` and Target Language can be changed through modifying the script

### Target Language
- Modifying `line 5` of `Code.gs` will change the target language which the script detects

![lang](https://i.imgur.com/ZWl2VLR.png)

- `LANGUAGE` can be changed to any of the values specified by [MangaDex's API](https://api.mangadex.org/docs.html#section/Language-Codes-and-Localization)

![possible lang](https://i.imgur.com/pjmdZFd.png)

### Trigger Interval
- Modifying `line 2` of `Code.gs` will change the interval at which new chapters are polled (in minutes)
![TRIGGER_INTERVAL](https://i.imgur.com/OOy1VOe.png)
- **However, the trigger interval should also be modified in the `Google Script`**
![script image](https://i.imgur.com/v07ck0S.png)
