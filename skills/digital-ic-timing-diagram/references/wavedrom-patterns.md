# WaveDrom Patterns

## 1) DFF Setup/Hold Example

```json
{ "signal": [
  { "name": "clk",  "wave": "p....|...." },
  { "name": "d",    "wave": "0.1..|0.1.", "node": "..a..|..b." },
  { "name": "q",    "wave": "0..1.|0..1"  }
],
  "edge": [
    "a~>b setup/hold window reference"
  ]
}
```

Use this pattern to explain which `d` value is captured at each rising edge.

## 2) Ready/Valid Handshake

```json
{ "signal": [
  { "name": "clk",   "wave": "p.....|....." },
  { "name": "valid", "wave": "0.1..0|1.0.." },
  { "name": "ready", "wave": "0..1.0|.1..." },
  { "name": "data",  "wave": "x.=..x|.=..x", "data": ["A", "B"] }
]}
```

Transfer occurs only where `valid=1` and `ready=1` overlap.

## 3) Asynchronous Reset Release

```json
{ "signal": [
  { "name": "clk",   "wave": "p....|...." },
  { "name": "rst_n", "wave": "0...1|...." },
  { "name": "state", "wave": "x...=|=...", "data": ["IDLE", "RUN"] }
]}
```

If reset deassertion is asynchronous, call out any required synchronization stages.

## Quick Symbols

- `0` low, `1` high
- `p` clock pulse train
- `.` repeat previous level/state
- `x` unknown
- `z` high impedance
- `=` data/value segment
