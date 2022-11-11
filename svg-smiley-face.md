---
layout: lesson
title: "SVG smiley face"
desc: "Hand write SVG code to create an interactive smiley face."

hide_show_for_marks: true
markbot_submit: true

extra_tutorials:
  - title: "Advanced SVG"
    url: advanced-svg
  - title: "Advanced SVG slide deck"
    url: "/courses/web-design-2/advanced-svg/"
  - title: "SVG cheat sheet"
    url: svg-cheat-sheet
    highlight: true
  - title: "CSS animations & effects cheat sheet"
    url: css-animations-effects-cheat-sheet

goal:
  before: |
    We’re going to look at hand writing some SVG & CSS to create an interactive smiley face.

    When hovering over the face the eyebrows will tilt from happy to angry positions.
  no_image: true
  video: "https://assets.learntheweb.courses/web-design-2/svg-smiley-face/goal.mp4"
  video_poster: "goal.jpg"
  notes:
    - label: "Type it, type it real good"
      text: "Remember the purpose of this lesson is to type the code out yourself—build up that muscle memory in your fingers!"

fork:
  url: "https://github.com/ltw-webdesign-2/svg-smiley-face"

steps:
  - title: "Set up project"
    before: |
      Before we get started, create some files and get ready.
    folders:
      - label: "smiley-face"
        type: folder
      - label: "index.html"
        indent: 1
      - label: "css"
        type: folder
        indent: 1
      - label: "main.css"
        indent: 2
    after: |
      1. Make an `index.html` & add the boilerplate code.
      2. Make a `main.css` in your `css` folder—it can remain empty.
    notes:
      - label: "Naming conventions"
        text: "Don’t forget to follow the [naming conventions](/topics/naming-paths-cheat-sheet/#naming-conventions)."
      - label: "HTML snippets"
        text: "Create the boilerplate with `html5`, `viewport`, `css`"

  - title: "SVG wrapper"
    before: |
      Inside our HTML we’ll start by writing the code for the SVG—specifically defining the dimensions and the artboard.
    code_lang: html
    code_file: "index.html"
    code: |
      ⋮
      </head>
      <body>

        <svg class="smiley" width="256" height="256" viewBox="0 0 256 256">

        </svg>

      </body>
      </html>
      ⋮
    lines:
      - num: "2-3"
        fade: true
      - num: 5
        text: |
          We can add `class` attributes to the SVG elements.

          The `width` & `height` define the dimensions of the image.

          ---

          The `viewBox` defines the artboard in the image, a cropping zone. It’s almost always the same as the width & height.

          - `0 0` — the top left corner’s x & y coordinates.
          - `256 256` — the width and height of the art board.
      - num: "9-10"
        fade: true

  - title: "Draw the face circle"
    before: |
      Using SVG’s `<circle>` tag we can create the face.
    code_lang: html
    code_file: "index.html"
    code: |
      ⋮
        <svg class="smiley" width="256" height="256" viewBox="0 0 256 256">
          <circle class="face" cx="128" cy="128" r="120" />
        </svg>
      ⋮
    lines:
      - num: 2
        fade: true
      - num: 3
        text: |
          - `cx` — the center x coordinate, measured from the left of the image
          - `cy` — the center y coordinate, measured from the the top of the image
          - `r` — the radius of the circle, measured from the `cx` & `cy`

          Notice the closing slash at the end of the `<circle … />` tag: because this is XML self-closing tags **must** include their own slash.
      - num: 4
        fade: true
    after: |
      You should see a black circle when you refresh in the browser.

      *Here’s an explanation of the different attributes on the `<circle>` tag:*

      ![](face.png)

  - title: "Make the face yellow"
    before: |
      SVGs use CSS for much of their visual style—the only difference is the properties that are used to apply visual design.
    code_lang: css
    code_file: "css/main.css"
    code: |
      .face {
        fill: gold;
      }
    lines:
      - num: 1
        text: "We select things the same as with HTML, using classes or tags."
      - num: 2
        text: "The `fill` property is used to colour SVG shapes."
    after: |
      ![](face-yellow.png)

  - title: "Add the eyes"
    before: |
      Using two more `<circle>` tags we can add the eyes onto our smiley face.
    code_lang: html
    code_file: "index.html"
    code: |
      ⋮
        <svg class="smiley" width="256" height="256" viewBox="0 0 256 256">
          <circle class="face" cx="128" cy="128" r="120" />
          <circle class="left-eye" cx="100" cy="104" r="12" />
          <circle class="right-eye" cx="156" cy="104" r="12" />
        </svg>
      ⋮
    lines:
      - num: "2-3"
        fade: true
      - num: "4-5"
        text: "Two new circles. We don’t need to add `fill` because they’ll automatically be black."
      - num: 6
        fade: true
    after: |
      ![](eyes.png)

  - title: "Add the mouth"
    before: |
      Using the SVG `<path>` tag we can create really complex paths and shapes. We can use it now to make the smile.
    code_lang: html
    code_file: "index.html"
    code: |
      ⋮
        <svg class="smiley" width="256" height="256" viewBox="0 0 256 256">
          <circle class="face" cx="128" cy="128" r="120" />
          <circle class="left-eye" cx="100" cy="104" r="12" />
          <circle class="right-eye" cx="156" cy="104" r="12" />
          <path class="mouth" d="M100,160 Q128,190 156,160" />
        </svg>
      ⋮
    lines:
      - num: "2-5"
        fade: true
      - num: 6
        text: |
          All the fanciness for the `<path>` is controlled by the `d=""` attribute—it gives coordinates for anchor points and for control handles.

          - `M100,160` — the starting anchor point for the path.
          - `Q128,190` — means we want to use a quadratic bézier curve, giving us only one control handle for the curve. The coordinates are the handle’s location.
          - `156,160` — the coordinate for the last anchor point.
      - num: 7
        fade: true

    after: |
      In the `d=""` attribute there’s a lot of complexity going on, here’s a break down of what each thing is doing.

      ![](mouth.png)

      **You won’t be able to see the mouth in your browser yet.**

  - title: "Style the mouth"
    before: |
      We can’t see the mouth in our SVG face yet because the path exists but it doesn’t have a defined, visible stroke. We do that with CSS.
    code_lang: css
    code_file: "css/main.css"
    code: |
      ⋮
      .face {
        fill: gold;
      }

      .mouth {
        fill: none;
        stroke: #000;
        stroke-width: 6px;
        stroke-linecap: round;
      }
    lines:
      - num: "2-4"
        fade: true
      - num: 8
        text: "The colour of the stroke on the shape."
      - num: 9
        text: "The thickness of the shape’s stroke."
      - num: 10
        text: "Makes the ends of the stroke into rounded corners instead of sharp edges."
    after: "*Now the mouth should be visible in the browser.*"

  - title: "Add the eyebrows"
    before: |
      Let’s use the `<rect>` tag to create a set of eyebrows.
    code_lang: html
    code_file: "index.html"
    code: |
      ⋮
        <svg class="smiley" width="256" height="256" viewBox="0 0 256 256">
          <circle class="face" cx="128" cy="128" r="120" />
          <circle class="left-eye" cx="100" cy="104" r="12" />
          <circle class="right-eye" cx="156" cy="104" r="12" />
          <path class="mouth" d="M100,160 Q128,190 156,160" />
          <rect class="left-eyebrow" x="97" y="66" width="6" height="32" rx="4" ry="4" />
          <rect class="right-eyebrow" x="153" y="66" width="6" height="32" rx="4" ry="4" />
        </svg>
      ⋮
    lines:
      - num: "2-6"
        fade: true
      - num: "7-8"
        text: |
          There are a bunch of attributes here to create the rectangle:

          - `x` — the top left x coordinate
          - `y` — the top left y coordinate
          - `width` — how wide the rectangle is
          - `height` — how tall the rectangle is
          - `rx` — the horizontal border-radius size
          - `ry` — the vertical border-radius size
      - num: 9
        fade: true
    after: |
      This is what we should be looking at in our browser right now:

      ![](eyebrows.png)

  - title: "Rotate the eyebrows"
    before: |
      Using the CSS `transform: rotate()` property we can adjust the eyebrows to look happy.
    code_lang: css
    code_file: "css/main.css"
    code: |
      ⋮
        stroke-width: 6px;
        stroke-linecap: round;
      }

      .left-eyebrow {
        transform: rotate(80deg);
      }

      .right-eyebrow {
        transform: rotate(100deg);
      }
    lines:
      - num: "2-4"
        fade: true
    after: |
      **If we look in the browser right now we won’t see the eyebrows any more.** It’s because `transform-origin` is set to the top-left of the SVG by default.

      Here’s a little visualization of what’s happening right now:

      ![](busted-eyebrows.png)

  - title: "Fix the eyebrow anchor points"
    before: |
        We want to get the `transform-origin` anchor point in the center of the rectangle, but `center center` doesn’t work on SVG.

        So we need to use pixel coordinates instead.
    code_lang: css
    code_file: "css/main.css"
    code: |
      ⋮
      .left-eyebrow {
        transform: rotate(80deg);
        transform-origin: 100px 82px;
      }

      .right-eyebrow {
        transform: rotate(100deg);
        transform-origin: 156px 82px;
      }
    lines:
      - num: 3
        fade: true
      - num: 4
        text: |
          - The horizontal point, `100px`, is the exact center of the rectangle measured from the left edge.
          - The vertical point, `82px`, is the exact center of the rectangle measure from the top edge.
      - num: 8
        fade: true
    after: |
      With these `transform-origin` properties we can now see the eyebrows exactly where we want them to be.

      Here’s a little visualization of where those numbers came from:

      ![](eyebrow-transform-origin.png)

  - title: "Interactivity with transitions"
    before: |
      Let’s add a little interactivity with transitions. We’re going to make the eyebrows rotate into an angry state when you hover over the face.
    code_lang: css
    code_file: "css/main.css"
    code: |
      ⋮
      .left-eyebrow {
        transform: rotate(80deg);
        transform-origin: 100px 82px;
        transition: all .5s linear;
      }

      .right-eyebrow {
        transform: rotate(100deg);
        transform-origin: 156px 82px;
        transition: all .5s linear;
      }

      .smiley:hover .left-eyebrow {
        transform: rotate(100deg);
      }

      .smiley:hover .right-eyebrow {
        transform: rotate(80deg);
      }
    lines:
      - num: "3-4"
        fade: true
      - num: 5
        text: "Add a `transition` to the default state for the eyebrows so they’ll be animated when hovered."
      - num: "9-10"
        fade: true
      - num: 14
        text: |
          Read this selector from right-to-left: “choose the `.left-eyebrow` when the user `:hover`s the `.smiley`.

          I’ve specifically done this so we don’t have to hover directly on the eyebrow for the animation to trigger, we can hover anywhere on the smiley face.
    after: |
      *Try it out!*

---
