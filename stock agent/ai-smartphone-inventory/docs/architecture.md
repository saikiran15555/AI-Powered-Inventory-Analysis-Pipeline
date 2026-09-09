# Architecture

```text
CSV / Excel data
      |
      v
     n8n
      |
      v
Data processing
      |
      v
Inventory calculations
      |
      v
AI analysis
      |
      v
Prioritized result
```

- **CSV / Excel data:** Inventory data is supplied as a file. The current workflow uses the sample CSV in `input/`.
- **n8n:** Reads the file and coordinates each workflow step.
- **Data processing:** Converts the CSV rows into data that n8n can work with.
- **Inventory calculations:** Calculates stock coverage days and compares coverage with supplier lead time.
- **AI analysis:** The workflow prepares a short analysis prompt. A real AI provider can be connected later without putting credentials in the repository.
- **Prioritized result:** The workflow formats each model with its inventory metrics, risk level, reason, and suggested action.
