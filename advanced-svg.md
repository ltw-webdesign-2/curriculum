---
layout: slide-deck
title: "Advanced SVG"
desc: "An introduction to writing SVG code by hand and integrating it with CSS effects like animations & transitions."

slides:
  - type: super-big-text
    content: |
      **Advanced SVG**

  - content: |
      ## SVGs are just code

      We can open them directly in our code editor

      *They’re completely hackable!*

  - content: |
      ## Writing SVG

      SVGs look very similar to HTML—but they are XML

      - `<svg>` — everything goes inside
      - `<circle>`
      - `<rect>`
      - `<ellipse>`
      - etc.
    notes: |
      SVG isn’t nearly as forgiving as HTML because XML, what SVG is built on, is extremely strict.

      - Unclosed tags will stop the whole image from working
      - Self-closing tags must have a `/` at the end

  - type: interactive
    svg: |
      <svg width="256" height="256" viewBox="0 0 256 256" xmlns="http://www.w3.org/2000/svg">
        <circle cx="120" cy="120" r="50" />
        <rect x="0" y="0" width="75" height="75" />
        <ellipse cx="200" cy="200" rx="50" ry="30" />
      </svg>
    svg_lines:
      - num: 1
        text: |
          The `width`, `height` & `viewBox` are always necessary. The `xmlns` attribute is required only when the SVG is in a separate file.
      - num: 2
        text: |
          The `<circle>` element will draw a circle to the screen. It needs a few different attributes:

          - `cx` — the centre “x” coordinate
          - `cy` — the centre “y” coordinate
          - `r` — the radius of the circle

          **Notice that this must have a closing slash (`/`) at the end inside the element. If we compare this to another self-closing tag: the `<img>` tag, the image doesn’t need the slash because its HTML, but the SVG elements does because its XML.

  - content: |
      ## SVGs use CSS!

      Most of the visual look of SVGs comes from CSS

      *Just the properties are a little different*

  - type: interactive
    notes: |
      You may notice that the CSS properties for SVG are named more similarly to what Illustrator calls things: like `fill` instead of `background-color`
    svg: |
      <svg width="256" height="256" viewBox="0 0 256 256" xmlns="http://www.w3.org/2000/svg">
        <circle cx="120" cy="120" r="50" />
        <rect x="0" y="0" width="75" height="75" />
        <ellipse cx="200" cy="200" rx="50" ry="30" />
      </svg>
    css_lines:
      - num: 2
        text: |
          The `fill` CSS property changes the shape’s colour.
      - num: '6-7'
        text: |
          We can add borders, called `stroke` in SVG using the `stroke-*` properties.
    css: |
      rect {
        fill: yellow;
      }
      ellipse {
        fill: limegreen;
        stroke: #000;
        stroke-width: 5px;
      }

  - content: |
      ## Styles on tags

      We can also write the styles directly on the tags—and when we export from Illustrator that’s what happens

      *The SVG style attributes can be overwritten by CSS*

  - type: interactive
    svg: |
      <svg width="256" height="256" viewBox="0 0 256 256" xmlns="http://www.w3.org/2000/svg">
        <circle fill="limegreen" cx="120" cy="120" r="50" />
      </svg>
    svg_lines:
      - num: 2
        text: |
          Notice the `fill` attribute on the `<circle>`: it’s the same as using the CSS `fill` property.
    css: |
      circle {
        fill: yellow;
      }
    css_lines:
      - num: 2
        text: |
          The `fill` attribute in the SVG can be overwritten by the `fill` CSS property.

  - content: |
      ## Why have an extra file?

      The SVG code can be embedded directly in your HTML

      *Just copy and paste all the SVG code*

  - type: interactive
    html: |
      <body>
        <svg width="256" height="256" viewBox="0 0 256 256">
          <circle cx="120" cy="120" r="50" />
        </svg>
      </body>
    html_lines:
      - num: 2
        text: |
          When embedding SVG inside an HTML document we can get rid of the `xmlns` attribute. Why write extra code when we don’t have to.

  - content: |
      ## SVG interactivity

      Embedded SVGs can have effects:

      - `:hover`
      - `transition`
      - `animation`
      - `transform`

  - type: interactive
    notes: |
      Since the SVG is embedded in our HTML we can apply effects to it in our CSS like `transition` and `:hover`
    html: |
      <svg id="black-hole" width="256" height="256" viewBox="0 0 256 256">
        <circle cx="120" cy="120" r="50" />
      </svg>
    css: |
      #black-hole {
        transition: all .5s linear;
      }
      #black-hole:hover {
        fill: lightsteelblue;
      }

  - content: |
      ## SVG symbols

      - Just like Illustrator there can be symbols in SVG
      - We can create a symbol library—a sprite sheet
      - And use the symbols many times in our website

      *Makes for a great icon sets.*
    notes: |
      When previewing a symbol library in Finder it will appear empty. That’s because the it doesn’t contain any artwork on the artboard—the symbols haven’t been used yet.

  - content: |
      ## Using SVG for icons

      - Icons can be at the top of the HTML
        <br>*or*
      - Icons can be in a separate file

      *A separate file is usually better for performance & maintenance because it can be shared, edited and reused.*

  - type: interactive
    html: |
      <!-- At the top of the HTML -->
      <svg hidden>
        <symbol id="the-circle" viewBox="0 0 48 48">
          <circle cx="24" cy="24" r="22" fill="tomato" />
        </symbol>
        <symbol id="the-triangle" viewBox="0 0 48 48">
          <polygon points="24,2 46,46 2,46" fill="yellowgreen" />
        </symbol>
      </svg>

      <!-- Further down the HTML -->
      <i class="icon i-128">
        <svg><use xlink:href="#the-triangle"></use></svg>
      </i>

      <i class="icon i-128">
        <svg><use xlink:href="#the-circle"></use></svg>
      </i>

      <i class="icon i-24">
        <svg><use xlink:href="#the-triangle"></use></svg>
      </i>
    html_hidden: |
      <link href="modules.css" rel="stylesheet">
    html_lines:
      - num: 2
        text: |
          We can paste the sprite sheet into the top of our HTML—notice how there is nothing inside the sprite sheet except `<symbol>` objects.
      - num: 3
        text: |
          Each symbol must have two pieces of information:

          1. An `id`—this is how we call to the icon and display it
          2. A `viewBox`—each `<symbol>` requires a unique `viewBox`, but the surrounding `<svg>` tag does not
      - num: 13
        text: |
          We can then import an SVG symbol into another `<svg>` graphic with the `<use>` tag. The `xlink:href` points to the `id` of the `<symbol>` we want to display.

  - type: interactive
    html: |
      <!-- Icons in a separate sprite sheet -->
      <i class="icon i-96">
        <svg><use xlink:href="images/icons.svg#the-circle"></use></svg>
      </i>

      <i class="icon i-128">
        <svg><use xlink:href="images/icons.svg#the-triangle"></use></svg>
      </i>

      <i class="icon i-48">
        <svg><use xlink:href="images/icons.svg#the-circle"></use></svg>
      </i>
    html_hidden: |
      <link href="modules.css" rel="stylesheet">
    html_lines:
      - num: 3
        text: |
          We can also import symbols from external SVG symbol libraries by providing a path to the `.svg` file followed by the icons’s `id`

  - type: interactive
    html: |
      <!-- No `fill` attributes in the symbol -->
      <svg hidden>
        <symbol id="the-circle" viewBox="0 0 48 48">
          <circle cx="24" cy="24" r="22" />
        </symbol>
      </svg>

      <i class="icon i-128">
        <svg><use xlink:href="#the-circle"></use></svg>
      </i>
    html_lines:
      - num: 4
        text: |
          If we completely remove the fill from a symbol we can control its colour in the CSS.

          To remove the fill set it to absolute black in Illustrator, `#000000`, then when exported it’ll get automatically removed.
    css: |
      .icon {
        color: tomato;
        transition: all .25s linear;
      }
      .icon:hover {
        color: orange;
      }
    css_lines:
      - num: "2-3"
        text: |
          We can add the `color` attribute (assuming we’ve included `modules.css`) to adjust the `fill` of the SVG symbol. Without `modules.css` we’d have to specify `fill` directly.

          And, of course, transitions work perfectly well too.

          ---

          **Why color works instead of fill?**

          We can use `color` instead of `fill` when `modules.css` is included because it has a little snippet of code to allow it.

          ```
          svg {
            fill: currentColor;
          }
          ```

          This snipped of code changes the `fill` to be the value of the current `color`
    html_hidden: |
      <link href="modules.css" rel="stylesheet">

  - type: figure
    image: spritebot.jpg
    caption: "Use Spritebot to combine different SVG graphics into a sprite sheet"
    notes: |
      Spritebot isn’t the only tool to create sprite sheets—there are a few others online but I didn’t find their user experience pleasant.

      Spritebot even allows you to edit a sprite sheet by dropping it in again where you can add & remove symbols.

  - content: |
      ## Videos & tutorials

      - [Image formats · SVG ➔](/topics/image-formats/#svg)
      - [Advanced SVG ➔](/topics/advanced-svg/)
      - [SVG cheat sheet ➔](/topics/svg-cheat-sheet/)

---
