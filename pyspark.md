# Running PySpark on IPython Notebook


### Download Spark

Here is Spark [page](http://spark.apache.org/). You can go to download
[page](http://spark.apache.org/downloads.html) in order to download Spark.

- Choose Spark release: `1.6.0`
- Choose a package type: `Pre-built for Hadoop 2.6 or later`
- Choose a download type: `Direct Download`

Then click download Spark link, it will download Spark (size around 276 MB compressed).
If you want to download to instance, just copy the link and use `wget` to download.


### Run PySpark on IPython notebook

Assume we download Spark into Desktop directory. We first have to path to Spark environment path
into `.bash_profile`, something like the following line

```bash
export SPARK_HOME=~/Desktop/spark-1.6.0-bin-hadoop2.6
```

Simple way to run `pyspark` is running `.bin/pyspark` (if you are in `spark-1.6.0-bin-hadoop2.6` folder).
However, we typically run `pyspark` on IPython notebook. And it will look something like

```bash
IPYTHON_OPTS="notebook" ~/Desktop/spark-1.6.0-bin-hadoop2.6/bin/pyspark
```

We can put a lot of configuration before we run Spark to prevent Memory error and all other things.
See more in [Spark configuration](http://spark.apache.org/docs/latest/configuration.html).
Here is a sample script to run Spark on EC2 cluster.

This is for `r3.8xlarge` instance

```bash
IPYTHON_OPTS="notebook --ip=* --no-browser" ~/spark-1.6.0-bin-hadoop2.6/bin/pyspark --master local[32] --driver-memory 64g --executor-memory 64g --conf spark.driver.maxResultSize=0
```

This is for `r3.xlarge` instance

```bash
IPYTHON_OPTS="notebook --ip=* --no-browser" ~/spark-1.6.0-bin-hadoop2.6/bin/pyspark --master local[4] --driver-memory 32g --executor-memory 32g --conf spark.driver.maxResultSize=0
```
