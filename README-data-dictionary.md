# Data Dictionary Browser - Prototype

## What This Is

A working prototype demonstrating how ReportAll's data dictionary could work as a browsable web application. This single HTML file contains all 133 field mappings and 1,700+ lookup codes from your existing CSV files.

## Key Features

- **Global Search**: Find any field by display name, FA column, or Rep column
- **Category Navigation**: Filter fields by category (Location, Building, Sales Transfer History, etc.)
- **Lookup Code Drill-Down**: Click any code group (like "garage" or "doc_type") to see all codes in a slide-over panel
- **Source Priority Indicators**: See whether each field prioritizes First American (FA) or ReportAll (Rep) data
- **PII Flags**: Redacted fields are marked for quick identification
- **Zero Dependencies**: Everything is in one HTML file—no server required

## How to Use

1. Open `data-dictionary-prototype.html` in any web browser
2. Use the search box to find specific fields
3. Click categories in the sidebar to filter
4. Click any blue "code link" to see the lookup values

## How This Fits Chris's Architecture

This browser can be **generated automatically** from structured data files (YAML/JSON) stored in your repository:

```
repo/
├── data/
│   ├── fields.yaml          # Field definitions (source of truth)
│   ├── codes/
│   │   ├── garage.yaml      # Lookup codes by group
│   │   ├── doc_type.yaml
│   │   └── ...
│   └── schema.yaml          # Metadata about the schema
├── scripts/
│   ├── generate-browser.py  # Creates this HTML file
│   └── detect-drift.py      # Alerts on undocumented columns
└── docs/
    └── data-dictionary.html # Generated output
```

**Benefits of this approach:**

1. Engineers update YAML alongside code (same commit, same PR)
2. Nightly job runs `detect-drift.py` to find undocumented columns
3. CI/CD runs `generate-browser.py` to rebuild the HTML
4. Browser auto-deploys to internal server / Confluence / GitHub Pages

## What's NOT in This Prototype

- Product-specific views (which fields are in LandGlide vs. API)
- Data lineage / transformation documentation
- Sample values for each field
- Last updated timestamps
- Change history

All of these can be added to the YAML schema and rendered in the browser.

## Technical Notes

- The HTML file is ~245 KB (includes all embedded data)
- Works in any modern browser (Chrome, Firefox, Safari, Edge)
- Could be converted to React for more interactivity if needed
- Data is embedded as JSON—easy to switch to fetching from an API

## Next Steps

1. Review this prototype with Chris and stakeholders
2. Agree on YAML schema for field definitions
3. Set up repository structure and automation
4. Begin documenting fields systematically
