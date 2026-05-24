# Interactive CV Portfolio

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat&logo=nginx&logoColor=white)](https://nginx.org/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A single-page interactive CV/portfolio website built entirely with vanilla HTML, CSS, and JavaScript. **Zero dependencies** -- no frameworks, no build tools, no npm packages. Just open the file and it works.

cv.theobs.fr
<!-- Replace screenshot.png with an actual screenshot of the site -->

---

## Features

- **Particle background animation** -- Canvas-based particle system with connecting lines in the hero section
- **Animated hero section** -- Typing effect greeting, letter-by-letter name reveal, and animated stat counters
- **Interactive terminal** -- Fully functional terminal emulator with commands: `help`, `whoami`, `skills`, `experience`, `contact`, `clear`
- **Neural network skills visualization** -- Canvas-based graph with nodes grouped by category (Orchestration, IaC, System, CI/CD, Middleware, Monitoring, Cloud), interactive hover with glow effects
- **FR/EN language switch** -- Full bilingual support with `localStorage` persistence
- **Custom cursor** -- Dot + glow cursor with hover state changes on interactive elements
- **Parallax scrolling** -- Depth effect on section headers and content blocks
- **Animated timeline** -- Work experience timeline with progressive line drawing on scroll and hover effects
- **Portfolio section with countdown timer** -- Live countdown to upcoming project releases
- **Live status page** -- Real-time service health checks via `fetch` with auto-refresh every 30 seconds
- **Copy-to-clipboard email** -- Click-to-copy email address with visual feedback
- **PDF export** -- Print stylesheet that renders a clean, print-friendly version of the CV
- **Uptime counter** -- Live counter showing how long the site has been running
- **Dynamic animated section backgrounds** -- Radial gradient backgrounds with drifting animations
- **3D tilt effect on skills canvas** -- Perspective-based tilt that follows the mouse cursor
- **Fully responsive design** -- Adapts to mobile, tablet, and desktop viewports
- **Scroll-snap navigation** -- Smooth section-by-section scrolling with IntersectionObserver-powered reveal animations

## Tech Stack

| Layer       | Technologies                                                                 |
|-------------|-----------------------------------------------------------------------------|
| **Markup**  | HTML5 (semantic sections, Canvas elements, data attributes for i18n)        |
| **Styling** | CSS3 -- custom properties, keyframe animations, grid, flexbox, print media queries |
| **Logic**   | Vanilla JavaScript -- Canvas API, IntersectionObserver, Fetch API, localStorage, Clipboard API |
| **Server**  | Nginx (Alpine-based Docker image)                                           |
| **Deploy**  | Docker, Docker Compose, Traefik-compatible labels                           |

## Getting Started

### Option 1: Just open the file

```bash
# No server needed -- just open index.html in your browser
open index.html
# or
xdg-open index.html
```

### Option 2: Docker Compose

```bash
docker compose up -d --build
```

The site will be available at `http://localhost:8080`.

> If you use Traefik as a reverse proxy, the compose file includes labels for automatic service discovery. Update the `Host` rule in `docker-compose.yml` to match your domain.

### Option 3: Docker only

```bash
docker build -t cv-portfolio .
docker run -d -p 8080:80 cv-portfolio
```

## Customization

### Personal Information

All personal data is concentrated in the HTML file (`index.html`). Here is where to find each section:

| What to change         | Where to find it                                                              |
|------------------------|-------------------------------------------------------------------------------|
| **Name**               | `<title>` tag, footer, JS letter animation (`'JOHN'.split(...)`)             |
| **Nav logo**           | `.logo` element in `<nav>` (currently `JD`)                                  |
| **Terminal prompt**    | `.terminal-bar span` (currently `user@devops:~`)                             |
| **About / Profile**   | Terminal lines in `#about` section + translations object in `<script>`       |
| **Skills graph**       | `skills` array in the Neural Network IIFE (name, sub-label, percentage, group) |
| **Work experience**   | `.tl-item` blocks in `#experience` + translations object                     |
| **Education**          | `.formation-card` blocks in `#formation`                                     |
| **Hobbies**            | `.hobby-card` blocks in `#hobbies`                                           |
| **Contact info**       | `.contact-card` blocks in `#contact` + `commands.contact` function           |
| **Social links**       | LinkedIn / GitHub `<a>` tags in `#contact`                                   |
| **Status page**        | `services` array in the Status Page IIFE (name, URL, host)                   |
| **Stat counters**      | `data-target` attributes on `.counter` spans in `#hero`                      |
| **Countdown target**   | `target` date in the Portfolio Countdown IIFE                                |
| **Uptime start date**  | `startDate` in the Uptime Counter IIFE                                       |

### Translations (i18n)

The `translations` object near the top of `<script>` contains all FR and EN strings. Each key matches a `data-i18n` attribute in the HTML. Add or modify entries to change any text.

### Styling

All styles are in the `<style>` block within the HTML. Key CSS custom properties at the top of the file:

```css
:root {
  --bg: #0a0a1a;       /* Background color */
  --surface: #12122a;  /* Card / section background */
  --accent: #4fc3f7;   /* Primary accent (cyan) */
  --accent2: #7c4dff;  /* Secondary accent (purple) */
  --accent3: #00e676;  /* Tertiary accent (green) */
  --text: #e8e8f0;     /* Main text color */
  --muted: #8888aa;    /* Muted / secondary text */
}
```

### Domain / Server Name

Update the `server_name` directive in `nginx.conf` and the Traefik `Host` rule in `docker-compose.yml` to match your domain.

## Project Structure

```
.
├── index.html          # Single-page CV (HTML + CSS + JS, all-in-one)
├── nginx.conf          # Nginx server configuration
├── Dockerfile          # Docker image definition (nginx:alpine)
├── docker-compose.yml  # Docker Compose with Traefik labels
└── README.md           # This file
```

## License

This project is licensed under the [MIT License](LICENSE).
