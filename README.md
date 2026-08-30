# Four-Port USB 3.x Hub

A one-upstream / four-downstream USB 3.x hub with SuperSpeed operation, USB-C upstream, per-port power switching and ESD protection.

This repository holds the design problem for a four-port USB 3.x hub: one upstream port, four downstream ports, and SuperSpeed operation built around a commercially available hub controller that has public hardware guidance. The brief fixes the port topology, that the upstream connector is USB-C, that per-port power switching/current limiting and ESD protection are present, that configuration EEPROM/flash is provided if the chosen controller requires it, and that the controller's required reference clock is supplied. It also fixes the routing discipline: a stackup appropriate for controlled differential impedance, short SuperSpeed pairs over continuous reference planes without unnecessary vias or stubs, adherence to the controller/connector pin escape recommendations, and correctly routed USB 2.0 pairs; placement, which the brief states as a 'should' rather than a 'must', is to be connector-driven and to respect high-speed lane ordering. Everything else - which controller, which connectors downstream, bus- versus self-powered operation and the VBUS budget, the protection and power-switch devices, the clock source, the rail set, the exact stackup and impedance target, and the board outline - is left to the design agent. The requirements the brief does state are to be treated as authoritative, and the choices it leaves open are to be made and documented as engineering decisions rather than back-filled as invented user requirements. The board is a consumer of the shared `PCBA_AutoDesignAndTest` toolkit; board-specific logic does not belong in the toolkit.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 18 requirements and deliberately leaves
18 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Port topology | One upstream, four downstream USB 3.x ports, SuperSpeed operation | brief |
| Hub controller | A commercially available hub controller with public hardware guidance; specific part not named by the brief | brief |
| Upstream connector | One USB-C connector | brief |
| Downstream connectors | Four downstream connectors; connector type/style not stated by the brief | brief |
| Port power handling | Per-port power switching / current limiting required | brief |
| ESD protection | Required; device class, coverage and placement not fixed by the brief | brief |
| Configuration memory | Configuration EEPROM/flash provided if the chosen controller requires it | brief |
| Reference clock | The controller's required reference clock must be provided; source and frequency follow the chosen controller | brief |
| Stackup intent | A stackup appropriate for controlled differential impedance | brief |
| High-speed routing rules | SuperSpeed pairs short, over continuous reference planes, no unnecessary vias/stubs, per controller/connector pin escape recommendations; USB 2.0 pairs also routed correctly | brief |
| Placement strategy | Connector-driven placement respecting high-speed lane ordering; the brief states this as a 'should', unlike the 'must' it uses for the routing rules | brief |
| Requirement authority | Stated requirements are authoritative; open choices are made and documented as engineering decisions, not invented as user requirements | brief |
| Likely layer count | 6 | metadata |
| Benchmark classification | Category high-speed-digital; difficulty 4/5; brief detail 4/5; stressors: 5Gbps differential pairs, USB connectors, power switches, ESD | metadata |
| Board outline, size and mounting | Not fixed by the brief - design agent's choice | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 25 of 32 |
| Category | high-speed-digital |
| Difficulty | 4 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 6 |
| Primary stressors | 5Gbps differential pairs, USB connectors, power switches, ESD |

Board 25 is a high-speed-digital case at difficulty 4/5 with a detail-4 brief: the brief is prescriptive about signal-integrity method (impedance-controlled stackup, short SuperSpeed pairs, continuous references, no gratuitous vias/stubs, vendor pin escapes, lane ordering) while deliberately naming no controller, connector, or protection part number. It tests whether an agent can run a 5 Gbps differential design against a commercially available controller's published hardware guidance rather than hand-waving, and whether it can integrate the messy support blocks - USB connectors, per-port power switching/current limiting, and ESD protection - without letting them corrupt the SuperSpeed channels. The scoring pressure sits on evidence: routing claims and impedance claims must be traceable to a stackup, a datasheet, and the controller's own guidance.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `.claude/skills/` | the claim-audit and accountability-review skills [CLAUDE.md](CLAUDE.md) requires before a push |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_USB3_Hub.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `14bc2d9647ea9610f8c5ea545e05617e6babf8881f33a6d3078326cd46aae86f`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
