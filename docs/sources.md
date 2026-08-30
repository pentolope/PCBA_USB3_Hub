# Sources — Four-Port USB 3.x Hub

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Hub controller datasheet and hardware design guide / reference design | The brief requires a controller with public hardware guidance; rail set, clock requirements, strapping, configuration memory need, and pin escape recommendations all come from these documents. |
| USB 3.x / SuperSpeed specification and its channel budget material | Fixes the differential impedance expectation, AC-coupling, skew and loss limits that 'short pairs, continuous references, no unnecessary vias/stubs' is being measured against. |
| USB 2.0 specification | The brief separately requires the USB 2.0 pairs to be routed correctly, which needs the D+/D- impedance and routing limits from the specification. |
| USB-C connector specification and specific connector datasheets | Fixes upstream pinout, CC handling, lane ordering, land pattern, and mechanical retention for the connectors actually chosen. |
| Downstream connector datasheets and land-pattern drawings | The downstream connector type is unfixed, so whatever is selected must supply its own pinout, escape geometry, and mounting footprint. |
| Power switch / current-limit device datasheets | Per-port switching and current limiting need documented limit accuracy, inrush and short-circuit behaviour, fault-flag semantics, and thermal ratings. |
| ESD / TVS protection device datasheets | Line capacitance, clamping voltage, and channel count must be shown compatible with 5 Gbps pairs rather than assumed. |
| Crystal or oscillator datasheet plus the controller's clock application guidance | Frequency, tolerance, load capacitance, drive level and jitter requirements are set jointly by the resonator and the controller. |
| Regulator datasheets for the rail topology chosen for the controller and support devices | The rail set and the switching-versus-linear choice are unfixed and follow from controller selection; each regulator's ratings, sequencing, and layout guidance must be cited. |
| PCB fabricator capability and stackup documentation | Layer count, dielectric, copper weight, minimum trace/space, via technology and impedance-control availability must come from the actual fabricator, not from assumption. |
| Impedance / field-solver output for the chosen stackup | The brief demands controlled differential impedance; the trace geometry that achieves it has to be derived and shown, not asserted. |
| Assembly house DFM and process documentation | Connector-heavy, double-sided boards depend on documented land patterns, paste rules, and assembly-side constraints. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
