# Text-to-SQL vs Direct Table-QA on Spider

This repository contains the code and findings for a project comparing two LLM-based pipelines for querying relational databases:

- **Text-to-SQL**: The model receives the database schema and a question, writes a SQL query, and the query is executed on SQLite to retrieve the answer.
- **Direct Table-QA**: The relevant tables are serialized into Markdown text and fed to the model, which returns the answer directly in JSON format (no SQL involved).

## Setup & Model
- **Model:** `Qwen/Qwen2.5-Coder-7B-Instruct`
- **Environment:** Google Colab (GPU support, 4-bit quantization).
- **Data:** 87 questions from the Spider benchmark, focusing on the `concert_singer` and `pets_1` databases.

*Note: The Spider dataset is not hosted in this repository. To reproduce the runs, download Spider and place it in your Google Drive following this structure:*
```text
/content/drive/MyDrive/spider/spider/
├── dev.json
└── database/
    ├── concert_singer/
    │   └── concert_singer.sqlite
    └── pets_1/
        └── pets_1.sqlite

```

## Evaluation & Results

Both pipelines were evaluated against the ground-truth outputs using Cell Precision, Cell Recall, and Tuple Cardinality.

| Method | Cell Precision | Cell Recall | Tuple Cardinality |
| --- | --- | --- | --- |
| Text-to-SQL | 0.9636 | 0.9598 | 0.9812 |
| Direct Table-QA | 0.6007 | 0.6459 | 0.6899 |

**Quick takeaway:** Text-to-SQL is vastly superior in this setup because the LLM delegates the actual relational math to SQLite. Table-QA works fine for basic lookups but breaks down on complex operations like aggregations, negative conditions, and multi-table reasoning.

## Repository Structure

```text
.
├── README.md
├── requirements.txt
├── text_to_SQL_vs_direct_table_QA.ipynb
├── report/
│   └── ATICS_PROJECT1.pdf
├── results/
│   ├── full_results.csv
│   ├── summary.csv
│   ├── sql_better_cases.csv
│   ├── qa_better_cases.csv
│   └── both_fail_cases.csv
└── src/
    └── text_to_SQL_vs_direct_table_QA.py

```

## How to Run

The easiest way to reproduce the results is by using the provided Colab notebook:

1. Open `text_to_SQL_vs_direct_table_QA.ipynb` in Google Colab.
2. Mount your Google Drive and ensure the Spider dataset is located at `/content/drive/MyDrive/spider/spider/`.
3. Run the dependency installation cell (or install via `pip install -r requirements.txt`).
4. Restart the Colab runtime if prompted.
5. Run the remaining cells to execute the pipelines.

The script will generate and save all output CSVs inside your designated results directory. For a detailed breakdown of the error analysis and qualitative examples, please check the technical report in `report/ATICS_PROJECT1.pdf`.
