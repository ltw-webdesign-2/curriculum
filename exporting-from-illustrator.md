---
layout: lesson
title: "Exporting from Illustrator"
desc: "A quick look at properly setting up an Illustrator file for exporting to SVG."

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
      To get started on this project we need to download an Illustrator file that we can manipulate & export.

      ### [Download these files.](https://assets.learn-the-web.algonquindesign.ca/web-design-3/exporting-from-illustrator-download.zip)

      Now create the following folder structure on your computer:
    folders:
      - label: "exporting-from-illustrator"
        type: folder
      - label: "prod"
        type: folder
        indent: 1
      - label: "dinosaurs.ai"
        indent: 2
        notes: "This is the file you downloaded"
      - label: "www"
        type: folder
        indent: 1
      - label: "images"
        type: folder
        indent: 2
    after: |
      The folders are used for the following purposes:

      - `prod` — (short for `production`) to keep perfect assets ready for exporting, in case they need to be changed
      - `www` — this is your GitHub repository, where all your HTML & CSS files are (we’re not using GitHub right now)
      - `www/images` — this is where the exported, smushed files go

      **Illustrator documents SHOULD NEVER be committed into your GitHub repository.**
    notes:
      - label: "Naming conventions"
        text: "Don’t forget to follow the [naming conventions](/topics/naming-paths-cheat-sheet/#naming-conventions)."

  - title: "Fix the artboards"
    before: |
      The artboard in Illustrator is extremely important, for two reasons:

      1. The name of the artboard is what you’re SVG will will be called
      2. The dimensions of the artboard dictate the basic dimensions of the SVG artwork

      ![](artboard-name.jpg)

      *Rename the two artboards: “herbivore” & “carnivore”.*

      ![](artboard-size.jpg)

      *Change the dimensions of the artboard to exactly “256 × 256”.* I like to use `256` as a good starting size for SVG artboards.

      We want to make sure the artboard perfectly matches the artwork—**if there extra spaces around the artboard, those will cause the SVG to look funny.**

      You can use the `Object > Artboard > Fit to Artwork Bounds` menu option to make it faster—but sometimes I don’t like the artwork touching the sides of the artboard.
    notes:
      - label: "Naming conventions"
        text: "Don’t forget to follow the [naming conventions](/topics/naming-paths-cheat-sheet/#naming-conventions) when naming your artboards."

  - title: "Name the layers"
    before: |
      Naming the layers in Illustrator can be super helpful, especially when we animate and make the SVGs interactive.

      ![](layers.jpg)

      *The names of the layers will export into the SVG as `id` attributes that we can target with CSS & JavaScript.*

      It’s also a really good idea to group things together—those groups will be represented in the SVG as different tags.
    notes:
      - label: "Naming conventions"
        text: "Don’t forget to follow the [naming conventions](/topics/naming-paths-cheat-sheet/#naming-conventions) when naming your layers."

  - title: "Export for screens"
    before: |
      Now that our Illustrator file is set up properly we’re ready to export the SVGs.
    image_steps:
      - url: "export.jpg"
        text: "To to the menu: `File > Export > Export for Screens…`"
      - url: "location.jpg"
        text: "Choose the location to export the SVGs—into the `images` folder in your `www` folder."
      - url: "svg.jpg"
        text: "Set the output format to `SVG`"
      - url: "svg-settings.jpg"
        text: "Adjust the SVG settings—you should only have to do this once, Illustrator should remember."
      - url: "svg-settings-screen.jpg"
        text: |
          Configure the following settings:

          - “Styling” — “Presentation Attributes”
          - “Font” — “Convert to Outlines”
          - “Images” — “Link”
          - “Object IDs” — “Layer Names”
          - “Decimal” — 1
          - “Minify” — checked
          - Make sure “Responsive” is <strong>not</strong> checked (for better browser support)
      - url: "export-artboards.jpg"
        text: "Finally, export the artboards—which will generate optimized SVG graphics"

  - title: "See the two exported files"
    before: |
      Illustrator should have exported the files for us and we can see them in our `images` folder:

      ![](images.jpg)

      **Never edit the SVG after it has been exported—that’s why we save the AI file. AI files are for editing, SVG files are for using on the website.**

  - title: "Smush the files"
    before: |
      We want to make the SVGs we use on the web as small as possible—Illustrator only does part of the job.

      Next up we need to drop the images into [**Spritebot**](https://github.com/thomasjbradley/spritebot) to really reduce their file size—it won’t reduce the quality in any way.

      ![](spritebot.jpg)

      You don’t have to save the files or anything, Spritebot will just overwrite your graphics with ones that are smaller size.

      **Now we have super small, super optimized graphics for our website that will help it load quickly.**

      You can go ahead and use these graphics in your HTML & CSS how you’re used to.

---
