# PCBA_USB3_Hub — Four-Port USB 3.x Hub
## Design brief

Design a one-upstream/four-downstream USB 3.x hub supporting SuperSpeed operation. Use a commercially available hub controller with public hardware guidance. Provide one USB-C upstream connector and four downstream connectors, per-port power switching/current limiting, ESD protection, configuration EEPROM/flash if required, and the controller's required reference clock. Use a stackup appropriate for controlled differential impedance. SuperSpeed pairs must be short, reference continuous planes, avoid unnecessary vias/stubs, and follow the controller/connector pin escape recommendations. USB 2.0 pairs must also be routed correctly. Placement should be connector-driven and respect high-speed lane ordering.

## Functional requirements

- One upstream and four downstream ports, usable together, each with a complete SuperSpeed and USB 2.0 path to the upstream connector.
- The controller must be in production with published hardware guidance, and deviations from that guidance recorded.
- Identify the configuration source, fit external memory where the descriptors need it, and report only power the hardware can deliver.

## Power and current limiting

- Each downstream VBUS is independently switched and limited; a fault on one port must not disturb the others or the upstream link, and a sustained short must be survivable.
- Over-current must reach the controller as a host-visible status change, and the port must recover on fault removal without a board power cycle.
- Each limit sits above that port's advertised current and below its connector, switch and copper rating; inrush limited, downstream bulk capacitance per specification.
- Controller rails hold tolerance through a four-port hot-plug; if self powered, the board must not back-drive upstream VBUS and must detect its presence.

## Interfaces, connectors and clock

- The upstream USB-C receptacle presents Rd on both CC pins, sources no VBUS onto the cable, and works in either orientation.
- The downstream connector family is open; each must carry SuperSpeed, USB 2.0 and its switched VBUS, advertising no more current than its limit allows.
- SuperSpeed transmit pairs must be AC coupled within the value range the USB specification requires, symmetric within the pair.
- The reference clock must meet the controller's frequency, stability and jitter requirements and the USB frequency accuracy limit.

## Signal integrity and routing

- The stackup must hold the differential impedance the USB specification defines for both pair types, verified by the fabricator.
- Every pair references a continuous plane over its whole length, crossing no split, void or plane edge.
- SuperSpeed pairs take the shortest route with fewest layer changes; an unavoidable via needs adjacent ground returns and a short stub.
- No test points, stubs or series parts on SuperSpeed pairs beyond the AC coupling; skew and crosstalk stay within the channel budget.
- Escapes follow the pin escape recommendations published for the controller and connectors; where two conflict, record which was followed.

## Placement and mechanical

- Connectors are placed first to suit the panel interface, then the controller oriented so its lane assignment reaches them without pairs crossing.
- Lane ordering is preserved and any inversion or reordering recorded; port switches sit near their connectors, the clock element near the controller, and connectors are mechanically retained.

## Protection and robustness

- Every exposed contact — VBUS, ground, D+/D−, SuperSpeed pairs, CC/SBU where present — has ESD protection as the first node on the net.
- Protection on SuperSpeed pairs must be low enough in capacitance, and placed so, that the pair still meets impedance and return-loss limits.

## Test and bring-up

- Every rail needs a measurement point with nearby ground; reset, port enables and fault signals observable, reset externally assertable.
- Configuration memory must be programmable in circuit if fitted, the clock verifiable without over-loading it, and a load applicable at each port to check its limit.

## Open choices

- The controller, and with it the generation supported, the rails needed, and whether external configuration memory is required.
- Bus powered versus self powered, the downstream connector family, and the current each port advertises.
- How the reference clock is realised, and whether upstream orientation is handled natively or by an external crosspoint.
- Layer count and stackup, board outline, connector positions and mounting, and the ESD immunity level.
