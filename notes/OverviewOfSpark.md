## Overview of Apache Spark
- Objective of this overview is to introduce and make you familiar about Apache Spark, as quick as possible
- It is meant to help those, who are in deciding process, to decide if Spark is for your purpose and should you invest more time in knowing about it.
- It can also help you, if you are impatient in knowing about Spark

### What is Apache Spark
A general-purpose cluster computing system, i.e., distributed computing environment, over a fault tolerant cluster of computing nodes.

Spark comes with an DAG execution engine with bunch of tools to support the cluster computing (execution) and monitoring same

### Framework services
Below are the primary services offered by spark, which you should know about

- Cluster computing
	- Job Scheduling
	- Directed acyclic graph execution (DAG Execution)
- Resilient Distributed Dataset (RDD)
- Spark Streaming
- Spark SQL, DataFrames and Datasets Guide
- Structured data processing
- GraphX
- MLib

### Version & Support details
| Current version | Languages supported                        | Operating systems supported |
|:----------------|:-------------------------------------------|:----------------------------|
| 2.4             | JAVA (8+)                                  |                             |
|                 | Scala (2.11) - Python (2.7+/3.4) - R (3.1) | Linux                       |
|                 | Python (2.7+/3.4) - R (3.1)                | Mac OS                      |
|                 | R (3.1)                                    | Windows                     |
|                 |                                            |                             |


### Cluster computing
- Cluster computing is what you use to run your applications as Spark applications
- Spark comes with high level APIs, you **submit** your your applications as jobs, which Spark schedules on its cluster before running. 
- Spark applications run as independent sets of processes on a cluster, coordinated by the SparkContext object in your main program (called the driver program).
- The components of Spark is as below
	![Apache Spark Components](https://spark.apache.org/docs/latest/img/cluster-overview.png "Spark components")
- From the image shown the **Task** is where your application runs, spark sends your applications to the executors, which run on cluster nodes, these nodes can be provided by any cluster provider (MESOS, Kubernetes, Hadoop, Standalone)
- Each driver program has a web UI, typically on port 4040, that displays information about running tasks, executors, and storage usage
- Spark gives control over resource allocation both across applications (at the level of the cluster manager) and within applications (if multiple computations are happening on the same SparkContext)
- Please refer [here](https://spark.apache.org/docs/latest/cluster-overview.html) to read more about the cluster mode of Spark

### Resilient Distributed Dataset (RDD)
- One of the core abstraction provided by Spark is RDD, the **R**esilient **D**istributed **D**ataset (RDD), which is a fault-tolerant collection of data elements that can be operated on in parallel.

- Other abstraction by Spark is **variables**, which are shared or broadcast, depending on you want to share data across tasks or between tasks. broadcast variables are cached on all nodes. Spark automatically broadcasts variables which are needed in computations across nodes. 

- We can taken any collection object from the program and parallelize it over the cluster, you can decide how many slices of the data you want to cut in parallelizing the data set, Spark does this automatically, however the API provides options for you to decide the number of partitions. 

- Choose RDD if you want to operate on the data in parallel and you are not concerned about the order of the data and/or processing

- RDD is immutable, distributed, and fault-tolerant.

- RDD can be in memory of the program or in external data store (HDFS, Filesystem, Cassandra, S3...)

- Using RDD will make your spark application stateful

- We can run `transformations` and `accumulation` type of operations on RDD, transformations are lazy and only computed when action required to return the computed data

- RDDs can be re-distributed over partitions using expensive operations known as **shuffle**

- Please refer [here](https://spark.apache.org/docs/latest/rdd-programming-guide.html#overview) to know more about RDD

### Spark Streaming
- Another important service by Spark is the streaming, which helps in processing of live data from stream sources like Kafka, Flume, Kinesis, Websockets or any other streaming source, these sources can be **Basic** (filesystem, sockets...) or **Advanced** (Kafka, Kinesis...)

- Internally spark creates batches of data knowns **Discretized stream** or **DStream**, these are nothing but sequence of RDD at time intervals
	![Spark Stream processing](https://spark.apache.org/docs/latest/img/streaming-flow.png "Spark Stream Processing") 
              
- DStreams supports applying operations, such as **Transformation**, **Windowed computations** and **Output**
	![Windowed computations](https://spark.apache.org/docs/latest/img/streaming-dstream-window.png "Windowed computations")

- Output operations allow DStream’s data to be pushed out to external systems like a database or a file system

- One of the fault tolerant feature of DStreams is **Checkpointing** to fault tolerant storage system, which helps in being resilient to failures. Checkpointing is useful in stateful transformations and in recovering from failures

- Please refer [here](https://spark.apache.org/docs/latest/streaming-programming-guide.html#overview) to know more about Stream processing

### Spark SQL, DataFrames and Datasets Guide
If you know the data structure of both the data and the computation being performed on it, then Spark SQL helps in querying the data as DataSets/DataFrame

- Spark SQL can also be uses in Spark shell based interactions

- DataSet is a distributed collection of data, is strongly typed and has operators like map, filter, flatMap

- DataFrame is a set of named column, each named column is a dataset, hence it can be compared to how a Table is structured in RDBMS

### Structured data processing

### GraphX
GraphX is one of very useful or powerful feature of Spark in processing for useful data insights, which often requires complex computations and having to do it in relation with a topology of data

Is a Property Graph, which is an extension of RDD to form abstraction of a graph, which is a directed multigraph with properties attached to each vertex and edge, it helps in graphs and graph-parallel computation.

- Property Graph is immutable, hence any changes to the values or structure of the graph produces a new graph

- Graph can be built by defining Vertexes and Edges, vertexes and edges are nothing but named collection of RDD

- Graphs are distributed and fault tolerant, similar to RDD

- Graph has similar operators as RDDs, and many Graph operators, like joinGrpah,subgraph and many core Graph Algorithm 

- Graph is supported with Pregel APIs for iterative algorithms, which helps computing state of a vertices basis its neighbors, you can process iteratively until a fixed point node is found

- Pregel (a portmanteu of the words Parallel, Graph, and Google) is a data flow paradigm and system for large-scale graph processing created at Google to solve problems that are hard or expensive to solve using only the MapReduce framework

- Graph also has triplets, which represents edge and has information about vertices and edge

### Support for Apache Parquet
Apache Parquet is a columnar storage available to data processing frameworks

