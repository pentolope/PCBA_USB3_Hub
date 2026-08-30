# Architecture — Four-Port USB 3.x Hub

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- 5Gbps differential pairs
- USB connectors
- power switches
- ESD

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## Hub controller selection

- Which commercially available hub controller is chosen, and what public hardware guidance (datasheet, hardware design guide, reference design) backs it?
- Does it natively provide one upstream and four downstream SuperSpeed ports, or is any cascading or port-count workaround needed?
- What strapping, mode pins, and reset behaviour does the controller require at power-up?
- What does the controller's guidance say about pin escape and lane assignment, and does the chosen package permit following it on the intended layer count?
- Is a configuration EEPROM/flash required by this controller, or does it operate from defaults?
- What package thermal path does the controller need, and is that compatible with the chosen stackup?

## Upstream USB-C port

- How is the upstream USB-C connector wired for the upstream role, and how are CC1/CC2 terminated?
- Does the design handle cable orientation, and if not, why is that acceptable for the chosen controller?
- What happens to SBU and any unused pins on the upstream connector?
- Where does upstream VBUS go, and is it a power source for the board, a sense input, or both?
- What ESD and overvoltage exposure does the upstream connector present, and which of its pin groups are given protection, by what device, and on what reasoning?

## Downstream ports and connectors

- What connector type is chosen for the four downstream ports, and what drives that choice?
- How are the four ports physically arranged so that placement remains connector-driven?
- Does the chosen downstream connector's pinout allow the controller's recommended lane ordering to be honoured without pair swaps or crossovers?
- If any pair must be polarity-swapped or lane-swapped, does the controller support that, and where is it documented?
- What mechanical retention, shell grounding, and mating-face keepout does each connector require?

## Per-port power switching and current limiting

- What device provides per-port switching and current limiting, and is it one channel per port or shared?
- What current limit is set per port, and what determines that number given the (unfixed) upstream power source?
- How do the enable and fault signals connect to the controller, and does the controller expect a specific polarity or timing?
- What VBUS bulk and bypass capacitance sits on each downstream port, and does inrush stay within the switch's limits?
- How is a short or overcurrent on one port kept from disturbing the other three or the controller rails?
- What is the total VBUS budget, and how is that reconciled with whatever upstream or auxiliary supply is chosen?

## ESD and transient protection

- Which lines are protected: SuperSpeed pairs, USB 2.0 pairs, CC/SBU, VBUS, and connector shells?
- What line capacitance can the SuperSpeed pairs tolerate, and does the chosen protection device stay under it?
- Where is each protection device placed relative to its connector, and what path does a transient take from the connector pin through that device?
- What return path does each protection device's clamped current take, and what sets the inductance of that path?
- What ESD immunity level, if any, is being claimed, and what evidence supports the claim?

## Reference clock and configuration memory

- What clock source does the chosen controller require, at what frequency, tolerance, and drive level?
- Crystal or oscillator, and what load capacitance and layout keepout does that choice imply?
- How is the clock net isolated from the SuperSpeed pairs and from whatever noisy power nodes the chosen rail topology creates?
- If configuration memory is required, what interface, size, and address does the controller expect?
- How are the configuration contents (descriptors, port settings) generated, programmed, and verified?

## Power rails and thermal

- What rails does the controller need, at what currents, and with what sequencing and tolerance?
- What regulator topology supplies each rail, and where does its input come from given the unfixed board power source?
- What noise does the chosen regulator topology put on the rails and planes, and how is it kept off the SuperSpeed reference planes and the clock?
- Where does heat from the controller and the port switches go, and what copper supports that?
- What decoupling does the controller's hardware guidance call for, and can it be placed as the guidance requires?

## Stackup and controlled differential impedance

- What layer count and stackup is used, and how does it satisfy 'appropriate for controlled differential impedance'?
- Which layers carry SuperSpeed pairs, and what continuous reference plane sits adjacent to each?
- What differential impedance target and tolerance are specified to the fabricator, and how is the trace geometry derived?
- Does the chosen fabricator offer impedance control for this stackup, and at what minimum trace/space?
- What impedance results for the USB 2.0 pairs - differential and single-ended - and for any other controlled nets?

## SuperSpeed routing and signal integrity

- What is the routed length of each SuperSpeed pair, and what makes it 'short' relative to the channel budget?
- Does every SuperSpeed pair reference a continuous plane over its whole length, and where are the plane splits and voids checked?
- How many vias does each SuperSpeed pair cross, and is each one necessary?
- If vias are unavoidable, what return-path stitching and stub management accompanies them?
- What intra-pair skew and inter-pair budget is enforced, and how is it measured?
- If AC-coupling capacitors are required, what size and placement do they take, and what discontinuity do they introduce?
- How are the SuperSpeed pairs kept clear of the USB 2.0 pairs, the clock, and whatever noisy power nodes the chosen rail design produces?

## USB 2.0 routing

- How are the D+/D- pairs routed for the upstream port and each of the four downstream ports?
- What differential impedance and length matching do the USB 2.0 pairs get, and against what reference?
- Do the USB 2.0 pairs share protection devices or ground returns with the SuperSpeed pairs, and does that create coupling?
- Are the USB 2.0 escapes consistent with the controller's and connectors' pin escape recommendations?

## Placement, outline and lane ordering

- What board outline and dimensions are chosen, and what fixes the connector edge geometry?
- Is placement genuinely connector-driven - does the controller orientation follow from the connectors rather than the reverse?
- Does the physical port order match the controller's lane ordering, and if not, what is the documented justification?
- Where do the port switches, protection devices, and bulk capacitors sit relative to each connector?
- What keepouts do the connectors, mounting hardware, and any enclosure impose?

## Manufacturability, bring-up and verification

- Which fabricator and assembly process are assumed, and does the design stay inside their published trace/space/via and impedance-control limits?
- Is assembly single- or double-sided, and does connector and switch placement follow from that?
- What test points, indicators, or debug access exist for verifying enumeration, per-port power, and fault behaviour?
- What is the bring-up sequence, and what would be measured to show SuperSpeed links actually train?
- What outputs (length reports, via counts, impedance report, DRC) will be cited as evidence that the routing requirements were met?

## Answers still owed

All of them. See [status.md](status.md).
