# Employee Data Management with Elasticsearch

## Overview

This project is a simple data management system that loads employee information from a CSV file and indexes it into an Elasticsearch database. It allows you to perform various operations such as creating, updating, and searching employee records. Elasticsearch is used for its robust indexing and searching capabilities, which makes it easy to retrieve information efficiently.

## Features

- Load employee data from a CSV file.
- Index data into Elasticsearch.
- Define mappings for various employee attributes.
- Supports searching and filtering employee information in Elasticsearch.
- Easy to extend and integrate into larger systems for managing employee records.

## Technologies Used

- Python
- Pandas
- Elasticsearch (Python Elasticsearch client)

## Requirements

- Python 3.x
- Elasticsearch (running at http://localhost:9200)
- Required Python libraries:
  - `pandas`
  - `elasticsearch`

## Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/your-username/employee-data-elasticsearch.git
   cd employee-data-elasticsearch

2. **Install Dependencies**

You can install the necessary Python libraries by running:
pip install pandas elasticsearch

3. **Set Up Elasticsearch**

Ensure Elasticsearch is running locally at http://localhost:9200. 
You can install Elasticsearch from Elasticsearch's official website.

4. Running the Notebook
Load the CSV Data

The notebook reads employee data from a CSV file named Employee_Sample_Data_1.csv. 
Make sure this file is available in the same directory.

Index the Data
The notebook will index the data into an Elasticsearch index called employee_data.
Search and Manage Data
Once the data is indexed, you can use Elasticsearch to search, filter, and manage the employee records.
Code Explanation
Connecting to Elasticsearch
The notebook connects to the Elasticsearch instance at http://localhost:9200.
python
Copy code
from elasticsearch import Elasticsearch
es = Elasticsearch("http://localhost:9200")
Loading Employee Data

The employee data is loaded from the CSV file using Pandas and cleaned.

python
Copy code
import pandas as pd
df = pd.read_csv("Employee_Sample_Data_1.csv", encoding="latin").dropna().reset_index()
Defining Mappings

Mappings are created to define the structure of the Elasticsearch index.

python
Copy code
mappings = {
    "properties": {
        "employee_id": {"type": "keyword"},
        "full_name": {"type": "text", "analyzer": "standard"},
        # More fields here...
    }
}
Indexing Data into Elasticsearch

Each employee record is indexed into Elasticsearch.

python
Copy code
for i, row in df.iterrows():
    doc = {
        "id": row["Employee ID"],
        "Full Name": row["Full Name"],
        # More fields here...
    }
    es.index(index="employee_data", id=i, document=doc)
License
This project is open-source and available under the MIT License.
