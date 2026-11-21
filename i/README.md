# 💌 Love Confession Website

A single-page, romantic confession website. It opens with a sealed envelope, plays a song, walks through love messages and a love letter, and ends with the big question: **"Will you be mine?"**

Works for any partner (boyfriend or girlfriend) — the text is gender-neutral.


**Live page:** [https://claude.ai/artifact/ByGdoXUneSY7Vyj5fLD5oz](https://fests-i.vercel.app/)

---

## ✨ Features

| Section | What it does |
|---|---|
| **Envelope gate** | Full-screen envelope. Tapping it opens the site, bursts hearts and **starts the song** (the tap is what lets browsers autoplay audio). |
| **Hero** | Shimmering script title with a typewriter confession line. |
| **What I love about you** | 6 flip cards (English + Hinglish messages), tap to flip. |
| **Love letter** | A paper-style letter whose lines fade in one by one as you scroll. |
| **Moments I dream of** | 6 illustrated SVG scenes: moonlit walk, sunset, flowers, balloons, chai, rain umbrella. |
| **Reasons I like you** | "Tap for a reason" cycles through 10 reasons with a typewriter effect. |
| **The big question** | The **No** button runs away and changes text; the **Yes** button keeps growing. |
| **Celebration** | Yes triggers confetti hearts, a thank-you screen and a **Tell me on WhatsApp** button that also shares the site link. |

**Extras:** smooth scrolling, scroll progress bar, floating hearts canvas, click-to-burst hearts, dark/light theme toggle, 🔊/🔇 music button, animated gradient background, glass-style cards, fully responsive, respects `prefers-reduced-motion`.

---

## 🛠 Tech

- Single self-contained HTML file — no build step, no dependencies
- Vanilla JavaScript, CSS custom properties (theme tokens), Canvas 2D
- `IntersectionObserver` for scroll-reveal animations
- Google Fonts: Dancing Script, Playfair Display, Poppins
- Song embedded as base64 MP3 and played through a `Blob` URL

---

## 🎨 Customize

### 1. Names and WhatsApp number

Near the top of the main `<script>`:

```js
const C = { to: 'Jaan', from: 'Your Admirer', phone: '' };
```

- `to` – your partner's name (or nickname)
- `from` – your name
- `phone` – optional WhatsApp number, **country code + digits only** (e.g. `919876543210`). If empty, WhatsApp lets the user pick the contact.

### 2. Messages and reasons

Edit the arrays in the script:

```js
const M = [['Your Smile', 'Teri ek smile se ...'], ...];  // flip cards: [title, message]
const R = ['Teri hasi meri bad mood ki dawai hai.', ...];  // "reasons" list
```

The love letter text is plain HTML inside `<section id="letter">`.

### 3. Use your real photos

Replace the `<svg>` inside any `<figure class="ph">` with an image:

```html
<figure class="ph reveal">
  <img src="photos/1.jpg" alt="Us"
       style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover">
  <figcaption>Our first trip</figcaption>
</figure>
```

If you host the page yourself, keep the `photos/` folder next to the HTML file (or embed images as base64 for a one-file page).

### 4. Colors

Change the CSS variables in `:root` (light) and in the dark blocks:

```css
--rose:#f0467f;  --gold:#e8a06a;
--g1:#ff7eb3;    --g2:#b660e8;   /* button + title gradient */
--bg:#fff0f7;    --bg2:#ffd9ec;  /* background */
```

### 5. Change the song or start time

The song is stored in `const SONG="..."` (base64). To make your own:

```bash
# Start at 0:20, fade in, compress to 128 kbps (keeps the page light for mobile data)
ffmpeg -ss 20 -i original.mp3 -vn -af afade=t=in:st=0:d=0.4 \
       -c:a libmp3lame -b:a 128k -ar 44100 song.mp3

# Convert to base64
python -c "import base64;print(base64.b64encode(open('song.mp3','rb').read()).decode())"
```

Paste the output between the quotes of `const SONG="..."`. Change `-ss 20` to any start second. The loop restarts from that same point.

> 💡 Keep the file small — a 2–3 MB song is ideal. Very large audio makes the page slow to open on mobile.

---

## 🚀 Run or host it

- **Locally:** open the HTML file in any modern browser.
- **Free hosting:** drag-and-drop the file to [Netlify Drop](https://app.netlify.com/drop), or push it to GitHub and enable GitHub Pages.
- Then send the link to your partner 💞

---

## ⚠️ Good to know

- **Autoplay:** browsers block sound until the user taps. That is why the song starts from the envelope tap. If it doesn't play, the 🔇 button lets the user start it.
- **Personalization is in the file:** names and settings are not stored in the link, so edit `C` before sharing.
- **Internet:** Google Fonts need a connection; without it, the page falls back to system fonts.

---

## 📁 Structure

```
confession.html   ← the whole site (HTML + CSS + JS + embedded song)
README.md         ← this file
```

---

Made with all my love ♥
