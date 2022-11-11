---
layout: slide-deck
title: "CSS animations"
desc: "A quick overview of CSS animation and keyframe properties."

slides:
  - type: super-big-text
    content: |
      **CSS animations**

  - content: |
      ## Animations

      *Complex keyframe-based animations that can autoplay*

      - Combination of two things:
        1. `@keyframes` block
        2. `animation` property

  - content: |
      ## `@keyframes`

      - Defines each change to CSS properties over time
      - Multiple different keyframes for every animation
      - Defined in percentages—allowing the animation time-length to be variable

  - type: code
    notes: |
      The `@keyframes` block defines what properties will change and how they’ll change but does not specify which element to affect.
    css: |
      @keyframes rainbow-y-fade-y-thing-y {

        0% {
          background-color: red;
        }

        50% {
          background-color: orange;
        }

        100% {
          background-color: yellow;
        }

      }
    css_lines:
      - num: 1
        text: |
          After the `@keyframes` declaration you can name the block whatever you want.
      - num: 3
        text: |
          Each keyframe is represented by a percentage.
      - num: 4
        text: |
          Inside the keyframe, any numerical property can be animated.

          **We do not specify the element that this affects, only the property that changes.**

  - content: |
      ## `animation`

      - Connects a specific set of `@keyframes` to an element
      - Controls how the keyframes are played: time, direction, iterations, etc.

  - type: code
    notes: |
      The `animation` property connects the `@keyframes` to an element.
    css: |
      .box {
        animation: rainbow-y-fade-y-thing-y 2s linear;
      }
    css_lines:
      - num: 1
        text: |

          There’s lots of information here—many pieces resemble `transition`

          1. `rainbow-y-fade-y-thing-y` is the name we came up with for the `@keyframes` block.
          2. `2s` is the time the keyframes will play.
          3. `linear` is the easing, aka no easing in this situation.

  - type: interactive
    html: |
      <div class="purple"></div>
    css: |
      .purple {
        transform-origin: right bottom;
        animation: spin 1s infinite alternate;
      }
      @keyframes spin {
        /* Markbot won’t like this spacing; */
        /* it’s compressed to fit on the screen */
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }
    css_lines:
      - num: 2
        text: |
          The `transform-origin` property controls the anchor point of a `transform`
      - num: 3
        text: |
          There are a few pieces of information:

          1. `spin` — the name of the keyframes block
          2. `1s` — the time the keyframes take to play
          3. `infinite` — repeat the keyframes infinite number of times
          4. `alternate` — play the keyframes forwards then backwards
    css_hidden: |
      div {
        width: 200px;
        height: 200px;
        margin: 100px;
      }
      .purple {
        background-color: #9d35af;
      }

  - type: image
    image: transition-or-animation.svg
    alt: "A flow-chart denoting when to pick `animation` & when to pick `transition`"
    notes: |
      1. Does the effect start immediately? Choose `animation`
      2. Does the effect require more properties changes than just start & end? Choose `animation`
      3. Otherwise choose `transition`

  - content: |
      ## Videos & tutorials

      - [CSS animations & effects ➔](/topics/css-animations-effects/)
      - [CSS animations & effects cheat sheet ➔](/topics/css-animations-effects-cheat-sheet/)

---
