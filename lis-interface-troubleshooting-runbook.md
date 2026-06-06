# Interface Troubleshooting Runbook
## LIS to Epic Beaker Interface — Result Transmission Failure

---

## Document Information
| Field | Detail |
|---|---|
| Document Type | Interface Troubleshooting Runbook |
| Facility Identifier | LAB0001 |
| Author | J. Lewis, Medical Laboratory Scientist |
| Status | Draft |
| Date | June 06 2026 |

---

## Overview
This runbook provides step-by-step guidance for identifying and resolving result transmission 
failures between instruments, LIS, and Epic Beaker. Transmission failures prevent providers 
from viewing patient results in the chart and must be resolved promptly to maintain patient 
care quality and turnaround time standards.

Common triggers for this runbook:
- Provider calls requesting results not visible in their chart
- Specimen on expected list with tracking stop but not received
- Results completed on instrument but not appearing in Beaker worklist
- Specimen loaded on Panther rack showing white — no test attached

---

## Platform-Specific Behavior

Understanding how each platform handles unmatched specimens is critical to fast troubleshooting:

| Platform | Behavior When Specimen Not Received in Beaker |
|---|---|
| Cepheid GeneXpert Infinity | Will load and run specimen even if not received in Beaker — result may not transmit |
| Hologic Panther | Displays unmatched specimen in rack as WHITE — no test attached — requires manual intervention before running |

**Key insight:** A white specimen on the Panther rack is an immediate signal to check receipt status and container IDs before the specimen is run.

---

## Troubleshooting Decision Tree

### Step 1 — Check receipt status FIRST
This is always the first check regardless of platform or symptom.

- Locate the specimen in Epic Beaker
- Confirm specimen has been received into the system
- **Check ALL container IDs associated with the order**

**Critical — Multiple Container IDs:**
Specimens arriving from external facilities via packing list may generate multiple specimen IDs 
for a single physical specimen. Each container ID must be individually checked.

Example:
| Specimen ID | Status |
|---|---|
| 26Y-000VI001.1 | Received |
| 26Y-000VI001.2 | Received |
| 26Y-000VI001.3 | NOT received |

The test may be attached to the unreceived container ID, preventing transmission.

**Resolution:**
- Identify which container ID the test is attached to
- Receive all unreceived container IDs in Epic Beaker
- Confirm all instances are received
- Proceed to Step 2

**Also check:** Was the test canceled on this specimen? 
Two separate scenarios apply:

**Scenario A — Incorrectly ordered test (wrong test code):**
Cancel the incorrect test and reorder using the correct test code.
Instrument trigger or manually add the corrected test to the specimen on the platform and proceed to Step 3.
No provider contact required — this is a laboratory correction.

**Scenario B — Test canceled for clinical reason:**
Contact the ordering provider before taking any action.
Provider determines whether to reorder or cancel entirely.
If provider reorders — place new order, add to specimen on platform, proceed to Step 3.
If provider cancels — document in Comm Log and no further action required.

---

### Step 2 — Check if test is attached to specimen

**On Hologic Panther:**
- If specimen is received but appears WHITE in rack — no test is attached
- Manually add the test through the Panther interface
- Confirm test is attached and specimen runs normally
- Result should transmit to LIS automatically after completion

**On Cepheid GeneXpert Infinity:**
- Specimen may have run without a matched order in Beaker
- Locate the result on the Cepheid interface
- Confirm order exists in Beaker and specimen is received
- Proceed to Step 3 to transmit result

---

### Step 3 — Transmit result from platform to LIS

If specimen ran on instrument but result did not transmit to LIS:

**Hologic Panther:**
- Navigate to the Panther interface
- Locate the specimen result
- Click **"Transmit to LIS"** button
- Confirm result populates in LIS and Epic Beaker

**Cepheid GeneXpert Infinity:**
- Navigate to the Cepheid interface
- Locate the completed result
- Manually transmit result to LIS
- Confirm result populates in LIS and Epic Beaker

**Note:** Instrument trigger in Epic Beaker is used to send a test TO the instrument 
BEFORE it is run — not to retrieve completed results. For completed results always 
use the platform interface to transmit directly to LIS.

---

### Step 4 — Canceled and reordered tests
If a test was incorrectly ordered, canceled, and reordered:
- The new order may require manual attachment to the specimen on the platform

**On Hologic Panther:**
- Instrument trigger first — sends the corrected order to the instrument through the system
- If instrument trigger was missed — manually add the correct test through the Panther interface

**On Cepheid GeneXpert Infinity:**
- Note: Instrument trigger does NOT apply to Cepheid — the Cepheid uses cartridge 
  and barcode scanning to identify specimens and tests
- Scan the patient specimen ID label
- Scan the cartridge barcode
- Select the exact test from the available options on that cartridge type
  - The 4-plex cartridge supports multiple test configurations:
    - COVID-19 only
    - COVID-19 + Influenza A/B (no RSV)
    - Full 4-plex: SARS-CoV-2 / Influenza A / Influenza B / RSV
- Confirm correct test selection before loading
- Cepheid will run the selected test and transmit result to LIS automatically upon completion
- If result does not transmit — navigate to Cepheid interface, locate result, 
  and manually transmit to LIS

---

### Step 5 — If transmission still fails — LIS issue

If result is visible on platform but will not transmit to LIS despite all above steps:
- This is an LIS-level issue requiring escalation
- Manually enter the result directly into Epic Beaker
- Print the results page from the platform interface
- Attach the patient label to the printed results page
- Submit printed results to supervisor for review and documentation
- Escalate to IT application support for LIS investigation

---

## Escalation Path
| Step failed | Escalate to |
|---|---|
| Receipt and container ID issues unresolved | Senior lab staff or supervisor |
| Platform transmission failure unresolved | IT Application Support |
| LIS not receiving results from any platform | IT Application Support — system-wide issue |
| Critical result delayed | Supervisor and ordering provider immediately |

---

## Manual Result Entry — Required Documentation
When manually entering results due to LIS failure:

| Item | Requirement |
|---|---|
| Result entry | Enter directly into Epic Beaker |
| Printed results page | Print from platform interface |
| Patient label | Attach to printed results page |
| Supervisor submission | Submit printed results with label for review |


---

## Disclaimer
All order codes, facility identifiers, and system configurations in this document are 
fictional and created for portfolio demonstration purposes only. Content reflects general 
Epic Beaker Clinical Pathology workflow knowledge and does not represent any specific 
health system's proprietary build configuration.
