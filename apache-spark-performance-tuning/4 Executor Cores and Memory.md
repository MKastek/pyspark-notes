## Executor Cores and Memory

Example of node (machine in the cluster) - during **spark-submit** we decide how many executors will be created and what will be allocation of cpu and memory:
- 3 executors (5 cores, 6 GB RAM)
![image](https://github.com/user-attachments/assets/6c6109c1-bca0-4a46-8294-0b44c9e5ca4b)

Number of executors, cores and memory should be optimal.

Leave out: 1 core and 1 GB RAM for OS/Hadoop/Yarn in each node.

### Fat executors  
Fat executors are executors which ocupies large portion of resources in node. For example one executor can use all resources. 
1 node -> 1 executor

#### Advantages - Fat executors   
- **Increased Parallelism**  
With more cores, fat executors can run more tasks in parallel. It is good for cases where:  
- [x] tasks require significant amount of data to be loaded in memory
- [x] managing many executors is a concern

- **Enhanced Data Locality**  
With fewer, large executors, the chances of data being processed on the node where it is stored increases - enhancing data locality. This reduces network traffic improving overall application speed

#### Disadvantages - Fat executors  
- **Under utilisation**   
Fat executor can lead to inefficient use of resources if all cores or memory are not utilised.

- **Fault Tolerance**  
Failure of a single executor has a bigger impact - because each executor is handling a large portion of data.

### Thin executors
Thise executors occupy minimal portion of resources from the node. 
1 core -> 1 executor
RAM on node / cores -> memory per executor 

#### Advantages - Thin executors  
- **Increased Parallelism**  
There are more executors handling smaller tasks. This is beneficial when tasks are lightweight.

- **Fault Tolerance**  
One executor with fauilure is easier to recover - small unit of work is done in one executor.

#### Disadvantages - Thin executors  
- **High Network Traffic**  
Thin executors may increase network traffic because each executor has a small memory and data has to be distributed across more executors for processing.

- **Reduced Data Locality**  
Data are spread accros multiple nodex - low data locality.

