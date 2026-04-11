# 🌐 Subhajit Sarkar — Personal Portfolio Website

> A dark-themed, cinematic, fully responsive personal portfolio built with pure **HTML**, **CSS**, and **vanilla JavaScript** — no frameworks, no build tools, just clean web fundamentals.

---

## 📸 Preview

| Section | Description |
|--------|-------------|
| Hero | Animated intro with role tags, CTA buttons, and social links |
| About | Bio, stats, and contact card |
| Skills | Categorized technical skill tags |
| Projects | Featured project cards with live/GitHub links |
| Education | Timeline-style background section |
| Certifications | Certification cards with Drive links |
| Contact | Contact info + Formspree-powered message form |

---

## 🗂️ Project Structure

```
portfolio/
├── index.html          # Main HTML file (entire site lives here)
├── assets/
│   └── logo.png        # Logo used in navbar and about card
└── README.md           # This file
```

> **Note:** The entire site is a **single-file application** — all CSS and JavaScript are embedded directly inside `index.html` using `<style>` and `<script>` tags. No external stylesheets or JS files are needed except Google Fonts (loaded via CDN).

---

## 🧱 Tech Stack

| Technology | Usage |
|------------|-------|
| HTML5 | Semantic page structure |
| CSS3 | Styling, animations, layout (Grid + Flexbox) |
| Vanilla JavaScript | Scroll reveal, active nav link highlight |
| Google Fonts | `Space Mono` (monospace) + `Syne` (display) |
| Formspree | Contact form email submission backend |

---

## 🎨 Design System

### CSS Custom Properties (`:root`)

All colors and theme values are defined as CSS variables at the top of the `<style>` block for easy customization:

```css
:root {
  --bg:       #080c14;   /* Page background (deep navy-black) */
  --surface:  #0d1220;   /* Section background */
  --surface2: #111827;   /* Card background */
  --border:   #1e2d45;   /* Border color */
  --accent:   #00e5ff;   /* Primary accent (cyan) */
  --accent2:  #7c3aed;   /* Secondary accent (purple) */
  --accent3:  #f59e0b;   /* Tertiary accent (amber) */
  --text:     #e2e8f0;   /* Primary text color */
  --muted:    #64748b;   /* Secondary/muted text */
  --green:    #10b981;   /* Status green (open to work) */
}
```

### Typography
- **`Syne`** — Display font for headings and body text (modern, geometric)
- **`Space Mono`** — Monospace font for labels, tags, code-style UI elements

### Noise Overlay
A subtle SVG fractal noise texture is layered over the entire page using a fixed `::before` pseudo-element on `body`, giving it a cinematic, tactile feel.

---

## 🗺️ Page Sections — Explained

### 1. `<nav>` — Fixed Navigation Bar
- **Position:** Fixed at the top, always visible while scrolling
- **Logo:** Displays `assets/logo.png` with a glow effect; shows fallback text `S~Sarkar`
- **Links:** Smooth-scroll anchor links to each section (`#about`, `#skills`, etc.)
- **Active state:** JavaScript highlights the current section's nav link as you scroll
- **Backdrop:** Uses `backdrop-filter: blur(16px)` for a frosted-glass effect

---

### 2. `#hero` — Hero Section
- **Background:** CSS Grid lines + two radial gradient glow spots (cyan top-right, purple bottom-left)
- **Tag badge:** "Available for remote opportunities" label with `>` prefix
- **Name heading:** Gradient text (`--accent` → `--accent2`) on the surname
- **Role tags:** Three role pills styled as `hero-role-tag`
- **CTA Buttons:**
  - `.btn-primary` → fills with `--accent`, goes white on hover
  - `.btn-outline` → bordered, turns cyan on hover
- **Social Links:** GitHub (`GH`), Hashnode Blog (`Bg`), Instagram (`IG`)
- **Animations:** All hero elements use `fadeUp` CSS keyframe with staggered `animation-delay`

---

### 3. `#about` — About Me
- **Layout:** Two-column CSS Grid (stacks to one column on mobile)
- **Left column:** Bio paragraphs + 4 stat cards (`2+ Projects`, `7+ Certifications`, etc.)
- **Right column:** Profile card (`about-card`) with:
  - Logo image inside an `about-avatar` box
  - Name, location, and "Open to Remote Work" green badge
  - Info rows: email, phone, GitHub, languages, status
- **Stat cards:** Each has a top gradient border stripe via `::before` pseudo-element

---

### 4. `#skills` — Technical Skills
- **Layout:** Auto-fit CSS Grid (min 300px per column)
- **Categories:** 6 skill groups — Languages, Frameworks, Backend/DB, Tools, Documentation, DevOps/Security
- **Tag types:**
  - Normal `.skill-tag` — standard border, turns cyan on hover
  - `.skill-tag.learning` — amber-tinted border to indicate skills currently being learned

---

### 5. `#projects` — Featured Projects
- **Layout:** Auto-fit CSS Grid (min 340px per column)
- **Cards:** `.project-card` — flex column layout, lifts on hover, animated top border via `::before scaleX`
- **Projects listed:**
  1. **Arjun AI** — Flask + MongoDB chatbot inspired by the Bhagavad Gita, deployed on Render
  2. **JARVIS-Style AI Agent** — Python local agent with plugin system, SQLite, and Ollama
