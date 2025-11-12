

Make cards glow and react to your mouse with dynamic angle-based gradients!

---

## 🧠 JavaScript (React + useRef)

```js
const handleMouseMove = (index) => (e) => {
  const card = cardRefs.current[index];
  if (!card) return;

  const rect = card.getBoundingClientRect();

  const mouseX = e.clientX - rect.left - rect.width / 2;
  const mouseY = e.clientY - rect.top - rect.height / 2;

  let angle = Math.atan2(mouseY, mouseX) * (180 / Math.PI);
  angle = (angle + 360) % 360;

  card.style.setProperty('--start', angle + 60);
};
```

✅ This calculates the angle from the card center to the cursor and applies it as a CSS variable.

---

## 🎨 CSS Styling for Glow

```css
.card {
  position: relative;
  --start: 0deg;
}

.glow {
  position: absolute;
  inset: 0;
  border-radius: inherit;
  pointer-events: none;
  z-index: -1;
  background: conic-gradient(
    from calc(var(--start) * 1deg),
    #0ff,
    transparent 60deg,
    #0ff
  );
  filter: blur(40px);
  opacity: 0.5;
  transition: background 0.2s ease;
}
```

✨ Uses `conic-gradient` to render a glowing beam effect  
💨 `blur()` softens the edges  
🎯 `--start` controls the direction of the glow  
🎛️ `transition` makes it smooth as butter

---

## 🔍 How It Works

| 🧩 Part | 💬 Description |
|--------|----------------|
| `getBoundingClientRect()` | Gets the position/size of the card |
| `e.clientX/Y` | Mouse position on the screen |
| `mouseX/Y` | Mouse position relative to card center |
| `Math.atan2()` | Calculates angle from center to cursor |
| `+60 offset` | Shifts glow to feel more dynamic |
| `--start` | CSS variable used to rotate the conic gradient |

---

## 🧪 Use Cases

- 💬 Testimonial cards
- 🪄 Glassmorphism hover effects
- 📦 UI dashboard tiles
- 🧲 Portfolio item hovers
- 🧬 Sci-fi or cyberpunk themes

---

## 🔁 Flashcard Recap

```txt
Q: How do I make a glow effect follow the cursor?
A: Use `atan2()` to find angle from center to mouse, then apply it as `--start` in a conic-gradient background.
```

---

## 🏷️ Tags

#css #react #ui-effects #glow #gradient #conic-gradient #hover #obsidian-snippet
