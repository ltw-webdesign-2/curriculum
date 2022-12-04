---
layout: lesson
title: "Animated clock"
desc: "A lesson in using CSS keyframe animations to make a clock face with rotating hands."

markbot_submit: true
hide_show_for_marks: true

extra_tutorials:
  - title: "CSS animations slide deck"
    url: "/courses/web-design-2/css-animations/"
  - title: "CSS animations & effects"
    url: css-animations-effects
  - title: "CSS animations & effects cheat sheet"
    url: css-animations-effects-cheat-sheet
    highlight: true
  - title: "Using images"
    url: using-images

goal:
  video: "https://video-assets.learntheweb.courses/web-design-2/animated-clock-goal.mp4"
  video_poster: goal.png
  no_image: true
  before: |
    We’re going to write some code that will animate the hands of a clock around to simulate 12 hours. We’ll be using CSS `@keyframes` and a bunch of SVG graphics to complete the animation.
  notes:
    - label: "Type it, type it real good"
      text: "Remember the purpose of this lesson is to type the code out yourself—build up that muscle memory in your fingers!"

fork:
  url: "https://github.com/ltw-webdesign-2/animated-clock/fork"

download:
  url: "https://assets.learntheweb.courses/web-design-2/animated-clock-download.zip"

steps:
  - title: "Project files"
    before: |
      After forking and cloning the repository & downloading and exporting the files you should have the following folder structure:
    folders:
      - label: "animated-clock"
        type: folder
      - label: "images"
        type: folder
        indent: 1
        notes: "Export these from Illustrator"
      - label: "clock-center.svg"
        indent: 2
      - label: "clock-face.svg"
        indent: 2
      - label: "hand-hour.svg"
        indent: 2
      - label: "hand-minute.svg"
        indent: 2
      - label: "css"
        type: folder
        indent: 1
      - label: "main.css"
        indent: 2
      - label: "modules.css"
        indent: 2
      - label: "index.html"
        indent: 1
    after: |
      *There’s also some HTML & CSS already coded so we can concentrate completely on styling the clock and making it animate.*

  - title: "Write some HTML"
    before: |
      We’ll start by writing out some HTML for the clock face. The centre piece and the two hands will be `<img>` tags, but the clock face will be a `background-image`
    code_lang: "html"
    code_file: "index.html"
    code: |
      ⋮
      <body>

        <div class="clock-face">
          <img class="hand hand-hour" src="images/hand-hour.svg" alt="">
          <img class="hand hand-minute" src="images/hand-minute.svg" alt="">
          <img class="clock-center" src="images/clock-center.svg" alt="">
        </div>

      </body>
      ⋮
    lines:
      - num: "5-6"
        text: |
          Notice that there are two classes here: `.hand` and a more specific one. We’re going to save some typing by putting the common CSS on the `.hand` class.
    after: |
      There isn’t really anything spectacular in that code—just plain ol’ HTML.

      *In the browser we should see this—which isn’t much to look at:*

      ![](html.png)

  - title: "Style the clock face"
    before: |
      Next up we need to style the clock face using `background-image` and a few other small things. It makes the most sense to use a `background-image` for the clock face for two reasons:

      1. It doesn’t animate, so we don’t really need to access it.
      2. The clock pieces, like the hands, are in front of it. Because the clock face is a background image it’s much less work to get the bits in front.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      *,
      *::before,
      *::after {
        box-sizing: inherit;
      }

      .clock-face {
        height: 300px;
        margin: 50px auto;
        position: relative;
        width: 300px;

        background: transparent url("../images/clock-face.svg") no-repeat center center;
      }
    lines:
      - num: "1-3"
        fade: true
      - num: 9
        text: |
          The `50px` margin is just to push the clock downwards from the top a little bit—we’d probably use `.pad-top` or something in a real website.
      - num: 13
        text: |
          To save some typing we have all the `background` properties on one line: `color`, `image`, `repeat`, `position`
    after: |
      So we should see this now:

      ![](clock-face.png)

  - title: "Style the hands"
    before: |
      Using `position` and some coordinates we can get the hands and the centre piece of the clock in place.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .clock-center {
        bottom: calc(50% - 14px);
        left: calc(50% - 14px);
        position: absolute;
        width: 28px;
      }

      .hand {
        bottom: calc(50% - 8px);
        left: calc(50% - 7px);
        position: absolute;
        width: 14px;

        transform-origin: 50% calc(100% - 8px);
      }
    lines:
      - num: "3-4"
        text: |
          We know that the centre piece is `28px` wide. So to get it exactly in the centre of the clock face we can set the `left` & `bottom` coordinates to `50% - 14px` (`14px` being half of `28px`).
      - num: 9
        text: |
          All these CSS properties are shared with both clock hands, that’s why we’re targeting the `.hand` class.
      - num: "10-11"
        text: |
          This is definitely a little silly because the black centre peice covers it but I wanted to create the impression that the clock hands weren’t pivoting on their edge, but that they had like a physical “pin” set in the bottom center of the rounded part—so I positioned them in a “realistic” fashion.
      - num: 15
        text: |
          The default `transform-origin` for an element is the direct centre—that doesn’t make sense for a clock hand. So this will change the anchor point to be placed in my invisible “pin” rotation point for the clock hands.
    after: |
      Refresh it in  your browser and you’ll see the hands and the centre piece are nicely aligned.

      ![](clock-hands.png)

  - title: "Animate the minute hand"
    before: |
      We’re going to start by animating the minute hand, because that’s the one we can see right now. We’ll need a `@keyframes` block and an `animation` property targeted at just that single hand.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .hand-minute {
        animation: hand-rotate .5s linear infinite;
      }

      @keyframes hand-rotate {

        0% {
          transform: rotate(0deg);
        }

        100% {
          transform: rotate(360deg);
        }

      }
    lines:
      - num: 3
        text: |
          The `animation` property is connecting the `@keyframes` block with this element. We are specifying the following things:

          - `hand-rotate` is the name we chose for the `@keyframes` block.
          - `.5s` is the time it takes for the hand to fully rotate around the clock.
          - `linear` means there is no easing.
          - `infinite` means that the animation never stops—it keeps looping.
      - num: 6
        text: |
          Immediately after the `@keyframes` keyword we need to come up with a name for this block, here we are naming these keyframes `hand-rotate`
      - num: "8-10"
        text: |
          At the start of the animation (`0%`) the rotation of the hand is `0deg`
      - num: "12-14"
        text: |
          At the end of the animation the rotation is `360deg` meaning the hand will complete a full rotation around a circle.
    after: |
      Try it out! You should see the minute hand moving around the clock.

  - title: "Animate the hour hand"
    before: |
      Finally we’re going to make the hour hand rotate. This one is really easy because it’s animation is exactly the same as the minute hand—it just takes a longer time to rotate.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .hand-hour {
        animation: hand-rotate 6s linear infinite;
      }
    lines:
      - num: 3
        text: |
          The only difference is that the time is now `6s`. From a clock perspective this allows the minute hand to rotate 12 times, 1 rotation for each hour, while the hour hand only rotates a single time.
    after: |
      That’s it—give it a whirl!

---
