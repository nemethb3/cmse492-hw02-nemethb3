# cmse492-hw02-nemethb3

**Homework 02 — SQL Mini-Project with Sakila**
*CMSE 492 | Brendan Nemeth*

---

## Project Overview

This project is a portfolio-ready SQL analysis using the [Sakila sample database](https://dev.mysql.com/doc/sakila/en/) — a fictional DVD rental store dataset. The analysis investigates **whether customers from different countries show measurably different genre preferences when renting films**, and whether certain countries skew toward specific categories relative to the global average.

The imagined audience is a **marketing analyst** looking to design region-specific promotions by understanding which genres are most popular in each country.

---

## What Is Accomplished

The notebook walks through a complete analytic workflow, structured around six SQL techniques:

| Section | Technique | Question Answered |
|---|---|---|
| 2 | Multi-table JOINs | Per-rental view of customer, country, film, and genre; per-customer rental counts and genre diversity |
| 3 | GROUP BY + HAVING | Which country/genre pairs have generated at least 50 rentals |
| 4 | CTE (`WITH` clause) | Global average rentals per genre, used to flag above/below average country preferences |
| 5 | Window functions (`OVER`) | Rank genres within each country by rental count; compute each genre's share of a country's total rentals |
| 6 | EXPLAIN / performance | Execution plan inspection on a complex multi-join query |
| 7 | Manager report table | Clean summary table ready for a slide or stakeholder meeting |

---

## Skills Showcased

- **SQL**: multi-table JOINs across 5+ tables, GROUP BY / HAVING, CTEs, window functions (`RANK()`, `SUM() OVER`), `EXPLAIN` query analysis
- **Python**: `sqlalchemy` engine and parameterized queries, `pandas` for result handling and light post-processing
- **Docker**: containerized MySQL + Adminer setup via `docker-compose`
- **Data validation**: row-count checks, spot-checks against base tables, sanity checks on aggregates

---

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running
- Python 3.x with the following packages:
  ```
  pip install pandas sqlalchemy pymysql jupyter
  ```

---

## Running the Database

The database runs in Docker using the pre-loaded `sakiladb/mysql` image. From the repo root:

```bash
docker compose up -d
```

This starts two containers:

| Container | Port | Purpose |
|---|---|---|
| `cmse492-mysql` | `3306` | MySQL with Sakila pre-loaded |
| `cmse492-adminer` | `8080` | Web-based DB browser (optional) |

To verify the containers are running:

```bash
docker ps
```

To stop the containers:

```bash
docker compose down
```

---

## Connecting to the Database

### From the Notebook (SQLAlchemy)

The notebook connects automatically using these credentials, which match the `sakiladb/mysql` image defaults:

| Field | Value |
|---|---|
| Host | `localhost` |
| Port | `3306` |
| Database | `sakila` |
| Username | `sakila` |
| Password | `p_ssW0rd` |

The connection is established in **Section 0** of the notebook and shared across all queries via a `run_sql()` helper that returns results as a `pandas` DataFrame.

### Via Adminer (Browser)

Once the containers are running, open [http://localhost:8080](http://localhost:8080) in a browser and log in with the credentials above (System: `MySQL`).

---

## Running the Notebook

1. Start the database (see above).
2. Launch Jupyter:
   ```bash
   jupyter notebook HW02-STUDENT.ipynb
   ```
3. Run all cells from top to bottom (**Kernel → Restart & Run All**).

Section 0 must succeed (database connection) before any query sections will work.
