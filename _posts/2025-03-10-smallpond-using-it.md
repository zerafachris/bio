---
title: "using Smallpond"
tags:
  - AI
  - LLM
  - PLatform
  - FeatureEngineering
toc: true
---

<figure>
	<a href=""><img src="https://i.imgur.com/HMbrU0Y.png"></a>
</figure>

Smallpond is a promising tool for distributed data processing, extending DuckDB's capabilities to handle massive datasets across multiple nodes. In this article, we’ll dive deeper into how Smallpond works, explore its architecture, and provide practical examples to help you get started.

## How Smallpond Works

Smallpond’s architecture is designed around three core principles: **Lazy DAG Execution**, **Logical to Execution Plan Conversion**, and **Ray Core for Distribution**. Let’s explore each in detail.

### Lazy DAG Execution

Smallpond employs lazy evaluation for operations such as `map()`, `filter()`, and `partial_sql()`. Instead of executing these operations immediately, it constructs a **logical execution plan** represented as a Directed Acyclic Graph (DAG). Each operation corresponds to a node in the DAG (e.g., `SqlEngineNode`, `HashPartitionNode`, `DataSourceNode`).

Execution is deferred until an action is explicitly triggered, such as:

- `write_parquet()` – Write data to disk.
- `to_pandas()` – Convert results to a Pandas DataFrame.
- `compute()` – Force computation explicitly.
- `count()` – Count rows.
- `take()` – Retrieve rows.

This lazy approach optimises performance by avoiding unnecessary computations and reducing redundant operations.

### From Logical to Execution Plan

When an action is triggered, the logical plan is converted into an **execution plan**. This execution plan consists of tasks (e.g., `SqlEngineTask`, `HashPartitionTask`) that correspond to the nodes in the logical plan. These tasks are the actual work units distributed across the cluster.

For example:
- A `SqlEngineTask` might execute a SQL query on a specific partition.
- A `HashPartitionTask` could redistribute data across nodes based on a hash function.

### Ray Core and Distribution

Smallpond leverages **Ray Core** for distributing tasks across nodes. The distribution mechanism operates at the Python level, with tasks assigned to partitions based on user-defined strategies:

- **Hash Partitioning:** Distributes data based on column values.
- **Even Partitioning:** Splits data evenly by files or row counts.
- **Random Shuffle Partitioning:** Randomly shuffles data across partitions.

<figure>
	<a href=""><img src="https://i.imgur.com/MB2CAyo.png"></a>
</figure>

Each partition runs independently within its own Ray task, using DuckDB instances to process SQL queries. This architecture prioritises horizontal scaling (adding more nodes) over vertical scaling (using larger machines). To use Smallpond effectively at scale, you’ll need a Ray cluster, which can be deployed on platforms like AWS, GCP, or Kubernetes. Alternatively, managed Ray services like Anyscale can simplify cluster management.



## Practical Examples

Let’s walk through some practical examples of using Smallpond for distributed data processing.

### Example 1: Setting Up and Loading Data

Start by installing Smallpond:

```bash
uv pip install smallpond
```

Then initialise a Smallpond session and load your dataset:

```python
import smallpond as sp

# Initialise Smallpond session
session = sp.init()

# Load a Parquet file
df = session.read_parquet("data/prices.parquet")

print(df.head())
```

### Example 2: Repartitioning Data for Parallel Processing

Repartition your dataset into multiple partitions for parallel processing:

```python
# Repartition the dataset into 4 partitions
df = df.repartition(4)

# Perform a simple transformation
df = df.filter("price > 100").map(lambda row: {"price_with_tax": row["price"] * 1.2})

# Trigger computation and write results to Parquet
df.write_parquet("output/prices_with_tax.parquet")
```

In this example:
1. The dataset is divided into four partitions.
2. Each partition is processed independently using DuckDB instances within Ray tasks.
3. The results are written back to disk as Parquet files.

### Example 3: Running Custom SQL Queries

You can run custom SQL queries on your dataset:

```python
# Run an SQL query on the dataset
df = df.partial_sql("SELECT category, AVG(price) AS avg_price FROM {0} GROUP BY category")

# Trigger computation and convert results to Pandas DataFrame
result = df.to_pandas()

print(result)
```

Here, `{0}` represents the placeholder for each partition during execution.

### Example 4: Building a Custom Pipeline

For more complex workflows, you can manually construct a pipeline using Smallpond’s low-level API:

```python
from smallpond.logical.dataset import ParquetDataSet
from smallpond.logical.node import Context, DataSourceNode, SqlEngineNode, LogicalPlan
from smallpond.execution.driver import Driver

def my_pipeline(input_paths: list):
  ctx = Context()
  dataset = ParquetDataSet(input_paths)
  node = DataSourceNode(ctx, dataset)
  node = SqlEngineNode(ctx, (node,), "SELECT * FROM {0} WHERE price > 100")
  return LogicalPlan(ctx, node)

if __name__ == "__main__":
  driver = Driver()
  driver.add_argument("-i", "--input_paths", nargs="+")
  plan = my_pipeline(driver.get_arguments()["input_paths"])
  driver.run(plan)
```

Run this script with:

```bash
python script.py -i "data/*.parquet"
```

This approach provides fine-grained control over the pipeline construction and execution process.



## Tips for Using Smallpond Effectively

1. **Start Small:** Begin with single-node experiments before scaling out to clusters.
2. **Optimise Partitioning:** Choose partitioning strategies that align with your workload (e.g., hash partitioning for joins).
3. **Leverage Managed Services:** Use managed Ray services like Anyscale to simplify cluster management.
4. **Monitor Performance:** Use profiling tools to identify bottlenecks in your pipeline.



## Conclusion

Smallpond offers a powerful yet flexible framework for distributed data processing, enabling DuckDB to scale beyond its single-node limitations. By leveraging lazy DAG execution, efficient task distribution via Ray Core, and customisable partitioning strategies, you can process massive datasets with ease. However, effective use of Smallpond requires careful planning around infrastructure and workload design.

With these examples and tips in hand, you’re ready to explore what Smallpond can do for your data processing needs!
