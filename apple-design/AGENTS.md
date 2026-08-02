# Apple Design Skill

## Purpose

Apple's approach to interface design and fluid, physical motion, translated for the web platform. Distilled from Apple's WWDC design sessions (chiefly _Designing Fluid Interfaces_, 2018) into CSS, Pointer Events, `requestAnimationFrame`, and spring libraries such as Motion / Framer Motion.

The through-line: an interface feels alive when motion starts from the current on-screen value, inherits the user's velocity, projects momentum forward, and can be grabbed and reversed at any instant.

## File Structure

```
apple-design/
  metadata.json        # Version, references, abstract
  SKILL.md             # Full guidelines (load this)
  AGENTS.md            # This file
```

No `rules/_sections.md` — the skill is short enough to load whole.

## Usage

Load `SKILL.md` for the complete guidelines. This skill covers **behavior, motion, material, and craft**. It is complementary to `web-design-guidelines` at the repo root, which covers accessibility, semantics, responsive layout, and performance. When both apply, `web-design-guidelines` wins on accessibility and semantics; this skill wins on how things move and feel.

## When to Apply

- Gesture-driven UI: drag, swipe, sheets, drawers, carousels, pull-to-dismiss
- Spring animations, momentum, and flick-to-dismiss behavior
- Any transition a user can interrupt or reverse mid-flight
- Translucent chrome, blur, depth, and layered surfaces
- Typography craft: optical sizing, size-specific tracking, leading
- Reduced-motion, reduced-transparency, and increased-contrast handling
- Reviewing an interface that is technically correct but feels dead or janky

## Priority Levels

| Level    | Sections                                                                                                                                                                   |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CRITICAL | Response (kill latency), Direct manipulation, Interruptibility                                                                                                             |
| HIGH     | Behavior over animation (springs), Velocity handoff, Momentum projection, Reduced motion and accessibility                                                                 |
| MEDIUM   | Spatial consistency, Gesture hinting, Rubber-banding, Gesture details, Frame smoothness, Materials and depth, Multimodal feedback, Typography, Design foundations, Process |

## Conventions

- Spring parameters are expressed as Apple does: **damping ratio** (overshoot) and **response** (seconds to target), not mass/stiffness/damping.
- Default to `damping 1.0` (critically damped). Reserve bounce for motion the user's own gesture set going.
- Code examples are vanilla CSS/JS, with Motion / Framer Motion where a spring library is required.
- Concrete values Apple ships are given in tables rather than described qualitatively.

## Never Do

- Never wait for `click` or touch-up to show press feedback — highlight on pointer-down
- Never animate only at the end of a gesture — feedback is continuous during it
- Never lock out input during a transition; every animation stays interruptible
- Never animate from the target value on interrupt — read the live presentation value or it visibly jumps
- Never drive gesture-linked motion with CSS transitions or `@keyframes` — they cannot be grabbed and reversed
- Never hard-cut velocity on a reversal — carry it through the re-target, or it reads as a brick wall
- Never run a single spring on 2D distance — decompose into independent X and Y
- Never snap to the nearest target from the release point — project the resting position from velocity first
- Never snap the dragged element to its own center on grab — respect the grab offset
- Never enter along one path and exit along another
- Never hard-stop at a boundary — rubber-band with progressive resistance
- Never stack a light translucent surface on another translucent surface — legibility collapses
- Never use one `letter-spacing` for all sizes — tracking is size-specific
- Never treat reduced motion as no feedback — substitute a gentler, non-vestibular equivalent
- Never let visual, audio, and haptic feedback land on different frames
