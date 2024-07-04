
# Real-Time Analytics Pipeline for Retail Data

This project sets up a Docker environment for a real-time analytics pipeline using Python, Polars, DuckDB, and Docker. The environment is designed to ingest retail data and provide a command-line interface (CLI) for querying the data using DuckDB.

### Dataset

The dataset used here is a transactional dataset which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. 
 <br>
Download the dataset here - [Online Retail](http://archive.ics.uci.edu/dataset/352/online+retail), and unzip it. 
<br>
To clean the raw dataset, download it from the website and load it into the data_cleaning.py script. 
<br>
For ease, the data set used in the container is a cleaned version of the `online_retail` dataset, loaded into a csv file. To reduce the size, the dataset is in its zip form, and the pipeline automatically unzips it.

### Dataset Content

The `online_retail.zip` file contains a CSV file with the following columns:

- `InvoiceNo`: Invoice number.
- `StockCode`: Product (item) code.
- `Description`: Product (item) name.
- `Quantity`: The quantity of each product (item) per transaction.
- `InvoiceDate`: Invoice date and time.
- `UnitPrice`: Unit price of each product (item).
- `CustomerID`: Customer number.
- `Country`: Country of the customer.

### Prerequisites

- Docker engine or Docker Desktop
- Git

### Project Structure

- `Dockerfile`: The Dockerfile to build the Docker image.
- `compose.yaml`: The Docker Compose file to manage services.
- `requirements.txt`: The Python dependencies required for the project.
- `data_ingestion.py`: The script for data ingestion.
- `online_retail.zip`: The zipped dataset for retail data.
- Other project-related files and scripts.

### Getting Started

1. **Clone the repository:**

   ```
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Build and start the Docker container:**

   ```
   docker compose up --build
   ```

   This will:
   - Build the Docker image based on the provided Dockerfile.
   - Install necessary dependencies.
   - Download and unzip the DuckDB CLI.
   - Unzip the retail dataset.
   - Run the data ingestion script.
   - Open the DuckDB CLI.

### Manually Running the DuckDB CLI

If the DuckDB CLI does not open automatically, you can manually start it by following these steps:

1. **Access the running container:**

   ```
   docker exec -it <container-id> /bin/bash
   ```

   Replace `<container-id>` with the ID of the running container, which you can find using:

   ```
   docker ps
   ```

2. **Run the DuckDB CLI:**

   ```
   ./duckdb /retail.db
   ```

   This will open the DuckDB CLI with the `retail.db` database loaded.

### Expected Output on Testing

After running the data ingestion script and opening the DuckDB CLI, you can query the `finance_data` table in the `retail.db` database. Below is an example of an expected output for a basic query:

1. **Select all data from the `finance_data` table:**

   ```
   SELECT * FROM finance_data;
   ```

   **Expected Output:**

   | StockCode | Total_cost_stock_sold | Average_cost_stock_sales | Min_sales | Max_sales |
   |-----------|------------------------|--------------------------|-----------|-----------|
   | 10002     | 10000.50               | 250.12                   | 10.00     | 500.00    |
   | 10003     | 8500.75                | 212.54                   | 5.00      | 400.00    |
   | ...       | ...                    | ...                      | ...       | ...       |


### Customization

- **Updating Dependencies:**
  
  If you need to update or add dependencies, modify the `requirements.txt` file and rebuild the Docker image:

  ```
  docker compose up --build
  ```

- **Data Ingestion:**
  
  Modify the `data_ingestion.py` script to change the data ingestion process according to your requirements.

### Troubleshooting

- **Container Issues:**

  If the container fails to start or the services do not work as expected, check the Docker logs:

  ```
  docker logs <container-id>
  ```

- **Dependency Issues:**

  Ensure all required dependencies are listed in the `requirements.txt` file.

### Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any enhancements or bug fixes.

---

Feel free to reach out for any questions or support. Happy coding!

    

