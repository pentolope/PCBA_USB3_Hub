# Benchmark entry — board 25 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_USB3_Hub` |
| Board id | `usb3_hub` |
| Category | high-speed-digital |
| Difficulty | 4 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 6 |
| Primary stressors | 5Gbps differential pairs, USB connectors, power switches, ESD |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

Board 25 is a high-speed-digital case at difficulty 4/5 with a detail-4 brief: the brief is prescriptive about signal-integrity method (impedance-controlled stackup, short SuperSpeed pairs, continuous references, no gratuitous vias/stubs, vendor pin escapes, lane ordering) while deliberately naming no controller, connector, or protection part number. It tests whether an agent can run a 5 Gbps differential design against a commercially available controller's published hardware guidance rather than hand-waving, and whether it can integrate the messy support blocks - USB connectors, per-port power switching/current limiting, and ESD protection - without letting them corrupt the SuperSpeed channels. The scoring pressure sits on evidence: routing claims and impedance claims must be traceable to a stackup, a datasheet, and the controller's own guidance.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
