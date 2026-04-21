# clarity_notebook
Notebook that ingests data from different files of three providers. 
It merges the result into a dataframe that follows a predifined schema.

# Target
This notebook should process these files and produce a unified view of the data.
The final result should be a data structure that allows the data science team to access all information for a given movie easily.


# Files
Contains data files from three different providers.
	.csv
	.json
	
# Model Schema
All these data files are imported into a Dataframe which must follow this model schema
model_schema = T.StructType([
    T.StructField("title", T.StringType(), True),
    T.StructField("year", T.IntegerType(), True),
    T.StructField("critic_score_pct", T.DoubleType(), True),
    T.StructField("top_critic_score", T.DoubleType(), True),
    T.StructField("total_critic_reviews", T.LongType(),True),
    T.StructField("audience_avg_score", T.DoubleType(), True),
    T.StructField("total_audience_ratings", T.LongType(), True),
    T.StructField("domestic_gross_usd", T.LongType(), True),
    T.StructField("international_gross_usd", T.LongType(), True),
    T.StructField("production_budget_usd", T.LongType(), True),
    T.StructField("marketing_spend_usd", T.LongType(), True)
])

# Read - Extract / Transform
The three providers classes inherit from a BaseProvider class which acts as a "Contract"
Providers must implement extract and transform functions
That way, in case of a new provider being added, just add a new class that implements the BaseProvider

# Provider's Schema
Each provider has its own schema following the file structure that's being ingested.
In case of having to modify any schema, just head to that cell.

# Data frames are merged into a unified one
Dataframes are combined (unionByName)
In case of conflicts (coalesce accross rows) a "_order" priority is applied so the first provider wins or remains.

# Unified dataframe
The unified dataframe can be then used in a Temporary View or saved to a Delta Table


# Orchestration
Orchestrate this notebook:
	1- Job scheduler
	2- Using an external tool such as Apache Airflow
	3- Databricks, Fabric DataFlow Gen2, etc..
