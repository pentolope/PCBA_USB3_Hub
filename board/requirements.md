# Requirements — Four-Port USB 3.x Hub

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `14bc2d9647ea9610f8c5ea545e05617e6babf8881f33a6d3078326cd46aae86f`.

## Fixed by the brief

### REQ-01 — The board is a USB 3.x hub with one upstream port and four downstream ports, supporting SuperSpeed operation.

Brief text:

> Design a one-upstream/four-downstream USB 3.x hub supporting SuperSpeed operation.

### REQ-02 — The hub controller must be a commercially available part for which public hardware design guidance exists.

Brief text:

> Use a commercially available hub controller with public hardware guidance.

### REQ-03 — The upstream connector is a single USB-C connector.

Brief text:

> Provide one USB-C upstream connector and four downstream connectors

### REQ-04 — Four downstream connectors must be provided.

Brief text:

> one USB-C upstream connector and four downstream connectors, per-port power switching/current limiting

### REQ-05 — Per-port power switching with current limiting must be provided.

Brief text:

> four downstream connectors, per-port power switching/current limiting, ESD protection

### REQ-06 — ESD protection must be provided.

Brief text:

> per-port power switching/current limiting, ESD protection, configuration EEPROM/flash if required

### REQ-07 — Configuration EEPROM/flash must be provided if the selected controller requires it.

Brief text:

> ESD protection, configuration EEPROM/flash if required, and the controller's required reference clock.

### REQ-08 — The reference clock required by the selected controller must be provided.

Brief text:

> configuration EEPROM/flash if required, and the controller's required reference clock.

### REQ-09 — The stackup must be one appropriate for controlled differential impedance.

Brief text:

> Use a stackup appropriate for controlled differential impedance.

### REQ-10 — SuperSpeed pairs must be kept short and must reference continuous planes.

Brief text:

> SuperSpeed pairs must be short, reference continuous planes, avoid unnecessary vias/stubs

### REQ-11 — Unnecessary vias and stubs on the SuperSpeed pairs must be avoided.

Brief text:

> avoid unnecessary vias/stubs, and follow the controller/connector pin escape recommendations.

### REQ-12 — Routing must follow the pin escape recommendations of the chosen controller and connectors.

Brief text:

> and follow the controller/connector pin escape recommendations. USB 2.0 pairs must also be routed correctly.

### REQ-13 — The USB 2.0 pairs must also be routed correctly, not just the SuperSpeed pairs.

Brief text:

> USB 2.0 pairs must also be routed correctly. Placement should be connector-driven and respect high-speed lane ordering.

### REQ-14 — Placement should be connector-driven.

Brief text:

> Placement should be connector-driven and respect high-speed lane ordering.

### REQ-15 — Placement should respect high-speed lane ordering.

Brief text:

> Placement should be connector-driven and respect high-speed lane ordering.

### REQ-16 — Choices the brief leaves open must be made and documented as engineering decisions; hidden user requirements must not be invented.

Brief text:

> where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements

### REQ-17 — The repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not be pushed into the toolkit.

Brief text:

> remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

### REQ-18 — The requirements stated in the brief are to be treated as authoritative: binding on the design rather than advisory.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions

## Open — the design agent decides

### OPEN-01 — Which hub controller to use, and in which package and configuration mode.

The brief constrains the controller only to being commercially available with public hardware guidance; it names no vendor, part, or package.

*Decision:* **not yet made.**

### OPEN-02 — What connector type, orientation and mounting style the four downstream ports use.

The brief fixes only the count (four) and that the upstream connector is USB-C; it says nothing about the downstream connector type.

*Decision:* **not yet made.**

### OPEN-03 — Whether the hub is bus-powered, self-powered, or both, and where downstream VBUS comes from.

The brief requires per-port power switching but never states a power source, an auxiliary input, or a total power budget.

*Decision:* **not yet made.**

### OPEN-04 — Per-port current-limit threshold, switch device family, and how fault/enable signals connect to the controller.

The brief says 'per-port power switching/current limiting' without naming a device, a limit value, or a fault-handling scheme.

*Decision:* **not yet made.**

### OPEN-05 — Which lines get ESD protection (SuperSpeed pairs, USB 2.0 pairs, CC/SBU, VBUS, shells), with what device class, and where each device sits.

The brief lists ESD protection as a required block and as a stressor, but fixes no device, no coverage list, no placement, and no ESD immunity level.

*Decision:* **not yet made.**

### OPEN-06 — Reference clock implementation: crystal versus oscillator, frequency, tolerance, drive level, and load capacitance.

The brief defers entirely to 'the controller's required reference clock', which is only knowable once the controller is chosen.

*Decision:* **not yet made.**

