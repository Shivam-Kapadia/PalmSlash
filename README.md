# 🥷 Fruit Ninja — but you're the blade

A little Fruit Ninja clone I built that uses your **webcam and your index finger** instead of a mouse or a touchscreen. Point at the screen, swipe through the fruit, and watch it split apart. No controller, no keyboard — just your hand in the air.

It's one single `index.html` file. That's the whole game. Open it and play.

**▶️ Play it here:** https://shivam-kapadia.github.io/fruit-ninja/
*(your browser will ask for camera permission — that's the whole point, say yes)*

---

## What it does

- Tracks the tip of your **index finger** in real time and turns it into a glowing blade.
- Fruit fall from the top — 🍊 oranges, 🍅 tomatoes, 🍉 watermelons, 🍌 bananas, 🍇 grapes, 🍓 strawberries, 🍋 lemons. Slice them for points; they burst into juice and fly apart in two halves.
- You get **3 lives**. Let three pieces of fruit hit the floor and it's over.
- Once you cross **30 points**, **💣 bombs** start dropping in with the fruit. They've got an angry red glow. Slice one and you're instantly done — so for those, keep your hands to yourself.
- Your **high score** is saved locally, so you've always got a number to beat.
- There's a pause button if life happens mid-run.

## How to play

1. Open the link above (or the file locally — see below).
2. Allow the camera.
3. Stand back far enough that your hand is comfortably in frame, with decent lighting.
4. Hold up your index finger and **swipe through the fruit**. Dodge the bombs once they show up.

Works best when the room isn't too dark and your hand isn't lost against a busy background.

## Running it yourself

Because it needs the camera, it has to be served over `http://localhost` or `https://` — double-clicking the file won't work (browsers block the camera on `file://`).

Quickest way, if you have Node:

```bash
npx http-server -p 8000
```

Then open `http://localhost:8000`. Any tiny static server does the job.

## How it's built

Nothing heavy — it's deliberately a single file with no build step.

- **[p5.js](https://p5js.org/)** for the canvas, the fruit, the juice particles, and the blade trail.
- **[MediaPipe Tasks – Hand Landmarker](https://ai.google.dev/edge/mediapipe)** (running on the GPU) for the actual hand tracking. It hands back 21 points on your hand every frame; I use the index fingertip.
- A **One-Euro filter** to smooth the cursor — it kills the jitter when your hand is still but stays snappy when you swipe fast. This was the single biggest thing that made it feel good instead of janky.
- The look is a neon, Discord-flavoured dark theme — deep indigo, blurple, magenta.

A couple of things I had to fight with along the way, in case you tinker:
- The webcam feed is cropped to fill the screen, so the raw landmark coordinates don't line up with what you see — everything has to go through the same crop/mirror transform or the blade drifts off your finger.
- I nudged the tracking to be a bit more reachable toward the bottom of the screen, since that's where hands tend to slip out of the camera's view.

## Heads up

- It's a webcam toy, so the experience depends on your camera, lighting, and machine. On a decent laptop it runs smooth; on something older it might chug a little.
- First load pulls the tracking model (a few MB) from a CDN, so the very first "loading hand tracking…" takes a moment.

---

Built for fun. If you get a stupidly high score, I don't want to know about it. 🍉
