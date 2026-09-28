# 🎧 Hand DJ

A music player you control with your hands, built in a week-long AI workshop.

It works in two stages:

1. **The player** already works with the mouse and keyboard, and plays free music from the internet.
2. **Your AI** is trained by you in Teachable Machine and connected to the player so it understands hand gestures.

## Get started

1. Download this project: click the green **Code** button, then **Download ZIP**, and unzip it.
2. Open the folder in **VS Code**.
3. Right-click `index.html` and choose **Open with Live Server** (install the *Live Server* extension if you don't see it).
4. Press **Play**. 🎶

> You can also just double-click `index.html`, but Live Server is best once the camera is involved.

## Controls

| Action   | Mouse      | Keyboard |
|----------|------------|----------|
| Play     | ▶ Play     | Space    |
| Pause    | ⏸ Pause    | Space    |
| Stop     | ⏹ Stop     | S        |
| Next     | Next ⏭     | →        |
| Previous | ⏮ Previous | ←        |

Click any song in the list to play it.

## Music from the internet

Songs come from [Jamendo](https://www.jamendo.com), where every track is free Creative Commons music.

- Open `js/config.js` and paste the **Client ID** your teacher gives you (or get your own free one at [devportal.jamendo.com](https://devportal.jamendo.com)).
- Change `MUSIC_STYLE` to pick your music: `pop`, `electronic`, `rock`, `hiphop`, `lounge`, `happy`, `chillout`.
- No Client ID or no internet? The player uses two built-in backup songs instead.

The artist and licence show under the playlist for every song. Always give artists credit.

## Stage 2: connect your AI

### Train your model
1. Go to [teachablemachine.withgoogle.com](https://teachablemachine.withgoogle.com) → **Get started** → **Image Project** → **Standard**.
2. Make these classes, spelled exactly like this:

| Class      | Gesture                   |
|------------|---------------------------|
| `Play`     | ✋ open palm              |
| `Pause`    | ✊ fist                   |
| `Next`     | 👍 thumbs up              |
| `Previous` | 👎 thumbs down            |
| `Stop`     | ✌️ peace sign             |
| `Nothing`  | no hand, just you or the room |

3. Record at least 100 pictures for each class, with different hands, angles and lighting.
4. Click **Train model**, then **Export model** → **Upload my model**, and copy the link.

### Wire it up
1. Open `js/ai.js`.
2. Paste your link into `MODEL_URL`.
3. Complete the `onGesture()` function. This is where each gesture tells the player what to do:

```js
function onGesture(gesture) {
  if (gesture === "Play") { player.play(); }
  // ...add the other gestures!
}
```

4. Save, refresh the page, and press **Start AI**. Show your hand to the camera. ✋

## Project map

```
hand-dj/
├── index.html      the page
├── css/style.css   how it looks
├── js/config.js    ⚙️ your settings (music style, Client ID)
├── js/player.js    🎵 the music player (no need to change)
├── js/ai.js        🤖 YOUR AI CODE – this is where you work
└── solution/ai.js  finished version for teachers
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| No sound | Click **Play** once with the mouse. Browsers block sound until you interact with the page. |
| "Backup songs" message | Add the Jamendo Client ID in `js/config.js`. |
| "Could not load the model" | Use the link from **Upload my model**, not the page address. |
| Camera blocked | Click the camera icon in the address bar and allow it. Use Live Server. |
| AI never reacts | Check class names match exactly (`Play`, not `play`). Watch the "AI sees" line and confidence bars. |
| AI reacts by accident | Add more pictures to `Nothing`, or raise `CONFIDENCE` in `js/ai.js`. |

## Challenges 🚀

- Add a `Volume` gesture (hint: you'll need to add a new command to `player.js`).
- Change `HOLD_FRAMES` and `COOLDOWN_MS` in `js/ai.js`. What feels best?
- Train your model with a friend's hands. Does it still work? Why or why not?
- Make your own theme by changing the colours at the top of `css/style.css`.
