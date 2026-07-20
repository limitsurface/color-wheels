# Getting Started

Color Wheels is a scene-linear Copernicus grading HDA for Houdini 22. It
provides familiar Lift, Gamma, Gain, and Offset controls through a custom
Parameter Editor interface.

## Add the node

1. Create or open a Copernicus network.
2. Connect an image to **Color Wheels** from
   `ScyTools/COPs/Utilities/` in the Tab menu.
3. Select the node to display the four-wheel interface.

At their neutral defaults, the controls produce an exact passthrough.

## Make an adjustment

- Drag inside a wheel to push that tonal region toward the displayed hue.
- Drag the horizontal strip beneath a wheel left or right to change its
  master value in stops. Hold **Shift** while dragging for finer control.
- Use **Wheel Range** beside each wheel to change the wheel's sensitivity.
- Enter exact values in the Y/R/G/B fields. Press **Enter** or leave the field
  to commit the value.
- Double-click a wheel or exposure strip to return that control to neutral.
- Use the small reset button to reset the entire section, including its range.

## What the wheels affect

- **Lift** primarily adjusts shadows and tapers toward highlights.
- **Gamma** primarily adjusts midtones while substantially anchoring black and
  white.
- **Gain** primarily adjusts highlights.
- **Offset** applies a global, exposure-like adjustment across the image.

Lift, Gamma, and Gain provide a master **Y** value plus individual RGB values.
Offset provides RGB values, with its horizontal strip acting as global
exposure.

## A simple workflow

1. Use **Offset** to establish the overall exposure and broad color balance.
2. Use **Lift** to balance the shadows.
3. Use **Gain** to shape the highlights.
4. Use **Gamma** for the remaining midtone balance.
5. Reduce **Wheel Range** when a wheel feels too sensitive for a subtle grade.

The HDA processes in scene-linear light and expresses corrections in stops.
Alpha is passed through unchanged.
