# PCBA_USB3_Hub — Four-Port USB 3.x Hub
## Design brief

Design a one-upstream/four-downstream USB 3.x hub supporting SuperSpeed operation. Use a commercially available hub controller with public hardware guidance. Provide one USB-C upstream connector and four downstream connectors, per-port power switching/current limiting, ESD protection, configuration EEPROM/flash if required, and the controller's required reference clock. Use a stackup appropriate for controlled differential impedance. SuperSpeed pairs must be short, reference continuous planes, avoid unnecessary vias/stubs, and follow the controller/connector pin escape recommendations. USB 2.0 pairs must also be routed correctly. Placement should be connector-driven and respect high-speed lane ordering.
