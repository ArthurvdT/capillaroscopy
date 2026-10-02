# Nailfold Capillaroscopy Annotator

Version 6.1.

A browser-based tool for annotating and counting nailfold videocapillaroscopy (NVC) images.
It runs entirely on the user's own computer. No image or measurement ever leaves the machine.

Developed by Arthur van der Tol, Ghent University, under the supervision of
Prof. Dr. Vanessa Smith.

**Research use only.** This software is intended for research and teaching. It is not a
medical device and must not be used for diagnosis or clinical decision-making.

**Licence.** CC BY-NC 4.0: free to use, share and adapt for non-commercial research,
provided you give credit. See `LICENSE`.

## How to cite

If you use this tool, or data produced with it, please cite:

> van der Tol A, Smith V. Nailfold Capillaroscopy Annotator (version 6.1).
> Ghent University, 2026. https://arthurvdt.github.io/capillaroscopy

State the version you used. It is shown next to the title in the tool and is included in
the CSV exports as `tool_version`, so counts from different centres remain comparable.

---

## 1. What it does

- Marks capillaries, giant capillaries, four types of abnormal shapes and microhaemorrhages,
  based on the EULAR consensus guidelines for standardising nailfold capillaroscopy (NFC)
- Measures capillary diameter in micrometres after a one-off scale calibration
- Counts everything per image and scores a pattern per image and per visit
- Exports one row per patient per visit in the column layout of the study database, as an
  Excel file and as a paste-ready block
- Stores all annotations as coordinates, so the original images are never modified

## 2. Requirements

Google Chrome or Microsoft Edge, recent version. Firefox and Safari can open images but
cannot write into the image folder. Work is then not saved automatically and must be kept
with "Save patient (ZIP)" or "Save all (ZIP)". To continue later, load the folder together
with the `project.json` from that ZIP.

No installation, no account, no internet connection needed after the first visit.

## 3. Installing

Open the tool's web address. That is all that is required.

To get a desktop icon and its own window, click the install icon in the address bar
(Chrome) or the three dots menu, "Cast, save and share", "Install page as app".
The tool then works offline and updates itself whenever a new version is published.

## 4. File and folder naming

The tool reads patient, visit, hand, finger and image number from the folder and file names.
Only two things are fixed: the visit must be written as `V1` to `V20` (or `Visit 1` to
`Visit 20`), and the image name must contain the hand, finger and image code, for example `L2A`.

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
| `V1` to `V20` | Visit | Required. Written as `V1` / `V01` or as `Visit 1`, either as a subfolder or inside the file name. The number is kept as written: `Visit 1` and `Visit 7` stay visit 1 and visit 7. |
| `L`, `R` | Hand | `L` = left, `R` = right |
| `2` to `5` | Finger | Second to fifth finger |
| `A`, `B` | Image | `A` = first image, `B` = second image of that finger |

Anything before the hand code is ignored, so `L2A.jpg` and `GHA008_V1_L2A.jpg` are both read
correctly. The order of the code may vary: `L2A`, `LA2` and `2LA` are read the same way.
Write the visit in English: translations such as `visita` or `Besuch` are not read.

If a name cannot be read, the field stays empty and the tree shows `No visit` or `No hand`.
Nothing is lost: fill it in through the Identification panel on the right. An annotated
image without a complete code cannot be placed in the database row; the export warns about
it and names the file.

## 5. Recommended workflow

1. **Load the image folder.** Click "Load folder" and select a patient folder. The tool reads
   the images and, if a `project.json` is present, restores all previous work. Use
   "Load another folder" to add more patients; each folder keeps its own `project.json`.
2. **Verify the patient list on the left.** Patient, visit, hand, finger and image number are
   read from the folder and file names. Correct anything in the Identification panel.
3. **Calibrate the scale.** Select the scale tool (9) and drag a line along one side of the
   1 mm square burned into the image. Choose the unit (mm) and confirm. Use
   "Apply scale to this patient" if the magnification is identical for that patient.
4. **Annotate inside the 1 mm square.** Only mark structures within the grid square, since
   the counts are reported per millimetre. See the shortcuts below.
5. **Export.** "Excel block" copies one row per patient per visit for all loaded patients,
   ready to paste below the last row of the study database. "Save patient (ZIP)" and
   "Save all (ZIP)" write the annotated images, `database_rows.xlsx` and `project.json`.
