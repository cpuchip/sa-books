# How the transcription was made

## Reading the pages

Every page was rendered at 200 dpi and read by two OCR models running locally: MinerU2.5-Pro-2605-1.2B
(opendatalab, Apache-2.0) and GLM-OCR (zai-org, MIT). Where the two agreed on every formula on a page, the page
text is MinerU2.5-Pro's. Where they disagreed on any formula, a third reader (claude-haiku-5-5) read the page image
together with both readings. The same third read by claude-sonnet-5-5 on 38 of those pages (3 in a prototype that priced
both models, then 35 that a check had flagged) was used to compare the two models; it is not the text of any page.

| document | pages | the two models agreed | third read |
|---|---|---|---|
| cbPhysicsIIb24 (the book) | 332 | 135 (40.7%) | 197 |
| OnLineQuizQuestionsIIa1 | 97 | 76 (78.4%) | 21 |
| OnLineQuizAnswersIIa1 | 153 | 104 (68.0%) | 49 |
| SACProblemsIIa14 | 51 | 24 (47.1%) | 27 |

The third read cost $0.927 in API use (claude-haiku-5-5 $0.3352 for 294 pages, its 3 prototype pages included; claude-sonnet-5-5
$0.0511 for the 3 prototype pages and $0.5407 for the 35 others, $0.5918 in all).

## Proofreading

Pages were then proofread against their page images when they held handwriting (the worked solutions in the quiz
answers), figure labels copied into the text, answer options shown as images, figures that could not be placed, or
the problems' fixed glyphs (below). `book.json` counts the pages by how they were read, and each page's front
matter says how it was read.

Where a quiz screenshot cuts a line off at the bottom of the page, the line is completed only when its visible
part and the line before it settle it; words cut off at the right edge are kept as far as they are visible.

## How good the unproofread pages are

A random sample of 24 pages that had not been proofread (12 from the local models, 12 from the third read) was
checked word by word and formula by formula against the page images. It found 18 errors on 9 pages. Most had a
cause that repeats, and each such cause was then fixed everywhere:

- the book's bold hatted unit vectors î, ĵ read by their shape as arrows or a hatted J, T or 1 (10 errors on 3 of the
  12 third-read pages): every page with such a reading, 20 of them, was proofread against its image, and a check
  now finds none left;
- the problem sets' headings ("SAC224") dropped, and Blackboard's buttons and radio marks kept: fixed in assembly.

What the sample found that no repeated cause explains: on 3 of the 12 pages from the local models, one error each
(a dropped integral sign, a dropped caption line under a table, a figure label missing its first letter); on the 12
third-read pages, none. Those three pages were then proofread. So a page read only by the local models may hold a
small error of that kind; about one in four did in this sample.

## The problems' render

The problems exist only as a 2008 Word file (`SACProblemsIIa14.doc`; the site's PDF link serves a "File Not Found"
page). It was rendered to PDF with LibreOffice (Ubuntu 24.04's package, with the OpenSymbol, DejaVu and Liberation
fonts). The file names a font, "Physics Symbols", that is not available, so six of its characters rendered as empty
boxes. Read from their context in the file, they are: ℰ (emf), I (current), î, ĵ, k̂ (unit vectors) and r. They were
rendered with a stand-in font that draws those characters at the same code points, which changes the glyphs and
nothing else: without the stand-in the render reproduces the earlier one pixel for pixel on all 51 pages, and with
it 9 pages change, only where those characters stand. `SACProblemsIIa14-render.pdf` is that render, the pages the
problems were read from.

## Figures

Figures are cropped from the page images at the boxes MinerU2.5-Pro marked. The quiz files are screenshots of
Blackboard, so not every box is a figure: Blackboard's icons (278 small crops: answer marks and book icons), its
buttons and empty dropdowns are not reproduced; crops that were text (answer options, small formulas) are
transcribed as text instead; and one image whose origin could not be settled (a rendered prism, quiz answers page
104) is left out. The checks and crosses beside "Selected Answer" and "Correct Answer" are kept as text.

## Not kept

The running heads and the page numbers; italics, except on the proofread pages.
