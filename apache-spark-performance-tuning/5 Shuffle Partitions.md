## Shuffle Partitions
Shuffling happens whenever there is wide transformation. Spark tries to get all the similiar data from different nodes.

![image](https://github.com/user-attachments/assets/93940604-54c9-49ea-9d6a-d415b5da3a6d)

P1, P2, P3, P4 - partitions  

**Shuffling operation**:  
```python
df.groupby(store_id).agg(sum)
```

### Why shuffling is important?
Default shuffle partitions is 200. Imagine there is 1000 core cluster, with these settings only 200 cores will be working and 800 cores will be idle.  
It results in:
- slow completion time
- underutilization of cluster 


### Example: data per shuffle partition is large
Default
```scala
spark.sql.shuffle.partitions = 200
```
Amount of shuffled data is 300 GB.

In cluster there are 5 executors with 4 cores, the total cores is 20.  
Shuffle paritions is 200.  

Size of data per shuffle partition = 300 x 1000 MB / 200 = 1.5 GB

**Optimal partition size is 1-200 MB**

Number of shuffle partition:  
(300 x 1000 MB) / 200 MB = 1500

When the data per shuffle partition is very large you should increase number of shuffle partition  

### Example: data per shuffle partition is small