### OPEN-07 — Whether configuration memory is populated at all, and if so its interface, size, addressing and default descriptor content.

The brief makes the EEPROM/flash conditional ('if required') on the chosen controller and specifies nothing about its contents.

*Decision:* **not yet made.**

### OPEN-08 — The rail set and regulator topology needed by the controller and support devices - switching versus linear included - along with sequencing and decoupling strategy.

The brief never mentions supply rails, regulators, voltages, or conversion topology; they all follow from the controller selection.

*Decision:* **not yet made.**

### OPEN-09 — USB-C upstream port details: CC pull configuration, role, whether any power-delivery or orientation handling is implemented, and SBU treatment.

The brief names the upstream connector type only; it is silent on CC behaviour, role negotiation, and orientation handling.

*Decision:* **not yet made.**

### OPEN-10 — If USB-C is chosen downstream, how CC pull-downs/pull-ups, VCONN and orientation are handled per port.

Downstream connector type is itself unfixed, so all of its associated signalling decisions are downstream of an unmade choice.

*Decision:* **not yet made.**

### OPEN-11 — The concrete stackup: layer assignment, dielectric materials and thicknesses, copper weights, and the trace geometry that achieves the impedance target.

The brief requires only a stackup 'appropriate for controlled differential impedance'; metadata suggests a likely layer count of 6 but fixes no dielectric, geometry, or tolerance.

*Decision:* **not yet made.**

### OPEN-12 — The differential impedance target and tolerance to be specified to the fabricator, and how it is verified.

No impedance value, tolerance, or verification method appears in the brief or metadata; the value has to be derived from the chosen controller's guidance and the USB specification, then stated.

*Decision:* **not yet made.**

### OPEN-13 — Intra-pair skew and inter-pair length budgets, and whether AC-coupling capacitors are needed on the SuperSpeed pairs and where they sit.

The brief gives qualitative routing rules ('short', 'continuous planes', 'no unnecessary vias/stubs') but no numeric budgets and no coupling-capacitor requirement.

*Decision:* **not yet made.**

### OPEN-14 — Board outline, dimensions, connector edge geometry, mounting holes, and any enclosure or keepout constraints.

The brief states no mechanical constraint at all beyond placement being connector-driven.

*Decision:* **not yet made.**

### OPEN-15 — Via strategy for the SuperSpeed escapes: through-hole versus blind/buried, back-drilling, anti-pad and stitching-via scheme.

The brief asks that unnecessary vias/stubs be avoided but does not fix a via technology or fabrication class.

*Decision:* **not yet made.**

### OPEN-16 — Shield/chassis-ground treatment for the connector shells, protection-device return paths, and any common-mode or EMI mitigation.

The brief is silent on grounding of shells and protection devices, on EMI measures, and on any emissions target.

*Decision:* **not yet made.**

### OPEN-17 — Bring-up and test provisions: test points, status/power indication, debug connectors, and how enumeration and per-port power are exercised.

The brief specifies no test, indicator, or debug features.

*Decision:* **not yet made.**

### OPEN-18 — Fabrication and assembly vendor and the resulting process limits (minimum trace/space, impedance-control option, single- versus double-sided assembly).

The brief names no fabricator, process class, or assembly constraint.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json). **That file is the authoritative
   record**, and the only one the benchmark's scripts read: a decision written
   only in prose is invisible to `board_status.py` and to any result that
   counts how many decisions an attempt actually made.
2. Answer it under its `OPEN-nn` heading here as well, with the reasoning and
   the evidence that made the choice. This file is the readable copy; where the
   two disagree, the JSON is what happened.
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Naming a hub controller without citing its public hardware guidance - the brief explicitly makes that guidance a selection criterion, so an uncited controller fails the requirement outright.
- Asserting 'controlled differential impedance' as achieved while giving no stackup, dielectric, or trace geometry; the impedance target and the geometry that produces it must both be derived from real fabricator data.
- Claiming the layout 'follows controller/connector pin escape recommendations' without pointing at the specific figure or table in the controller and connector documents that was followed.
- Inventing per-port current limits and a total VBUS budget: the brief never says bus-powered or self-powered, so any current number that is not derived from a stated, chosen power source is fabricated.
- Treating 'ESD' as solved by dropping in a generic protection array without checking its line capacitance against 5 Gbps pairs or showing where the transient return path goes.
- Declaring SuperSpeed pairs 'short' and 'over continuous planes' without length reports, via counts, and a plane-void check to back the claim.
- Reading the metadata's 'likely layer count: 6' as a fixed requirement, or conversely ignoring it and then failing to justify a different stackup.
- Fabricating mechanical constraints - outline, dimensions, connector spacing, enclosure fit - that the brief never states, instead of recording them as design decisions.
