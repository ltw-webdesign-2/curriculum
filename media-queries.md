---
layout: slide-deck
title: "Media queries"
desc: "A quick introduction to what media queries are, what they’re trying to achieve, and how they’re used."

slides:
  - type: super-big-text
    content: |
      **Media queries**

  - content: |
      ## The Web is for everybody

      It’s our job as web designers to make our website work in as many situations as possible

      **The web is responsive by default—if it doesn’t work on a specific device it’s your fault!**

  - type: code
    html: |
        <!-- Tells the browser we support whatever size it is & not to zoom in -->
        <meta name="viewport" content="width=device-width,initial-scale=1">
    css: |
      html {
        /* Tells the browser not to automatically scale the fonts—we want complete control */
        -webkit-text-size-adjust: 100%;
        text-size-adjust: 100%;
      }
    notes: |
      We’re going to start adding some new boilerplate code to our files.

      - One more line in the HTML: the viewport
      - A couple more lines in the CSS: text adjustments

  - content: |
      ## Media queries

      Detect the dimensions of the user’s screen and make layout adjustments

      - minimum width/height, orientation

      ---

      ### Or other things

      - print, black & white, retina, touch, mouse, etc.

  - content: |
      ## Do not use pixels—use em

      Try to avoid using pixels in media queries—they make us think in terms of devices instead of content

      **Our media queries should be based on content irregularities not on device sizes**

  - content: |
      ## Converting px to em

      Divide by 16 (the browser’s default size)

      ```
      400px ÷ 16 = 25em
      960px ÷ 16 = 60em
      ```

  - content: |
      ## Common media query widths

      - `25em` — small screens
      - `38em` — medium screens
      - `60em` — large screens
      - `90em` — extra large screens

      *I found these numbers work for me based on making lots of websites and seeing what numbers appear most often*

  - content: |
      ## Always start small!

      Media queries compound on top of each other and rely on the previous CSS

      1. Design for the small screen first
      2. Add media queries when the content becomes awkward

      **Do not start on large screens first—it doubles the amount of CSS you need to write!**

  - type: interactive
    resizable: true
    html: |
      <h1>Media queries</h1>
    css: |
      h1 {
        background-color: red;
      }

      @media only screen and (min-width: 25em) {
        h1 {
          background-color: green;
        }
      }

      @media only screen and (min-width: 38em) {
        h1 {
          background-color: yellow;
        }
      }
    css_lines:
      - num: "5-9"
        text: |
          When the content has `25em` of available space make the colour of the `<h1>` green.
      - num: "11-15"
        text: |
          When the content has `38em` of available space make the colour of the `<h1>` yellow.

  - type: interactive
    resizable: true
    html: |
      <ul>
        <li>Pteranodon</li>
        <li>Quetzalcoatlus</li>
      </ul>
    css: |
      ul {
        padding: 0;
        list-style-type: none;
      }
      li {
        padding: .5em .7em;
        background-color: #00675a;
        color: #fff;
      }
      @media only screen and (min-width: 60em) {
        ul { text-align: center; }
        li { display: inline-block; }
      }
    css_lines:
      - num: "10-13"
        text: |
          When the content has `60em` of available space make the `<li>` tags `inline-block` so they are side-by-side on the same line.

  - type: interactive
    resizable: true
    html: |
      <section>
        <h2>Hot Pink Purses</h2>
        <article>
          <h3>Pretty Pink Clutch</h3>
          <p>Just the right size to carry only what you need.</p>
          <a href="#">Buy now</a>
        </article>
        <article>
          <h3>Misty Morning Handbag</h3>
          <p>It’s bigger on the inside—a total bag of holding.</p>
          <a href="#">Buy now</a>
        </article>
      </section>
    css: |
      section {
        display: grid;
        grid-template-columns: 1fr;
        grid-template-areas: "header" "col1" "col2";
        gap: 1rem;
      }
      h2 {
        grid-area: header;
      }
      @media only screen and (min-width: 38em) {
        section {
          grid-template-columns: 1fr 1fr;
          grid-template-areas:
            "header header"
            "col1   col2";
        }
      }
    css_hidden: |
      html {
        font-size: 120%;
      }
      section {
        background-color: mistyrose;
        padding: 1rem;
      }
      h2 {
        margin: 0;
        color: mediumvioletred;
      }
      h3 {
        margin: 0;
        color: hotpink;
      }
      a {
        font-weight: bold;
        font-size: 1.125rem;
        color: mediumvioletred;
        border-bottom: 0;
        text-decoration: underline;
        text-decoration-thickness: .2em;
      }
    notes: |
      **We can really easily change our layouts by just changing the grid itself—all the elements all into place.**

  - type: code
    html: |
      <header>
        <h1>Quetzalcoatlus</h1>
        <nav>
          <ul>
            <li><a href="#env">Environment</a></li>
            <li><a href="#diet">Diet</a></li>
            <li><a href="#size">Dimensions</a></li>
          </ul>
        </nav>
      </header>
    css: |
      @media print {
        nav {
          display: none;
        }
      }
    notes: |
      We can target other things than just screen sizes with media queries. Here’s an example: `@media print` will allow us to change how our website looks when it’s printed to paper.

  - content: |
      ## Videos & tutorials

      - [All devices setup ➔](/topics/all-devices-setup/)
      - [Media queries ➔](/topics/media-queries/)
      - [Screen sizes cheat sheet ➔](/topics/screen-sizes-cheat-sheet/)

---
