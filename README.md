# Bedside Comms

**A free communication board for hospital patients who can't speak — driven by eyes, mouth, blink, a switch, or touch. Runs in the browser on almost any smartphone or tablet. No app, no account, no cost, no network required after first load.**

Built by an ICU nurse who was tired of watching intubated patients try to mouth words at 3am while commercial eye-gaze devices cost $3,000–$15,000 and take weeks to arrive.

## Try it

Open the page on a phone or tablet (it must be served over **HTTPS** for the camera modes — see Hosting below). Prop the device where the patient can see it — a cheap gooseneck phone clamp on the bed rail works well. Pick an input mode on the setup screen. That's it.

## How it works

The screen shows a few large coloured zones. The patient indicates *which zone* holds what they want; the zone splits into more choices; two or three steps later a full sentence is spoken aloud by the device.

**Coarse in, precise out.** The board never asks for pointing accuracy. Any signal that can answer *"this one, not those"* drives the whole thing — which means it degrades gracefully from working eyes all the way down to a single reliable blink.

### Input modes (pick per patient, per shift)

| Mode | The patient... | Good for |
|---|---|---|
| **Touch** | taps zones directly | learning the board, carer-assisted use |
| **Auto-scan + tap** | taps anywhere when the right zone lights up | limited reach, gross motor only |
| **Switch / keyboard** | presses one button (Space/Enter) when the right zone lights up | any Bluetooth accessibility switch — they present as keyboards, so a ~$30 switch just works |
| **Blink-dwell** (camera) | closes their eyes and holds when the right zone lights up | one reliable movement is enough |
| **Eye direction** (camera) | looks right = next, looks left = previous, closes eyes = pick | decent eye control, fastest camera mode, no calibration needed |
| **Mouth** (camera) | opens mouth + holds = pick, big smile = back | patients who can shape words silently; works around an endotracheal tube |

### Emergency fast-path

A deliberate **triple blink** (configurable: double / off) from anywhere in any camera mode triggers a full-screen flashing alarm, a repeating beep, and a spoken *"Please call the nurse — urgent."* The **CAN'T BREATHE** button does the same. Safety-critical needs never sit three menus deep. The alarm is dismiss-by-carer only.

### Also built in

- Screen wake lock — the board doesn't fall asleep mid-shift
- Face-lost detection — scanning pauses if the patient turns away, so nothing gets selected by accident
- Settings persist per device — set up each ward iPad once
- Carer re-entry — triple-tap the status text to reopen setup; patients can't accidentally exit
- Installable PWA — after the first load everything (including the face-tracking model) is cached and works **fully offline**
- Sentence bar with repeat — answers to "did you say pain?" are one tap away

## Privacy

All face processing happens **on the device** (MediaPipe Face Landmarker, running locally in the browser). No video, image, audio, or text is recorded, stored, or transmitted — by design there is no server to send anything to. Turn the network off after loading and everything still works.

## Device support

Roughly: iPhone 6s and newer (iOS 14.3+), and any Android phone/tablet with Chrome from ~2019 onward. Camera modes require the page to be served over HTTPS.

## Hosting your own copy

It's four static files — any static host works.

**GitHub Pages (free, ~5 minutes, no command line):** fork or create a repo, upload `index.html`, `sw.js`, `manifest.json`, `icon.svg`, then Settings → Pages → deploy from branch `main`, folder `/ (root)`. Your board is live at `https://<you>.github.io/<repo>/`.

**Netlify Drop:** drag the folder onto https://app.netlify.com/drop.

## Ward / clinical notes

- This is an **assistive communication aid** in the same category as a paper letter board — it is **not a medical device**, makes no measurements, and must never replace clinical observation, nurse-call systems, or monitoring.
- On iPads, pair it with **Guided Access** (Settings → Accessibility) to lock the device to the board.
- Input mode is a per-shift decision — the same patient varies day to day. Reassess like you'd reassess anything else.

## Contributing

Issues and PRs welcome. The entire app is one HTML file on purpose — keep it that way. Particularly wanted: translations of the vocabulary tree, vocabulary suggestions from nurses/SLTs in other specialties (paeds, palliative, stroke), and testing reports from real hardware.

## License

MIT. Use it, change it, ship it, sell it, we don't care — just get it to a patient who needs it.
