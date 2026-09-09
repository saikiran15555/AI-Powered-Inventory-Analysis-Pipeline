# AI Smartphone Inventory & Model Prioritizer

An n8n-based foundation for analyzing smartphone inventory and prioritizing brands and models by stock risk.

## Problem

Inventory teams need a simple way to see which smartphone models may need replenishment. This project starts with calculated stock coverage and a clear place to add AI analysis later.

## Current workflow

The workflow reads the sample CSV, calculates stock coverage days, compares coverage with supplier lead time, and sends the prepared metrics to a Google Gemini model for a reason and recommended action. It then appends each result to a Google Sheet. Credentials are selected in n8n after import and are not stored in this repository.

## Structure

- `docker/`: Docker Compose configuration
- `n8n/data/`: Persistent n8n data
- `input/`: Future input files
- `output/`: Future generated files
- `workflow/`: Importable n8n workflow export
- `src/`: Notes for future application code
- `docs/`: Architecture documentation
- `screenshots/`: Optional project screenshots
- `input/sample_inventory.csv`: Sample inventory data

## Start n8n

From the project root:

```bash
docker compose -f docker/docker-compose.yml up -d
```

Open n8n at <http://localhost:5678>.

Stop n8n with:

```bash
docker compose -f docker/docker-compose.yml down
```

Input files will later be placed in `input/`, and generated output files in `output/`.

The Docker configuration allows n8n to access only the mounted `/files/input` and `/files/output` folders. Restart the container after changing Docker configuration.

## Import the workflow

1. Open n8n at <http://localhost:5678>.
2. Open the workflows menu and choose **Import from File**.
3. Select `workflow/inventory_prioritizer.json`.
4. Open **Analyze Inventory** and select or create a Google Gemini API credential in n8n.
5. Open **Save to Google Sheets**, select a Google Sheets credential, then select the target spreadsheet and sheet.
6. Add headers in row 1 that match the result fields, such as `Brand`, `Model`, `CurrentStock`, `RiskLevel`, `Reason`, and `RecommendedAction`.
7. Run the workflow with **Execute Workflow**.

The workflow reads `/files/input/sample_inventory.csv`, which is the Docker path for `input/sample_inventory.csv`.