6. **Close finished patients.** "Save and close" next to a patient in the tree saves its
   `project.json` and removes it from the list.

Work is saved automatically into `project.json` inside each patient folder, every few seconds.
The next time, "Load folder" offers to reopen the same folders.

### Arrow direction

The four small arrows (up, right, down, left) in the Capillary and Giant buttons set the
direction of new arrows. The chosen direction is shared by both tools. To turn an existing
arrow, click it with Select (V) and then click a direction, or press R.

### Shortcuts

| Key | Action |
|---|---|
| V | Select |
| 1 | Capillary |
| 2 | Giant (50 µm or more) |
| 3 | Abnormal shape 1 (`$`) |
| 4 | Abnormal shape 2 (`$#`) |
| 5 | Abnormal shape 3 (`$$`) |
| 6 | Abnormal shape 4 (`$$*`) |
| 7 | Haemorrhage |
| 8 | Measure |
| 9 | Set scale |
| R | Turn the selected arrow by 90° |
| G | Make the selected arrow thick (giant) or thin |
| F | Fit the image to the window |
| Delete, Backspace | Remove the selected item |
| Esc | Deselect |
| Ctrl/Cmd + Z, Ctrl/Cmd + Y | Undo, redo |
| Ctrl/Cmd + S | Save now |
| Arrow left/right, Page Up/Down | Previous or next image |
| Space + drag, Shift + drag | Pan |
| Scroll, pinch | Zoom |

The number keys work on the top row without Shift, also on AZERTY keyboards, and on the
numeric keypad. Combinations with Ctrl, Cmd or Alt are left to the browser.

## 6. Scale calibration

Pixels mean nothing until the tool knows how large one pixel is. Magnification, camera and
working distance differ per device, so the scale has to be set from the image itself.

**How to calibrate.** Select the scale tool (key 9) and drag a line along one side of the
1.00 x 1.00 mm square that the capillaroscope burns into the image. A dialog appears asking
what real distance that line represents. Enter the value and, next to it, choose the unit.

**Choose `mm`, not `µm`.** One side of the square is 1 mm. Entering `1` with the unit set to
µm makes every later measurement a thousand times too small. Before confirming, read the
preview line in the dialog: it shows something like `742 px = 1000 µm → 742 px/mm ·
1.348 µm/px`. If that line looks wrong, the calibration is wrong.

**One scale per image.** The calibration belongs to the image it was made on. If all images
of a patient were recorded at the same magnification, press "Apply scale to this patient" to
copy it to every image of that patient. It is never copied to other patients. Recalibrate
whenever the magnification or the working distance changes.

**Effect on measurements.** With a scale set, every measurement is reported in micrometres
and is classified automatically: normal below 20 µm, dilated from 20 to 49.9 µm, giant from
50 µm. Without a scale, measurements are shown in pixels and are not classified. Changing the
scale afterwards recalculates all existing measurements on that image; the annotations
themselves are stored as coordinates and are never affected.

**Where it ends up.** The calibration is written to `project.json` and appears in
`image_level.csv` as `px_per_mm`, so any reviewer can verify how a diameter was derived. A
scale bar is drawn in the bottom right corner of the canvas as a visual check.

## 7. Counting definitions

These definitions are fixed in the software. They must be agreed on before multicentre use,
because the tool enforces consistency in clicking, not in judgement.

| Item | Definition as implemented |
|---|---|
| Capillary | One arrow per capillary loop counted in the distal row |
| Giant | Homogeneously enlarged loop with a diameter of 50 µm or more, marked with the thick arrow |
| Dilation | A measurement between 20 µm and 49.9 µm |
| Abnormal shape 1 (`$`) | Abnormal shape (consensus definition) |
| Abnormal shape 2 (`$#`) | Abnormal shape with multiple crossing capillaries (3 or more) |
| Abnormal shape 3 (`$$`) | Neoangiogenesis / ramification |
| Abnormal shape 4 (`$$*`) | Neoangiogenesis / ramification and dilated over 50 µm |
| Microhaemorrhage | Marked with a filled triangle; only presence is recorded (yes/no) |
| Diameter | Measured perpendicular to the long axis of the loop, at its widest point |

