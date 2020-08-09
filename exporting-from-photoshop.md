---
layout: lesson
title: "Exporting from Photoshop"
desc: "A quick look at properly exporting raster graphics from Photoshop."

hide_show_for_marks: true
markbot_submit: true

extra_tutorials:
  - title: "Preparing images slide deck"
    url: "/courses/web-design-3/preparing-images/"
  - title: "Website file organization"
    url: organization
  - title: "Images for the web"
    url: image-formats
    highlight: true

steps:
  - title: "Download & set up files"
    before: |
      To get started on this project we need to download a few raster graphics that we can manipulate & export.

      ### [Download these files.](https://assets.learn-the-web.algonquindesign.ca/web-design-3/exporting-from-photoshop-download.zip)

      Now create the following folder structure on your computer:
    folders:
      - label: "exporting-from-photoshop"
        type: folder
      - label: "assets"
        type: folder
        indent: 1
      - label: "mars.jpg"
        indent: 2
        notes: "The file you downloaded"
      - label: "rpg.png"
        indent: 2
        notes: "The file you downloaded"
      - label: "prod"
        type: folder
        indent: 1
      - label: "unicorn.psd"
        indent: 2
        notes: "The file you downloaded"
      - label: "www"
        type: folder
        indent: 1
      - label: "images"
        type: folder
        indent: 2
    after: |
      The folders are used for the following purposes:

      - `assets` — for files that are sourced or downloaded from another location that aren’t ready to be exported. *These files usually need to be credited to the author because you didn’t create them.*
      - `prod` — (short for `production`) to keep perfect assets ready for exporting, in case they need to be changed
      - `www` — this is your GitHub repository, where all your HTML & CSS files are (we’re not using GitHub right now)
      - `www/images` — this is where the exported, smushed files go

      **Photoshop documents SHOULD NEVER be committed into your GitHub repository.**
    notes:
      - label: "Naming conventions"
        text: "Don’t forget to follow the [naming conventions](/topics/naming-paths-cheat-sheet/#naming-conventions)."
      - label: "Older is sometimes better"
        text: |
          Photoshop has some newer ways of exporting graphics—that may work really well for mobile apps but are inferior for The Open Web.

          - `Generator` is okay for lots of tiny assets, but isn’t ideal for good compression. It also messes with layer names.
          - `Export As…` is a newer version of generator but removes file size controls that are so essential so saving for the web.

          So we’re going to stick to the `Save for Web…` option because it is still the best tool—even though Adobe wants us to think otherwise by labeling it as “Legacy”.

  - title: "Exporting a JPG"
    before: |
      JPG is a lossy format, meaning the exported file cannot be opened again because it has lost much of the information—**always save the PSD for JPGs you export!**

      ### Save the JPG as a PSD

      We want to maintain as much of the original document as possible and PSD can do that. JPGs are throw away graphics—they should never be edited after they’ve been compressed for the web.

      Make sure to put this PSD in your `prod` folder:
    folders:
      - label: "exporting-from-photoshop"
        type: folder
      - label: "assets"
        type: folder
        indent: 1
      - label: "mars.jpg"
        indent: 2
        notes: "This file should never be touched again"
      - label: "rpg.png"
        indent: 2
        fade: true
      - label: "prod"
        type: folder
        indent: 1
      - label: "mars.psd"
        indent: 2
        notes: "This file is the one we edit"
      - label: "unicorn.psd"
        indent: 2
        fade: true
      - label: "www"
        type: folder
        indent: 1
        fade: true
      - label: "images"
        type: folder
        indent: 2
        fade: true
    after: |
      ### Resize to the right dimensions

      Change the width of the graphic to `2000` pixels for this example. The “Resolution” should be `72` because browsers literally don’t understand resolution.

      ![](jpg-resize.jpg)

      *We’ll talk a little more about retina graphics next week.*

      ### Save for web

      Next up we’ll use the best exporting tool: `File > Export > Save for Web (Legacy)…`

      ![](save-for-web-menu.jpg)

      #### Save for web settings

      The “Save for Web” dialog presents a bunch of great settings to help use reduce the file size as much as possible.

      ![](jpg.jpg)

      **Our goal is to make the file size as small as possible without compromising the quality of the graphic too much.**

      ![](file-size.jpg)

      Watch this file size here while adjusting the quality—anything above `250 KB` should make you feel sick to your stomach.

      ![](quality.jpg)

      Because the image is extremely detailed and complex we can reduce the quality quite a lot without noticing too much degradation. *If this were a human or animal pay special attention to the face and eyes.*

      Also note these settings:

      - Check “Progressive”
      - Un-check “Embed Color Profile”
      - Check “Convert to sRGB”
      - Set “Preview” to “Internet Standard RGB (No Color Management)”
      - Set “Metadata” to “None”

      Press the “Save” button and put it into your `images` folder.

      ![](images-jpg.jpg)

      *Also make sure to save the PSD—all the Save for Web settings are stored in the PSD so that if you have to re-export the graphic everything is remembered.*
    notes:
      - label: "Save the PSD"
        text: "Never edit the JPG in Photoshop after you’ve exported it—always go back to your original PSD file."

  - title: "Exporting a PNG"
    before: |
      We can use the PNG format for graphics that are too complex for SVGs—but try to use SVG first.

      **Always keep the PSD for graphics you’ve exported in case you want to edit them later—never edit from the PNG file.**

      Open up the `unicorn.psd` graphic—it’s already saved as a PSD for you; the dimensions are correct; and the resolution is set at `72`.

      So we’re ready to “Save for Web”. **Choose PNG-24.** The format supports millions of colours and 256 levels of transparency.

      ![](png.jpg)

      Notice these important settings:

      - Check “Interlaced”
      - Un-check “Embed Color Profile”
      - Check “Convert to sRGB”
      - Set “Preview” to “Internet Standard RGB (No Color Management)”
      - Set “Metadata” to “None”

      Press the “Save” button and put it into your `images` folder.

      ![](images-png.jpg)

      *Also make sure to save the PSD—all the Save for Web settings are stored in the PSD so that if you have to re-export the graphic everything is remembered.*
    notes:
      - label: "Save the PSD"
        text: "Never edit the PNG in Photoshop after you’ve exported it—always go back to your original PSD file."

  - title: "Exporting a PNG-8"
    before: |
      If the graphic has only a few colours and rasterization of the graphic is important, we can use a PNG-8.

      The PNG-8 format only supports 256 different colours. Photoshop’s implementation is broken and only supports 1-bit transparency (like a GIF) but other applications, like [ImageAlpha](https://pngmini.com/), can give us 8-bit transparency.

      **Always keep the PSD for graphics you’ve exported in case you want to edit them later—never edit from the PNG file.**

      Open up the `rpg.png` and immediately save it as a PSD.
    folders:
      - label: "exporting-from-photoshop"
        type: folder
      - label: "assets"
        type: folder
        indent: 1
      - label: "mars.jpg"
        indent: 2
        fade: true
      - label: "rpg.png"
        indent: 2
        notes: "This file should never be touched again"
      - label: "prod"
        type: folder
        indent: 1
      - label: "mars.psd"
        indent: 2
        fade: true
      - label: "rpg.psd"
        indent: 2
        notes: "This file is the one we edit"
      - label: "unicorn.psd"
        indent: 2
        fade: true
      - label: "www"
        type: folder
        indent: 1
        fade: true
      - label: "images"
        type: folder
        indent: 2
        fade: true
    after: |
      The dimensions and resolution are good, so we’re ready to “Save for Web”.

      ![](png-8.jpg)

      When saving as a PNG-8 we want to reduce the number of colours as small as possible without compromising the quality of the graphic. In this illustration, `17` colours seems to be perfect.

      Notice these important settings:

      - You can play with “Perceptual” and “Diffusion” to control the dithering—but it won’t make any difference for this graphic
      - “Transparency” doesn’t need to be checked because we don’t need transparency for this graphic
      - Check “Interlaced”
      - Un-check “Embed Color Profile”
      - Check “Convert to sRGB”
      - Set “Preview” to “Internet Standard RGB (No Color Management)”
      - Set “Metadata” to “None”

      Press the “Save” button and put it into your `images` folder.

      ![](images-png-8.jpg)

      *Also make sure to save the PSD—all the Save for Web settings are stored in the PSD so that if you have to re-export the graphic everything is remembered.*
    notes:
      - label: "Save the PSD"
        text: "Never edit the PNG in Photoshop after you’ve exported it—always go back to your original PSD file."

  - title: "Smush the files"
    before: |
      We want to make the images we use on the web as small as possible—Photoshop only does part of the job.

      Next up we need to drop the images into [**ImageOptim**](https://imageoptim.com/mac) to really reduce their file size—it won’t reduce the quality in any way.

      ![](imageoptim.jpg)

      You don’t have to save the files or anything, ImageOptim will just overwrite your graphics with ones that are smaller size.

      *If you’re on Windows you can use [FileOptimizer](http://nikkhokkho.sourceforge.net/static.php?page=FileOptimizer) to perform the same task as ImageOptim.*

      **Now we have super small, super optimized graphics for our website that will help it load quickly.**
---
