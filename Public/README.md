# Marginalia ReadMe

Oct 11, 2026 · @Awyer

Marginalia is a free, light PDF editor that runs entirely in the browser. It fills in forms, edits a PDF's own text in its original font, adds notes and drawings, and rearranges pages, and your files never leave your device.

## Quick start

Marginalia opens with a sample equipment loan form, so you can try every tool before using your own file.

1. Click **Open PDF**, or drag a PDF onto the page area.
2. Pick a tool from the second toolbar row, or press its letter key (see Tools).
3. Click or drag on the page to add or change things. Click a form field to type in it.
4. Use **Undo** and **Redo** (Ctrl or Cmd + Z, Ctrl or Cmd + Shift + Z) freely. Every change can be taken back.
5. Click **Save**. You get a copy named after the original with "-edited" added, for example *lease-edited.pdf*. The original file is never changed.

## Tools

Every tool has a one-letter shortcut. Shortcuts are ignored while you are typing in a field or text box.

| Tool | Key | What it does |
| --- | --- | --- |
| Select | V | Click or drag a box to select notes, text lines, table borders, shading and images. Shift adds to the selection. Drag to move, Delete to remove. |
| Edit text | E | Click a line of the document's own text to rewrite it in the same font. |
| Add text | T | Click anywhere to type new text. The font menu lists the document's own fonts first. |
| Highlight | H | Drag over text to highlight it. |
| Draw | P | Freehand pen, useful for signatures. |
| Box | R | Rectangle outline. |
| Oval | O | Ellipse outline. |
| Arrow | A | Straight arrow. |
| Whiteout | W | Covers content with white. The text underneath stays in the file, so use Edit text to truly change words. |

Other shortcuts:

| Keys | Action |
| --- | --- |
| Ctrl or Cmd + Z | Undo |
| Ctrl or Cmd + Shift + Z, or Ctrl + Y | Redo |
| Ctrl or Cmd + A | Select everything on the current page |
| Delete or Backspace | Delete the selection |
| Esc | Clear the selection, then return to Select |
| Ctrl or Cmd + S | Save (see Limits for a note about this inside Claude) |

The colour swatches, custom colour picker and line width slider apply to the selected item or to whatever you draw next.

## Filling in forms

If a PDF has fillable fields, Marginalia finds them on open, shows a short note with the count, and tints each field light blue.

- **Text boxes, dropdowns and lists:** click and type or pick. Fields with a character limit stop at that limit.
- **Checkboxes and radio buttons:** click to tick. Only one radio button in a group can be on.
- **Linked fields:** fields that share a name (for example your name on page 1 and page 3) update together.
- **Read-only fields** stay as they are.
- Fields work with the Select and Edit text tools. With a drawing tool active, clicks go to the drawing instead.

When you save, the copy is still a fillable form, so the next person can change the answers in any PDF reader.

Tick **Lock answers on save** (top toolbar, shown only for forms) to turn the answers into ordinary page text instead. The saved copy then has no fields, and the answers can't be changed in a PDF reader. Use this for a final version you send off.

**XFA forms:** some government and tax forms use an older Adobe format called XFA that only Adobe Acrobat and Reader can fill. Marginalia tells you when it opens one. Use Adobe Reader for those.

## Editing the document's own text and tables

Marginalia changes what is actually in the PDF, not just what sits on top of it.

**Text.** With Edit text (E), click a line, retype it, and press Enter or click away. The new words use the document's own font, size and colour, and the old words are removed from the file. You can also drag an edited line to move it.

PDFs often carry only the letters they originally used from a font. If you type a letter that isn't there, a tag under the line says so and a close-match font fills in. For a perfect match, click **Use font file…** and choose the .ttf or .otf file from your computer's Fonts folder.

**Tables, lines, shading and images.** With Select (V), click or drag a box around them. You can then:

- delete them (Delete key or the bin button);
- recolour them with the swatches, or pick **No color** to remove an outline or fill;
- drag them somewhere else.

**Items added in other apps.** Text boxes and notes added in apps such as macOS Preview become normal Marginalia items you can select, edit, move and delete.

## Pages

Each page has a small button bar above it:

| Button | What it does |
| --- | --- |
| Rotate left / Rotate right | Turns the page 90 degrees. Notes and form fields turn with it. |
| Move up / Move down | Changes the page order. |
| Insert blank page after | Adds an empty page of the same size. |
| Delete page | Removes the page. Undo brings it back. |

Bookmarks and internal links survive these changes. A bookmark that pointed at a deleted page now points at the nearest remaining page. Use **Fit**, **+** and **−** in the top toolbar to zoom.

## Saving and privacy

Your PDF is opened, edited and saved inside your browser. It is never uploaded anywhere. The only things the page downloads are three open-source code libraries (listed under Hosting).

**Where the file goes.** Save always creates a new copy ending in "-edited.pdf".

- Inside Claude, a prompt shows the file name and size first. Accept it and the file lands in your browser's Downloads folder (or the share sheet on iPhone and iPad).
- On a self-hosted copy, it downloads like any other file.

**What is really removed.** When you save, these are deleted from the file itself, not just hidden:

- pages you deleted, including their text, images and form fields;
- text you replaced with Edit text;
- table borders, shading and images you deleted.

**What is not removed.** Whiteout only paints over content. Anyone can still copy or search the text beneath it. To remove words, use Edit text or delete the item.

**Save notes.** After saving, a message may mention lines that were covered instead of replaced (text drawn in a way that can't be edited), letters that used a close-match font, or form answers that couldn't be written. Everything else saved normally.

The document's title, author and bookmarks are kept. Only the modification date changes.

## Hosting it yourself

Marginalia is a single HTML file of about 140 KB with no server code, database or accounts. Any static host works: Netlify, Cloudflare Pages, GitHub Pages, or a folder on an existing website. Upload the file (rename it *index.html* if it is the only page) and share the link.

It loads three open-source libraries when the page opens:

| Library | Version | Used for | Licence | Loaded from |
| --- | --- | --- | --- | --- |
| [PDF.js](https://mozilla.github.io/pdf.js/) | 3.11.174 | Showing pages, reading text and form fields | Apache 2.0 | cdnjs.cloudflare.com |
| [pdf-lib](https://pdf-lib.js.org/) | 1.17.1 | Writing the saved PDF | MIT | cdnjs.cloudflare.com |
| [@pdf-lib/fontkit](https://github.com/Hopding/fontkit) | 1.1.1 | Embedding fonts for new and edited text | MIT | cdn.jsdelivr.net |

All three licences allow free use, including on client sites. Keep the licence notices if you copy the libraries onto your own server.

**Security notes**

- Serve it over HTTPS (every host above does this by default).
- Because files never reach the server, there is no user data on the host to leak.
- PDF.js 3.11 had a known flaw with booby-trapped font files. Marginalia turns off the affected feature (`isEvalSupported: false`), which is the fix the PDF.js team recommends for this version.
- To stop relying on the CDNs, download the three library files into the same folder and change the three `<script src>` lines plus the `workerSrc` line near the end of the file to the local names.

## Limits and troubleshooting

Marginalia covers everyday edits. A few jobs still need a full editor such as Adobe Acrobat:

- **Scanned pages** are pictures of text, so Edit text can't change them. Use Whiteout plus Add text instead.
- **XFA forms** can't be filled (see Filling in forms).
- **New form fields** can't be created; existing ones can be filled.
- **Digital signatures:** a drawn signature is just ink on the page, not a certificate-based digital signature.
- **Password-protected PDFs** that need a password to open must have the password removed first.
- **Undo** keeps the last 80 steps.

| Problem | Fix |
| --- | --- |
| I can't click into a form field | Switch to Select (V) or Edit text (E). Drawing tools take over clicks. |
| Saved file isn't in Downloads | Inside Claude, accept the save prompt that appears. Then check your browser's download list (Ctrl + J, or Cmd + Option + L on a Mac). |
| Ctrl + S doesn't save inside Claude | The browser can catch that shortcut there. Use the Save button. |
| Edited text looks slightly off | The PDF lacked some letters, so a close match was used. Click Use font file… and pick the real font. |
| A line was covered, not replaced | That text is drawn in a way that can't be edited. The new words sit on a patch that matches the background. |
| Pages look blank while scrolling a long file | Pages load as they come into view. Pause a moment and they appear. |
