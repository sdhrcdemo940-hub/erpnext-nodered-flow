# ERPNext Node-RED Flow

This repository contains a Node-RED flow for integrating ERPNext with CSV-based inventory updates. The flow reads stock data from a CSV file, validates the records, and posts stock entries to ERPNext through the ERPNext REST API.

## Overview

The project is designed to automate inventory synchronization using Node-RED. A scheduled flow can read a CSV file, parse each row, validate required fields, and create ERPNext `Stock Entry` records.

The main flow includes:

- Scheduled trigger (daily or custom schedule)
- CSV file input
- CSV parsing
- Row-by-row validation
- HTTP request to ERPNext
- Response handling and debug output

## Included Files

- `clean-flow.json` – cleaned version of the main ERPNext inventory sync flow
- `flows-minimal.json` – simplified flow example
- `flows_with_gemini_3.5_flash.json` – experimental flow variant referencing Gemini 3.5 Flash
- `ERPNext Inventory Sync.json` – ERPNext inventory sync flow configuration
- `ERPNext_NodeRED_User_Manual.docx` – user manual document
- `data/` – folder for runtime data files
- CSV sample files such as `test.csv` and `Stock Balance_RISB(1).csv`

## Typical Workflow

1. Place a CSV file into the configured input folder.
2. Node-RED reads the file.
3. The CSV is parsed row by row.
4. Required fields are validated (`item_code`, `qty`, `warehouse`).
5. A `POST` request is sent to ERPNext to create a `Stock Entry`.
6. The result is logged and debugged for monitoring.

## Example Data Flow

The main `clean-flow.json` flow contains the following logical sequence:

- `inject` -> file read -> CSV parse -> split rows -> validate -> HTTP request -> response handler -> debug

The HTTP action is pointed to:

- `http://backend:8000/api/resource/Stock Entry`

This suggests the flow expects a backend service or ERPNext instance reachable at the `backend` host on port `8000`.

## Prerequisites

Before importing and running this flow, ensure you have:

- Node-RED installed and running
- Access to an ERPNext instance
- API access to create `Stock Entry` records
- A valid bearer token or authentication method configured in Node-RED
- A CSV file with the expected inventory columns

## Recommended CSV Format

Your CSV should contain at least the following fields:

- `item_code`
- `qty`
- `warehouse`

Additional ERPNext-compatible fields may also be included depending on your business process.

## Node-RED Setup

1. Import one of the JSON flow files into Node-RED.
2. Configure the file input node to point to your import directory.
3. Set the ERPNext URL to match your server environment.
4. Add the correct authentication token or API credentials.
5. Verify the schedule or inject trigger.
6. Test with a sample CSV file.

## Example Runtime Path

The sample flow reads from:

- `/data/csv-drop/test.csv`

Adjust this to match your actual file storage path and environment.

## Notes

- This project is intended as an example/integration flow and may require adaptation to your ERPNext schema and warehouse structure.
- Some files in the repository appear to be sample/test data and may not be production-ready.
- The repository includes a `.docx` user manual that may contain additional setup guidance.

## Suggested Next Steps

- Review the `ERPNext_NodeRED_User_Manual.docx` for implementation details.
- Import `clean-flow.json` as the primary flow.
- Validate the ERPNext API endpoint and credentials.
- Test with a small dataset before enabling production automation.

## License

No explicit license file is included in the repository. Please check repository settings or contact the project owner before reusing the flow in a production environment.

## Contact / Maintainer

This repository appears to be a personal or experimental project. If you are using it for a team deployment, review and update the ERPNext endpoints, credentials, and CSV mappings before production use.
