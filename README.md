# Campus Housing Availability Monitor

<img width="346" height="465" alt="image" src="https://github.com/user-attachments/assets/d25c576c-14cf-47e1-aa4e-85d6d9485596" />

Campus Housing Availability Monitor is an **unofficial** browser extension that
watches a signed-in StarRez housing page and alerts you via discord or desktop notifications when selected campus
options appear or disappear.

This release includes four campus filters:

**- Polytechnic
- Tempe
- Downtown Phoenix
- West**

The extension does not sign in for you, store a housing password, select a
room, or submit housing forms. The only thing is does it notify you.

## Requirements

- Chrome, Edge, or Opera
- A Windows computer that can remain awake
- Access to the supported StarRez **Choose My Community** page
- Discord webhook (optional)

## Install the extension

1. Download the project ZIP from GitHub and extract it.
2. Open the browser's extensions page:
   - Chrome: `chrome://extensions`
   - Edge: `edge://extensions`
   - Opera: `opera://extensions`
3. Turn on **Developer mode**.
4. Select **Load unpacked**.

<img width="96" height="32" alt="image" src="https://github.com/user-attachments/assets/b8e6da73-4fa0-4118-a225-e00455f685dd" />


6. Choose the extracted project folder containing `manifest.json`.
7. Pin **Campus Housing Availability Monitor** to the browser toolbar.

## First-time setup

### 1. Choose campuses

Open the extension and select the campuses to watch:

- Bright button: monitored
- Dark button: ignored

The choices can be changed at any time.

### 2. Set the check interval

Choose how often the housing page should refresh. Five minutes is a reasonable
starting point. The minimum interval is two minutes.

### 3. Set up Discord notifications (optional)

Desktop notifications work without Discord. To also receive Discord messages:

1. In Discord, open the text channel where alerts should be posted.
2. Open **Edit Channel > Integrations > Webhooks**.
3. Create a webhook and select **Copy Webhook URL**.
4. Double-click `start-discord-alerts.cmd`.
5. Keep the PowerShell window open.
6. Paste the webhook URL into **Discord notifications** at the bottom of the
   extension popup.
7. Select **Save**, then **Test Discord**.

Use a regular text channel. Forum and media channels are not supported.

Treat the webhook URL like a password. Anyone who has it can post to that
Discord channel. Delete and recreate the webhook if it is exposed.

### 4. Start monitoring

1. Sign in to the housing portal normally.
2. Open the **Choose My Community** page.
3. Open the extension while that page is the active tab.
4. Select **Start monitoring**.

The page refreshes immediately and is checked again at the selected interval.

## Everyday use

Keep these running:

- The browser
- The monitored housing tab
- `start-discord-alerts.cmd`, if using Discord

The browser may be minimized and the housing tab may remain in the background.
The computer must stay awake. Disable tab sleeping or memory saving for the
housing portal.

## Popup controls

- **Start monitoring**: begins watching the current housing page.
- **Open housing tab**: switches to the tab already being monitored.
- **Scan now**: checks the page immediately without waiting for the timer.
- **Test Discord**: sends a test message using the saved webhook.
- **Send current result**: sends the campuses found during the last check.
- **Restart monitor**: resets the comparison history and reloads the monitored
  tab.
- **Pause**: stops automatic refreshing until monitoring is started again.

## Alert behavior

The monitor compares each result with the previous result.

Examples:

```text
West is now available.
Downtown Phoenix is no longer available.
Tempe is now available. West is no longer available.
```

- An unchanged result does not send another alert.
- A campus that disappears generates a **no longer available** message.
- Polytechnic becoming available mentions `@everyone` in Discord.
- Other campus alerts do not mention `@everyone`.
- A notification means the campus appeared selectable when checked. It does
  not guarantee that space will remain available.

## Updating

To keep browser settings such as the webhook and campus choices:

1. Replace the files inside the existing extension folder.
2. Open the browser's extensions page.
3. Select **Reload** for Campus Housing Availability Monitor.
4. Restart `start-discord-alerts.cmd` if Discord notifications are enabled.

Avoid removing and reinstalling the extension unless saved settings should be
reset.

## Troubleshooting

### "Open the supported Choose My Community page before starting"

Open the signed-in housing results page, then select **Start monitoring** again.

### "Discord alerts are not running"

Double-click `start-discord-alerts.cmd` and keep its PowerShell window open.

### Discord test fails

- Confirm the webhook came from a regular Discord text channel.
- Save the webhook again.
- Restart `start-discord-alerts.cmd`.
- Confirm the webhook still exists in Discord.

### Monitoring stopped

- Confirm the housing tab is still open.
- Sign in again if the housing session ended.
- Prevent the computer from sleeping.
- Disable browser tab sleeping for the housing portal.

### No campus was detected

The page may currently have no matching campus cards. Select **Scan now** after
confirming that the **Choose My Community** page is visible.

## Privacy and security

- The extension reads visible text and `SELECT` controls only on supported
  StarRez pages.
- Housing credentials are never requested or stored.
- The Discord webhook is saved in the browser's local extension storage.
- The local Discord helper listens only on `127.0.0.1`, so other computers
  cannot connect to it.
- No webhook URL is included in this repository.

## Project files

- `manifest.json`: browser extension configuration
- `background.js`: monitoring, refresh, and notification logic
- `popup.html`, `popup.css`, `popup.js`: extension interface
- `start-discord-alerts.cmd`: Discord helper launcher
- `discord-alert-relay.ps1`: local Discord delivery helper
- `icons/`: original project icons

## Disclaimer

This is an unofficial community project. It is not affiliated with, sponsored
by, or endorsed by any university or housing portal provider. All third-party
names belong to their respective owners.
