[back to home](../README.md)


# Download Spark

Here is Spark [page](http://spark.apache.org/). You can go to download
[page](http://spark.apache.org/downloads.html) in order to download Spark.
Here is what I choose when I download Spark version `1.6.0`

- Choose Spark release: `1.6.0`
- Choose a package type: `Pre-built for Hadoop 2.6 or later`
- Choose a download type: `Direct Download`

Then click download Spark link, it will download Spark (size around 276 MB compressed).
If you want to download to instance, just copy the link (right click and copy)
and use `wget` to download.

### Run PySpark with IPython notebook

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
PYSPARK_DRIVER_PYTHON=ipython PYSPARK_DRIVER_PYTHON_OPTS="notebook --ip=* --no-browser" ~/spark-1.6.0-bin-hadoop2.6/bin/pyspark --master local[32] --driver-memory 64g --executor-memory 64g --conf spark.driver.maxResultSize=0
```

This is for `r3.xlarge` instance

```bash
PYSPARK_DRIVER_PYTHON=ipython PYSPARK_DRIVER_PYTHON_OPTS="notebook --ip=* --no-browser" ~/spark-1.6.0-bin-hadoop2.6/bin/pyspark --master local[4] --driver-memory 32g --executor-memory 32g --conf spark.driver.maxResultSize=0
```


### Run Spark Snippet

If we're going to run small example snippet in case you're submitting the job on
computer cluster. First, we can create python file name `spark_example.py`.

```python
import os
from pyspark import SparkConf, SparkContext

# Configure the environment                                                     
if 'SPARK_HOME' not in os.environ:
    os.environ['SPARK_HOME'] = '/home/ubuntu/spark-1.6.0-bin-hadoop2.6'

conf = SparkConf().setAppName('pubmed_open_access').setMaster('local[32]')
sc = SparkContext(conf=conf)

if __name__ == '__main__':
    ls = range(100)
    ls_rdd = sc.parallelize(ls, numSlices=1000)
    ls_out = ls_rdd.map(lambda x: x+1).collect()
    print 'output!: ', ls_out
```

Here is the bash script to run the code above.

```bash
~/spark-1.6.0-bin-hadoop2.6/bin/pyspark --master local[8] --driver-memory 12g --executor-memory 12g spark_example.py
```
