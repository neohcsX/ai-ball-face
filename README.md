# AI Ball with a Face — Firmware 9.1.0

XiaoZhi voice assistant with an animated face instead of the emoji display.

[![Watch the video](https://img.youtube.com/vi/jVZ4FdJq-Uc/hqdefault.jpg)](https://www.youtube.com/shorts/jVZ4FdJq-Uc)

**Only for:** SpotPear ESP32-S3 AI ball (ESP32-S3 **N16R8**, round 1.28" display 240×240,
touch, speaker). This file will not run on other devices.

File: `ki-kugel-9.1.0-2026-11-12.bin` (single file, written at address 0x0)
SHA-256: `5a82fbdd70b7f29b4c65a51b770db24cc2b5571c9e194aaad7335aa9bb5c6df0`

Update file: `ki-kugel-9.1.0-2026-11-12-update.bin` (keeps settings, written at address **0xd000**)
SHA-256: `2bfd184ff695c90df0c3a8be31a4e616f9cb42d43ddfa584fdb2f14013099744`

## Flashing

**Note:** Flashing the full file also erases stored settings (Wi-Fi, activation, saved looks).
The ball starts like new afterwards. To keep them, see "Update without losing data".

### Option A — in the browser (easiest)
1. Open Chrome or Edge: <https://espressif.github.io/esptool-js/>
2. Connect the ball via USB-C (data cable, not a charge-only cable), click **Connect**,
   choose "USB JTAG/serial debug unit".
3. Flash address `0x0`, select `ki-kugel-9.1.0-2026-11-12.bin`, click **Program**.
4. After "Done", unplug the ball briefly or press reset.

Trouble?
- Firefox and Safari cannot do this, use Chrome or Edge.
- No device in the list: try another cable or USB port. On Linux your user must be in the
  `dialout` group.
- "Failed to connect": another program (serial monitor, Arduino IDE) is using the port — close it.

### Update without losing data
If an earlier version of **this** firmware is already on the ball, the update file keeps Wi-Fi,
activation and saved looks. Same as above, but flash address **`0xd000`** and file
`ki-kugel-9.1.0-2026-11-12-update.bin` — **never write it at 0x0**, the ball would not boot
(then simply flash the full file at 0x0). Command line:
`esptool --chip esp32s3 write-flash 0xd000 ki-kugel-9.1.0-2026-11-12-update.bin`
Coming from the original/factory firmware or in case of trouble, always use the full file.

### Option B — command line
```bash
pip install esptool
esptool --chip esp32s3 write-flash 0x0 ki-kugel-9.1.0-2026-11-12.bin
```
(The port is usually found automatically; otherwise add `-p /dev/ttyACM0` or `-p COM5`.)

## First start
1. The ball opens a Wi-Fi network "Xiaozhi-…". Connect with your phone and enter your
   own Wi-Fi in the browser page. It remembers up to 10 networks; add another one via the menu
   (extras → wifi, tap twice).
2. It then shows an **activation code**. Create an account at <https://xiaozhi.me> and add the
   device with that code. Language, voice and role are set there. The ball understands requests in
   English as well as German; its short acknowledgements ("sure" / "gern") follow the language you speak.
3. Wake it with **"Jarvis"** (clearly, from 0.5–1 m) or tap the display briefly. With music or TV playing
   in the room the wake word easily gets lost — then just tap. (Up to 9.0.0 the wake word was "Hi ESP",
   which the ball hardly ever recognised.)

## What it can do (examples, just say it)
- **Colours:** 33 colours (e.g. gold, turquoise, navy, rose, olive) for eyes, ball, background,
  glasses, brows, mouth and pupils
- **Looks:** "make the eyes blue", "cute look", "glasses on", "ball red", "shoes off",
  "2D mode", "keep still" / "move again" (head, gaze and zooming stop; in 2D the face then fills the whole screen), "randomize your look", "remember this" / "save as outfit …", "put on outfit …"
- **Looks (built in):** robot, visor, cute, box, **cat**, pill, pixel, egg, hex, **otto**, **capsule**, **alien**, **alien green**, **droplet**, **flame**, **gas flame** — "droplet look": a sky-blue water-drop head with round white eyes and rippling water inside; tap or swipe it and ripples start where your finger is, a fly or butterfly landing on it makes a ripple too, and the drop tilts with the head. "flame look": the head burns like an old demo fire effect ("gas flame": the same in blue). Blow into the microphone and the flames flicker and duck; blow long and hard and the flame goes out with a puff of smoke, then flares up again. Flies and butterflies that come too close burn up (it is sad about that — or gloats, depending on its character). While asleep the fire turns into glowing embers (the gas flame into a small ring of blue flames), blowing makes the embers glow brighter. "alien look" brings slanted black almond eyes on a white drop-shaped head ("alien green": green head, no glow). "capsule look" brings tall,
  glowing cream-white eyes (an arc when happy, with blushing cheeks). "otto look" brings light-blue
  boxy eyes with scanlines and a small filled mouth (line, smile, mound or small "o" depending on
  the mood, opens while talking). "be a cat" brings almond eyes
  with slit pupils, cat ears on the ball (in 2D mode two strokes above the eyes), a snout with whiskers and paws (as shoes and instead of hands); now and then it meows, and it plays with a ball of yarn instead of the football
- **Single parts:** "cat ears / round ears / ears off", "orange ears", "ears behind the head",
  "cat snout", "whiskers on/off", "pink whiskers", "wireframe eyes" / "wireframe eyes with outline" ("3D" back), "paws instead of hands", "boots on", "hexagon eyes", "slit pupils",
  "make the pupils smoother", "smooth eye edges"
- **Mouth/brows:** "mouth on", "filled mouth", "mouth higher/wider", "round eyebrows", "brown brows"
- **Timer / alarm:** "timer 5 minutes", "remind me in 20 minutes about the tea", "wake me at 7", "is an alarm set?" — a running timer shows a
  ring, a set alarm a faint light-blue ring like a 12-hour dial (dot = alarm time). A running timer survives a restart of the ball
  (not a power loss)
- **Gestures & fun:** "dance", "kick the ball", "play with the ball", "juggle", "wave",
  "go to sleep" (it snores then; while asleep, a tap wakes it more reliably than "Jarvis"), "soap bubbles", "let a fly / butterfly fly", "draw a heart / star",
  "bounce your eyes", "frog eyes", "yawn", "stretch", "jump", "get scared" / "boo", "hop back" — the whole ball squashes, hops and
  stretches (when happy it hops, a bang makes it hop back)
- **You draw for it:** "I want to draw something for you" — draw with your finger on the display,
  then ask "what did I draw?"; it looks at the picture and guesses
- **It draws for you:** "draw me a cat / a car / Pac-Man" — the AI plans a line drawing and the
  ball paints it with a glowing pen. "Draw me a surprise" = guessing game ("guess what it is!").
  "Look at your picture again" = it has its own drawing checked and offers to improve it
  (drawings are childlike and don't always work — that's part of the fun)
- **It composes:** "play me a song", "make a melody with glockenspiel" — the AI invents the notes,
  the ball plays them (8–30 s, chiptune or glockenspiel); sometimes it hums them again later
  — it often adds a matching melody to a drawing
- **Gallery:** "show me your pictures" — it redraws its latest pictures (until restart), each with
  its melody
- **Tap games:**
  - "let's play Simon" — four coloured buttons at the edge; it plays a tone sequence, you tap it back
    (the whole quarter of the screen counts); one more tone each round
  - "shell game" — it shows the ball under one of three cups and shuffles; tap the right one
    (left/middle/right). Faster every round
  - "tic-tac-toe" — you are the red X, it is the yellow O; the next game follows right away (score on top)
  - "whack-a-mole" — tap the moles for 30 seconds, faster and faster
  - "reaction test" — tap as soon as the edge turns green; 5 tries, then the average in milliseconds
  - "memory" — 8 face-down cards in a circle around it; find the pairs with as few tries as possible
  - "balloon" — blow into the microphone to inflate it; stop before it bursts
  - "rock paper scissors" — against it, first to win 3 rounds
  - "guess the number" — you think of a number, it guesses and you say higher/lower
  - "snake" — the snake runs on a round field; swipe (or tap in the direction) to steer, food makes it
    longer and faster, hitting the edge or itself ends it
  - "let's play ping pong" (or menu → games → vs me → "round" / "square") — its eyes turn into paddles,
    the pupils fly together into the ball. Round in the face area: your paddle is the right arc,
    move it with a finger near the edge; "square" gives the classic field in the face area (right
    paddle, finger up/down). First to 5 points, then it turns back into a
    face. Without a finger it plays both sides; when bored it also plays alone — a finger in the field joins
    in, talking to it ends it. Classic Pong beeps
  - **Quit:** press the display for 1 second
  - It hangs up by itself for the game; talking to it ("Jarvis") ends the game, tic-tac-toe also after
    20 s without a move
  - **Records** are saved (new record: "NEW RECORD!" + applause); "what are my records?",
    "delete the whack-a-mole record" / "delete all records"
- **Menu (without voice / without internet):** long press on the display. Three fields:
  **games** (solo | vs me), **extras** (clock, Wi-Fi setup, movement on/off, 2D ears on the eyes / on the head, glow low/mid/high, top bar as text or icons), **settings** (volume, effects,
  brightness). The centre goes back or closes. The games run entirely on the ball
- **Volume:** "effects quieter / off" (ball, babbling, play sounds … separate from speech and
  alarm), "show the volume permanently", "show the battery level", "show the Wi-Fi signal"
  (small Wi-Fi icon at the right edge: white = good, orange = weak, red = very weak)
- **Weather:** tell it your city once ("my city is Hamburg") — it then fetches the weather itself
  every 30 minutes (Open-Meteo). "Show the weather clock" = time, weather symbol, temperature,
  today's high/low and chance of rain. When the AI tells the weather, the face reacts: rain or snow
  falls over the face, gusts blow past when windy, it sweats when hot and shivers when cold. When it
  rains outside, it now and then looks up by itself
- **Character:** it has a mood of its own — "be grumpy / cheerful / shy / sleepy / normal" changes
  how it talks and moves (kept after a restart). It has a favourite colour and look and one colour
  it dislikes ("what is your favourite colour?"), knows the time of day, how long you were away and
  what it did meanwhile ("what did you do while I was away?"), and knows how it looks right now.
  **It gets to know you:** it counts your talks, games and strokes, remembers your favourite game, the
  usual time of day and a few shared moments, and greets you happily after a longer break (never with
  reproaches). It remembers wins and losses — after a losing streak it looks suspicious, after a winning
  streak confident. Now and then it **wants to play** itself: it looks at you, a gamepad bubble appears,
  and it starts Pong on its own — put a finger on it to join in
- **On its own:** babbles now and then, keeps itself busy when bored (ball, bubbles, fly,
  butterfly, drawing, music, game sounds, tic-tac-toe against itself, whack-a-mole on its own — a tap
  still wakes it as usual), yawns when falling asleep and stretches when waking up, **dances along** when
  music with a clear beat plays in the room (head and feet on the beat)
- **Clock:** swipe vertically across the display (flip clock → analog → weather clock → face);
  swipe horizontally = stroke it (several quick swipes = tickle), long press = menu

## Notes
- The firmware reports version 9.1.0 so that XiaoZhi does **not** replace it automatically with
  the original firmware. To go back to the original, flash that again.
- Conversations run through the xiaozhi.me servers (cloud). Face, sounds and animations run
  entirely on the ball. A drawing you made is only sent to the server (image recognition) when
  you finish it or ask about it — it is not stored on the ball. It only sends its own drawings
  when you ask it to check them.
- Weather: once a city is set, the ball sends only its coordinates to api.open-meteo.com every
  30 minutes (plain HTTP, no account). Weather data by Open-Meteo.com (CC BY 4.0).
- The ball announces itself every 2 seconds on your own Wi-Fi (UDP port 4210, local network only,
  not the internet) with name, look and mood — for playing together with other faces. From other
  devices it only accepts look commands (look, colour, pupil, brows, mouth).
- Licence notices for the included software (XiaoZhi, ESP-IDF, LovyanGFX and others):
  `LICENSES.txt` (German: `LIZENZEN.txt`) — please always include it when passing the firmware on.
