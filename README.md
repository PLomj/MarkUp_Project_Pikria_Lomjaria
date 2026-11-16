# Spotify Redesign — Responsive Markup

A static recreation of the Spotify Home screens from Figma, built with HTML5 and CSS3. Desktop and mobile share one `index.html`. Mobile styles apply at viewport widths of **900 px and below**.

| Layout | Figma reference viewport |
| --- | --- |
| Desktop Home | 1771 × 1024 CSS px |
| Mobile Home | 390 × 844 CSS px |

## Run locally

1. Open [`index.html`](index.html) in Chrome. No build step, server, or dependencies are required.
2. Use Chrome DevTools' Responsive mode to check the reference viewport sizes above.
3. To reproduce the verified typography, download Satoshi directly from [Fontshare](https://www.fontshare.com/fonts/satoshi) and place its Regular, Medium, and Bold WOFF2 files in `assets/fonts/`. See the [font setup and license notes](assets/fonts/README.md) for the exact filenames. The page uses a system fallback if the font files are absent.

## Implemented scope

- **Desktop:** Top Navigation, Library Sidebar, Main Content with category filters and two recommendation rows, and a Bottom Player showing track metadata and a static progress bar.
- **Mobile:** Music, Podcasts, and Audiobooks filters, six quick-access cards, **Made For You** and **Your top mixes** with horizontal scrolling, a fixed mini-player, and a five-item bottom navigation: Home, Discover, Search, Library, and Me.

The mobile device status bar and extra recommendation sections were excluded by agreement. The project uses HTML and CSS only. The filters, search, destination icons, and player controls reproduce visual states. They do not provide filtering, search, destination navigation, or audio playback.

## Known limitations

- Four Made For You cards retain empty artwork slots because usable original exports were unavailable.
- Mobile uses agreed neutral placeholders for the **Around the world** artwork, the two mini-player action glyphs, and the **Me** icon.
- Figma access limits prevented a fresh comparison of some mobile details, including exact thumbnail crops and icon sizing.

## Accessibility

The page has a main landmark, a page heading, named navigation regions, and section headings. Decorative images use empty alt text when neighboring text already provides the name. CSS truncation keeps full card titles in the HTML. Only the navigation for the current layout is exposed, and static controls are kept out of the keyboard tab order. Both mobile recommendation rows can be reached and scrolled by keyboard in Chrome. Muted player text follows the Figma palette and has limited contrast.

## Project structure

```text
index.html          Shared Desktop and Mobile Home markup
styles/             Base, Grid, navigation, sidebar, content, player, and mobile CSS
assets/icons/       Original SVG icons
assets/images/      Original cover artwork, avatar, and player images
assets/fonts/       Font setup and license; local WOFF2 files are ignored by Git
read.me             Raw Figma CSS export used as a design reference
```

## Figma references

- [Desktop Home](https://www.figma.com/design/8UksFEHIDxpnQnoTszs5Kh/10X-markup-exam-project---Spotify--Copy-?node-id=298-16461)
- [Mobile Home](https://www.figma.com/design/8UksFEHIDxpnQnoTszs5Kh/10X-markup-exam-project---Spotify--Copy-?node-id=24-310)
- [Mobile bottom navigation](https://www.figma.com/design/8UksFEHIDxpnQnoTszs5Kh/10X-markup-exam-project---Spotify--Copy-?node-id=188-27232)
