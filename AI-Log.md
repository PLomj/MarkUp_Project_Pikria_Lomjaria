# AI Log — Spotify Redesign Markup Project
Project: Spotify Redesign --- responsive HTML/CSS markup
Repository: https://github.com/PLomj/MarkUp_Project_Pikria_Lomjaria\
AI tools used: ChatGPT and OpenAI Codex (VS Code).
Other tools: Figma, Figma MCP, VS Code, Chrome DevTools, Git and
GitHub.

## How I used AI

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

## 1. Getting Figma MCP access to the design

At the beginning, I wanted Codex to inspect the Figma design rather than
guess measurements from screenshots. I installed the Figma MCP
integration in VS Code, but access to the original design initially
failed because of editing permissions.

Representative prompt: I am implementing a Spotify redesign from
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

## 2. Font setup and asset-export limitations

The design used Satoshi Regular, Medium and Bold. I prepared WOFF2
font files and checked that the font weights could be used in CSS. I
also needed icons, album artwork and an avatar.

Representative prompt: Check which fonts and image assets are
required for the desktop Spotify layout. Explain the best formats,
filenames and folder structure. Keep the project HTML/CSS only.

Problem and decision: Figma MCP access did not automatically mean
that all artwork could be exported. The available Figma plan restricted
the export workflow. Rather than ask Codex to invent images or keep
retrying unsupported exports, I used manual asset export and
organized SVG icons and PNG artwork in the project.

What I learned: AI can inspect a design and produce an asset
checklist, but some work depends on the source tool's permissions and
plan limits. My original intention was to keep the Satoshi binaries out
of Git for licensing reasons and document local setup in the README.
The three WOFF2 files were later added in commit `0201aad` and are now
tracked. The bundled `assets/fonts/FFL.txt` records the license terms.

## 3. Deciding how to split the CSS

I wanted the markup to remain understandable instead of putting every
rule into one very large stylesheet. Codex helped organize the project
by responsibility.

Representative prompt: Suggest a clear CSS file structure for
this Spotify markup project. Separate the main page layout from
navigation, sidebar, recommendations, player and responsive rules.
Explain why each file exists.
The final structure was:

```text
index.html
styles/
  base.css
  layout.css
  navigation.css
  sidebar.css
  main-content.css
  player.css
  mobile.css
```

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

## 4. Understanding Grid versus Flexbox in the desktop layout

One of my important learning questions was whether the website was built
only with Flexbox. A later read-only Codex audit confirmed that both
CSS Grid and Flexbox are used.

Representative prompt: Audit every CSS file. Show where
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

## 5. Matching the desktop design instead of accepting approximate results

The desktop reference was 1771 × 1024. The layout needed accurate
placement of the header, sidebar, content panel and player, not just a
page that looked generally similar.

Representative prompt: Compare the current desktop markup with
the Figma reference at 1771 × 1024. Report differences in region
positions, dimensions, spacing and artwork. Make only narrowly scoped
changes and preserve the rest of the page.

Problem and decision: A visually plausible result was not enough. I
used specific reference dimensions to review the layout and personally
confirmed the desktop layout visually in Chrome. Codex reported the
main content starting at x = 273, y = 60 and the player at y = 933.

What I learned: AI-generated CSS still needs a measurable acceptance
criterion. Precise viewport checks make feedback actionable and reduce
unrelated changes.

## 6. Building the mobile layout without breaking desktop

The mobile reference was 390 × 844, with six quick-access tiles,
horizontally scrolling recommendation cards, a fixed mini-player and a
fixed bottom navigation.

Representative prompt: Implement the mobile design using a
breakpoint at 900px. Reuse the existing HTML and shared card markup
where possible. Keep the desktop layout unchanged and verify the mobile
mini-player, bottom navigation and scrolling behavior.
The mobile rules switch the outer page from the desktop Grid to normal
block flow at 900px and below. However, Grid is still used for the
two-column quick-access tiles and bottom navigation. Flexbox
continues to arrange the contents of cards and controls.

Problem and decision: Fixed bottom elements can cover the final
content while scrolling. The solution was to reserve bottom space in the
feed. Codex's audit recorded 172px of clearance: 95px navigation +
61px player + 16px additional spacing.

