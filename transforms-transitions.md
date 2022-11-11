---
layout: slide-deck
title: "Transforms & transitions"
desc: "A quick overview of the CSS transform & transition properties for animating websites."

slides:
  - type: super-big-text
    content: |
      **Transforms & transitions**

  - content: |
      ## CSS effects

      CSS has a bunch off different effect properties built-in, with slightly different features.

      We’ll look at the two easier ones this week: `transform` & `transition`

  - content: |
      ## `transform`

      Visual effects that can be applied to any HTML element; but, by themselves, they are not interactive.

      - Rotations
      - Skewing
      - Scaling up or down
      - etc.

  - type: interactive
    notes: |
      Use the `transform` property to affect an element—there are whole bunch of built-in transformations but there are really only a few commonly used ones.
    html: |
      <div class="violet"></div>
      <div class="purple"></div>
      <div class="green"></div>
    css_lines:
      - num: 2
        text: "The `rotate()` transformation simply rotates an element and all its contents. You can use negative numbers, like `rotate(-33deg)` to go backwards."
      - num: 8
        text: |
          If you want to have more than one `transform` you can’t use the `transform` property multiple times; the way CSS works, only the last `transform` will be applied.

          So we must put each different transform function on the same line, separated by a space.

          This will both scale *and* rotate the element.
    css: |
      .violet {
        transform: rotate(33deg);
      }
      .purple {
        transform: skew(24deg);
      }
      .green {
        transform: scale(1.5) rotate(-6deg);
      }
    css_hidden: |
      div {
        width: 100px;
        height: 100px;
        margin: 50px 100px;
      }
      .violet {
        background-color: #5e54af;
      }
      .purple {
        background-color: #9d35af;
      }
      .green {
        background-color: #00675a;
      }

  - content: |
      ## `transition`

      Transitions are user initiated easing effects. When a user interacts with an element we can apply some kind of easing-like animation.

      - Triggered when a property changes on an element
      - **Must always be written on the default state**
      - Can animate any element that’s a number: `padding`, `color`, `transform`, etc.

  - type: interactive
    notes: "Transitions require a user to interact with an element for the easing to occur, like a hover or a click."
    html: |
      <a class="btn" href="#">T-Rex!</a>
    css_lines:
      - num: 3
        text: |
          The transition will slowly animate between the two colours: the original colour and the hover colour.

          There are three pieces of information that should be supplied for transitions:

          1. `all` — what property to transition, `all` means every numerical property that changes; but you could write `color` or `border-width` or something specific instead.
          2. `200ms` — the length of time the transition should take, can be written in milliseconds (`ms`) or in seconds (`s`): `200ms = .2s`
          3. `linear` — the type of easing: `ease-in`, `ease-out`, etc. (Same as AfterEffects.) `linear` means “no easing”.
      - num: 5
        text: |
          **Do not put `transition` in `:hover`—it won’t do what you expect.**

          They should always go in the original state. Transitions need to be “set-up” so that when a user does hover the transition is ready to go.

    css: |
      .btn {
        background-color: #5e54af;
        transition: all 200ms linear;
      }
      .btn:hover {
        background-color: #3c3670;
      }
    css_hidden: |
      .btn {
        display: inline-block;
        padding: .5em .75em;
        border: 0;
        border-radius: 10px;
        text-decoration: none;
        color: #fff;
      }

  - content: |
      ## Videos & tutorials

      - [CSS animations & effects ➔](/topics/css-animations-effects/)
      - [CSS animations & effects cheat sheet ➔](/topics/css-animations-effects-cheat-sheet/)
---
