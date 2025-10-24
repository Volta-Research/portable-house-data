# portable-house-data

The Portable House Data format is a lightweight, machine-readable JSON format for describing Canadian homes so that data can be cleanly exchanged between assessment tools, modelling engines, utilities, municipalities, and services providers, including energy advisors and other related consultants. It's designed for interoperability to support various workflows across the country, enabling a healthy ecosystem of software services today and in the future.

[![Schema: v1.0.1](https://img.shields.io/badge/schema-v1.0.1-blue.svg)](https://volta-research.github.io/portable-house-data/schema/versions/1.0.1/portableHouseData.schema.json)

## Why this standard

-   Retrofit at scale in Canada: Portable, comparable house data is needed to accelerate discovery, planning, delivery, and verification of home retrofits.
-   Interoperability: Data shouldn’t be trapped in proprietary silos. A clear, open schema lowers integration costs and avoids re-entering the same information.
-   Industry alignment: The schema is designed to align with other commonly used data formats and terminology (e.g. HOT2000, HPXML). In the future, it hopes to support the continued delivery of EnerGuide Rating System (ERS) services and preserve the role of Registered Energy Advisors by keeping inputs/outputs portable, allowing tools such as Virtual Home Energy Assessments to communicate with Energy Advisors and vice versa.
-   A healthy ecosystem: An open, low-barrier data layer invites new software and consulting services that may include analytics, retrofit planning and design, quote estimation, program delivery, financing, permitting, and more.

## Repository Structure

_Current schema:_ `v1.0.1`

```
portable-house-data/
├── docs/                                                   # Documentation for the portable house data format
│   ├── BACKGROUND.md                                       # Context and rationale
│   ├── inputs.rst                                          # Inputs data model (building/site/enclosure/systems/occupancy)
│   ├── outputs.rst                                         # Outputs data model (energy, GHG, peaks, by-fuel/by-end-use)
│   ├── metadata.rst                                        # Metadata (service provider, client, timestamps, versions)
├── sample_files/                                           # Example JSON instances
│   └── base.json                                           # Minimal valid object (quick start)
├── schema/                                                 # JSON Schema and validation examples
├── latest/portableHouseData.schema.json                    # The latest JSON Schema version
├── versions/                                               # Past JSON Schema versions
├── ├── 1.0.0/portableHouseData.schema.json
├── └── 1.0.1/portableHouseData.schema.json
│   └── test-validate.json                                  # VS Code example for inline validation
├── CHANGELOG.md                                            # Outlines changes between schema versions
├── MIGRATIONS.md                                           # Tips on migrating to newer schema versions
└── README.md                                               # You are here

```

## Quick Start

1. Clone the repo and open it in VS Code.
2. Open `schema/test-validate.json`. VS Code will validate it against the schema and display errors both in-line and in the Problems tab.
3. use `sample_files/base.json` as the starting point for your own data!

Tip: Put a `$schema` link at the top of any data file:

```
{
    "$schema": "../schema/latest/portableHouseData.schema.json",
    "inputs": {...}
}
```

## Sample Files

Sample files are in the `sample_files/` directory.

-   `base.json` is the smallest valid object. It can be used for testing pipelines and editor validation. It includes essential items like year built, location (e.g., postal code), floor area, foundation type, and primary heating fuel.

Tip: Use `base.json` as a template for building your own exporter/importer before handling the full schema.

### Validating Files

#### Option A - VS Code (Zero Config)

-   Open a JSON file that references the schema via `$schema`
-   Violations appear as red squiggles with details in the Problems tab.

#### Option B - Node.js (via AJV CLI)

```bash
npx ajv-cli \
  -s schema/portableHouseData.schema.json \
  -d sample_files/base.json \
  --spec=draft2020 -c ajv-formats --strict=false
```

#### Option C - Python (via jsonschema)

```python
import json
from jsonschema import Draft202012Validator, FormatChecker

with open("schema/portableHouseData.schema.json") as f: schema = json.load(f)
with open("sample_files/base.json") as f: data = json.load(f)

Draft202012Validator(schema, format_checker=FormatChecker()).validate(data)
```

## Data Model Overview

-   Inputs: location, building info, enclosure (foundation/walls/ceilings/windows/doors), systems (heating/cooling/hot water/heat pumps/ventilation/solar PV/storage), occupancy, base & atypical loads, temperature control.
-   Outputs: energy performance totals, fuel-type breakdowns, emissions, peak loads (availability-dependent)
-   Metadata: provenance, timestamps, software/tool versions

Minimal Object: see `sample_files/base.json`

## Contributing

1. Open an issue describing the change (new field, enum, unit, or constraint).
2. Add/adjust docs in docs/ and update portableHouseData.schema.json.
3. Include samples under sample_files/ and a validation case under schema/.
4. Submit a PR. We use semantic versioning for the schema (see below).

## Versioning

The schema follows SemVer:

-   MAJOR — breaking changes (rename keys, remove fields)
-   MINOR — new optional fields/enums
-   PATCH — clarifications, doc fixes

Reference the version in your data via metadata, e.g.:

```
"metadata": { "schemaVersion": "1.0.0" }
```

# FAQ

_Q: Do I have to provide a full address?_
A: No. Location supports multiple combinations (e.g. postal code, city + region, or lat/long).

_Q: Are outputs required?_
A: No. Outputs are not always computed and are optional to include alongside inputs and metadata.

## License & Contact

-   [License](LICENSE)
-   Contact: info@voltaresearch.org

The work encompassing the first version of the portable house data standard was made possible by funding provided by Alberta Ecotrust. The work was completed by Volta Research, with support from Lightspark. We hope the community of contributors to this work broadens as we continue our efforts towards helping Canada achieve its low-carbon, low-cost building goals.
