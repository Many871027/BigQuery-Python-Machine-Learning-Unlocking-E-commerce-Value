# BigQuery, Python, & Machine Learning: Unlocking E-commerce Value                               

This project analyzes customer behavior and predicts Customer Lifetime Value (CLV) using the Olist Brazilian E-commerce public dataset.  The project utilizes a combination of data from Kaggle, data warehousing with Google BigQuery, data manipulation with pandas, machine learning with scikit-learn, and visualization with matplotlib and Plotly.

**Project Goals:**

*   Download and prepare the Olist E-commerce dataset.
*   Upload the data to Google BigQuery for efficient data warehousing and querying.
*   Perform Exploratory Data Analysis (EDA) using SQL queries within BigQuery and visualize key trends.
*   Segment customers using K-Means clustering based on their purchasing behavior (CLV and Average Order Value).
*   Build and evaluate regression models (Linear Regression, Random Forest, and a tuned XGBoost model) to predict CLV.
*   Provide actionable insights and recommendations based on the customer segmentation and CLV predictions.

**Dataset:**

The dataset used in this project is the Olist Brazilian E-commerce dataset, publicly available on Kaggle: [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce).  It contains information about orders, products, customers, and reviews from 2016 to 2018.  The dataset consists of multiple CSV files, which are loaded, processed, and merged for analysis.

**Tools and Technologies:**

*   **Programming Language:** Python
*   **Data Manipulation:** pandas
*   **Machine Learning:** scikit-learn
*   **Visualization:** matplotlib, seaborn, Plotly
*   **Data Warehousing:** Google BigQuery
*   **Cloud Services:** Google Cloud Platform (GCP)
*  **Kaggle API:** kagglehub

**Project Structure:**

1.  **Data Download (Kaggle):** Downloads the dataset from Kaggle using the `kagglehub` library. Includes error handling for potential download issues.
2.  **Data Loading (Pandas):** Loads the downloaded CSV files into pandas DataFrames.  Handles potential encoding issues.
3.  **BigQuery Setup:** Sets up the connection to Google BigQuery using service account credentials stored in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable.  Creates the necessary dataset within BigQuery.
4.  **Upload Data to BigQuery:** Uploads the pandas DataFrames to BigQuery tables, replacing existing tables if necessary.
5.  **Data Analysis (SQL Queries and Visualizations):** Performs EDA using SQL queries directly within BigQuery.  This section includes:
    *   Monthly Sales Trend Analysis
    *   Top 10 Product Categories Analysis
    *   Sales by Payment Type Analysis
    *   Top Products Trends in 2017 Analysis
    *   Sales by State Analysis and Visualization
    *   Visualizations using matplotlib and Plotly.
6.  **Data Preparation for CLV and Clustering:** Merges the necessary DataFrames, calculates CLV (using a simplified formula: `CLV = total_purchases * AOV`), and prepares the data for customer segmentation.
7.  **Customer Segmentation (K-Means Clustering):**
    *   Handles outliers using Winsorizing.
    *   Scales the data using `StandardScaler`.
    *   Determines the optimal number of clusters using the Elbow Method and Silhouette Score.
    *   Performs K-Means clustering using the chosen number of clusters.
    *   Visualizes the clusters using an enhanced scatter plot with annotations.
    *   Provides detailed cluster analysis and interpretation, including summary statistics and business recommendations for each cluster.
    *  Analyzes and visualizes distributions within clusters (product categories, customer cities).
8. **CLV Prediction:**
    *  **Feature Engineering and Aggregation:** This stage uses a complex SQL query within BigQuery to create aggregated customer-level features, including order count, total spent, average review score, payment type counts, customer lifespan, and a `clv_proxy`.
    * **Data Preparation:** Selects relevant features, handles missing values, scales the data, and splits it into training and testing sets.
    * **Model Training:** Trains three regression models: Linear Regression, Random Forest, and a tuned XGBoost model. The XGBoost model is tuned using `GridSearchCV` to find the best hyperparameters.
    * **Model Evaluation:** Evaluates the models using MSE, RMSE, R-squared, and MAE.
    * **Model Comparison:** Compares the performance of the models using interactive Plotly bar charts and a 3D scatter plot.
    * **Save Model:** Save the best trained model.
    * **Load Model:** Load saved model
    * **Comparate Prediction vs Real:** Create dataframe, predict with trainned model and show some graphics to compare and analize prediction vs real data.
9.  **Model Evaluation and Comparison:**  Loads the trained XGBoost model, makes predictions on the test set, and compares the predicted CLV values to the actual values using:
    * Scatter Plot (Predicted vs. Actual)
    * Time Series Plot (for a subset of customers)
    * Distribution Plot (Histograms of predicted and actual CLV)
    * Residual Plot
    * Head first 5 rows

**How to Run the Code:**

1.  **Install Required Libraries:**

    ```bash
    pip install pandas matplotlib seaborn scikit-learn google-cloud-bigquery pandas-gbq kagglehub plotly joblib
    ```
2.  **Set up Google Cloud Credentials:**
    *   Create a service account in your Google Cloud project.
    *   Download the service account key file (JSON).
    *   Set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable to the path of your service account key file.  For example, in your `.bashrc` or `.zshrc` file:

        ```bash
        export GOOGLE_APPLICATION_CREDENTIALS="/path/to/your/service_account_key.json"
        ```
        Or, set it directly in your Python script (less secure, not recommended for production):
        ```python
        os.environ['GOOGLE_APPLICATION_CREDENTIALS'] = "/path/to/your/service_account_key.json"
        ```
3.  **Set up Kaggle API Credentials:**
    *   Create a Kaggle API token (kaggle.json) from your Kaggle account settings.
    * The `kagglehub` library should automatically detect your Kaggle credentials if they are placed in the standard location (`~/.kaggle/kaggle.json` on Linux/macOS, `C:\Users\<Windows-username>\.kaggle\kaggle.json` on Windows). If not found automatically you will be prompted.
4.  **Replace Placeholders:**
    *   Replace `"tactical-hydra-440201-p5"` with your actual Google Cloud project ID.
    *   Adjust `gross_profit_margin` in the `Parameters` section to reflect your business's actual gross profit margin.
    *   Ensure any hypothetical filepaths are correct.
5.  **Run the Script:** Execute the Python script.

**Key Improvements and Considerations:**

*   **BigQuery Integration:** The code heavily leverages BigQuery for data warehousing and preprocessing, making it efficient for large datasets.
*   **Error Handling:** Includes error handling for data loading and BigQuery operations.
*   **Clear Methodology:** The code is well-structured and follows a clear data science workflow.
*   **Detailed Cluster Analysis:**  Includes in-depth analysis of the customer segments, with recommendations for each.
*   **Hyperparameter Tuning:** Uses `GridSearchCV` to find the best hyperparameters for the XGBoost model, leading to improved performance.
*   **Comprehensive Evaluation:** Evaluates the models using multiple metrics and provides visualizations for comparison.
*   **Reproducibility:** Uses `random_state` for reproducibility in clustering and model training.
* **Save and load model:** Use of `joblib` library for save and load best trainned model.
* **Compare real and prediction:** Use load model, and prepare new data for predict, use prediction and show some graphics for compare.
