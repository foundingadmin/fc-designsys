# File type icons

Mint glyph on a black tile, the small sibling of the `.icon-tile` component. Built for the Files table in ClickUp task descriptions, where an icon sits beside one line of text in both light and dark mode.

Glyphs are Streamline Micro Line, drawn on a 10px grid, placed 3px in from each edge of a 16px tile with a 3px corner radius. Colors are `--mint` #7EF893 on `--n-black` #000000. Each SVG names its source glyph in a comment.

## Files

Every icon ships three ways:

- `name.svg` · 16 by 16, the source
- `name.png` · 16 by 16
- `name@2x.png` · 32 by 32

## The set

- `document` · Google Doc, Word file, any written document
- `pdf` · PDF exports and selects
- `sheet` · Google Sheet, Excel, CSV
- `slides` · Google Slides, PowerPoint, Keynote
- `image` · stills, renders, photos
- `video` · animatics, renders, recordings
- `folder` · Drive folders
- `design` · Figma frames, sections and files
- `link` · any web page without its own type
- `archive` · zip files and packages
- `email` · an email thread
- `chat` · a Slack or ClickUp chat thread
- `task` · a ClickUp task
- `log` · a page in a list's Log doc

## Using one in ClickUp

Reference the PNG by its full URL on the brand site, one per row:

```
| ![](https://brand.foundingcreative.com/assets/icons/filetype/pdf.png) PDF | [Current picks](https://example.com) | Updated Oct 27 2026 |
```

ClickUp draws an image at its own pixel size, so the 16px PNG sits at text height. Never hotlink third party favicons or Drive's type icons in its place.

## Adding one

Pick the glyph from Micro Line so the set stays one family, build it with the same tile, and add it to the list above. Never overwrite previous versions of an icon that cards already link; give a redrawn icon a new name.
