[back to home](../README.md)

## Index columns of PySpark dataframe

Here are 3 related Stack Overflow posts

- [Enumerate without converting to Pandas](http://stackoverflow.com/questions/32760888/pyspark-dataframes-way-to-enumerate-without-converting-to-pandas)
- [Access PySpark by index](http://stackoverflow.com/questions/39544796/pyspark-spark-how-to-select-last-row-and-also-how-to-access-pyspark-dataframe-b)
- [Add new column to spark dataframe](http://stackoverflow.com/questions/33681487/how-do-i-add-a-new-column-to-spark-data-frame-pyspark)


First, we'll create sample dataframe.

```python
from pyspark.sql import Row
from pyspark.sql.functions import col
from pyspark.sql.types import StructType, StructField, LongType

df = sqlContext.createDataFrame([Row(a=1, b=2), Row(a=3, b=4), Row(a=4, b=6), Row(a=5, b=9)])
df.show() # example dataframe
```

Now, we can grab columns from the dataframe and add index column to it.

```python
row = Row(df.columns)
row_with_index = Row(df.columns.append("index"))

schema  = StructType(
    df.schema.fields[:] + [StructField("index", LongType(), False)])

df_indexed = (df.rdd # Extract rdd
    .zipWithIndex() # Add index
    .map(lambda ri: row_with_index(*list(ri[0]) + [ri[1]])) # Map to rows
    .toDF(schema)) # It will work without schema but will be more expensive
```

Then to select index, we can use `where`, as following

```python
indexes = [2,3]
df_indexed.where(col('index').isin(indexes)).show()
```


## Adding new column to Spark DataFrame

There are multiple way to add new column to Spark DataFrame. One technique is to
create user-defined function (UDF) and apply to another column.

- [Adding new column using UDF](http://stackoverflow.com/questions/33681487/how-do-i-add-a-new-column-to-spark-data-frame-pyspark)
