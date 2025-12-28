# Star Schema vs. Unified Star Schema Benchmark

This repository contains a benchmark comparing the performance and characteristics of a traditional **Star Schema** against the **Unified Star Schema (USS)** approach.

## Dataset

The benchmark is performed using the **TPC-DS** dataset with a **Scale Factor of 100 (SF100)**.

## Schemas

### Star Schema

In the traditional Star Schema, each fact table is directly related to its corresponding dimension tables.

![Star Schema](./Star%20Schema.png)

### Unified Star Schema (USS)

In the Unified Star Schema, a central `_bridge` table connects all dimension tables to all fact tables. This simplifies the model by centralizing relationships.

![Unified Star Schema](./Unified%20Star%20Schema.png)

## Benchmark Queries

The benchmark consists of the following DAX queries, designed to test various aspects of query performance:

| Query | Description |
| :--- | :--- |
| **P1_store_sales_by_year** | Aggregates store sales by year. |
| **P2_store_sales_by_year_category** | Aggregates store sales by year and item category. |
| **P3_store_sales_many_groups** | Aggregates store sales by year, item category, and store. Tests performance with multiple grouping columns. |
| **P4_top100_items_store_sales_2002** | Retrieves the top 100 items by store sales for the year 2002. |
| **P5_net_store_sales_by_month** | Calculates net store sales (Sales - Returns) by month. Involves joining sales and returns data. |
| **P7_total_sales_all_channels_by_year** | Calculates total sales across all channels (Store, Web, Catalog) by year. |
| **P9_inventory_wh_category_year_2002** | Aggregates inventory quantity by warehouse and item category for the year 2002. |
| **P10_store_sales_yoy_by_year** | Performs a Year-over-Year (YoY) analysis of store sales, calculating Sales, Sales PY, YoY Delta, and YoY %. |
| **P11_distinct_customers_with_orders** | Counts distinct customers who have placed an order across any channel (Store, Web, or Catalog). |

## Project Structure

- **`TPC-DS Generator.ipynb`**: Notebook used to generate the TPC-DS data.
- **`TPC-DS Benchmark.ipynb`**: Notebook used to execute the benchmark queries and analyze the results.

## Benchmark Results

### Performance by Dataset

![Performance by Dataset](./By%20Dataset.png)

### Performance by Query

![Performance by Query](./By%20Query.png)

## Methodology

The benchmark compares query execution times and other relevant metrics between the two schema modeling techniques. The Unified Star Schema aims to simplify the data model while maintaining or improving performance compared to the classic Star Schema.

The benchmarking process is automated using the `TPC-DS Benchmark.ipynb` notebook and follows a rigorous adaptive execution strategy to ensure reliable results:

1.  **Warmup Phase**:
    *   Each query is executed **2 times** (warmup runs) before measurement begins.
    *   These runs ensure that the engine caches and internal structures are primed, reducing cold-start variability.

2.  **Adaptive Measurement Phase**:
    *   After warmup, the query is executed repeatedly to collect performance data.
    *   **Minimum Runs**: At least **5** measured runs are performed.
    *   **Stability Check**: The system calculates the **Coefficient of Variation (CV)** of the execution times.
    *   **Stop Condition**: Execution stops when the CV drops below **5%** (indicating stable performance) or when a maximum of **100** runs is reached.

3.  **Error Handling**:
    *   If a query fails more than **3 times**, the benchmark for that specific query is aborted to prevent infinite loops.

4.  **Metrics Collected**:
    *   Execution duration (ms).
    *   Row and column counts of the result set.
    *   Result hash (to verify data consistency between runs).

## Contributions

We welcome contributions to make this benchmark as fair and comprehensive as possible!

While the initial hypothesis favors the Unified Star Schema (USS), the goal is to conduct an unbiased comparison. We encourage you to:

*   **Suggest new queries**: If you have complex DAX patterns or scenarios where you believe one schema might outperform the other, please submit them.
*   **Optimize existing queries**: If you see a way to write a more efficient query for either schema, let us know.
*   **Report issues**: If you find any flaws in the methodology or the data generation, please open an issue.

To contribute, please open an issue or submit a pull request with your proposed changes or new query definitions. Let's build a robust benchmark together!
