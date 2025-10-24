# ✅ README.md 


---

````markdown
# Sales Analytics – dbt Project

A real-world **Sales Analytics** pipeline built using `dbt` + BigQuery.

This project cleans and transforms raw sales data into **trusted business insights**, while also serving as a learning environment to practice dbt:

✅ Staging models  
✅ Final analytics models  
✅ Sources + Schema tests  
✅ Documentation + GitHub Pages hosting  
✅ CI-ready project structure

---


````

## 🔧 Setup Instructions

### 1️⃣ Create Virtual Environment

```bash
python -m venv dbt-env
dbt-env\Scripts\activate   # Windows

### 2️⃣ Install dbt (BigQuery adapter)

```bash
pip install dbt-bigquery
```

### 3️⃣ Check installation

```bash
dbt --version
```

### 4️⃣ Configure BigQuery Profile

File: `~/.dbt/profiles.yml`

```yaml
sales_analytics:
  target: dev
  outputs:
    dev:
      type: bigquery
      method: service-account
      project: sales-analytics-476020
      dataset: sales_database
      keyfile: path/to/service_account.json
      threads: 4
```

---

## 📦 Project Structure

```
Sales_Analytics/
  models/
    staging/
      stg_sales.sql
      sales_final.sql
  macros/
    dynamic_partition.sql
  dbt_project.yml
```

---

## ✅ Common dbt CLI Commands

| Command             | Purpose                  |
| ------------------- | ------------------------ |
| `dbt debug`         | test database connection |
| `dbt run`           | execute models           |
| `dbt test`          | run tests                |
| `dbt clean`         | remove target folder     |
| `dbt docs generate` | build documentation      |
| `dbt docs serve`    | preview docs locally     |
| `dbt compile`       | only compile SQL         |
| `dbt deps`          | install packages         |

---

## ❌ My Mistakes & ✅ How I Fixed Them

| Issue                                    | What Happened                                     | Solution                                                               |
| ---------------------------------------- | ------------------------------------------------- | ---------------------------------------------------------------------- |
| ✅ 1. Virtual env not activated           | `dbt not recognized` error                        | Use: `dbt-env\Scripts\activate` BEFORE running dbt                     |
| ✅ 2. Wrong dbt path quoting              | Used `'project.dataset.table'` → SQL syntax error | Must use **backticks** in BigQuery: <br> `` `project.dataset.table` `` |
| ✅ 3. Macro missing                       | `dynamic_partition` undefined                     | Removed unused macro / ensured correct syntax                          |
| ✅ 4. Wrong reference to raw table        | Missing `source()`                                | Used: `from {{ source('sales_database', 'raw_sales') }}`               |
| ✅ 5. Stale target folder caused failures | BigQuery still saw failed view                    | Fix: `dbt clean && dbt run`                                            |

✅ All fixed successfully ✔

---

## 🧪 Tests Included

* `not_null`
* `unique`
* Relationship tests between staging and final models

---

## 📊 Documentation

To build docs locally:

```bash
dbt docs generate
dbt docs serve
```

GitHub Pages live docs:
🔗 [*(deployment steps below)*](https://mosamir70.github.io/Sales_Analytics/#!/overview)

---

## 🚀 Future Enhancements

* Add more fact & dimension models
* CI/CD automation using GitHub Actions
* Data quality alerts

---

## 👤 Author

**Muhammad Samir**
GitHub: [@MoSamir70](https://github.com/MoSamir70)

