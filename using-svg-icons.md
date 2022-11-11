---
layout: lesson
title: "Using SVG icons"
desc: "Use Illustrator & Spritebot to generate some SVG icons and use them in a website."

extra_tutorials:
  - title: "Advanced SVG slide deck"
    url: "/courses/web-design-2/advanced-svg/"
  - title: "Advanced SVG"
    url: advanced-svg

markbot_submit: true
hide_show_for_marks: true

goal:
  image: goal.gif
  before: |
    We’re going to look at creating an SVG sprite sheet with some icons inside. Then we’ll use the icons on a website in a simple layout.
  notes:
    - label: "Type it, type it real good"
      text: "Remember the purpose of this lesson is to type the code out yourself—build up that muscle memory in your fingers!"

fork:
  url: "https://github.com/ltw-webdesign-2/using-svg-icons"

download:
  url: "https://assets.learntheweb.courses/web-design-2/using-svg-icons-download.zip"
  export_notes: "We’ll be walking through setting up this Illustrator document together so there’s no need to do anything with it right away."

steps:
  - title: "Set up project"
    before: |
      After forking, cloning & downloading we should have a folder structure like this:
    folders:
      - label: "using-svg-icons-lesson"
        type: folder
      - label: "prod"
        type: folder
        indent: 1
      - label: "dino-icons.ai"
        indent: 2
      - label: "using-svg-icons"
        type: folder
        indent: 1
        notes: "This is the cloned GitHub repo"
      - label: "index.html"
        indent: 2
      - label: "css"
        type: folder
        indent: 2
      - label: "main.css"
        indent: 3
      - label: "images"
        type: folder
        indent: 2
    after: |
      1. Make an `index.html` & add the boilerplate code.
      2. Make a `main.css` in your `css` folder—add `border-box` & `text-size-adjust`.
      4. Make an `images` folder.
    notes:
      - label: "Naming conventions"
        text: "Don’t forget to follow the [naming conventions](/topics/naming-paths-cheat-sheet/#naming-conventions)."
      - label: "HTML snippets"
        text: "Create the boilerplate with `html5`, `viewport`, `css`"

  - title: "Organize the Illustrator file"
    before: |
      The first step to using SVG icons is to organize the Illustrator document so it can be exported properly.

      For icons, the way we export is no different from standard SVGs: resize & name the artboards.

      Open up the Illustrator file and you should see this:

      ![](illlustrator.jpg)

      Our first step is to create multiple artboards—**each artboard should be `256px` × `256px`**

      ![](artboard.jpg)

      Move the dinosaur icons so that they are on individual artboards. I resized each icon to be `252px` wide.

      I named each artboard this:

      1. `brachiosaurus`
      2. `micropachycephalosaurus`
      3. `velociraptor`

      ![](all-artboards.jpg)

      The final change we need to make is the `fill`. Since we’re interested in colouring the icons in our CSS and want to have different hover colours we need to remove the fill colours in Illustrator.

      ![](fill-black.jpg)

      The simplest way to remove fill colours when exporting from Illustrator is to set all their colours to black—absolute black, `#000000`. The default `fill` in SVG is black, so the optimizer will leave the fill off.

      **Of course you could remove the fill colour in Illustrator but then you wouldn’t be able to see the graphic and that’s just annoying.**

      *If you want differently coloured or multi-coloured icons then leave the fill.*

  - title: "Export the SVGs"
    before: |
      We’re ready to export our SVGs from Illustrator now. Go to:

      ```
      File > Export > Export for Screens…
      ```

      Assuming you’ve exported using “Export for Screens” before there shouldn’t really be any settings we need to change.

      [If you haven’t used “Export for Screens” before, see this tutorial.](/topics/image-formats/#export-for-screens)

      ![](export.jpg)

      **Be sure to set the correct output location: the `images` folder inside your `using-svg-icons` folder.**
    notes:
      - label: "Keyboard shortcut"
        text: |
          Export for screens: `⌥⌘E`

  - title: "Generate a sprite sheet"
    before: |
      We should now have 3 completely separate SVG files in our SVG folder, looking like this:
    folders:
      - continue: true
      - label: "using-svg-icons"
        type: folder
      - label: "index.html"
        indent: 1
        fade: true
      - label: "css"
        type: folder
        indent: 1
        fade: true
      - label: "images"
        type: folder
        indent: 1
      - label: "brachiosaurus.svg"
        indent: 2
      - label: "micropachycephalosaurus.svg"
        indent: 2
      - label: "velociraptor.svg"
        indent: 2
    after: |
      Drop all 3 of the images into [**Spritebot**](https://github.com/thomasjbradley/spritebot)—which will compress and optimize the images for us.

      ![](spritebot.jpg)

      When Spritebot is ready we want to merge all the SVGs into a single file. This is called a sprite sheet. The benefit is performance: less downloads & faster websites.

      ![](delete-singles.jpg)

      After we’ve created & saved the sprite sheet, the original SVG graphics are useless—delete them.

      Now we’re ready to use the icons in our HTML!

  - title: "Write the HTML code"
    before: |
      Let’s write out the HTML we need to show the icons. For this quick example we’ll use a list and some links.
    code_lang: "html"
    code_file: "index.html"
    code: |
      ⋮
      </head>
      <body>

        <ul>
          <li>
            <a href="#">
              <i class="icon">
                <svg><use xlink:href="images/dino-icons.svg#brachiosaurus"></use></svg>
              </i>
              <span>Brachiosaurus</span>
            </a>
          </li>

          <!-- Add all the other <li> tags here-->

        </ul>

      </body>
      </html>
    lines:
      - num: "2-3"
        fade: true
      - num: 8
        text: |
          We’ll use the `<i>` tag and the `.icon` class to define the box surrounding our SVG icons.
      - num: 9
        text: |
          Now the `<svg>` tag. Inside it we have a `<use>` tag that points to our image.

          The `xlink:href=""` attribute on a `<use>` tag is comparable to the `src=""` attribute on an `<img>` tag.

          There are a few important parts to look at:

          1. `images/dino-icons.svg` — this is the path to the sprite sheet image file.
          2. The `#brachiosaurus` is the ID that Spritebot assigned the icon within the sprite sheet. The icon’s ID always matches it’s filename.
    after: |
      **Make sure you spell the ID properly in the `xlink:href=""`—Spritebot always makes the ID the same as the original filename you used to generate the sprite sheet.**

      Go ahead and put 2 more `<li>` tags into the code for each of the two other icons:

      - `#micropachycephalosaurus`
      - `#velociraptor`

  - title: "Preview in browser with “localhost”"
    before: |
      Now let’s load it up in our browser and see the icons.

      ![](chrome-error.jpg)

      *Or not…*

      If you’re using Firefox or Safari the icons should load right away. Chrome has tighter security restrictions and requires us to use a web server to see the icons.

      Luckily, Markbot has a web server built into it for use during our web development.

      ![](markbot.jpg)

      Press the “Browse Website” toolbar button or, in the `File` menu, go to `Browse Local Website` (`⌘B`)—this will pop open your default browser with the URL to your project running over with a web server.

      The URL will most likely be: [**https://localhost:8000/**](https://localhost:8000/).

      ![](chrome-security.jpg)

      Next up we’ll see a security error about the connection not being private. The browser doesn’t believe the HTTPS certificate Markbot uses is secure because it wasn’t signed by an authority.

      **You should never bypass this error message on websites.** In this situation it’s okay because we’re loading our “localhost” testing server.

      So, click “ADVANCED”.

      ![](chrome-security-proceed.jpg)

      Then click “Proceed to localhost (unsafe)”.

      ![](default-icons.jpg)

      Now we should see our icons!

  - title: "Create the layout"
    before: |
      Let’s start our CSS by making the basic layout for our icons.

      We’ll use Grid to put the icons side-by-side and Flexbox within the `<a>` tags for vertical alignment.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      *::after {
        box-sizing: inherit;
      }

      ul {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        justify-items: center;
        margin: 0;
        padding: 0;
      }

      a {
        display: flex;
        flex-direction: column;
        align-items: center;
      }
    lines:
      - num: "2-4"
        fade: true

  - title: "Style the icons"
    before: |
      Below is some boilerplate CSS code for styling icons—**you can copy-and-paste it into every website that uses SVG icons.**
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
        flex-direction: column;
        align-items: center;
      }

      .icon {
        position: relative;
        height: 8em;
        width: 8em;
      }

      .icon svg {
        left: 0;
        height: 100%;
        position: absolute;
        top: 0;
        width: 100%;
        fill: currentColor;
      }
    lines:
      - num: "2-4"
        fade: true
      - num: "8-9"
        text: |
          The `width` & `height` are the only parts you’ll want to change from website-to-website.
      - num: 18
        text: |
          The `currentColor` `fill` for the SVG it really important—it allows us to change the icon SVGs colour based on the parent element’s colour.

  - title: "Add colours & hovers"
    before: |
      Our icons are currently using the default link colours: blue & purple. (If you click on them they should all go purple.)

      So let’s add a little touch of CSS to colour the links better.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      a {
        display: flex;
        flex-direction: column;
        align-items: center;
        color: #76a500;
      }

      a:hover,
      a:focus {
        color: #acc300;
      }

      .icon {
        position: relative;
        height: 8em;
      ⋮
    lines:
      - num: "3-5,14-16"
        fade: true
      - num: 6
        text: |
          Because we did the SVG `currentColor` code for the icon’s SVG we can change its colour dynamically.
      - num: "9-12"
        text: |
          The dynamic colour change is really helpful when doing hover & focus effects!
    after: |
      A real basic green colour and a slightly different hover green.

      Test it out—should work great.
---
