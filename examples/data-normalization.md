# Example run: making supplier product data consistent

All results are proposals. Supplier names are replaced with "Supplier A" and "Supplier B".

## Problem
- **System:** an importer that turns each supplier's product data files (JSON) into one standard catalog with search filters.
- **Must improve:** complete, consistent data for every supplier.
- **Core contradiction:** we want consistent data across every supplier, but getting it seems to need a person to hand-name fields and redo the mapping for each new supplier.
- **Known facts (from a field-by-field diff):** the two suppliers share few field names. Pressure and flow are stored differently (A: text with the unit inside, like "5000 psi"; B: a number plus a separate unit field). B uses several names for one thing (`seal`, `seals`, `seal_material`). Filler values exist ("Other", "See graph", empty fields). Only 3 of 13 shared filters match in both shape and spelling.
- **Decisions already made:** (1) the front-end search filters are the source of truth for which attributes matter; (2) material names use the generic name, not brand names; (3) filler is reported as missing, not stored as a value; (4) original files are never edited.

## The 40
| # | Principle → question | Suggestion (proposal) | Tag |
|---|---|---|---|
| 1 | Segmentation | Split the importer into small fixed stages: name match, unit parse, synonym fix, split packed values, filler check. Each new supplier reuses all of them. | useful |
| 2 | Taking out | Move every supplier-specific rule out of code into one small match file per supplier. | useful |
| 3 | Local quality | Be strict on fields that feed filters; keep display-only fields as printed. | useful |
| 4 | Asymmetry | Map supplier → standard only, never supplier → supplier. | useful |
| 5 | Merging | Handle B's duplicate names with the same synonym table used across suppliers. | useful |
| 6 | Universality | Each dictionary entry (unit, type, allowed values) is also the validation rule. | useful |
| 7 | Nested doll | Store each value with its original wording inside it. | useful |
| 8 | Counterweight | Every confirmed match becomes evidence for the next supplier's proposals. | useful |
| 9 | Preliminary anti-action | Run the diff against the dictionary before importing a new supplier. | useful |
| 10 | Preliminary action | Seed synonym tables now from known industry terms. | useful |
| 11 | Beforehand cushioning | Unmatched values go to a quarantine list and quality report; the import never blocks. | useful |
| 12 | Equipotentiality | Store numbers in one canonical unit; convert only for display. | useful |
| 13 | Inversion | Start from each search filter and find which supplier field answers it, instead of mapping every supplier field. | useful |
| 14 | Curvature | Nothing useful here. | nothing |
| 15 | Dynamics | Confidence thresholds: strong matches auto-proposed, weak ones wait for review. | useful |
| 16 | Partial action | Aim for 100% on the filters for a category; keep everything else as printed. | useful |
| 17 | Another dimension | Add a "meaning" tag (quantity, role) between field and attribute. | maybe |
| 18 | Vibration | Nothing useful here. | nothing |
| 19 | Periodic action | Re-run the diff after each data batch to catch new spellings. | maybe |
| 20 | Continuity | Each import adds to the shared tables, improving the next. | useful |
| 21 | Skipping | Nothing new beyond 15/16. | nothing |
| 22 | Blessing in disguise | The messy overlaps are the evidence that proves a match. "See graph" can link to the datasheet page. | useful |
| 23 | Feedback | Track filter fill per supplier after each import; drops flag themselves. | useful |
| 24 | Intermediary | The standard dictionary sits in the middle: N mappings, not N×N. | useful |
| 25 | Self-service | The importer proposes its own matches from evidence and checks itself. | useful |
| 26 | Copying | Test every rule change on frozen sample files first. | useful |
| 27 | Cheap short-living objects | Probe-import 20 records of a new supplier, read the report, discard. | maybe |
| 28 | Mechanics substitution | Use AI to read label plus sample values and propose matches, with evidence shown. | useful |
| 29 | Pneumatics/hydraulics | Nothing useful here. | nothing |
| 30 | Thin films | Thin per-supplier adapter around a fixed core. | dup (#2) |
| 31 | Porous | Store gaps explicitly as "missing, reason X" so they're counted. | useful |
| 32 | Color change | Per-supplier, per-filter green/yellow/red readiness grid. | useful |
| 33 | Homogeneity | One value type per attribute across all suppliers. | useful |
| 34 | Discarding and recovering | Clean layer can be thrown away and rebuilt from raw files plus rules. | useful |
| 35 | Parameter change | Split values holding two facts into separate fields. | useful |
| 36 | Phase transitions | Nothing useful here. | nothing |
| 37 | Thermal expansion | Nothing useful here. | nothing |
| 38 | Enriched atmosphere | Fill empty records from source documents before matching. | maybe |
| 39 | Inert atmosphere | Import into staging; nothing goes live until the supplier passes the check. | useful |
| 40 | Composite | A match needs several signals to agree: name, label words, value overlap, unit, range. | useful |

**Tally:** 28 useful (one is a dup), 5 maybe, 7 nothing.

## Top ideas
1. **Start from the filters (#13 + #24).** For each filter, find which supplier field answers it. Effort per supplier is capped at that category's filters.
   - *Could worsen:* non-filter fields stay unmapped (kept verbatim).
   - *Cheapest test:* run it on sample files for 5 filters and compare fill counts.
   - *Label:* **rediscovery** of decision (1). It confirms the decision; it isn't new.
2. **Match by values, not names (#25 + #40 + #8).** Propose a match only when value lists, units, and ranges agree. Confirmed matches feed the next supplier.
   - *Could worsen:* a wrong match that looks strong.
   - *Cheapest test:* score A's "Seal Material" against B's `seal`; it should score high and a random pair low.
   - *Label:* **new**.
3. **One small match file per supplier (#2 + #4).** Dictionary and rules stay fixed; adding a supplier never means redoing the mapping.
   - *Could worsen:* the dictionary becomes a bottleneck if no one owns it.
   - *Cheapest test:* write B's match file by hand for 10 fields and time it.
   - *Label:* **new** in form; consistent with decision (4).
4. **Gaps recorded as missing, with reason (#31 + #11).**
   - *Could worsen:* reports grow noisy.
   - *Cheapest test:* count filler values per supplier on the sample files.
   - *Label:* **rediscovery** of decision (3).
5. **Rebuildable clean layer plus staging (#34 + #39).**
   - *Could worsen:* extra storage and a rebuild step.
   - *Cheapest test:* rebuild the sample import twice and diff the outputs.
   - *Label:* **rediscovery** of decision (4).

## Still unproven
- Whether value-based matching scores well in practice (test 2).
- How many filters each category really uses (test 1).

## Review note
A domain expert reviewed this and pointed out that idea 1 was already their standing decision. Of the top ideas, only value-based matching was truly new. That's a typical, honest outcome.
