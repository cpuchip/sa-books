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
the problems' fixed glyphs (below); so were two pages where the second reader (below) found a drop. `book.json`
counts the pages by how they were read, and each page's front matter says how it was read.

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

## A second reader for dropped content

After the first publication, every page read only by the local models and not proofread (312), with the sample's 12
third-read pages as a control, was compared with its page image by a second reader built on OpenCV 5.0.0. It runs four
checks:
- text lines outside every block the reader marked, or a block holding more text than the transcription gives it;
- drawings with no figure;
- integral signs and radicals counted against the text;
- the words of each line, read by OpenCV's DNN text recognizer (CRNN, from opencv_zoo), that do not occur in the text in
  order.

Before it was trusted, it was shown to stay quiet on three pages proved exact, and to catch drops planted in copies of
five pages. It also caught one of the sample's three real drops; the other two (one letter, and a mark smaller than a
letter) are below its reach.

It flagged 13 of the 312 pages, and 4 held up against the page image; none of the controls' 5 flags did. The 4 were
corrected:
- a column header and a check mark (quiz answers page 107);
- a drawing with no figure (book page 271);
- two figure crops that had cut off part of their drawing (problems page 43, book page 186).

That last kind led to a sweep of every figure crop. For each crop, it looks for page ink connected to the drawing that
falls outside the crop's box, and for marks near the box that are in no block of text. Before it was trusted, it was
shown to catch three crops deliberately cut too tight and to stay quiet on the crops of the exact pages.

Of 568 crops it flagged 26, and 6 held up, the two above among them: problems page 43, and book pages 125 (two crops),
126, 186 and 201. Those were re-cut to take in the whole drawing. The other 20 were:
- text the transcription carries (7);
- Blackboard's interface (7);
- a dashed axis line running on past the crop with nothing on it (6), left as they are.

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
104) is left out. The checks and crosses beside "Selected Answer" and "Correct Answer" are kept as text. Seven
figures were cut by hand: the six re-cut after the sweep above, and the drawing on book page 271, for which the reader
drew no box. On book page 186 the antenna runs down beside two paragraphs, so its crop takes in their lines. The
transcription carries those paragraphs, so in the crop they are painted white and only the drawing is left.

## Not kept

The running heads and the page numbers; italics, except on the proofread pages.
