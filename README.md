# Nailfold Capillaroscopy Annotator

Version 2.4

A browser-based tool for annotating and counting nailfold videocapillaroscopy (NVC) images.
It runs entirely on the user's own computer. No image or measurement ever leaves the machine.

Developed by Arthur van der Tol, Ghent University, under the supervision of
Prof. Dr. Vanessa Smith.

**Research use only.** This software is intended for research and teaching. It is not a
medical device and must not be used for diagnosis or clinical decision-making.

---

## 1. What it does

- Marks individual capillaries, giant capillaries, abnormal shapes and microhaemorrhages based on the EULAR consensus guidelines for standardizing nailfold capillaroscopy (NFC).
- Measures capillary diameter in micrometres after a one-off scale calibration
- Counts everything per image and exports it to CSV and to a paste-ready Excel block
- Stores all annotations as coordinates, so the original images are never modified

## 2. Requirements

Google Chrome or Microsoft Edge, recent version. Firefox and Safari work but cannot open a
whole folder at once and cannot write files back, so a browser based on Chromium is
strongly recommended.

No installation, no account, no internet connection needed after the first visit.

## 3. Installing

Open the tool's web address. That is all that is required.

To get a desktop icon and its own window, click the install icon in the address bar
(Chrome) or the three dots menu, "Cast, save and share", "Install page as app".
The tool then works offline and updates itself whenever a new version is published.

## 4. File and folder naming

The tool reads patient, visit, hand, finger and image number from the folder and file names.
Only two things are fixed: the visit must be written as `V1` or `V2` (or `Visit 1` and
`Visit 2`), and the image name must contain the hand, finger and image code, for example `L2A`.

Both layouts below work. Choose whichever suits your centre.

```
GHA008/                        GHA008/            <- folder name = patient identifier
  GHA008_V1_L2A.jpg              Visit 1/
  GHA008_V1_L2B.jpg                L2A.jpg
  GHA008_V1_L3A.jpg                L2B.jpg
  ...                              L3A.jpg
  GHA008_V2_R5B.jpg              Visit 2/
                                   R5B.jpg
```

| Part | Meaning | Rules |
|---|---|---|
| Folder name | Patient identifier | Any name: `GHA008`, `Ptn3`, `Patient 12`. Avoid names that are only `V1`, `L`, `R` or `D3`. |
| `V1`, `V2` | Visit | Required. Written as `V1` / `V2` or as `Visit 1` / `Visit 2`, either as a subfolder or inside the file name. `V1` = first visit, `V2` = follow-up. |
| `L`, `R` | Hand | `L` = left, `R` = right |
| `2` to `5` | Finger | Second to fifth finger |
| `A`, `B` | Image | `A` = first image, `B` = second image of that finger |

Anything before the hand code is ignored, so `L2A.jpg` and `GHA008_V1_L2A.jpg` are both read
correctly. Write the visit in English: `V1` and `V2`, or `Visit 1` and `Visit 2`. Translated
words such as `visita`, `Besuch` or `bezoek 1` are not read.

If a name cannot be read, the field simply stays empty and the tree shows `No visit` or
`No hand`. Nothing is lost: fill it in through the Identification panel on the right, or use
**Assign 16 images at once** to fill a whole visit in one click.

## 5. Recommended workflow

1. **Link the image folder.** Click "Link folder" and select the patient folder. The tool
   reads the images and, if a `project.json` is already present, restores all previous work.
2. **Verify the patient list on the left.** Patient, visit, hand, finger and image number are
   read from the folder name and the file names. Anything the tool could not read can be
   corrected in the Identification panel on the right.
3. **Calibrate the scale.** Select the scale tool (7) and drag a line along one side of the
   1 mm square burned into the image. Choose the unit (mm) and confirm. Use
   "Apply scale to all images" if the magnification is identical across the set.
4. **Annotate inside the 1 mm square.** Only mark structures within the grid square, since
   the counts are reported per millimetre. Keys 1 to 6: capillary, giant, abnormal shape 1,
   abnormal shape 2, haemorrhage, measure. Ctrl+Z undoes, Delete removes the selected item.
5. **Export.** "Excel block" copies a 5 by 16 table for one visit. "Save all (ZIP)"
   writes the annotated images, both CSV files and the project file.

Work is saved automatically into `project.json` inside the linked folder, every few seconds.

## 6. Counting definitions

These definitions are fixed in the software. They must be agreed on before multicentre use,
because the tool enforces consistency in clicking, not in judgement.

| Item | Definition as implemented |
|---|---|
| Capillary | One arrow per capillary loop counted in the distal row |
| Giant | Homogeneously enlarged loop with a diameter of 50 µm or more, marked with the thick arrow |
| Dilation | A measurement between 20 µm and 49.9 µm |
| Abnormal shape 1 | Marked with `$` |
| Abnormal shape twisted >=3 | Marked with `#/$` |
| Microhaemorrhage | Marked with a filled triangle |
| Diameter | Measured perpendicular to the long axis of the loop, at its widest point |

Density is not reported as a separate figure. All annotations are placed **inside the
1.00 x 1.00 mm square** burned into the image by the capillaroscope, so the number of
capillaries in that square is the density per millimetre. If capillaries outside the square
are also marked, the reported count will be too high.

The 50 µm threshold and the 20 µm dilation threshold are set in the source code
(constants `GIANT` and `DILAT`). Do not change them mid-study.

## 7. Output files

| File | Contents |
|---|---|
| `project.json` | All annotations as coordinates. This is the editable master file. |
| `image_level.csv` | One row per image: counts per category, and the mean, minimum and maximum measured diameter |
| `measurements.csv` | One row per individual measurement in µm, with its classification |
| `*.png` | Flattened images with the annotations drawn on. Not editable. |

Every CSV row and the project file carry a `tool_version` field. Report that version in any
publication, and check it before pooling data from several centres.

## 8. Data protection

All processing happens in the browser. Images are read from disk by the browser itself and
are not uploaded. There is no server component, no analytics and no external library.

Note that the file names may contain patient identifiers. The tool copies those names into
the CSV files. Use pseudonymised file names before sharing any export.

## 9. Publishing the tool

The folder contains everything needed for static hosting, for example GitHub Pages:

```
index.html
manifest.webmanifest
sw.js
icon.svg
icon-192.png
icon-512.png
icon-512-maskable.png
README.md
```

Upload the folder to a repository, enable Pages on the main branch, and share the resulting
address. HTTPS is required: the folder access and the install option do not work over plain
HTTP or from a local file.

When publishing a new version, raise `APP_VERSION` in `index.html` and the cache name in
`sw.js` so that existing users receive the update.

## 10. Contact

If there are issues, please contact arthur.vandertol@ugent.be
