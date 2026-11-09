# From Field to Code: Remote Sensing from Scratch

**Del campo al código: teledetección desde cero**

Learn remote sensing the way an engineer works: start with a real question about a real wildfire, make a plan, choose the data and the method, check every result, and finish with an answer you can defend.

Book 2 of the *From Field to Code* series. Written in Spanish and English.

> Status: work in progress (started November 2026).

## The question

In April 2026 a wildfire burned the Sierra de Leirosa, between Allande and Tineo (Asturias, Spain). Three public sources give three different burnt areas. How much really burned, how sure can we be, and how long does a satellite still "see" the fire?

We answer it step by step with Sentinel-2 images, free platforms and one day of field work. No previous knowledge of remote sensing, physics or programming is needed: everything is explained when it is first used, including the dead ends.

## The series

*From Field to Code* is a series of open books for engineers and field specialists who want to work with spatial data the way the industry does today. Each book follows one real project from the question to a published result.

1. [PyQGIS from Scratch](https://github.com/ElviraGD-lab/field-to-code-pyqgis)
2. Remote Sensing from Scratch (this book)

## Read and build

The book is written in [MyST Markdown](https://mystmd.org). To build it locally:

```bash
npm install -g mystmd@1.12.0
cd book
myst start
```

## Licence

- Code: Apache License 2.0 (`LICENSE`)
- Text and figures: CC BY 4.0 (`LICENSE-docs`)
- Contains modified Copernicus Sentinel data (2026), processed by the author.

© 2026 Elvira Gayanova
