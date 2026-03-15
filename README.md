# Customer Segmentation using RFM Analysis and K-Means Clustering

## Project Overview

This project performs customer segmentation on an e-commerce transaction dataset using RFM (Recency, Frequency, Monetary) analysis combined with K-Means clustering. The goal is to identify distinct customer groups based on their purchasing behavior, which can help businesses tailor marketing strategies and improve customer relationship management.

The project was developed in Google Colab as a data science learning exercise, focusing on practical application of unsupervised machine learning techniques for customer analytics.

## Dataset Description

The project uses the **Online Retail Dataset**, which contains approximately **540,000 transactions** from an e-commerce platform. The dataset includes the following columns:

- **InvoiceNo**: Unique invoice number for each transaction
- **StockCode**: Product code
- **Description**: Product description
- **Quantity**: Number of items purchased
- **InvoiceDate**: Date and time of the transaction
- **UnitPrice**: Price per unit of the product
- **CustomerID**: Unique identifier for each customer
- **Country**: Country where the transaction occurred

## Project Workflow

The analysis follows a structured data science pipeline:

1. **Data Loading**
   - Import the dataset into the analysis environment

2. **Data Cleaning**
   - Remove rows with missing `CustomerID` values
   - Remove cancelled invoices (identified by `InvoiceNo` starting with 'C')
   - Remove transactions with negative `Quantity` values
   - Remove transactions with zero `UnitPrice` values

3. **Feature Engineering**
   - Calculate `TotalPrice` = `Quantity` × `UnitPrice` for each transaction

4. **RFM Analysis**
   - **Recency**: Calculate the number of days since each customer's last purchase
   - **Frequency**: Count the total number of transactions per customer
   - **Monetary**: Sum the total spending (`TotalPrice`) per customer

5. **Feature Scaling**
   - Apply `StandardScaler` to normalize RFM features for clustering

6. **Optimal Cluster Selection**
   - Use the Elbow Method to determine the optimal number of clusters

7. **Customer Segmentation**
   - Apply K-Means clustering with k=4 to segment customers

8. **Cluster Analysis**
   - Analyze and interpret the characteristics of each customer segment

9. **Visualization**
   - Use Principal Component Analysis (PCA) to visualize customer segments in 2D space

## Technologies Used

- **Python**: Core programming language
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computations
- **Scikit-learn**: Machine learning algorithms (K-Means, StandardScaler, PCA)
- **Matplotlib**: Data visualization
- **Seaborn**: Statistical data visualization

## Machine Learning Method

### RFM Analysis
RFM analysis is a customer segmentation technique that evaluates:
- **Recency (R)**: How recently a customer made a purchase
- **Frequency (F)**: How often a customer makes purchases
- **Monetary (M)**: How much money a customer spends

These three metrics provide a comprehensive view of customer value and engagement.

### K-Means Clustering
K-Means is an unsupervised machine learning algorithm that partitions customers into k clusters based on their RFM scores. The algorithm:
- Groups customers with similar purchasing behaviors together
- Minimizes within-cluster variance
- Enables identification of distinct customer segments

The optimal number of clusters (k=4) was determined using the Elbow Method, which evaluates the within-cluster sum of squares (WCSS) for different values of k.

## Results

The K-Means clustering algorithm successfully identified **4 distinct customer segments** based on RFM characteristics:

1. **Champions**: High recency, frequency, and monetary value - most valuable customers
2. **Loyal Customers**: Regular purchasers with good frequency and monetary value
3. **At Risk**: Customers with declining recency who may need re-engagement
4. **Lost Customers**: Low recency, frequency, and monetary value - inactive customers

Each segment exhibits distinct behavioral patterns that can inform targeted marketing strategies:
- Champions may benefit from loyalty programs and premium offers
- At Risk customers may need win-back campaigns
- Lost customers may require reactivation strategies

## Visualization

The project includes visualizations to better understand the customer segments:

- **Elbow Method Plot**: Shows the optimal number of clusters by plotting WCSS against k values
- **PCA Visualization**: 2D scatter plot of customer segments using Principal Component Analysis, showing how different segments are distributed in reduced-dimensional space
- **RFM Distribution Plots**: Histograms and box plots showing the distribution of Recency, Frequency, and Monetary values across segments

## How to Run the Project

### Prerequisites
- Google Colab account (or Jupyter Notebook environment)
- Python 3.x
- Required libraries: pandas, numpy, scikit-learn, matplotlib, seaborn

### Steps

1. **Open the notebook in Google Colab**
   ```python
   # Upload the notebook file to Google Colab
   ```

2. **Upload the dataset**
   - Ensure the Online Retail Dataset is available in your Colab environment
   - Update the file path in the data loading section if needed

3. **Install required libraries** (if not already installed)
   ```python
   !pip install pandas numpy scikit-learn matplotlib seaborn
   ```

4. **Run all cells sequentially**
   - Execute cells in order from top to bottom
   - The notebook will perform data cleaning, RFM analysis, clustering, and visualization

5. **Review results**
   - Examine the cluster analysis output
   - Review visualizations to understand customer segments

### Note
Make sure to adjust file paths and parameters according to your specific dataset location and requirements.

## Future Improvements

Potential enhancements to this project include:

- **Dynamic Cluster Selection**: Implement automated methods (e.g., Silhouette Score) for optimal cluster selection
- **Advanced Clustering Algorithms**: Experiment with DBSCAN, Hierarchical Clustering, or Gaussian Mixture Models
- **Feature Engineering**: Incorporate additional features such as product categories, seasonality, or customer demographics
- **Time-based Analysis**: Perform temporal analysis to track how customer segments evolve over time
- **Business Recommendations**: Develop actionable marketing strategies for each identified segment
- **Model Evaluation**: Add quantitative metrics to evaluate clustering quality
- **Interactive Dashboards**: Create interactive visualizations using Plotly or Tableau
- **Deployment**: Convert the analysis into a production-ready pipeline for real-time customer segmentation

---

**Note**: This project is intended for educational purposes and demonstrates fundamental data science techniques for customer segmentation analysis.