- **Links:** Live Demo (`↗`) and GitHub (`⌥`) per project

---

### 6. `#education` — Education & Background
- **Layout:** Vertical timeline with a gradient left border line
- **Timeline dots:** Positioned absolutely using `.timeline-dot`, glowing cyan circles
- **Entries:**
  1. Diploma in CSE — Hailakandi Polytechnic (2024–Present)
  2. Ethical Hacking — TryHackMe self-study
  3. Technical Writing — Hashnode blog
- **Links:** Institution names link to official websites

---

### 7. `#certifications` — Certifications & Achievements
- **Layout:** Auto-fit CSS Grid (min 280px per column)
- **Cards:** Each shows an emoji icon, cert title (linked to Google Drive), issuer, and description
- **Certifications listed (all from Infosys Springboard + 1 from CEC):**
  - DCA (Computer Education Centre)
  - Data Warehouse Testing
  - Cloud Computing
  - Python Beginner
  - Data Science
  - MongoDB Development
  - Internet of Things 101

---

### 8. `#contact` — Contact Section
- **Layout:** Two-column grid (stacks on mobile)
- **Left column:** Short intro text + 5 clickable contact items (email, phone, GitHub, blog, live project)
- **Right column:** Contact form powered by **Formspree** (`https://formspree.io/f/mlgoqrrb`)
  - Fields: Name, Email, Subject, Message
  - Hidden fields for subject line and captcha disable
  - Styled submit button

---

### 9. `<footer>` — Footer
- Copyright text with highlighted name
- Quick links to GitHub, Blog, and Email

---

## ⚙️ JavaScript Functionality

### Scroll Reveal Animation
```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.classList.add('visible');
  });
}, { threshold: 0.12 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```
- Uses the **Intersection Observer API** to watch all `.reveal` elements
- When an element enters the viewport (12% visible), the class `visible` is added
- CSS transitions (`opacity` + `translateY`) then animate the element into view
- Elements start hidden (`opacity: 0`, `translateY: 24px`) and slide up to natural position

### Active Navigation Highlight
```js
window.addEventListener('scroll', () => {
  let current = '';
  sections.forEach(s => {
    if (window.scrollY >= s.offsetTop - 120) current = s.getAttribute('id');
  });
  navLinks.forEach(a => {
    a.style.color = a.getAttribute('href') === '#' + current ? 'var(--accent)' : '';
  });
});
```
- Listens for scroll events and compares `scrollY` against each section's `offsetTop`
- Highlights the matching nav link in `--accent` cyan for the currently visible section

---

## 📱 Responsive Design

| Breakpoint | Behavior |
|------------|----------|
| `> 768px` | Full two-column layouts for About and Contact |
| `≤ 768px` | Stacks to single column; hides nav links |
| `≤ 480px` | About stats go single column |
| `prefers-reduced-motion` | Disables all reveal transitions for accessibility |

---

## 🚀 How to Run Locally

No dependencies or build steps required.

```bash
# Clone the repository
git clone https://github.com/OSubhajit/portfolio.git

# Navigate to the folder
cd portfolio

# Open in browser
# Option 1: Double-click index.html
# Option 2: Use VS Code Live Server extension
# Option 3: Use Python's built-in server
python -m http.server 8000
# Then visit: http://localhost:8000
```

---

## 🌍 Deployment

This site can be deployed on any static hosting platform:

| Platform | Steps |
|----------|-------|
| **GitHub Pages** | Push to `main` branch → Enable Pages in repo settings |
| **Netlify** | Drag & drop the folder into Netlify dashboard |
| **Vercel** | Import GitHub repo → auto-deploys on every push |
| **Render** | Create a static site → point to `index.html` |

---

## ✏️ Customization Guide

### Change Colors
Edit the `:root` CSS variables at the top of the `<style>` block in `index.html`.

### Update Personal Info
Search for these fields in `index.html` and replace with your own:

| Field | Where to find it |
|-------|-----------------|
| Name | `hero-name`, `about-name`, footer |
| Email | `contact-item`, `info-row`, form action |
| Phone | `info-row`, `contact-item` |
| GitHub URL | `social-link`, `contact-item`, footer |
| Blog URL | `social-link`, `contact-item`, footer |
| Logo image | `assets/logo.png` — replace the file |

### Add a New Project
Copy one `.project-card` div in `#projects` and update:
- `project-num` label
- `project-title`
- `project-desc`
- `.tech-tag` list
- `.project-link` hrefs

### Update Contact Form
Replace the Formspree endpoint in the `<form action="...">` attribute with your own from [formspree.io](https://formspree.io).

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👤 Author

**Subhajit Sarkar**
- 📧 subhajitsarkar0708@gmail.com
- 🐙 [github.com/OSubhajit](https://github.com/OSubhajit)
- ✍️ [osubhajit.hashnode.dev](https://osubhajit.hashnode.dev/)
- 🌐 [arjun-ai.onrender.com](https://arjun-ai.onrender.com)

---

*Built with passion from Hailakandi, Assam, India 🇮🇳*
