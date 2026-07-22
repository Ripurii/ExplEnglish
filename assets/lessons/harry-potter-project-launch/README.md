Images for the Sorting Ceremony widget (`_includes/house-sorter.html`, used on the Launch Lesson page). Save your own image files here with these **exact filenames** — the code already references these paths, so nothing else needs to change once they're in place.

| Filename | What it is | Notes |
|---|---|---|
| `bg-space.jpg` | The purple nebula/starfield background | Any landscape-ish image works; it's covered by a dark overlay in CSS so text stays readable. |
| `owl.png` | The owl carrying a letter, used in the "delivering the news" animation | Best as a **transparent-background PNG** — a white background will show as a white box when it flies in. If your source image has a white background, run it through a free background remover (e.g. remove.bg) first. |
| `crest-gryffindor.png` | Gryffindor crest | Any square-ish image works — it's cropped into a circle badge on the wheel and shown full-size on the reveal card. |
| `crest-slytherin.png` | Slytherin crest | Same as above. |
| `crest-hufflepuff.png` | Hufflepuff crest | Same as above. |
| `crest-ravenclaw.png` | Ravenclaw crest | Same as above. |

Once the files are here, `git add` + commit them like any other asset (see the main [README.md](../../../README.md)). Keep each file well under GitHub's 100MB limit — these are just images, so that's not a concern in practice.
