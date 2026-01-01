# Pipeline Repository Starter

This repository is the starter template for the CSAI-382 data pipeline project. It gives you a clean folder layout to organize Databricks or Jupyter notebooks, SQL scripts, automation code, and small sample datasets while you connect the repo to Databricks.

## Purpose
- Keep all pipeline assets (notebooks, SQL, automation, data samples) in one GitHub repository.
- Practice saving notebooks to GitHub through a Databricks-connected repo.
- Document what each folder is for so teammates and instructors can navigate quickly.

## Repository Structure
```
├── notebooks/
├── sql/
├── etl_pipeline/
├── data_samples/
└── README.md
```

- **notebooks/** — Databricks or Jupyter notebooks used for ETL tasks.
- **sql/** — Independent SQL transformation files.
- **etl_pipeline/** — Python scripts or workflow definitions used for automation.
- **data_samples/** — Small example datasets for testing (starter Parquet samples included).
- **README.md** — Overview of the project and quick instructions for using the repo.

## Getting Started
1. Accept the GitHub Classroom assignment to create your repository.
2. In Databricks, open **Repos → Add Repo**, link your GitHub account, and clone this repository into your workspace. This enables you to edit notebooks and push commits back to GitHub.
3. Add or create notebooks inside the `notebooks/` folder and save regularly so changes sync to GitHub.
4. Add SQL transformations to `sql/` and automation code to `etl_pipeline/` as you progress through the course.

## README Guidance
- Replace this text with your own description of the project and its purpose.
- Document what you put in each folder (especially new notebooks or scripts) and how to run them.
- Keep the README concise but clear enough that an instructor can find your work quickly.

## Checklist for Submission
- [ ] Repository is connected to Databricks (commits show Databricks-originated notebook changes).
- [ ] Required top-level folders exist: `notebooks/`, `sql/`, `etl_pipeline/`, `data_samples/`.
- [ ] README clearly explains the project and the purpose of each folder.
- [ ] Notebook and script updates are committed and pushed to GitHub.

## Notes on AI Usage
You may use Databricks AI helpers to learn or generate ideas. Always read, understand, and verify generated code before trusting it. Write your own README content and create folders manually to ensure you fully understand your project structure.
