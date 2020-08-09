---
layout: slide-deck
title: "Preparing images"
desc: "A quick introduction to exporting and preparing images for the web from common Adobe applications."

slides:
  - type: super-big-text
    content: |
      **Preparing images**

  - content: |
      ## App dictates format

      - Using Illustrator — Export SVG
      - Using Photoshop — Export JPG (or PNG)
    notes: |
      There’s no real reason to export PNGs or JPGs from Illustrator—it’s a vector tool, export as vector.

      Vice-versa, you can—but shouldn’t—export SVGs from Photoshop—it’s a bitmap tool, export as a bitmap.

  - content: |
      ## Default to SVG

      If you can use an SVG—use an SVG
    notes: |
      SVG will give you the best resolution & clarity of any image format because it’s just code & match. It’s automatically scaled for retina screens.

  - content: |
      ## Backup is JPG

      Photos should be JPGs
    notes: |
      When exporting a photo, always use a JPG. It’ll give you a good file size with a good enough quality.

      There are newer formats like WebP, but they aren’t supported quite as well in all browsers yet.

  - content: |
      ## Try to avoid PNGs

      In most cases anything that can be done in a PNG can be done better in an SVG*

      <small>*In most cases</small>

  - content: |
      ## Avoid GIFs—period

      - GIFs are **huge** files!
      - They have poor user experience
      - Bad accessibility: flashing that can cause seizures & can’t be stopped

      Avoid them at all costs.
    notes: |
      If you *must* include auto-playing snippets of video (which you should avoid as much as you can) it’s much better to provide a small video encoded as an MP4.

  - type: image
    image: choice-flow-chart.svg

  - content: |
      ## Videos & tutorials

      - [Website file organization](/topics/organization/)
      - [Images for the web](/topics/image-formats/)

---
