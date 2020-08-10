---
layout: slide-deck
title: "Effects & accessibility"
desc: "Effects can be really beautiful, and they can push a design to that extra level—but often they’re also a hinderance."

slides:
  - type: super-big-text
    content: |
      **Effects & accessibility**

  - content: |
      ## Effects can affect

      - Animations can be a distraction
      - Flashing images can cause seizures
      - A contrast levels work differently for everybody
      - Some of you are using dark-mode, some light-mode

      *We each have preferences—let’s help our users get the content the most efficient way for them.*

  - content: |
      ## Animated GIFs

      **Never use an animated GIF—ever.**

      - They cannot be stopped
        - If there’s too much flashing it could induce seizures
        - They could distract users from their task
      - They are *huge* files & terrible for performance

      *Instead, use a MP4: stoppable, pausable, streamable.*

  - content: |
      ## Autoplay

      **Don’t autoplay anything on your website.**

      - It’s distracting
      - It’s bandwidth hogging
      - It’s poor accessibility

      *Thankfully most browsers have features to prevent autoplay now—which I have enabled.*

  - type: text-code
    content: |
      ## Prefers colour scheme

      *Some of you prefer the dark colour scheme—some prefer the light colour scheme.*

      Accomodate that in your CSS.
    css: |
      main {
        background-color: #f2f2f2;
      }

      @media (prefers-color-scheme: dark) {
        main {
          background-color: #111;
        }
      }

  - type: text-code
    content: |
      ## Prefers reduced motion

      *Animations are distracting & annoying to lots of people’s concentration—or cause more serious problems.*

      Accomodate that in your CSS.
    css: |
      .ball {
        animation: spin 1s infinite;
      }

      @media (prefers-reduced-motion) {
        .ball {
          animation: none;
        }
      }

  - content: |
      ## Other preferences

      *Upcoming media features worth knowing:*

      - `prefers-contrast` — Determine if a high-contrast interface is requested
      - `prefers-reduced-transparency` — Determine if a reduced use of transparency is requested

  - content: |
      ## Videos & tutorials

      - [Accessibility of animations & effects ➔](/topics/accessibility-of-animations-effects/)

---
