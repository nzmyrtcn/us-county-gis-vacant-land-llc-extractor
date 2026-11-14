# US County GIS 200+ Acre Vacant Land, 4-State LLC Mailing & Infrastructure Datasets

[![Run on Apify Console](https://img.shields.io/badge/Run_on_Apify_Console-00C853?style=for-the-badge&logo=apify&logoColor=white)](https://apify.com/nazim_data_ops/us-vacant-land-200-acres-gis)

Queries public US County ArcGIS REST FeatureServer endpoints and state corporate registries across FL, GA, AZ, and OH. It isolates 200+ acre and 160-acre Homestead vacant land tracts with zero building value. Commercial Registered Agents get filtered out automatically. Every run outputs a 5-sheet Excel workbook, Google Earth KML and QGIS GeoJSON boundary polygons in a single archive, an HTML summary report, and structured JSON dataset rows. The repository also includes the 3-tab Puerto Rico Telecom Tower, OGPe Solar, and LUMA/AAA Utility Directory sample workbook.

## Pre-Configured Cloud Tasks (1-Click Run on Apify)
- [US County 200+ Acre Vacant Land GIS & Absentee Owner Finder](https://apify.com/nazim_data_ops/us-vacant-land-200-acres-gis/examples/us-county-vacant-land-200-acre-gis-extractor): Queries County ArcGIS FeatureServer layers to isolate 200+ acre vacant land tracts, absentee individual owners, and KML/GeoJSON polygon boundaries.
- [US Real Estate LLC Principal & Off-Site Mailing List Extractor](https://apify.com/nazim_data_ops/us-vacant-land-200-acres-gis/examples/us-real-estate-llc-decision-maker-mailing-extractor): Filters out commercial Registered Agents (CSC, Cogency Global, CT Corp) and property situs addresses to extract verified principal mailing addresses across FL, GA, AZ, and OH.
- [Alaska KPB 160-Acre Homestead & Quarter-Section GIS Mapper](https://apify.com/nazim_data_ops/us-vacant-land-200-acres-gis/examples/alaska-kpb-homestead-quarter-section-gis-mapper): Isolates exact 160-acre PLSS quarter-section homestead parcels with zero building value ($0 improvement value) and packages KML/GeoJSON boundary rings.

## Sample Deliverables (Included in `/samples`)
1. [`samples/US_GIS_Vacant_Land_and_LLC_Audit.xlsx`](./samples/US_GIS_Vacant_Land_and_LLC_Audit.xlsx): 5-sheet Excel workbook with native `=SUM` formulas:
   - `Tab 1 - Verified Qualifying`: 200+ acre vacant private parcels ($0 improvement value) with absentee owner mailing addresses and WGS84 centroid coordinates.
   - `Tab 2 - Manual Review`: 160-acre PLSS quarter-section homestead parcels and sub-threshold reference tracts.
   - `Tab 3 - Excluded Properties`: Disqualified municipal, native corporation, or improved parcels logged with exact exclusion reasons.
   - `Verified_LLC_Mailing_List`: 16 SFR investor LLC records across FL, GA, AZ, and OH with SOS Document IDs, managing member names, and off-site mailing addresses.
   - `Verification_QC_Audit`: Cross-verification audit trail comparing county tax roll situs addresses against state SOS corporate filings.
2. [`samples/US_GIS_Vacant_Land_GIS_Polygons.zip`](./samples/US_GIS_Vacant_Land_GIS_Polygons.zip): Packaged `.geojson` and `.kml` parcel boundary polygons ready for Google Earth Pro or QGIS.
3. [`samples/US_GIS_Vacant_Land_Report.html`](./samples/US_GIS_Vacant_Land_Report.html): Standalone HTML executive summary report.
4. [`samples/PR_Infrastructure_Utility_Directory_Sample.xlsx`](./samples/PR_Infrastructure_Utility_Directory_Sample.xlsx): 3-sheet Puerto Rico infrastructure workbook:
   - `Table 1 - Installers Directory`: OGPe and CIAPR certified solar PV and cistern contractors with DACO/NEPR audit logs.
   - `Table 2 - Telecom Mapping`: FCC ASR and FAA registered telecom towers with GPS coordinates, height (m), and carrier host details.
   - `Table 3 - Utility Playbooks`: LUMA Energy, AAA Water, and telecom onboarding workflows, required documents, deposits, and activation timelines.
5. [`samples/sample_dataset.json`](./samples/sample_dataset.json): Structured 32-record JSON dataset output.

## Input Schema (`schema/input_schema.json`)
```json
{
  "arcgisEndpoints": [
    "https://services.arcgis.com/XdwPqILKwMlOaw4F/arcgis/rest/services/KPB_Parcels/FeatureServer/0"
  ],
  "minAcreage": 200,
  "includeHomestead160": true,
  "maxImprovementValue": 2000,
  "maxLiveParcels": 5,
  "includeVerifiedKpb16": true,
  "includeLlcDirectory": true,
  "llcStates": ["FL", "GA", "AZ", "OH"]
}
```

## Run via Apify API (cURL)
```bash
curl -X POST "https://api.apify.com/v2/acts/nazim_data_ops~us-vacant-land-200-acres-gis/runs?token=<YOUR_APIFY_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{"minAcreage": 200, "includeHomestead160": true, "includeVerifiedKpb16": true, "includeLlcDirectory": true}'
```
