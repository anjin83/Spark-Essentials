# Spark Notes:

## Chapter 1:

### SparkSession

### Dataframes: 
- Immutable Structured API that represents a table of data with rows and columns. Column names and data types are part of the schema.

### Partitions: 
- A partition is a collection of rows that sit on one physical machine in a cluster. A Dataframes partitions represent how the data is physically distributed across the cluster during execution. With Dataframes you do not manipulate partitions manually, Spark will determine how the data will partition automatically. With RDDs you can manipulate partitions automatically.

### Transformations:
- Narrow Transforms: 
  - Each input partition will contribute to only one output partition
- Wide Transforms: 
  - Input partitions contribute to many output partitions. Also referred to as a __shuffle__. When __Shuffles__ occur, Spark writes the results to disk.
- Pipelining:
  - If multiple filters are specified they'll all be performed in-memory. This can only occur one narrow transformations.

### Lazy Transformations:
- Lazy evaluation means that Spark will wait to execute the graph of computation instructions
- Transformations are built into a __plan__. This __plan__ is only executed when an __action__ is taken.
- Allows Spark to optimize the plan.
- __Predicate pushdown__ is an example of optimization where a filter that is applied at the end of the plan is executed earlier to reduce the amount of data being processed.

### Actions
- __Actions__ trigger Spark plans.
- Three kinds of actions
  - Actions to view data in the console
  - Actions to collect data to native objects in the respective language
  - Actions to write to output data sources
- __Plans__ can be monitored using the Spark UI

### Spark UI
- Job progress can be monitored through the Spark web UI. This can be accessed through __Port 4040__ of the driver node.
  - If running in local mode: _http://localhost:4040_

### Misc.
- Spark defaults to output 200 shuffle partitions. To change this, use the following: ```spark.conf.set("spark.sql.shuffle.partitions", "<number of partitions>")```

### Syntax  __ORGANIZE LATER__
- Create a SQL view on a dataframe: ```<dataframe>.createOrReplaceTempView("<view name>")```
- Load a csv into a dataframe: ```<dataframe> = spark.read.csv("<file path>")```
- Add an option: ```.option("<option>", "<args>")```
  - Infer Schema: ```.option("inferSchema", "true")```
  - Imply header: ```.option("header", "true")```
- Sort dataframe: ```<dataframe>.sort("<column>", "<sort options>)```
- Take a number of rows: ```<dataframe>.take(<number>)```