What I learned: Responsive design is not simply shrinking desktop
widths. It can require a different layout flow, different visibility
rules and explicit room for fixed elements.

## 7. Correcting small visual and CSS-cascade details

After the broad layout worked, smaller details still mattered:
horizontal card scrolling, image sizes, text truncation and CSS rules
overriding one another.

Representative prompt: Inspect the recommendation cards and
explain why a specific title width or card size differs from the general
mobile rule. Check selector specificity and do not change unrelated
cards.
One documented example was the Fall Out Boy Radio title. Its
specific selector set a 120px maximum width, while a general mobile
heading rule used 100px. The more specific selector could win even
though it appeared in an earlier stylesheet.
Another example was the recommendation card width: desktop used
flex: 0 0 170px, while mobile changed only flex-basis to 141px.
The cards still did not grow or shrink.

What I learned: When a later CSS rule seems ineffective, the reason
may be specificity rather than file order. I also learned to inspect
shorthand properties before overriding only one part of them.

## 8. Making Spotify links work without changing the design

The initial assignment was static markup, but I later decided to make
navigation links open real Spotify pages. I wanted to preserve every
visual detail and avoid adding JavaScript.
I first requested a read-only link audit. Codex identified verified
destinations, ambiguous playlist names and controls that should remain
static.

Representative prompt: Audit the existing navigation and cards.
Suggest Spotify destinations without editing files. Distinguish exact
track URLs from personalized playlists that should use Spotify Search.
Keep playback controls and filters static.
Codex could not reliably identify exact personalized playlists from the
artwork alone. I made three explicit decisions:
Discover should open Spotify's Made For You hub.
Around the world should open Daft Punk's specific track.
All recommendation cards should open the corresponding Spotify
Search results rather than invented playlist IDs.
I then approved a narrowly scoped implementation prompt requiring native
anchors, new-tab behavior, keyboard focus, and no visual redesign.

Result: Codex reported 38 Spotify links: desktop navigation,
sidebar, mobile quick-access tiles, shared recommendation cards and
mobile bottom navigation. Codex reported that before-and-after
screenshots matched pixel for pixel at the desktop and mobile reference
sizes.
Personalized Spotify results and signed-in library content were not
independently verified.

What I learned: When AI cannot establish an exact destination, the
correct solution is to make an explicit product decision, not invent
data.

## 9. Reviewing, testing and committing only approved changes

Throughout the project, I separated implementation from review and Git
operations. I asked Codex to inspect changes, report test results and
wait for approval before committing or pushing.

Representative prompt: Validate the approved Spotify link changes
at desktop and mobile reference sizes, test the 900/901px breakpoint,
check keyboard focus and external-link attributes, and report the
changed files. Do not commit or push until I approve.
Codex's link implementation report listed seven modified files, no asset
changes, a clean git diff --check, and no console errors or broken
images in the checked browser sessions. After review, I authorized a
separate commit-and-push step.
Commit `194cbfe` (`feat: add external Spotify navigation links`)
implemented the external links. For that step, Codex reported a normal
fast-forward push, a clean working tree and synchronized local and
remote `main` branches.

What I learned: A successful AI response is not the same as a
reviewed change. Small tasks, explicit constraints, visual checks and
controlled commits made the project easier to understand and safer to
finish.

## Final reflection

The most useful part of working with AI was not receiving ready-made
HTML and CSS. It was learning how to ask better questions and how to
recognize when a proposed solution was incomplete.
There were real obstacles: Figma access permissions, asset-export
limitations, exact visual matching, responsive fixed-element
clearance, CSS specificity, and uncertain Spotify playlist
destinations. Some were solved by changing the workflow, some by
inspecting actual CSS, and some by making decisions that AI could not
make reliably on its own.
I used ChatGPT to plan tasks, clarify concepts and review Codex reports.
I used Codex to inspect the project, implement approved changes and run
focused checks. I retained responsibility for choosing requirements,
accepting compromises and approving commits.
The finished project is a responsive HTML/CSS-only Spotify redesign
with external Spotify navigation. It does not implement real music
playback, authentication or JavaScript-driven application behavior.
