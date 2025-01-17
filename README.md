# Stock Price Prediction 

Personalized Financial Advisor Using Large Language Models. 

### Introduction 

Stock price prediction is crucial for investors, but the volatile nature of markets makes it challenging. Traditional methods rely on technical and fundamental analysis, while machine learning now enables more accurate predictions using historical data and indicators. This project develops a deep learning model to predict the next day's closing price based on last 60 day’s closing price for 24 major companies. Using LSTM networks for temporal patterns and Representation Learning with an embedding layer for stock-specific characteristics, the model combines technical indicators(RSI, SMA20, MACD) with stock identifiers for robust predictions. The project evaluates the model's performance, highlights limitations, and proposes enhancements, contributing to data-driven financial forecasting for traders, investors, and researchers. 

### Project Objectives
#### Problem Addressed
1. Financial markets are complex, making stock trend prediction challenging for investors.
2. Stock market being volatile, it becomes crucial for market dealers or investors to maximize their profits

#### Proposed Solution
1. Utilize AI models to analyze historical data and predict future stock prices.
2. Incorporate 60-day historical trends to deermine the 61st day price.

#### Impact
1. Simplifies investment decision making and provides data-driven insights for strategic financial planning.
2. Demonstrates the practical application of machine learning in finance.

### Dataset Preparation
1. Alpha Vantage is a provider of financial market data APIs that offer real-time and historical data for various financial instruments such as stock prices, technical indicators, sector performance, exchange rates, and more.
2. Stock data for 23 equities was collected using Alpha Vantage API.
3. This data included timestamp, volume, open price, high price, close price and rsi.
4. New features such as SMA20 and MACD were created. These engineered features along with others were fed into the model. 

### Dataset Preprocessing
#### Normalize X_price:
Features like price and indicators have different ranges. Normalizing them to a common range (e.g., 0 to 1) ensures the model trains effectively. MinMaxScaler was used to normalize the data.

#### Encode X_stock:
Stock IDs are categorical, and the model cannot process them directly. These IDs are converted into numeric form for embedding. 

#### Split the Dataset:
The data is split into training and test sets using train_test_split to ensure that the model is evaluated on unseen data.

![image](https://github.com/user-attachments/assets/03d19b8e-a52a-4b5f-81b9-dad3860b6d3e)

### Model Architecture
#### Sequential Data Processing:
The price_input is passed into LSTM layers:
  1. LSTM (Long Short-Term Memory): Processes sequential data, capturing temporal dependencies in stock price trends and indicators over the 60-day period.
  2. Outputs a reduced representation summarizing the sequence.

#### Stock ID Processing: 
The stock_input is passed into an Embedding layer:
  1. Embedding Layer: Converts each stock ID into a dense, low-dimensional vector representation.
  2. Captures relationships between stocks. Stocks with similar IDs may learn similar patterns.

#### Feature Combination:
The outputs from the LSTM and the embedding layer are concatenated:
  1. Combines sequential features with stock-specific characteristics.

#### Fully Connected Layers:
The concatenated features are passed through Dense (fully connected) layers:
  1. Learns the relationship between sequential patterns, stock ID, and the target variable (61st day's price).
  2. Reduces the combined feature vector step by step to a single output.

![image](https://github.com/user-attachments/assets/fe11cdbb-669d-48fe-9388-8a8c71d12f85)

### Project Outcome

![image](https://github.com/user-attachments/assets/2376d6b0-7a79-4bb9-b469-e9406b42662a)

### Model Performance
1. Results are promising when comparing the actual and predicted prices.
2. Predicted prices are similar to actual prices and are close with minimum deviations.
3. Highest actual prices are visible in equity named GS, UNH and MSFT and the model has still perfomed well. 
4. The model has given accurate results even for lower stock value prices such as WBA, VZ, INTC, DOW, CSCO and KO. 

![image](https://github.com/user-attachments/assets/e7b07b94-8339-4004-abf9-b060ecf0f8d2)

### Research Findings 
#### Novel Representation Learning Approach 
Introduced stock-specific embeddings to encode unique behaviors and relationships, enabling the model to differentiate stocks and generalize effectively. 

#### Integration of Temporal and Stock-Specific Features 
Combined LSTM outputs with stock embeddings to merge sequential trends with stock-specific nuances, creating a robust predictive framework. 

#### Discovery: Transformer Limitations 
Found that transformer models underperformed compared to LSTMs, likely due to transformers' difficulty capturing fine-grained temporal dependencies in sequential financial data. 

### Implications of Results 
#### Positive Outcomes: 
1. Accurate Predictions: LSTMs capture trends and volatility effectively; embeddings enable stock-specific predictions. 
2. Scalability: Handles multiple stocks via embeddings, learning relationships between similar stocks. 
3. Comprehensive Features: Combines technical indicators and temporal patterns for robust predictions. 
4. Low MAE: Strong performance for stable stocks (e.g., JNJ: 1.10, PG: 1.08). 
5. Adaptable Design: Modular architecture supports new features and alternative models like transformers. 

#### Identified Limitations: 
1. Performance Variability: Higher errors for volatile stocks (e.g., INTC: 3.82, UNH: 4.04). 
2. Historical Data Dependence: Lacks adaptation to unforeseen events like news or economic shifts. 
3. Simplified Context: Embeddings miss macroeconomic and inter-stock relationships. 
4. Short-Term Focus: A 60-day window overlooks long-term trends. 
5. Non-Price Factors Omitted: No integration of external drivers like earnings reports or sentiment. 

#### Future Research: 
1. Advanced Models: Use transfer learning and pre-trained large models. 
2. External Data: Incorporate macroeconomic indicators and sentiment analysis. 
3. Dynamic Embeddings: Adapt embeddings to stock performance.
4. Longer Windows: Capture medium and long-term trends efficiently.
5. Portfolio Insights: Apply predictions for optimized portfolio management. 
