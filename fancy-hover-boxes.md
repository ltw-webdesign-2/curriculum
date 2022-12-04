---
layout: lesson
title: "Fancy hover boxes"
desc: "An exercise using transitions to create hover boxes that fade from black & white to colour."

markbot_submit: true
hide_show_for_marks: true

extra_tutorials:
  - title: "Transforms & transitions slide deck"
    url: "/courses/web-design-2/transforms-transitions/"
  - title: "Position & z-index"
    url: position-zindex
    highlight: true
  - title: "CSS animations & effects"
    url: css-animations-effects
    highlight: true
  - title: "CSS animations & effects cheat sheet"
    url: css-animations-effects-cheat-sheet
    highlight: true
  - title: "Images cheat sheet"
    url: images-cheat-sheet

goal:
  before: |
    We’re going to explore how to use transitions to make fancy hover boxes where images go from greyscale to coloured and zoom in when hovered.
  no_image: true
  video: "https://video-assets.learntheweb.courses/web-design-2/fancy-hover-boxes-goal.mp4"
  video_poster: goal.jpg
  notes:
    - label: "Type it, type it real good"
      text: "Remember the purpose of this lesson is to type the code out yourself—build up that muscle memory in your fingers!"

fork:
  url: "https://github.com/ltw-webdesign-2/fancy-hover-boxes"

steps:
  - title: "Project files"
    before: |
      After forking & cloning the repository to your computer you should have the following files:
    folders:
      - label: "fancy-hover-boxes"
        type: folder
      - label: "images"
        type: folder
        indent: 1
      - label: "black.jpg"
        indent: 2
      - label: "blue.jpg"
        indent: 2
      - label: "orange.jpg"
        indent: 2
      - label: "yellow.jpg"
        indent: 2
      - label: "css"
        type: folder
        indent: 1
      - label: "main.css"
        indent: 2
      - label: "index.html"
        indent: 1
      - label: "humans.txt"
        indent: 1
        notes: "Citations for image usage"
    after: |
      *There’s also some HTML & CSS already coded so we can concentrate completely on making the hover boxes work.*

  - title: "Start some HTML"
    before: |
      The HTML boilerplate already exists for us, we just need to write the hover box HTML. Open up `index.html` and we’ll add in the HTML for the hover boxes.
    code_lang: "html"
    code_file: "index.html"
    code: |
      ⋮
      <body>

        <section>
          <a class="hover-box" href="#">
            <img src="images/orange.jpg" alt="">
            <h2>Orange butterflies</h2>
          </a>
          <a class="hover-box" href="#">
            <img src="images/black.jpg" alt="">
            <h2>Black butterflies</h2>
          </a>
          <a class="hover-box" href="#">
            <img src="images/blue.jpg" alt="">
            <h2>Blue butterflies</h2>
          </a>
          <a class="hover-box" href="#">
            <img src="images/yellow.jpg" alt="">
            <h2>Yellow butterflies</h2>
          </a>
        </section>

      </body>
      ⋮
    lines:
      - num: "2,23"
        fade: true
      - num: 5
        text: |
          Notice the `.hover-box` class is on the `<a>` tag—we’ll be styling that later.
    after: |
      If we were to refresh in the browser right now we’d see some text & images. So we need a little CSS.

  - title: "Style the basic grid"
    before: |
      Let’s create the basic grid to lay out the butterfiles in their boxes.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      section {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(20rem, 1fr));
      }
    lines:
      - num: 4
        text: |
          We’ll use `repeat()` and `auto-fit` & `minmax` to get the browser to intrinsically layout the boxes in a row.
    after: |
      After typing out the above code, refresh in the browser and you see this row of butterflies:

      ![](row.jpg)

  - title: "Style the image & caption"
    before: |
      Before we can make any transitions, we need to get the image & caption looking nice.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .hover-box {
        position: relative;
        overflow: hidden;
        text-decoration: none;
        color: #fff;
      }

      .hover-box h2 {
        position: absolute;
        bottom: 0;
        width: 100%;
        padding: 1rem;
        margin: 0;
        text-align: center;
        background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.5));
        text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.9);
      }

      .hover-box img {
        filter: grayscale(100%);
      }
    lines:
      - num: 3
        text: |
          Make the hover box position relative so it can contain the caption inside.
      - num: 4
        text: |
          Chop off anything that exists outside the hoverbox: this will be important later.
      - num: "10-11"
        text: |
          Use position absolute & coordinates to get our heading into the right place.
      - num: 21
        text: |
          The `filter` property allows us to add a bunch of different effects to all HTML elements, including text. Here we’re using the `grayscale()` filter to desaturate the image into black & white. The `100%` specifies that we want complete greyscale, a lower percent would be less greyscale and have more colour.

          **Make sure to spell “gray” the American way.**

    after: |
      Check it out in the browser:

      ![](captions.jpg)

  - title: "Make the captions disappear"
    before: |
      Let’s use some CSS positioning & hover effects to make the captions disappear & reappar.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .hover-box h2 {
        position: absolute;
        bottom: -4em;
        width: 100%;
        padding: 1rem;
        margin: 0;
        text-align: center;
        background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.5));
        text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.9);
      }

      .hover-box:hover h2,
      .hover-box:focus h2 {
        bottom: 0;
      }

      .hover-box img {
        filter: grayscale(100%);
        transition: all 0.2s linear;
      }
    lines:
      - num: "3,5-10,18-21"
        fade: true
      - num: 4
        text: |
          Make the bottom coordinate of the caption a negative number, therefore shoving it off the bottom.

          Because we added `overflow: hidden` earlier, we can’t see the caption any more.
      - num: "13-16"
        text: |
          Add hover & focus effects to the `.hover-box`, targetting the `<h2>` and reset it’s bottom coordinate to `0`.

  - title: "Add the caption transition"
    before: |
      Now let’s make this a little fancy with a transition on the caption. The `transition` will allow the caption to animate into it’s location instead of just popping into place.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .hover-box-caption {
        background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.5));
        text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.9);
        transition: all .2s linear;
      }
      ⋮
    lines:
      - num: "3-4"
        fade: true
      - num: 5
        text: |
          The `transition` property will allow any CSS numerical changes to animate. In this case only the `bottom` property changes, so it will be the thing that animates.

          - `all` properties that change will be animated.
          - `.2s` is the length of time the animation will take.
          - `linear` is the type of easing, “linear” meaning “no easing”.

  - title: "Add effects to the image"
    before: |
      Since this lesson is all about being “fancy” let’s fancify the image too. We’re going to make the image black & white, then when hovered it will become coloured and zoom in a little bit.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .hover-box img {
        filter: grayscale(100%);
        transition: all .2s linear;
      }

      .hover-box:hover img,
      .hover-box:focus img {
        filter: grayscale(0);
        transform: scale(1.1);
      }
    lines:
      - num: 3
        fade: true
      - num: 4
        text: |
          Since the `filter` is a numerical property we can totally transition it too.
      - num: 9
        text: |
          Undo the greyscale filter by setting it to `0`
      - num: 10
        text: |
          We can use the `transform` property to grow the image a little bit. The `scale()` function will allow us to grow or shrink HTML elements: `1` is what an element currently is, so `1.1` is just slightly larger.
    after_video: "https://video-assets.learntheweb.courses/web-design-2/fancy-hover-boxes-effect.mp4"
    after: |
      Wonderful! Some fancy-fied butterflies.

---
