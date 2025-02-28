<h1 align="center">Hello, I'm <a href="https://github.com/sazhirom">George Romanov</a> 👋</h1>

<p align="center">
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExaGJuc2J1YjExMm9jdDF4bGhkaGF3ZGg0bXkyYzRvdDQ3c25qYXk3biZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/4k9BkIfSbgr2LTRB8P/giphy.gif" width="180"/>
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExdnFxY2hibGhhZHRoZGpoeTZocnhneWxjM2h0ZXFjNXVxYmQzd3k3OSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ySeD2PB1OfMSKFEheH/giphy.gif" width="180"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Data%20Engineer-FFD43B?style=for-the-badge&logo=python&logoColor=blue" alt="Data Engineer Badge">
  <img src="https://img.shields.io/badge/Business%20Analyst-323330?style=for-the-badge&logo=soundcharts&logoColor=white" alt="Business Analyst Badge">
</p>

---

## 📋 Table of Contents

- [🔥 Complex ETL Projects](#etl)
  - [💰 Betting Analyzer (*Python: BS4, Selenium, Pandas, NumPy → GoogleCloud → Airflow, Redis → Kafka → ClickHouse → Grafana)*](#betting)
  - [🎮 Steam Scraper (*Python: BS4, Selenium, Pandas, NumPy → AWS → PostgreSQL → Metabase)*](#steam-scraper)
- [📈 Smaller Projects](#small)
  - [📊 Dashboard - Key Performance Indicators for a Petrochemical Holding (*SQL - PowerBI*)](#dashboard-production)
  - [🏆 Kaggle Competition - Child Mind (*Python: Pandas, SNS, matplotlib, LGBM*)](#kaggle)
- [🎓 About Me](#about-section)
- [🛠️ Skills](#skills-section)
- [💼 Work Experience](#experience-section)
- [📬 Contacts](#contacts-section)

---
<br>
<br>

<a id="ETL"></a>
## 🔥 Complex ETL Projects
---
<a id="betting"></a>
### 💰 Betting Analyzer - Result here: [Grafana Dashboard](http://35.221.182.237:3000/public-dashboards/d10f4d4c98d44da3900a12b173f9a3bb)

---
![Project Diagram](https://raw.githubusercontent.com/sazhirom/images/refs/heads/main/mermaid-diagram-2025-01-08-082426.svg)

---
#### 🎯 Project Goal
A system that **synchronizes live odds from the three largest betting sites** and identifies the best betting opportunities.

#### 🔍 Challenges & Solutions
- **Website restrictions**: Platforms are protected from scraping and require authorization.  
- **Limited server resources**: The 1-2 GB RAM servers required **code optimization** and **efficient memory management**.  
- **Real-time data analysis**: Data must be **collected synchronously with random timing**—requiring a **coordinator and error handling system**.  
- **Optimizing ClickHouse for 2GB RAM**: ClickHouse is not designed for small instances, requiring fine-tuning for stability.  

#### 🔧 Implementation  
The system consists of **five servers**:
1. **Coordinator server**:
   - A **Python script** monitors scraper readiness, generates random parsing intervals, manages event triggers, and restarts instances when failures occur.  
   - **Redis** is used for fast data exchange.  
   - **Airflow** manages task scheduling and recovery.  
   - **Kafka Producer** sends data to the database server.  
   - A **Python processing script** matches events and selects the best betting odds.  
   - **Grafana dashboard** visualizes results from ClickHouse.  
2. **Three scraper servers**:
   - Collect live betting odds at specified intervals.  
   - Also scrape **pre-match** odds and match results.  
3. **Database server**:
   - **Kafka Receiver** for incoming data.  
   - **ClickHouse** to store and process betting data.  

#### 🛠️ Technologies  
- **Programming**: Python  
- **Database**: ClickHouse, PostgreSQL (for Airflow)  
- **Infrastructure**: Google Cloud, Airflow automation, Redis, Kafka  
- **Visualization**: Grafana  

---

## 📊 Link to Dashboard  
Updated **live** from **06:00 to 16:00 CET**:  
[Grafana Dashboard](http://35.221.182.237:3000/public-dashboards/d10f4d4c98d44da3900a12b173f9a3bb)  

---

### 🔥 **Project Functions & Technologies**

| **Function**         | **Description**                                  | **Technologies** |
|----------------------|--------------------------------------------------|------------------|
| [**Data Scraping**](https://github.com/sazhirom/ibet#ibet-scrape)  | Scraping data from three betting websites and storing in Redis. Also scrapes match results.  | Python, Selenium, BeautifulSoup, Pandas, regex |
| [**Data Processing**](https://github.com/sazhirom/ibet#ibet-merge)  | Aggregates data from Redis. Finds matching events via transliteration & custom functions. | Pandas, NumPy, regex |
| [**VNC Server**](https://github.com/sazhirom/ibet#ibet-VNC) | VNC setup for login/captcha bypass. | VNC |
| [**Redis**](https://github.com/sazhirom/ibet#ibet-redis)  | Redis configuration for data transfer.  | Redis |
| [**Kafka**](https://github.com/sazhirom/ibet#ibet-kafka) | Kafka setup using KRaft mode for data transfer to ClickHouse. | Kafka |
| [**ClickHouse**](https://github.com/sazhirom/ibet#ibet-clickhouse) | Running and configuring ClickHouse on a 4GB RAM server. | ClickHouse, SQL |
| [**PostgreSQL**](https://github.com/sazhirom/ibet#ibet-postgres) | Used for Airflow stability & metadata storage. | PostgreSQL |
| [**Airflow**](https://github.com/sazhirom/ibet#ibet-airflow) | Workflow automation (8 DAGs). | Airflow |
| [**GCP & Bash**](https://github.com/sazhirom/ibet#ibet-bash) | Cloud setup, IAM permissions, logging, and environment configuration. | Bash, GCP CLI |
| [**Grafana**](https://github.com/sazhirom/ibet#ibet-grafana) | Creating a live analytics dashboard. | Grafana, SQL |

---
<br>
<br><br>
<a id="steam-scraper"></a>

### 🎮 Steam Scraper - Result here: [Metabase Dashboard](http://47.129.223.184:3000/public/dashboard/1a51169a-8c3c-4d9e-8ee7-a508fb3f7539)

---
![Project Diagram](https://raw.githubusercontent.com/sazhirom/images/969a0f40bed959fac421447a24223250edea6b76/steam-diagram.svg)

---
#### 🎯 Project Goal
Automating the search for **the most profitable deals** on trading platforms **Market-CSGO, Buff, and C5Game**.  
The system **collects all buy and sell offers** from three sites and finds the best deals.

#### 🔍 Challenges & Solutions
- **Platform restrictions**: Websites are protected against scraping; Buff requires authentication; more than **40,000 items** are available.  
- **Limited resources**: The **1GB RAM server** requires **code optimization, reduced I/O operations, and efficient memory management**.  
- **Data analysis**: Price volatility and a large number of extreme values require considering **sales statistics and demand levels**.  

#### 🔧 Implementation
1. Generates a **list of potential deals** based on **price differences** between platforms.  
2. Collects **historical sales data** (prices and dates) for each item.  
3. Ranks recommendations using a **formula that considers profitability, data reliability, and potential selling speed**.  

#### 🛠️ Technologies
- **Programming**: Python  
- **Database**: PostgreSQL  
- **Infrastructure**: AWS, Bash automation, Docker testing & debugging  
- **Visualization**: Metabase  

#### 📊 Link to Dashboard
Available **08:00 - 20:00 CET**:  
[Metabase Dashboard](http://47.129.223.184:3000/public/dashboard/1a51169a-8c3c-4d9e-8ee7-a508fb3f7539)  

---

### 🔥 **Project Functions & Technologies**

| **Function**         | **Description**                                  | **Technologies** |
|----------------------|--------------------------------------------------|------------------|
| [**Data Scraping**](https://github.com/sazhirom/scraping#scraping-section)  | Collecting data from three websites and storing it as CSV.  | Python, Selenium, BeautifulSoup, Pandas, regex |
| [**Data Processing**](https://github.com/sazhirom/scraping#wrangling-section)  | Cleaning and analyzing data, identifying profitable deals, verifying sales history for the top 150 items, validating data, and generating final recommendations. | Pandas, NumPy, regex |
| [**SQL Database**](https://github.com/sazhirom/scraping/#SQL-section)  | Creating the database, connecting via a bastion server, storing data with psycopg2, and periodic record cleanup. | PostgreSQL, AWS, Python, psycopg2 |
| [**AWS Infrastructure**](https://github.com/sazhirom/scraping#AWS-section)  | Setting up VPC, EC2, RDS PostgreSQL, S3, CloudWatch, IAM, security groups, and service integrations. | AWS (VPC, EC2, S3, CloudWatch, IAM) |
| [**Docker**](https://github.com/sazhirom/scraping#Docker-section)  | Creating a container for running **Google Chrome** on EC2.  | Docker |
| [**Bash Automation**](https://github.com/sazhirom/scraping#bash-section)  | Automating EC2 processes with Bash scripts.  | Bash |
| [**Metabase Visualization**](https://github.com/sazhirom/scraping#Metabase-section)  | Connecting to the database via a bastion server, creating an interactive dashboard. | Metabase |

---
<br>
<br>

<a id="small"></a>
## 📈 Smaller projects

---

<a id="dashboard-production"></a>
### 📊 Dashboard - key production metrics of petrochemical holding  

#### 📊 Dashboard description  

This dashboard integrates data from three sources:  

1. **Actual Production** — extracted from SAP.  
2. **Initial Plan** — data as of the first day of the month.  
3. **Updated Plan** — data as of the current date.  

For six plants, plans are stored in six separate Excel files, while actual production data from SAP is saved in a seventh file.  

#### Dashboard Functionality

**Current Date**  
- **Displays actual production metrics.**  
- **Difference**: calculated as `Plan - Actual` and visualized in a graph.  

**End of Month**  
- **Total Actual Production**: displays data from the 1st of the month to the current date.  
- **Updated Plan**: includes projected data for the remaining days of the month.  
- **End-of-Month Difference**: shows changes in the plan made throughout the month.  

#### Benefits  
This dashboard allows users to:  
1. **Monitor actual production metrics.**  
2. **Quickly analyze updated forecasts** for key product categories by the end of the month.  
3. **Identify deviations from the initial plan** and investigate their causes.  

<details>
  <summary><strong>📜 Дэшборд</strong></summary>

<div align="center">
    <img src="https://raw.githubusercontent.com/sazhirom/images/main/DB1.PNG" alt="Внешний вид дэшборда" width="100%" />
    <img src="https://raw.githubusercontent.com/sazhirom/images/main/db2.PNG" alt="Внешний вид дэшборда" width="100%" />
    <img src="https://raw.githubusercontent.com/sazhirom/images/main/db3.PNG" alt="Внешний вид дэшборда" width="100%" />
</div>  
</details>

---  
---
<br>
<br>

<a id="kaggle"></a>
### 🏆 Kaggle competition - Child Mind - Pandas, SNS, matplotlib, LGBM 

**Objective**: Predict which children and teenagers may have problematic internet usage.  

**Data**: Anonymous survey data containing demographic, psychological, and behavioral information, helping to understand the relationship between various factors and susceptibility to problematic internet behavior.  

**Super Simple Description**:  
The dataset includes information on 4,000 children, covering their academic performance, physical education grades, weight/height, achievements in various sports metrics, BMI, and more. Additionally, for approximately 900 children, accelerometer data is available, which seems rather useless in my opinion (data is present for 29% of children, and in the test dataset, only 2 out of 30 cases—6%). Based on these characteristics, the task is to predict the SII level—a measure of how dependent a child is on the internet and how negatively it affects their life.  

**Idea**  
Analysts aim to predict SII—a target categorical variable. Instead, I attempted to predict PCIAT-TOTAL—the result of a questionnaire that determines SII. Unlike SII, PCIAT-TOTAL is not discrete and operates based on the following formula:  
1. From 0 to 20 points - 0 dependency category  
2. From 21 to 40 points - 1 dependency category, and so on.  
   Since this value is continuous rather than discrete like SII, the prediction should theoretically be more accurate.  

**Result**  
Becoming a data scientist isn't happening anytime soon for me. My result—0.38, while the top 1,000 scores range from 0.4 to 0.5.  
Kaggle notebook link: [https://www.kaggle.com/code/georgiiromanov/child-mind-final](https://www.kaggle.com/code/georgiiromanov/child-mind-final)  

<details>
  <summary><strong>📜 Код Kaggle</strong></summary>

```python
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.preprocessing import LabelEncoder
import numpy as np 
import pandas as pd 
os
from sklearn.impute import KNNImputer 

count = 0
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
        count +=1
        if count >= 15:
            break
    if count >= 15:
        break
        
data_train = pd.read_csv(r'/kaggle/input/child-mind-institute-problematic-internet-use/train.csv')
data_test = pd.read_csv('/kaggle/input/child-mind-institute-problematic-internet-use/test.csv')
data_train.head()

# Remove rows with null values in the target metric and plot the distribution
filtered_data = data_train[data_train['sii'].notna()].reset_index()

sns.countplot(data = filtered_data, x = 'sii')

plt.title('Sii Distribution')
plt.xlabel('Sii Value')
plt.ylabel('Count')
plt.show()

# Distribution by gender and age
sns.countplot(data = filtered_data, x = 'Basic_Demos-Age', hue = 'Basic_Demos-Sex' )

plt.title('Age/Sex Distribution')
plt.xlabel('Count')
plt.legend(['Male','Female'], title = 'Gender')
plt.show()

# Another distribution visualization using stacked columns
pivot_table = filtered_data.pivot_table(index = 'Basic_Demos-Age', columns = 'Basic_Demos-Sex', aggfunc = 'size', fill_value = 0)
pivot_table.head()

pivot_table.plot(kind = 'bar', stacked = True)
plt.title('Another visualization for clarity')
plt.legend(['Male', 'Female'], title ='Gender')
plt.tight_layout()
plt.show()

# Remove columns that are not in the test dataset, except for the target variable
columns_to_drop = [col for col in data_train.columns if col not in data_test.columns]
print(columns_to_drop)
columns_to_drop.remove('PCIAT-PCIAT_Total')
filtered_data.drop(columns = columns_to_drop, inplace = True)

# Plot missing values percentage for each column and choose a threshold of 35%
graph = filtered_data.isnull().sum().apply(lambda x: x/len(filtered_data['PCIAT-PCIAT_Total'])*100).sort_values(ascending = False)
graph.plot(kind = 'barh', figsize = (20,30))
plt.gca().yaxis.set_tick_params(labelsize=18, pad=5)
plt.tight_layout()
plt.gca().grid()
ticks = [x*5 for x in range(1,21)]
plt.gca().xaxis.set_ticks(ticks)

# Remove columns with more than 35% NaN values
indexes_to_delete = graph.index[graph > 35].tolist()
filtered_data.drop(columns = indexes_to_delete, inplace = True)

# Also remove ID columns as accelerometer data is not used
columns_to_drop_2 = ['index','id']
filtered_data.drop(columns = columns_to_drop_2, inplace = True)

# Convert categorical columns to numeric values (mainly seasons when tests were conducted)
column_to_label = filtered_data.select_dtypes(include = 'object').columns

labeled_data = filtered_data.copy()
label_coder = LabelEncoder()
for col in column_to_label:
    labeled_data[f'{col}'] = label_coder.fit_transform(labeled_data[f'{col}'])

# Build a heatmap in sns, analyze visually, choose a threshold of 70%, remove highly correlated columns (mostly body mass/composition metrics)
matrix = labeled_data.corr()
plt.figure(figsize=(40, 40))
sns.heatmap(matrix, annot=True, cmap='coolwarm', linewidths=0.5, fmt='.2f', vmin=-1, vmax=1)

limit = 0.7

drop_columns_3 = set()
for i in range(len(matrix.columns)):
    for j in range(i):
        if abs(matrix.iloc[i, j]) > limit:
            col = matrix.columns[i]
            drop_columns_3.add(col)

drop_columns_3.discard('PCIAT-PCIAT_Total')

cleaned_data = labeled_data.drop(columns=drop_columns_3)

imputers = {}
imputed_dataset = {}

imputers = KNNImputer(n_neighbors=17)
    
imputed_dataset = pd.DataFrame(
    imputers.fit_transform(cleaned_data), 
    columns=cleaned_data.columns)

# Create the model and tune hyperparameters
from sklearn.model_selection import train_test_split, RandomizedSearchCV
from sklearn.metrics import mean_squared_error
import lightgbm as lgb
import pandas as pd
import numpy as np

SEED = 42

X = imputed_dataset.drop(columns=['PCIAT-PCIAT_Total'])
y = imputed_dataset['PCIAT-PCIAT_Total']

# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=SEED)

# Parameter grid for hyperparameter tuning
param_grid = {
    'learning_rate': [0.05],  
    'max_depth': [4, 6],
    'num_leaves': [200, 300, 400, 500],
    'min_data_in_leaf': [10],  
    'feature_fraction': [0.4, 0.5, 0.6],
    'bagging_fraction': [0.9],
    'bagging_freq': [3],  
    'lambda_l1': [1, 2, 3, 4, 4.735462555910575],
    'lambda_l2': [3e-05, 3e-04, 4.735028557007343e-06],
}

model = lgb.LGBMRegressor(random_state=42, verbose=-1)

search = RandomizedSearchCV(
    estimator=model,
    param_distributions=param_grid,
    n_iter=10,
    scoring='neg_mean_squared_error',
    cv=5,
    random_state=42,
    verbose=1
)

search.fit(X_train, y_train)
print("Best Parameters:", search.best_params_)
print(f"Best RMSE: {(-search.best_score_)**0.5:.4f}")

best_model = search.best_estimator_
columns_final = list(imputed_dataset.columns)
columns_final.remove('PCIAT-PCIAT_Total')
X_test = data_test[columns_final]

# Transform categorical columns
column_to_label_2 = X_test.select_dtypes(include='object').columns
for col in column_to_label_2:
    X_test.loc[:, col] = label_coder.fit_transform(X_test[col])

X_final_test = pd.DataFrame(
    imputers.fit_transform(X_test), 
    columns=X_test.columns)

y_pred = best_model.predict(X_final_test)
X_final_test['PCIAT_TOTAL'] = y_pred
X_final_test['sii'] = np.where(X_final_test['PCIAT_TOTAL']<21,0,
                              np.where(X_final_test['PCIAT_TOTAL']<31,1,2))
X_final_test['id'] = data_test['id']
X_final_test[['id','sii']].to_csv('submission.csv', index=False, na_rep='null')


```

</details>

---  
---
<br>
<br>

<a id="about-section"></a>

## 💼 Work Experience & Achievements

- 🏢 **11 years of experience in the petrochemical industry**  
  - **Supply chain management, business analytics, and data analytics**.  
- 🎓 **MBA Graduate from RANEPA**  
  - Accredited by **AMBA** and **AACSB**.  
- 🌍 **Internship in Germany (Deutsche Management Akademie Niedersachsen, Hansa-Flex)**  
- 📊 **IELTS 8.0 (C1 English)**  
- 📜 **IBM Data Engineer Professional Certificate**  
- ☁️ **AWS Certified Cloud Practitioner**  

---
<br>
<a id="skills-section"></a>

## 🛠️ Skills

### 👨‍💻 Programming & Scripting
- **Python (Pandas, NumPy, Matplotlib, Seaborn, Selenium, BeautifulSoup, regex)**  
- **SQL (PostgreSQL, ClickHouse, MySQL)**  

### 📊 Data Visualization Tools
- **Power BI**  
- **Metabase**  
- **Grafana**  

### ☁️ Cloud & Other Technologies
- **AWS Cloud Practitioner**  
- **Docker**  
- **Airflow, Kafka, Redis**  

---
<br>
<a id="contacts-section"></a>

## 📬 Contact Me

<p align="left">
  <a href="https://t.me/poi8lkj" target="_blank">
    <img src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram">
  </a>
  <a href="https://www.linkedin.com/in/georgii-romanov-3a62a526a/" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  </a>
</p>
