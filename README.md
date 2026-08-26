# Nailfold Capillaroscopy Annotator

Version 1.3

A browser-based tool for annotating and counting nailfold videocapillaroscopy (NVC) images.
It runs entirely on the user's own computer. No image or measurement ever leaves the machine.

Developed by Arthur van der Tol, Ghent University, under the supervision of
Prof. Dr. Vanessa Smith.

**Research use only.** This software is intended for research and teaching. It is not a
medical device and must not be used for diagnosis or clinical decision-making.

---

## 1. What it does

- Marks individual capillaries, giant capillaries, abnormal shapes and microhaemorrhages
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

## 4. Recommended workflow

1. **Link the image folder.** Click "Link folder" and select the patient folder. The tool
   reads the images and, if a `project.json` is already present, restores all previous work.
2. **Check the tree.** Patient, visit, hand, finger and photo are read from the folder name
   and the file names. Anything the tool could not read can be corrected in the
   Identification panel on the right.
3. **Calibrate the scale.** Select the scale tool (7) and drag a line along one side of the
   1 mm square burned into the image. Choose the unit (mm) and confirm. Use
   "Apply scale to all images" if the magnification is identical across the set.
4. **Annotate inside the 1 mm square.** Only mark structures within the grid square, since
   the counts are reported per millimetre. Keys 1 to 6: capillary, giant, abnormal shape 1, abnormal shape 2,
   haemorrhage, measure. Ctrl+Z undoes, Delete removes the selected item.
5. **Export.** "Excel block" copies a 5 by 16 table for one visit. "Save all (ZIP)"
   writes the annotated images, both CSV files and the project file.

Work is saved automatically into `project.json` inside the linked folder, every few seconds.

## 5. Counting definitions

These definitions are fixed in the software. They must be agreed on before multicentre use,
because the tool enforces consistency in clicking, not in judgement.

| Item | Definition as implemented |
|---|---|
| Capillary | One arrow per capillary loop counted in the distal row |
| Giant | Homogeneously enlarged loop with a diameter of 50 µm or more, marked with the thick arrow |
| Dilation | A measurement between 20 µm and 49.9 µm |
| Abnormal shape 1 | Marked with `$` |
| Abnormal shape 2 | Marked with `#/$` |
| Microhaemorrhage | Marked with a filled triangle |
| Diameter | Measured perpendicular to the long axis of the loop, at its widest point |
| Density | Not reported separately: the capillary count inside the 1 mm grid is the density per millimetre |

Density assumes that all annotations are placed **inside the 1.00 x 1.00 mm square** burned
into the image by the capillaroscope. Under that protocol the number of capillaries in the
square is the density per millimetre, so no division is applied. If capillaries outside the
square are also marked, the reported density will be too high.

The 50 µm threshold and the 20 µm dilation threshold are set in the source code
(constants `GIANT` and `DILAT`). Do not change them mid-study.

## 6. Output files

| File | Contents |
|---|---|
| `project.json` | All annotations as coordinates. This is the editable master file. |
| `image_level.csv` | One row per image: counts, density, mean, minimum and maximum diameter |
| `measurements.csv` | One row per individual measurement in µm, with its classification |
| `*.png` | Flattened images with the annotations drawn on. Not editable. |

Every CSV row and the project file carry a `tool_version` field. Report that version in any
publication, and check it before pooling data from several centres.

## 7. Data protection

All processing happens in the browser. Images are read from disk by the browser itself and
are not uploaded. There is no server component, no analytics and no external library.

Note that the file names may contain patient identifiers. The tool copies those names into
the CSV files. Use pseudonymised file names before sharing any export.

## 8. Publishing the tool

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

## 9. Contact

Add a contact address here before distributing the tool to other centres.
