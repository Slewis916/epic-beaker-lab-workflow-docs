# Epic Beaker CP — Specimen Lifecycle Workflow
## Respiratory Pathogen 4-Plex Panel

---

## Document Information
| Field | Detail |
|---|---|
| Document Type | Clinical Workflow Documentation |
| Facility Identifier | LAB0001 |
| Author | J. Lewis, Medical Laboratory Scientist |
| Status | Draft |
| Date | June 2026 |

---

## Overview
This document outlines the complete specimen lifecycle for the Respiratory Pathogen 4-Plex Panel (SARS-CoV-2 / Influenza A / Influenza B / RSV) within Epic Beaker CP, from order entry through result release to the provider chart.

---

## 1. Order Entry

| Step | Detail |
|---|---|
| Provider action | Places order in Epic |
| Diagnosis code | ICD-10 diagnosis code assigned at order entry |
| Order priority | STAT or Routine — determined by patient location or provider override |

**Order priority rules:**
- Emergency Department, OR, Inpatient → STAT (automatic)
- Outpatient / Ambulatory → Routine (default)
- Provider may manually upgrade any order to STAT at time of entry

---

## 2. Specimen Collection

| Acceptable Specimens | Detail |
|---|---|
| NP swab in VTM | Nasopharyngeal swab in Viral Transport Media |
| NP swab in UTM | Nasopharyngeal swab in Universal Transport Media |
| Throat swab in VTM or UTM | Acceptable — special routing applies (see Step 4) |

| Rejected Specimens | Reason |
|---|---|
| eSwab | Incorrect container — not validated for this assay |
| Incorrect source | Any source other than NP or Throat |
| Insufficient volume | Recollection required |

---

## 3. Receipt and Accessioning

| Step | Action |
|---|---|
| Specimen receipt | Specimen received and timestamped in Epic Beaker — TAT clock starts |
| Container ID verification | All container IDs associated with the order verified as received |
| External facility specimens | All packing list container IDs checked — partial receipt is a common cause of transmission failure |
| Routing | Specimen routed to correct laboratory department |

**Critical check:** If specimen appears on expected list with tracking stopped but not received — check all container IDs before proceeding. External facility specimens may generate multiple container IDs (e.g. LAB0001-26Y-000VI001.1, .2, .3) — all must be received.

---

## 4. Routing Decision

| Condition | Platform | TAT |
|---|---|---|
| STAT order + NP source | Cepheid GeneXpert Infinity | 47 minutes |
| Routine order + NP source | Hologic Panther | 3.5 hours |
| Any order + Throat source | Hologic Panther | 3.5 hours |

**Routing Exception — Throat Specimens:**
Cepheid GeneXpert Infinity is NOT validated for throat specimens for 4-plex testing. All throat specimens route to Hologic Panther regardless of order priority or patient location. This override takes precedence over all other routing rules.

**Platform-specific behavior:**
- Cepheid GeneXpert Infinity — scan specimen ID label, scan cartridge barcode, select exact test configuration before loading
- Hologic Panther — specimen displayed as WHITE in rack if not received or test not attached — verify receipt and manually add test if needed

---

## 5. CER Rules Evaluated

After result is generated on platform and transmitted to LIS, Epic Beaker evaluates CER rules to determine if result can auto-verify.

| CER Rule | Pass Condition | Pass Action | Fail Action |
|---|---|---|---|
| All 4 components resulted | Each analyte has a valid Detected or Not Detected result | Proceed to next rule | Hold — incomplete panel |
| No critical value designation | This panel has no critical value configuration | Proceed to next rule | N/A |
| Result within expected parameters | Detected or Not Detected result generated | Proceed to next rule | Hold — manual review |
| QC valid for run | Current QC within acceptable limits | Proceed to next rule | Hold — QC review required |
| CT value within threshold | CT value at or below cutoff threshold | Auto-verify and release | Hold — manual review required |

---

## 6. Auto-Verification Outcome

| Outcome | Condition | Action |
|---|---|---|
| Auto-verification passes | ALL CER rules pass | Result auto-verifies and releases to provider chart automatically |
| Auto-verification fails | ANY CER rule fails | Result held in queue for manual tech review and verification |

**Co-detection note:** Multiple analytes simultaneously positive (e.g. SARS-CoV-2 + RSV, SARS-CoV-2 + Influenza A/B) is a valid clinical result. Co-detection does not trigger a hold — all components report independently and auto-verify normally if all CER rules pass.

---

## 7. Result Release

| Step | Detail |
|---|---|
| Auto-verified results | Released to provider chart immediately upon auto-verification |
| Manually verified results | Tech reviews held result, verifies, and releases to provider chart |
| TAT monitoring | Specimens exceeding TAT threshold flagged with red highlighting in Beaker worklist |
| STAT TAT threshold | 47 minutes from receipt (Cepheid GeneXpert Infinity) |
| Routine TAT threshold | 3.5 hours from receipt (Hologic Panther) |

---

## Complete Workflow Summary

```
Order Entry in Epic
        ↓
Specimen Collection
(NP/VTM, NP/UTM, Throat/VTM, Throat/UTM — eSwab REJECTED)
        ↓
Specimen Receipt in Epic Beaker
(All container IDs verified — TAT clock starts)
        ↓
Accessioning and Routing Decision
        ↓
    ┌─────────────────────────────────────┐
    │                                     │
STAT + NP Source              Routine + NP Source
OR Any Throat Source          
Cepheid GeneXpert Infinity    Hologic Panther
47 min TAT                    3.5 hr TAT
    │                                     │
    └──────────────┬──────────────────────┘
                   ↓
        Result Transmitted to LIS
                   ↓
        CER Rules Evaluated in Beaker
                   ↓
    ┌──────────────────────────────────┐
    │                                  │
All Rules Pass               Any Rule Fails
Auto-Verification            Hold for Manual
                             Tech Review
    │                                  │
    └──────────────┬───────────────────┘
                   ↓
    Result Released to Provider Chart
    (TAT monitored — red highlight if exceeded)
```

---

## Disclaimer
All order codes, facility identifiers, and system configurations in this document are fictional and created for portfolio demonstration purposes only. Content reflects general Epic Beaker Clinical Pathology workflow knowledge and does not represent any specific health system's proprietary build configuration.
