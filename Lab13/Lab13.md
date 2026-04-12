# CST8921 Lab 13:  ETL vs ELT
## Elizabeth Kaganovsky (040956095)

## Part 1. Setup
To prevent configuration errors, this lab was done on a VM. The environment is activated, pyspark is installed and confirmed, requirements are saved and the necessary files/directories are created.
![](/Lab13/Screenshots/Step_1.png)

## Part 2. Create Project Files
The contents of etl_elt_lab.py are filled in with vi (headless interface).
![](/Lab13/Screenshots/Step_2.png)

## Part 3. Run the Script
The script is run and `orders_raw` and `orders_clean` are populated.
![](/Lab13/Screenshots/Step_3_1.png)
![](/Lab13/Screenshots/Step_3_2.png)
![](/Lab13/Screenshots/Step_3_3.png)

## Part 4. Discussion Questions

### Both pipelines produced the same final output. What is the key architectural difference between them? 
Extract, Transform, Load: 
    - Data is first extracted from the source
    - Data is then transformed in a seperate engine
    - Data is finally loaded into a storage (such as a file or a data warehouse, in this case, `orders clean`)
ETL pipelines are preferrable for smaller datasets or those requiring some kind of cleaning before being stored.

Extract, Load, Transform:
    - Data is first extracted from the source
    - Data is then loaded into a storage (in this case, `orders_raw`)
    - Data is finally transformed
ELT pipelines are preferrable for larger, unstructured datasets.

### The ELT pipeline preserved the raw data in orders_raw. Why is this valuable when business requirements change? 
Preservation of raw data allows for later return to that data if necessary. Data that is not considered important at the moment will still be saved, and if useful for future analysis, would not have been discarded. Conversely, an ETL pipeline discards some amount of data in the transformation process and would not allow for future querying.

### The ELT pipeline built a category_summary mart as a second SQL step without touching the ETL path. How does this demonstrate ELT's flexibility? 
Creating this as an intermediate step allows for additional pipelines to query the data from the warehouse, rather than loading it from the source. This reduces dependency on the machine hosting the original data source or the in-memory storage of a pipeline, simplifying the processes of future data operations.

### If this dataset were 100 GB on a distributed Spark cluster, which approach would likely perform better and why? 
ELT would be far preferrable for large datasets, since ETL pipelines are limited by the capabilities of the transformation server, creating a significant bottleneck between data extraction and data loading into storage. Comparatively, an ELT pipeline puts the computationally-heavy transform step at the end, where it is unlikely to cause throttling. When the destination is a cloud data warehouse, Massively Parallel Processing (MPP) can be leveraged for in-place data transformation, reducing the dependence on a transformation server.

### Identify one real-world scenario where you would still prefer ETL over ELT. 
Situations where concerns arise in the cloud are prime candidates for ETL rather than ELT. For example, a company dealing with private medical data is required to follow regional laws on storing PII, such as enforcing masking on data stored long term. In this case, the data must be transformed before being loaded into a warehouse.