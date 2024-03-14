# Data Processing Pipeline

This repository contains Jupyter notebooks that form an end-to-end data processing pipeline, structured into three layers: Bronze, Silver, and Gold.

## Pipeline Architecture

Below is a high-level overview of the data processing pipeline:

![Data Lake Architecture](images/architect.jpeg "Data Lake Architecture")

## Bronze Layer (`bronze.ipynb`)

The `bronze.ipynb` notebook is responsible for initial data ingestion and preliminary cleaning.

### Key Steps:

- **Initialize Spark**: Set up the Spark session to process the data.
- **Define Schemas**: Specify the schema for each of the source files to ensure data consistency.
- **Read Files**: Load data from CSV and Excel files into Spark DataFrames.
  - NSPL21_AUG_2023_UK.csv and NSP21CL_AUG23_UK_LU.csv files have first 2000 rows of their original files due to GitHub 100 MB file size limitation. Please use original files from their websites.
- **Nulls and Duplicates**: Count and handle null values and duplicates within each column.
- **Clean Post Codes**: Perform specific cleaning operations for columns containing postal codes.
- **Save to Silver Layer**: Persist the cleaned DataFrames to the Silver layer for further processing.

## Silver Layer (`silver.ipynb`)

In the `silver.ipynb` notebook, further transformations and joins are performed on the cleaned data.

### Key Steps:

- **Initialize Spark**: Reinstantiate the Spark session.
- **Read Files**: Bring in the cleaned data from the Bronze layer.
- **Join Tables**: Execute joins on DataFrames to combine data according to business logic.
- **Save Processed Data**: Output the transformed data, ready for the Gold layer.

## Gold Layer (`gold.ipynb`)

The `gold.ipynb` notebook finalizes the data transformation process and prepares data for analysis or reporting.

### Key Steps:

- **Initialize Spark**: Ensure the Spark session is active.
- **Read Table**: Load the processed data from the Silver layer.

### Distribution of Area Names

![Distribution of Area Names](images/plot1.png "Distribution of Area Names")

This bar chart shows the distribution of various area names in the dataset, highlighting how frequently each name appears.

### Unique Organizations per District

![Unique Organizations per District](images/plot2.png "Unique Organizations per District")

This horizontal bar chart represents the number of unique organizations present in each district, providing insights into regional diversity.

## Getting Started

To run these notebooks, you will need an environment capable of executing Jupyter notebooks with Apache Spark. Refer to the installation guides for Apache Spark and Jupyter if you haven't set up your environment.

### Prerequisites

- Apache Spark
- Python
- Jupyter Notebook or JupyterLab
- Required Python libraries (`pyspark`, `pandas`, etc.)

### Installation

1. Clone the repository to your local machine.
2. Ensure you have the prerequisites installed.
3. Launch Jupyter Notebook or JupyterLab.
4. Navigate to the notebook you wish to run and open it.
5. Execute the cells in order to process the data through each layer.

---



## Schedule Management (`schedule.ipynb`)

The `schedule.ipynb` notebook is designed to orchestrate the data processing workflow, ensuring smooth transitions and automated task management across the Bronze, Silver, and Gold layers.

### Key Features:

- **Task Scheduling**: Automates the execution of the `bronze.ipynb`, `silver.ipynb`, and `gold.ipynb` notebooks in the correct sequence.
- **Dependency Management**: Ensures that each layer's prerequisites are met before proceeding to the next stage.
- **Notification System**: Optionally, sends alerts or updates regarding the pipeline's status, completion, or any errors encountered.
- **Logging**: Maintains a detailed log of each task's execution status, facilitating troubleshooting and audit trails.

### Usage Instructions:

1. Review and adjust the scheduling parameters as necessary to fit your project's timeline and resource availability.
2. Execute the notebook to initiate the automated workflow.
3. Monitor the progress through the logs or notification system.

This notebook is essential for maintaining a seamless and efficient pipeline, reducing manual oversight, and ensuring data is processed accurately and timely.

## Author

- Mansur Can
