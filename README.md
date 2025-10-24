# ✅ README.md 


---


# Sales Analytics – dbt Project

Step-by-Step Guide to End to end data engineering project (dbt + BigQuery, Github)

1. Set up Google Cloud Platform (GCP) and BigQuery
2. Create a BigQuery Dataset with  (1M+ rows) in BigQuery
3. Install and Configure dbt for BigQuery
4. Initialize a dbt Project
5. Connect dbt to BigQuery
6. Write dbt Models (SQL Transformations)
7. Run dbt Pipeline in BigQuery
8. Test and Document Your dbt Project
9. Push to github
10. Make a public doumention



#### 🔧 Setup Instructions



## Create Virtual Environment

```bash
python -m venv dbt-env
dbt-env\Scripts\activate   # Windows
```


## Create a BigQuery Dataset

```bash
Google Big query Consol: https://console.cloud.google.com/bigquery?project=temporal-parser-476019-m6&ws=!1m0
```

##  Initialize a dbt Project

```bash
dbt init Sales_Analytics
```

Which database would you like to use?
[1] bigquery

Enter a number: 1
[1] oauth
[2] service_account
Desired authentication method option (enter a number): 1
project (GCP project id): sales-analytics-476020
dataset (the name of your dbt dataset): sales_database
threads (1 or more): 4
job_execution_timeout_seconds [300]: 300
[1] US
[2] EU
Desired location option (enter a number): 1


---


## Install dbt (BigQuery adapter)

```bash
pip install dbt-bigquery
```

## Check installation

```bash
dbt --version
```

###  Configure BigQuery Profile

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

## Connect dbt to BigQuery


```bash
gcloud auth application-default login

If U have this error:
gcloud : The term 'gcloud' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is 
correct and try again.

Download SDK From: https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe
---- hint during Auth U must check right in all checkboxes
```


IF U Wonna permanet Solution for this error make SDK in System  variables 

-- Firstly check in it exists 

$env:PATH -split ';' ===>> search for C:\Program Files (x86)\Google\Cloud SDK\google-cloud-sdk\bin

-- if not exists add it  in is system  variables 

1- Windows Search → “Environment Variables” → Open.

2- Under System variables, select any Path → Edit.

3- Click New, and add: C:\Program Files (x86)\Google\Cloud SDK\google-cloud-sdk\bin

4- Click OK → OK → OK.

5- Restart VS Code again.

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
dbt docs serve --port 8080
```

Public docs:
🔗 [*(GitHub Pages Deployment)*](https://mosamir70.github.io/Sales_Analytics/#!/overview)

---

## 🚀 Future Enhancements

* Add more fact & dimension models
* CI/CD automation using GitHub Actions
* Data quality alerts

---

## 👤 Author

**Muhammad Samir**
GitHub: [@MoSamir70](https://github.com/MoSamir70)

