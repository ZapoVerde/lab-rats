# Plan

## Product requirements

Create a browser application whose primary experience is an animated simulation inside a large circular arena.

- Begin with two independently moving balls.
- Keep every ball contained within the circular arena.
- Balls should bounce naturally from the arena boundary.
- Balls should collide with and bounce from one another.
- Each collision between two balls should create one additional ball.
- A sustained contact must not create an uncontrolled stream of duplicate collision events.
- New balls should enter the simulation in a physically and visually sensible way.
- The simulation should remain stable and responsive as the ball population increases.
- Provide sensible controls for interacting with the experience, including at minimum a way to restart the simulation.
- The layout should work well across desktop and mobile-sized browser viewports.

## Experience and visual quality

Treat visual and interaction quality as part of the product, not as optional decoration.

The animation should feel exceptionally smooth. Motion, collisions, spawning, transitions, typography, layout, effects, and controls should form a coherent visual experience. Make deliberate design choices rather than relying on browser defaults.

The exact aesthetic, effects, animation treatment, control design, and other presentational choices are intentionally left open.

## Engineering approach

Keep simulation state separate from rendering and interface concerns so that the core behavior remains understandable and testable.

Use a frame-rate-independent simulation approach. Account for elapsed time rather than assuming a fixed display refresh rate, and avoid allowing a long frame or resumed browser tab to destabilize the simulation.

Model circular-boundary collisions geometrically using each ball's radius. Resolve ball-to-ball collisions in a way that avoids obvious overlap, sticking, repeated false collision events, or explosive energy growth.

Treat spawning as a discrete consequence of a newly detected collision rather than a consequence of two balls merely remaining in contact.

Choose data structures and collision handling that are appropriate for a growing population. The application does not need to support an unlimited number of balls, but growth should not immediately make it unusable.

## Structure

Organize the implementation around clear responsibilities such as:

- simulation state and update loop
- collision detection and resolution
- spawning/lifecycle behavior
- rendering and visual effects
- application controls and responsive layout

These are responsibilities, not mandated files or components. Choose the structure that keeps the implementation clear without unnecessary abstraction.

## Verification

Before considering the work complete, verify at least:

- the application builds and runs cleanly
- balls remain inside the circular boundary
- boundary collisions behave consistently from different approach angles
- ball-to-ball collisions visibly resolve rather than passing through or sticking together
- one collision produces one new ball rather than repeated spawns from sustained contact
- restarting returns the simulation to its initial two-ball state
- resizing does not break containment or layout
- the simulation remains responsive after substantial population growth
- no obvious runtime errors occur during normal use

Add automated tests where they provide useful confidence, particularly for deterministic simulation or geometry behavior. Do not substitute tests for actually running and inspecting the finished experience.

## Completion standard

The result should satisfy the functional requirements, be technically sound, and feel finished. A technically correct animation that looks or feels like an unpolished prototype is not complete.
