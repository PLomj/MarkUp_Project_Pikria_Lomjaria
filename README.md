# Spotify Redesign — Responsive Markup

[Project demo](https://markupprojectpikrialomjaria.vercel.app/) · [GitHub repository](https://github.com/PLomj/MarkUp_Project_Pikria_Lomjaria)

A static recreation of the Spotify Home screens from Figma, built with HTML5 and CSS3. Desktop and mobile share one `index.html`. Mobile styles apply at viewport widths of **900 px and below**.

| Layout       | Figma reference viewport |
| ------------ | ------------------------ |
| Desktop Home | 1771 × 1024 CSS px       |
| Mobile Home  | 390 × 844 CSS px         |

## Run locally

1. Open [`index.html`](index.html) in Chrome. No build step, server, or dependencies are required.
2. Use Chrome DevTools' Responsive mode to check the reference viewport sizes above.
3. The page loads Satoshi Regular, Medium, and Bold from the WOFF2 files currently tracked in `assets/fonts/`. If the files are absent, download them directly from [Fontshare](https://www.fontshare.com/fonts/satoshi) and place them in that folder, or use the system fallback. See the [bundled font license](assets/fonts/FFL.txt) for the terms, including restrictions on redistribution.

## Implemented scope

- **Desktop:** Top Navigation, Library Sidebar, Main Content with category filters and two recommendation rows, and a Bottom Player showing track metadata and a static progress bar.
- **Mobile:** Music, Podcasts, and Audiobooks filters, six quick-access cards, **Made For You** and **Your top mixes** with horizontal scrolling, a fixed mini-player, and a five-item bottom navigation: Home, Discover, Search, Library, and Me.

The mobile device status bar and extra recommendation sections were excluded by agreement. The project uses HTML and CSS only. Selected navigation items and cards open Spotify in a new tab. Recommendation playlists and mixes open Spotify Search results. Filters and playback controls remain visual only, and the project has no audio playback or JavaScript.

## Known limitations

- Four Made For You cards retain empty artwork slots because usable original exports were unavailable.
- Mobile uses agreed neutral placeholders for the **Around the world** artwork, the two mini-player action glyphs, and the **Me** icon.
- Figma access limits prevented a fresh comparison of some mobile details, including exact thumbnail crops and icon sizing.

## Accessibility

The page has a main landmark, a page heading, named navigation regions, and section headings. Decorative images use empty alt text when neighboring text already provides the name. CSS truncation keeps full card titles in the HTML. Only the navigation for the current layout is exposed, and static controls are kept out of the keyboard tab order. In Chrome, tabbing through recommendation links brings the focused cards into view. Muted player text follows the Figma palette and has limited contrast.

## Project structure

```text
.gitignore          Git ignore configuration
AI-Log.md           AI-assisted workflow and learning notes
README.md           Project overview and setup
index.html          Shared Desktop and Mobile Home markup
styles/             Base, Grid, navigation, sidebar, content, player, and mobile CSS
assets/
├── icons/          Original SVG icons
├── images/         Original cover artwork, avatar, and player images
└── fonts/          Satoshi WOFF2 files, setup notes, and bundled license
```

## Figma references

- [Desktop Home](https://www.figma.com/design/8UksFEHIDxpnQnoTszs5Kh/10X-markup-exam-project---Spotify--Copy-?node-id=298-16461)
- [Mobile Home](https://www.figma.com/design/8UksFEHIDxpnQnoTszs5Kh/10X-markup-exam-project---Spotify--Copy-?node-id=24-310)
- [Mobile bottom navigation](https://www.figma.com/design/8UksFEHIDxpnQnoTszs5Kh/10X-markup-exam-project---Spotify--Copy-?node-id=188-27232)
