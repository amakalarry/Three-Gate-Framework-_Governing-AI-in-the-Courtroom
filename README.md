# Three-Gate Framework: Governing AI in the Courtroom

An interactive companion to **“Governing AI in the Courtroom”** (Femi-Adeyinka & Varol, ISDFS 2027), a framework for deciding when AI-generated or AI-transformed digital evidence should be admitted in court.

The framework first asks whether a tool is **extractive** (it only locates, copies, or formats existing records) or **interpretive** (it classifies, infers, enhances, or generates). Extractive output proceeds under ordinary authentication rules. Interpretive output must clear three gates, and the proponent bears the burden at each one:

| Gate | Question | Requirements |
| --- | --- | --- |
| **1 · Disclosure** | Do we know what the tool is and how it was built and validated? | Model card · Datasheet for data · Tool identification · Validation report · Source code access (on particularized need) |
| **2 · Reliability as applied** | Is it reliable *for this input, in this case*? | Domain validation · Error-rate specification · Version-specific results · Explainability output |
| **3 · Provenance** | Can every transformation from source to exhibit be traced and reproduced? | Provenance record (CASE/UCO) · Cryptographic integrity · Non-deterministic parameter logging · Reproducibility pathway |

## What the companion tool includes

- **Framework explorer**: a flowchart of the decision path with pass and fail routes. Select any step to see its requirements and the legal standards they map to (Daubert, Frye, FRE 702, NIST AI RMF, EU AI Act, CASE/UCO). Pick a scenario, such as facial recognition or AI-enhanced video, to trace its path.
- **Case analyses**: 16 decided matters analyzed through the three gates. Open any gate badge to see each requirement, whether it was met, and why.
- **Jurisdiction comparison**: how the US (federal and Frye states), EU, UK, India, Canada, and the Council of Europe handle each gate.
- **Assessment checklist**: classify a tool, check off the requirements the proponent can document, and see which gates clear.

## Repository layout

```
index.html               The companion tool: page, styles, and logic in one file
data/cases.json          Case summaries and requirement-by-requirement gate analyses
data/jurisdictions.json  Jurisdiction comparison table
```

## Viewing it

**Online:** if GitHub Pages is enabled for this repository, the tool is served at
`https://amakalarry.github.io/Three-Gate-Framework-_Governing-AI-in-the-Courtroom/`.

**Locally:** browsers block a page opened straight from disk from reading the JSON files, so serve the folder instead:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Any static file server works.

## Editing the case data

Cases live in `data/cases.json`. You can add, remove, or reword them without touching `index.html`, and the case counts on the page update automatically. Each case looks like this:

```jsonc
{
  "id": "puloka",                       // unique, lowercase, no spaces
  "name": "State v. Puloka",
  "year": 2024,
  "jurisdiction": "Washington (Frye)",
  "evidenceType": "AI-enhanced video",
  "icon": "video",                      // icon name, see below
  "theme": "red",                       // card color: red, amber, coral, green, teal, blue, purple
  "outcome": { "label": "Excluded", "icon": "ban", "theme": "red" },
  "summary": "One-paragraph account shown when the card is selected.",
  "gates": {
    "g1": {
      "result": "fail",                 // pass, fail, partial, na, none
      "requirements": [
        { "requirement": "Model card", "status": "not_met", "why": "One sentence explaining the call." }
        // ...one entry per requirement, in the order listed in the table above
      ]
    },
    "g3": { "result": "na", "note": "Why this gate was not reached." }
  }
}
```

- **Gate `result`** is the badge on the card. `none` means a court admitted the evidence without applying any gate scrutiny.
- **Requirement `status`** is one of `met`, `not_met`, `partial`, `na`, or `not_examined`.
- A gate has either a `requirements` list (5 for G1, 4 for G2, 4 for G3, in table order) or a single `note` when the gate wasn’t reached. The `requirement` labels are there for readability; the page uses each item’s position in the list.
- **Icons** available for cases: `video`, `face`, `dna`, `phone`, `photo`, `brain`, `chart`, `shield`, `fsearch`, `wave`, `cpu`. For outcomes: `ban`, `check-c`, `alert`, `fsearch`, `x`.

Jurisdictions in `data/jurisdictions.json` take `name`, `icon` (`building`, `pin`, `flag`, `crown`, `leaf`, `world`), `disclosure`, `reliability`, and `provenance`.

If a case has the wrong number of requirements for a gate, the browser console shows a warning that names the case.

## Note on the analyses

Gate analyses for *Puloka*, *Kohls v. Ellison*, *Schulte v. LinkedIn*, *ShotSpotter/Chicago*, and *Ferlito* follow the paper. The other eleven are illustrative applications of the framework to each case’s published facts and should be checked against the paper before being cited.

## Citation

Femi-Adeyinka & Varol, “Governing AI in the Courtroom,” *ISDFS 2027*. Sam Houston State University.