**Density.** Density is not reported as a separate figure. All annotations are placed
**inside the 1.00 x 1.00 mm square** burned into the image by the capillaroscope, so the
number of capillary arrows (thin and thick) in that square is the density per millimetre.
If capillaries outside the square are also marked, the reported count will be too high.
The abnormal shape symbols are added next to the arrow and do not count as capillaries.

**Giants.** The giant count is the number of thick arrows. A measurement of 50 µm or more
turns the nearest arrow thick automatically. A measurement of 50 µm or more with no thick
arrow beside it also counts as one giant. A `$$*` symbol does not count as a giant by itself.

**Abnormal shapes.** The total is the sum of the four symbols. The database also lists each
symbol separately.

The 50 µm threshold and the 20 µm dilation threshold are set in the source code
(constants `GIANT` and `DILAT`). Do not change them mid-study.

## 8. Pattern score

The tool scores a pattern per image from the counts above, using these rules in this order:

| Code | Pattern | Rule |
|---|---|---|
| 4 | Late | No giants, density 3 or less, and at least one abnormal shape |
| 3 | Active | Giants present and density 6 or less |
| 2 | Early | Giants present and density 7 or more |
| 1 | Non-specific | No giants, and density below 7 and/or dilations, abnormal shapes or haemorrhages |
| 0 | Normal | Density 7 or more and nothing else |

The overall pattern of a visit is the most severe pattern among its images. Images without
annotations are not scored and do not count. The score is shown live per image in the panel
on the right and next to each visit in the tree.

**This is a mechanical rule applied to counts, not an expert judgement.** A single image can
determine the overall pattern of a visit. The rules are under review by Prof. Dr. Vanessa
Smith and must be confirmed before the scores are used in any analysis.

## 9. Output files

| File | Contents |
|---|---|
| `project.json` | All annotations as coordinates. This is the editable master file. |
| `database_rows.xlsx` | One row per patient per visit, with a header row, in the layout of the study database (174 columns). Part of every ZIP. |
| `*_annotated.png` | Flattened images with the annotations drawn on, in `patient/Visit X/` folders. Not editable. Ignored when a folder is loaded, so unpacking an export into the image folder is harmless. |
| `image_level.csv` | Via the CSV button: one row per image with counts per category and the measured diameters |
| `measurements.csv` | Via the CSV button: one row per individual measurement in µm, with its classification |

**Database layout.** Column A is the identifier (the patient folder name), column B the visit
(`visit 1`, `visit 7`, ...). Then, for each image in the fixed order L2a, L2b, L3a, L3b,
L4a, L4b, L5a, L5b, R2a, R2b, R3a, R3b, R4a, R4b, R5a, R5b, ten columns: density, giants,
dilations, abnormal shapes total, shape 1 `$`, shape 2 `$#`, shape 3 `$$`, shape 4 `$$*`,
haemorrhage (1 = yes, 0 = no) and pattern (0 to 4). The last twelve columns summarise the
visit over its annotated images: mean (SD) and median of density, dilations, abnormal
shapes and giants, presence of abnormal shapes, haemorrhages and giants (1 = yes), and the
overall pattern. Missing or unannotated images give empty cells.

The "Excel block" button copies the same rows without the header, ready to paste below the
last row of the study database.

**Export warnings.** The Excel window and the ZIP export warn when an annotated image cannot
be placed in a row (no visit, hand, finger or image number), or when two annotated images
claim the same position. Correct these before pasting.

The CSV files carry a `tool_version` column and `project.json` an `app_version` field.
Report the version in any publication, and check it before pooling data from several centres.

## 10. Data protection

All processing happens in the browser. Images are read from disk by the browser itself and
are not uploaded. There is no server component, no analytics and no external library.

Note that folder and file names may contain patient identifiers. The tool copies those names
into the CSV files, `project.json` and the Identifier column of the database rows. Use
pseudonymised names before sharing any export.

## 11. Publishing the tool

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
LICENSE
CITATION.cff
```

Upload the folder to a repository, enable Pages on the main branch, and share the resulting
address. HTTPS is required: the folder access and the install option do not work over plain
HTTP or from a local file.

When publishing a new version, raise `APP_VERSION` in `index.html` and the cache name in
`sw.js` so that existing users receive the update.

## 12. Contact

If there are issues, please contact arthur.vandertol@ugent.be
