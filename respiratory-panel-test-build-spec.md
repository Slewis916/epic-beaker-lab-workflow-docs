# Test Build Specification
## Respiratory Pathogen 4-Plex Panel
### SARS-CoV-2 / Influenza A / Influenza B / RSV

---

## Document Information
| Field | Detail |
|---|---|
| Document Type | Test Build Specification |
| Facility Identifier | LAB0001 |
| Author | J. Lewis, Medical Laboratory Scientist |
| Status | Draft |
| Date | June 2026 |

---

## Test Overview
| Field | Detail |
|---|---|
| Test Name | Respiratory Pathogen 4-Plex Panel |
| Order Code | LAB0001-RESP4 |
| Test Type | Molecular — Multiplex PCR |
| Performing Lab | Virology |
| Result Type | Coded — Detected / Not Detected per analyte |

---

## Analyte Components
| Component | Result Code | Possible Results |
|---|---|---|
| SARS-CoV-2 | LAB0001-COV19-R | Detected / Not Detected |
| Influenza A | LAB0001-FLUA-R | Detected / Not Detected |
| Influenza B | LAB0001-FLUB-R | Detected / Not Detected |
| RSV | LAB0001-RSV-R | Detected / Not Detected |

**Co-detection:** Multiple analytes may be simultaneously positive on a single specimen. Common co-detections include SARS-CoV-2 + RSV, SARS-CoV-2 + Influenza A/B, and Influenza A/B + RSV. Each component result reports independently regardless of other analyte results. Co-detection does not trigger a hold or special routing — all components report normally upon successful auto-verification.

---

## Specimen Requirements
| Field | Detail |
|---|---|
| Acceptable Specimen Types | Nasopharyngeal swab in Viral Transport Media (VTM) |
| | Nasopharyngeal swab in Universal Transport Media (UTM) |
| | Throat swab in VTM or UTM (see routing exception below) |
| Unacceptable Specimen Types | eSwab — incorrect container, not validated for this assay |

### Rejection Criteria
| Rejection Reason | Action |
|---|---|
| eSwab container received | Reject — request recollection in VTM or UTM |
| Specimen source other than NP or Throat | Reject — incorrect source |
| Insufficient volume | Reject — request recollection |

---

## Order Priority Configuration
| Patient Location | Order Priority | Platform | TAT |
|---|---|---|---|
| Emergency Department | STAT (automatic) | Cepheid GeneXpert Infinity | 47 minutes |
| Operating Room | STAT (automatic) | Cepheid GeneXpert Infinity | 47 minutes |
| Inpatient Floors | STAT (automatic) | Cepheid GeneXpert Infinity | 47 minutes |
| Outpatient / Ambulatory | Routine (default) | Hologic Panther | 3.5 hours |
| Any location — provider override | STAT (manual) | Cepheid GeneXpert Infinity | 47 minutes |

**Note:** Order priority is driven by patient location. ED, OR, and inpatient patients are automatically assigned STAT priority. Outpatient orders default to Routine unless provider manually upgrades to STAT at order entry.

---

## Specimen Routing Logic
| Condition | Platform | Rationale |
|---|---|---|
| STAT order + NP source | Cepheid GeneXpert Infinity | Validated for NP specimens, 47-min TAT |
| Routine order + NP source | Hologic Panther | Validated for NP specimens, 3.5-hr TAT |
| Any order + Throat source | Hologic Panther | Cepheid GeneXpert Infinity NOT validated for throat specimens for 4-plex testing — routing override applies regardless of order priority or patient location |

**Routing Exception:** Throat specimens must always route to Hologic Panther regardless of patient location or order priority. This override takes precedence over all other routing rules.

---

## Add-On Testing — Mini Respiratory Panel
Providers may add on a Mini Respiratory Panel to test for additional analytes.

| Patient Location | Specimen Source | Platform |
|---|---|---|
| Inpatient floors | NP/VTM/UTM | Diasorin PLEX + Hologic Panther |
| Emergency Department | NP/VTM/UTM | Diasorin PLEX only |
| Cancer patients (Oncology) | NP/VTM/UTM | Diasorin PLEX only |
| Labor and Delivery | NP/VTM/UTM | Diasorin PLEX only |
| Operating Room | NP/VTM/UTM | Diasorin PLEX only |
| Any patient | Throat source | Hologic Panther only |

---

## CER Rules — Auto-Verification Criteria
Auto-verification will trigger when ALL of the following conditions are met:

| CER Rule | Pass Condition | Pass Action | Fail Action |
|---|---|---|---|
| All 4 components resulted | Each analyte has a valid Detected or Not Detected result | Proceed to next rule | Hold — one or more components missing or invalid |
| No critical value designation | This panel has no critical value configuration | Proceed to next rule | N/A |
| Result within expected parameters | Detected or Not Detected result generated | Proceed to next rule | Hold — manual review |
| QC valid for run | Current QC within acceptable limits | Proceed to next rule | Hold — QC review required |
| CT value within threshold | CT value at or below cutoff threshold | Auto-verify and release to provider chart | Hold — manual review required |

**Auto-verification outcome:**
- ALL rules pass → Result auto-verifies and releases to provider chart automatically
- ANY rule fails → Result held in queue for manual tech review and verification

**Critical Value Configuration:** No critical value designation configured for any component of this panel. All results — Detected or Not Detected — route to provider chart upon successful auto-verification without mandatory provider callout requirement.

**Note on CT Value Cutoff:** CT value cutoff threshold to be verified from platform package insert prior to build configuration. Approximate threshold is 40-42 cycles — confirm exact value before finalizing build.

---

## TAT Monitoring
| Field | Detail |
|---|---|
| TAT Tracking Start | Specimen receipt timestamp in Epic Beaker |
| TAT Alert | Specimens exceeding TAT threshold flagged with red highlighting in Beaker worklist |
| STAT TAT threshold | 47 minutes from receipt (Cepheid GeneXpert Infinity) |
| Routine TAT threshold | 3.5 hours from receipt (Hologic Panther) |

---

## Result Routing
| Condition | Action |
|---|---|
| All CER rules pass | Auto-verify and release to provider chart |
| Any CER rule fails | Hold in queue for manual tech review and verification |
| Multiple analytes positive | Each component reports independently — no special routing triggered |

---

## Disclaimer
All order codes, facility identifiers, and system configurations in this document are fictional and created for portfolio demonstration purposes only. Content reflects general Epic Beaker Clinical Pathology workflow knowledge and does not represent any specific health system's proprietary build configuration.
