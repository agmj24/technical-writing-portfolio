# Equipment Maintenance Procedures (Sanitized Sample)

> This describes a fictional wafer-handling module ("Handler Unit A2") and made-up procedures. It's built to demonstrate how I write hardware maintenance documentation — the kind of content I produced for semiconductor equipment at a previous role — without using any real equipment names, part numbers, or procedures from that work.

## About This Document

Semiconductor equipment procedures live or die on precision. Skip a step, get the order wrong, or leave out a safety note, and you're not looking at a typo — you're looking at damaged hardware or a safety incident. So the writing style here is intentionally plain and repetitive in structure: prerequisites first, then numbered steps, then a way to confirm you actually did it right. No creative language, no burying a warning in the middle of a paragraph.

These three procedures — routing, installation, and de-installation — usually live together in a manual because they're the physical lifecycle of a module: getting cable and hose routing right during install, then reversing it cleanly during de-install for service or replacement.

---

## Procedure 1: Cable and Hose Routing for Handler Unit A2

### Purpose

Defines the correct routing path for the power, signal, and vacuum lines connected to Handler Unit A2, so the module has full range of motion without straining or pinching any line.

### Prerequisites

- Handler Unit A2 is mechanically mounted but not yet connected.
- System main power is OFF and locked out.
- Routing kit (cable ties, strain relief clips, conduit) is on hand.

### Safety Notice

⚠️ **Do not connect any cable or hose until routing is complete and inspected.** Connecting first and routing after risks pulling a live connection loose.

### Steps

1. Identify the three line groups: power cable (labeled PWR-A2), signal cable (SIG-A2), and vacuum hose (VAC-A2).
2. Route the power cable along the left-side cable channel, securing it every 15 cm with a strain relief clip. Keep at least 5 cm of slack at the module end to allow for service movement.
3. Route the signal cable along the same channel, but keep it separated from the power cable by the provided divider strip — running them together can introduce electrical noise into the signal line.
4. Route the vacuum hose along the rear channel, away from both cables. Avoid any bend tighter than the hose's rated minimum bend radius (check the hose's printed spec if you're unsure).
5. Once all three lines are routed, confirm the module can move through its full range of travel without any line pulling taut or rubbing against a chassis edge.

### Verification

- Manually cycle the module through full travel and visually confirm no line is under tension at any point.
- Confirm strain relief clips are seated and none of the lines has been pinched at a channel edge.

---

## Procedure 2: Installing Handler Unit A2

### Purpose

Covers physical installation and initial connection of Handler Unit A2 after routing (Procedure 1) is complete.

### Prerequisites

- Routing complete and verified per Procedure 1.
- System main power OFF and locked out.
- Two technicians required — the module is not rated for single-person lifting.

### Steps

1. Position Handler Unit A2 onto the mounting bracket, aligning the two guide pins on the underside of the module with the corresponding holes in the bracket.
2. Secure the module with the four mounting bolts, tightening in a diagonal pattern (bolt 1, then the bolt diagonally opposite it, then the remaining two) rather than working around in a circle. This keeps the module seated evenly and avoids warping the mounting plate.
3. Connect PWR-A2, SIG-A2, and VAC-A2 in that order. Connecting power last, right before signal, is the wrong order — always land power first so you're not back-feeding voltage through an unpowered signal line.
4. Restore main power and confirm the module's status LED shows solid green. A slow blink means it's powered but not yet communicating — check the signal connector before assuming it's a bigger problem.
5. Run the built-in self-test from the system console (`Diagnostics > Handler > Self-Test`). This should complete with no faults reported.

### Verification

- Status LED: solid green.
- Self-test: passes with zero faults.
- Manual jog of the module across its full range, confirming smooth motion with no unexpected resistance.

If the self-test reports a fault, don't proceed to production use — go back through the connection order in step 3 before escalating to the next troubleshooting tier.

---

## Procedure 3: De-installing Handler Unit A2

### Purpose

Covers safe removal of Handler Unit A2 for service, replacement, or decommissioning.

### Prerequisites

- System main power OFF and locked out.
- Module has been idle for at least 5 minutes (allows residual vacuum pressure to bleed off — check the vacuum gauge reads zero before disconnecting VAC-A2).
- Two technicians required.

### Steps

1. Confirm the vacuum gauge reads 0 before touching VAC-A2. This isn't optional — disconnecting a pressurized vacuum line can cause it to whip loose.
2. Disconnect in the reverse order of installation: signal (SIG-A2) first, then vacuum (VAC-A2), then power (PWR-A2) last.
3. Remove the four mounting bolts, again working in the diagonal pattern rather than around in a circle, to release tension evenly.
4. With both technicians supporting the module's weight, lift it clear of the guide pins and set it down on the padded service cart.
5. Cap all three disconnected lines (power, signal, vacuum) with the provided end caps to keep debris out while the module is off-line.

### Verification

- All three lines capped.
- Mounting bracket inspected for any damage before a new or repaired module is installed.
- De-installation logged in the maintenance record with date, technician names, and reason for removal.

---

## A Note on How I Approach This Kind of Documentation

I write the "why," not just the "what," wherever it matters for safety or for avoiding a mistake I've seen happen — for example, why power connects first and disconnects last isn't obvious unless someone explains the back-feed risk, so I don't leave that as an unexplained rule. But I also keep that reasoning short and out of the numbered steps themselves, so a technician following along under time pressure isn't wading through explanation to find the next action. The steps stay terse; the "why" sits in a nearby note instead.
