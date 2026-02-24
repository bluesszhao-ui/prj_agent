---
name: digital-ic-timing-diagram
description: Generate, revise, and validate digital IC timing diagrams for synchronous and asynchronous logic. Use when asked to create or explain timing for clocks, resets, enables, handshakes, bus transactions, setup/hold windows, pulse widths, edge relationships, and protocol waveforms.
---

# Digital IC Timing Diagram

## Workflow

1. Extract requirements before drawing:
- List signals and direction (`clk`, `rst_n`, control, data, status).
- Define time base (cycle count, ns/us, or symbolic steps).
- Mark initial values and unknown periods.
- Capture constraints (setup/hold, min pulse width, latency, ordering).

2. Choose output format:
- Default to WaveDrom JSON for precise and editable timing.
- Use Mermaid only if user explicitly asks for it.
- Provide ASCII timing only for quick terminal-friendly previews.

3. Build waveform lanes:
- Keep `clk` first, then reset, then control, then data/status.
- Use stable run-lengths (`.`) instead of repeating identical states manually.
- Represent unknown/high-impedance explicitly (`x`, `z`) when required.

4. Add timing annotations:
- Add nodes and edges for causal/event relationships.
- Label setup/hold windows and edge-triggered sampling points.
- Call out assumptions directly when protocol timing is underspecified.

5. Validate before returning:
- Check that sampled data is stable in setup/hold windows.
- Check pulse widths and spacing constraints.
- Check reset sequencing and post-reset signal validity.
- Flag contradictions instead of silently guessing.

6. Return complete result:
- Provide the diagram source block.
- Provide a short rendered interpretation in plain language.
- Provide a checklist of satisfied and violated timing constraints.

## WaveDrom Defaults

- Prefer a single top-level object with `signal` array.
- Use concise labels and consistent naming across lanes.
- For buses, use `=` and `data` labels to show value transitions.
- For events/constraints, use `node` and `edge`.

## Clarifying Questions (Only When Needed)

Ask only missing essentials:
- What is the clock period or symbolic step size?
- On which edge does sampling occur?
- Are reset assertion/deassertion async or sync?
- What are setup/hold and min pulse requirements?

## Reusable Patterns

Use examples in [references/wavedrom-patterns.md](references/wavedrom-patterns.md) for:
- DFF setup/hold visualization
- `ready/valid` handshake timing
- Asynchronous reset release timing
