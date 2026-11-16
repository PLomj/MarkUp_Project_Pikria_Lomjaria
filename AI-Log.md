AI-LOG --- Spotify Redesign Markup Project
Project: Spotify Redesign --- responsive HTML/CSS markup
Repository: https://github.com/PLomj/MarkUp_Project_Pikria_Lomjaria\
AI tools used: ChatGPT and OpenAI Codex (VS Code).
Other tools: Figma, Figma MCP, VS Code, Chrome DevTools, Git and
GitHub.

How I used AI
I used AI as a development assistant, an explanation tool, and a
reviewer. My goal was not to generate an entire website without
understanding it. I wanted to translate a Figma design into a responsive
HTML/CSS page, understand the layout choices, test the result, and keep
control of each change. The assignment was markup only: no
JavaScript, React, or functional audio player.
The prompt examples below are representative reconstructions of the
tasks I gave Codex, not necessarily verbatim transcripts. Where a
particular issue or decision is confirmed by our project discussions or
Codex audit reports, I describe it as such. I do not treat an
AI-generated report as proof of something I did not independently
verify.

1. Getting Figma MCP access to the design
   At the beginning, I wanted Codex to inspect the Figma design rather than
   guess measurements from screenshots. I installed the Figma MCP
   integration in VS Code, but access to the original design initially
   failed because of editing permissions.
   Representative prompt: > I am implementing a Spotify redesign from
   Figma using HTML and CSS only. Inspect the Figma file through MCP and
   explain which layout measurements, styles and assets I need before
   coding. Do not make changes yet.
   Problem and decision: Repeating the same access request would not
   solve a Figma permission problem. I duplicated the design into a file I
   could access, then retried the MCP workflow. This was a tooling/access
   dead end, not a CSS bug.
   What I learned: Before asking AI to implement a design, make sure it
   can actually inspect the intended source. An access error is different
   from an implementation error.
2. Font setup and asset-export limitations
   The design used Satoshi Regular, Medium and Bold. I prepared WOFF2
   font files and checked that the font weights could be used in CSS. I
   also needed icons, album artwork and an avatar.
   Representative prompt: > Check which fonts and image assets are
   required for the desktop Spotify layout. Explain the best formats,
   filenames and folder structure. Keep the project HTML/CSS only.
   Problem and decision: Figma MCP access did not automatically mean
   that all artwork could be exported. The available Figma plan restricted
   the export workflow. Rather than ask Codex to invent images or keep
   retrying unsupported exports, I used manual asset export and
   organized SVG icons and PNG artwork in the project.
   What I learned: AI can inspect a design and produce an asset
   checklist, but some work depends on the source tool's permissions and
   plan limits. I also kept the Satoshi font binaries out of Git because of
   licensing considerations, while documenting font setup in the README.
3. Deciding how to split the CSS
   I wanted the markup to remain understandable instead of putting every
   rule into one very large stylesheet. Codex helped organize the project
   by responsibility.
   Representative prompt: > Suggest a clear CSS file structure for
   this Spotify markup project. Separate the main page layout from
   navigation, sidebar, recommendations, player and responsive rules.
   Explain why each file exists.
   The final structure was:
   index.html
   styles/
   base.css
   layout.css
   navigation.css
   sidebar.css
   main-content.css
   player.css
   mobile.css
   base.css provides shared defaults and link styling; layout.css
   controls the desktop page shell; navigation.css and sidebar.css
   style their respective areas; main-content.css handles filters and
   recommendation cards; player.css handles the player; and mobile.css
   contains responsive changes.
   My decision: Keep component-specific CSS separate and load
   mobile.css last, instead of mixing desktop and mobile overrides
   throughout every file.
   What I learned: File organization is not only cosmetic. It makes it
   easier to identify which rule is responsible when a design changes
   unexpectedly.
4. Understanding Grid versus Flexbox in the desktop layout
   One of my important learning questions was whether the website was built
   only with Flexbox. A later read-only Codex audit confirmed that both
   CSS Grid and Flexbox are used.
   Representative prompt: > Audit every CSS file. Show where
   display: grid and display: flex are used, with selectors and line
   numbers. Explain the relationship between the parent container and its
   children.
   The desktop page uses a Grid shell with named areas for the top
   navigation, library sidebar, main content and bottom player. The shell
   includes a 259px sidebar column and a flexible right column. Flexbox
   is used inside the header, sidebar, recommendation rows and player
   groups.
   What I learned: Grid is useful for positioning large regions in rows
   and columns, while Flexbox is useful for aligning elements within those
   regions. They are complementary, not competing technologies.
