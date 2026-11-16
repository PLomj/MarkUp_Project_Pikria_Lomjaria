# Satoshi fonts

Desktop and Mobile Home load Satoshi locally through CSS `@font-face` rules in `styles/navigation.css` and `styles/main-content.css`.

| Local file in this folder | Weight | Style | Example use |
| --- | --- | --- | --- |
| `Satoshi-Regular.woff2` | 400 | Normal | Navigation labels, descriptions, and player metadata |
| `Satoshi-Medium.woff2` | 500 | Normal | Recommendation card titles |
| `Satoshi-Bold.woff2` | 700 | Normal | Section headings and the selected desktop filter |

Download Satoshi directly from [Fontshare](https://www.fontshare.com/fonts/satoshi) and place the three unmodified WOFF2 files in this folder using the filenames above. The stylesheet falls back to system fonts when these files are missing.

The bundled [Fontshare license](FFL.txt) permits the licensee to self-host the font for their own websites and restricts redistribution through repositories. Git currently tracks all three WOFF2 files listed above. Refer to `FFL.txt` for the full terms.
