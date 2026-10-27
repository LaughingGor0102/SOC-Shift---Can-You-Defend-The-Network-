# SOC Shift

**Can you defend the network?**

SOC Shift is a lightweight, browser-based cybersecurity learning game where you play as a Security Operations Center (SOC) analyst. Review simulated security alerts, inspect raw logs, and decide whether each event is safe, suspicious, or an attack—all before the timer runs out.

No cybersecurity experience is required: each decision comes with an explanation to help you learn as you play.

## Features

- **Three difficulty levels:** Easy, Normal, and Hard, with different decision timers.
- **Timed alert decisions:** Make a call before the countdown reaches zero.
- **Scoring and streak bonuses:** Faster correct answers and consecutive correct decisions earn more points.
- **Hints:** Reveal a clue at a point cost.
- **Daily Challenge:** Play a repeatable daily set of alerts.
- **Results and learning review:** See your score, accuracy, decision times, analyst tier, and explanations for the alerts.
- **Leaderboard:** Save scores and filter results by game mode and difficulty.
- **Responsive interface:** Designed to work on desktop and mobile-sized screens.
- **Simulated scenarios:** The game uses fictional activity and example IP address ranges; it does not connect to or defend a real network.

## How to Play

1. Open the game in your browser.
2. Choose a difficulty:
   - **Easy:** 35 seconds per alert
   - **Normal:** 25 seconds per alert
   - **Hard:** 15 seconds per alert
3. Select **Start my shift** or **Daily Challenge**.
4. Review the alert story and its raw log.
5. Choose one of the three actions:
   - **Safe** — the activity appears normal; dismiss the alert.
   - **Suspicious** — investigate further.
   - **Attack** — treat it as a real threat and block/escalate as appropriate to the scenario.
6. Read the feedback and explanation, then continue to the next alert.
7. After eight alerts, review your score and what you learned. Optionally save your result to the leaderboard.

You can use a hint during an alert, but doing so reduces the points earned for that answer. Leaving a shift early discards its progress.

## Scoring

The game contains eight alerts per shift. Points are awarded as follows:

| Outcome | Points |
| --- | ---: |
| Correct answer | 100 base points, plus a speed bonus of up to 50 |
| Correct-answer streak | Up to 40 additional points |
| Close answer | +30 |
| Incorrect answer | -50 |
| Time runs out | -25 |
| Hint used | Subtracts the selected difficulty's hint cost |

Hint costs are **10 points on Easy**, **20 points on Normal**, and **30 points on Hard**.

The final score determines your analyst tier:

| Minimum score | Tier |
| ---: | --- |
| 0 | Curious Newcomer |
| 300 | Junior Analyst |
| 600 | SOC Analyst |
| 900 | Senior Analyst |
| 1100 | Threat Hunter |

## Alert Scenarios

The game draws eight alerts from a larger set of simulated scenarios, including:

- Brute-force login attempts and password spraying
- Impossible travel and suspicious sign-ins
- Routine backups and authorised vulnerability scans
- Possible data theft and insider risk
- Malicious documents, phishing, and removable-media attacks
- Port scanning
- Unauthorised administrator account creation
- Ransomware activity
- DNS tunnelling
- Exposed cloud storage
- Approved software deployments and employee onboarding

The Daily Challenge uses a date-based shuffle and Normal difficulty, so players get a consistent daily alert order for that date.

## Getting Started

### Requirements

- A modern web browser with JavaScript enabled
- No build tools, package manager, or server-side application is required for local play

### Run locally

1. Download or clone this project.
2. Keep `index.html` and `config.js` in the same directory.
3. Open `index.html` in a modern browser.

For a local web server, you can also run:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

## Leaderboard Configuration

The game supports a local leaderboard and an optional Firebase Realtime Database leaderboard. Configuration is read from `config.js` using `window.SOC_CONFIG.databaseURL`. See `config.js` for the setting.

### Local-only leaderboard

Leave `databaseURL` as an empty string:

```js
window.SOC_CONFIG = {
  databaseURL: ""
};
```

Scores will be saved in the browser's `localStorage` on that device and browser. They are not automatically shared with other players or browsers.

### Global leaderboard

To enable the global leaderboard:

1. Create or select a Firebase project with Realtime Database enabled.
2. Configure a Realtime Database URL in `config.js`.
3. Configure database security rules deliberately before publishing the game.
4. Test saving and loading scores from the deployed site.

**Important:** `databaseURL` must be the Realtime Database instance URL used by the application, not the Firebase Console URL. The supplied `config.js` currently contains a Firebase Console URL, which is not the database REST endpoint the game expects. Replace it with the actual database URL (typically in the form `https://<database-name>.<region>.firebasedatabase.app` or `https://<project-id>-default-rtdb.firebaseio.com`, depending on the instance).

The game sends score records to the `/scores.json` endpoint and reads up to 200 records for the global leaderboard. Configure Firebase rules to match your intended access model; do not assume the current client-side implementation provides authentication, abuse prevention, or score validation.

## Project Files

| File | Purpose |
| --- | --- |
| `index.html` | Contains the game interface, styling, alert scenarios, gameplay logic, scoring, results, and leaderboard display. |
| `config.js` | Holds the optional Firebase Realtime Database URL configuration. |

## Technologies

- HTML5
- CSS
- Vanilla JavaScript
- Browser `localStorage` for local scores
- Optional Firebase Realtime Database REST API for global scores

Google Fonts are loaded for the interface typography, so an internet connection may be needed for the intended fonts. The game itself can otherwise be run as a local HTML page.

## Privacy and Safety

- Alert data is simulated; the game does not inspect or interact with your actual network.
- Example IP ranges are used in the scenarios.
- Local leaderboard entries remain in that browser's storage unless the user clears it.
- If a global Firebase leaderboard is enabled, score records may be sent to that database. Do not enter sensitive personal information as a leaderboard name.

## Troubleshooting

- **The page does not load correctly:** Make sure both `index.html` and `config.js` are present in the same directory and JavaScript is enabled.
- **The global leaderboard does not work:** Verify that `databaseURL` is the actual Realtime Database URL, the database is enabled, and its security rules permit the required reads and writes.
- **Scores only appear on this device:** This is expected when the database URL is empty or the global database cannot be reached.
- **Fonts look different:** Google Fonts may be unavailable offline; the browser will use fallback fonts.

## License

No license information is included in the supplied files. Add a `LICENSE` file and update this section if you intend to distribute the project under a specific open-source license.
