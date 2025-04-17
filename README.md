<h1 align="center">Hello, I'm <a href="https://github.com/sazhirom">George Romanov</a> 👋</h1>

<p align="center">
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExaGJuc2J1YjExMm9jdDF4bGhkaGF3ZGg0bXkyYzRvdDQ3c25qYXk3biZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/4k9BkIfSbgr2LTRB8P/giphy.gif" width="180"/>
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExdnFxY2hibGhhZHRoZGpoeTZocnhneWxjM2h0ZXFjNXVxYmQzd3k3OSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ySeD2PB1OfMSKFEheH/giphy.gif" width="180"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Business%20Analyst-323330?style=for-the-badge&logo=soundcharts&logoColor=white" alt="Business Analyst Badge">
  <img src="https://img.shields.io/badge/ETL%20Developer-4B8BBE?style=for-the-badge&logo=docker&logoColor=white" alt="ETL Developer Badge"> 
</p>

---

## 📋 Table of Contents

- [📊 Dashboards (*Tableau + Grafana)*](#dashboards)
- [🔥 Complex ETL Projects](#etl)
  - [💰 Betting Analyzer (*Python: BS4, Selenium, Pandas, NumPy → GoogleCloud → Airflow, Redis → Kafka → ClickHouse → Grafana)*](#betting)
  - [🎮 Steam Scraper (*Python: BS4, Selenium, Pandas, NumPy → AWS → PostgreSQL → Metabase)*](#steam-scraper)
- [📈 Smaller Projects](#small)
  - [🏆 Kaggle Competition - Child Mind (*Python: Pandas, SNS, matplotlib, LGBM*)](#kaggle)
  - [📚 World Global Values survey analysis (*Python: Pandas - Tableau*)](#WVS)
- [🛠️ Skills](#skills-section)
- [💼 Work Experience](#experience-section)
- [📬 Contacts](#contacts-section)

---
<br>
<br>

<a id="Dashboards"></a>
## 📊 Dashboards

Main Showcase for Dashboards is here - [**Tableau Profile**](https://public.tableau.com/app/profile/george.romanov/vizzes)
<br>
<br>  


| **Dashboard**         | **Description**                                  | **Link** |
|----------------------|--------------------------------------------------|------------------|
| ![**Hotel Survey / Linker Diagram**](https://github.com/sazhirom/Tableau/blob/main/hotel.png?raw=true)  | Dashboard featuring a Linker Diagram, custom filters, and highlight actions. Based on synthetic data generated with Python Faker.  | [**Link to Tableau Public**](https://public.tableau.com/app/profile/george.romanov/viz/HotelSurveyLinkerExample/Dashboard1) |
| ![**Purchasing Power: Europe Comparison**](https://github.com/sazhirom/Tableau/blob/main/costliving.png?raw=true)  | Not overly complex, but illustrates a histogram and a map linked with the histogram, highlight actions, and the ability to customize maps. Data from Numbeo.  | [**Link to Tableau Public**](https://public.tableau.com/app/profile/george.romanov/viz/CostoflivingEurope/Dashboard1) |
| ![**KPI Dashboard**](https://github.com/sazhirom/Tableau/blob/main/mini.png?raw=true)  | Allows dynamic month-to-month KPI comparisons and year-over-year running sum analysis across all key metrics. The most complex feature involves advanced formulas with fixed views to display a running sum of percentage values, illustrating the cumulative profit ratio. | [**Link to Tableau Public**](https://public.tableau.com/app/profile/george.romanov/viz/MinimalisticDashboardwithKPI/Dashboard1) |
| ![**Green Energy**](https://github.com/sazhirom/Tableau/blob/main/green.png?raw=true)  | Compares the share of green energy in the top 10 GDP countries, with the ability to view both absolute and relative values. | [**Link to Tableau Public**](https://public.tableau.com/app/profile/george.romanov/viz/GlobalGreenEnergyTrends/Dashboard1) |
| ![**Betting Analyzer ETL**](https://github.com/sazhirom/Tableau/blob/main/grafana.PNG?raw=true)  | Grafana dashboard for that [ETL_project](#betting). Featuring conditinal colour formatiing for different values, bunch of optimization to reduce server load and a lot of SQL. | [View the Grafana Dashboard](http://138.2.100.167:3000/public-dashboards/5c64055a2d0a432aafe2d29dae512883) |


---
<br>
<br>

<a id="ETL"></a>

## 🔥 Complex ETL Projects
---
<a id="betting"></a>

### 💰 Betting Analyzer  
📈 [View the Grafana Dashboard](http://138.2.100.167:3000/public-dashboards/5c64055a2d0a432aafe2d29dae512883)



---

#### 🎯 Project Goal
A system that **synchronizes live odds from the three largest betting sites** and identifies the best betting opportunities.

#### 🔍 Challenges & Solutions
- **Website restrictions**: Platforms are protected from scraping and require authorization.  
- **Limited server resources**: The 1-2 GB RAM servers required **code optimization** and **efficient memory management**.  
- **Real-time data analysis**: Data must be **collected synchronously with random timing**—requiring a **coordinator and error handling system**.  
- **Optimizing ClickHouse for 4GB RAM**: ClickHouse is not designed for small instances, requiring fine-tuning for stability.  

---
#### 🔀 Project Data Flow
![Project DataFlow](https://raw.githubusercontent.com/sazhirom/images/refs/heads/main/diagram3.svg)  

#### 🛠️ Project Data Architecture
![Project Diagram](https://raw.githubusercontent.com/sazhirom/images/refs/heads/main/mermaid-diagram-2025-01-08-082426.svg)

---
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
[Grafana Dashboard](http://138.2.100.167:3000/public-dashboards/5c64055a2d0a432aafe2d29dae512883)  

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

<a id="kaggle"></a>
### 🏆 Kaggle competition - Child Mind - Pandas, SNS, matplotlib, LGBM 

**Objective**: Predict which children and teenagers may have problematic internet usage.  

**Data**: Anonymous survey data containing demographic, psychological, and behavioral information, helping to understand the relationship between various factors and susceptibility to problematic internet behavior.  
 
**Result**  

 Kaggle notebook link: [https://www.kaggle.com/code/georgiiromanov/child-mind-final](https://www.kaggle.com/code/georgiiromanov/child-mind-final) 
 
--- 
<br>

<a id="WVS"></a>
### 📚 World Global Values survey analysis - Python: Pandas, Tableau

**Objective**: Analyze a large-scale survey to uncover meaningful insights.

**Data**: 270,000 survey responses from the World Values Survey (Wave 7, 2017–2022).

**Idea**: I aimed to identify the most significant generational gaps within a very specific demographic: middle-aged Europeans. I compared two closely matched groups — individuals aged 25–34 and those aged 55–64. Both groups share many similarities: most have children, stable jobs, and rely on the Internet as their primary source of news. This makes the differences between them especially interesting.

<details>
  <summary>Python code</summary>
  
```python
import pandas as pd
import re

df = pd.read_csv(r'C:\Users\user\Desktop\tableau\world global quest\wvs.csv')


#only European countries
df = df[df["B_COUNTRY"].isin([
    8, 20, 40, 112, 56, 70, 100, 191, 203, 208, 233, 246, 250, 276,
    300, 348, 352, 372, 380, 428, 438, 440, 442, 470, 498, 492, 499,
    807, 528, 578, 616, 620, 642, 674, 688, 703, 705, 724, 752, 756,
    804, 826, 336
])]

# define cols with age and questions for analysis
cols_age = [col for col in df.columns if '003' in col][0]
cols_q = [col for col in df.columns if re.match(r'Q\d+', col)]

print(cols_q)

df1 = df.melt(id_vars = cols_age, value_vars = cols_q, value_name = "Answer",var_name = 'Question')
df1=df1[df1['Answer']>-1]

df1 = df1.groupby(list(df1.columns)).size().reset_index(name='count')
df1.rename(columns = {'X003R':'Age Group'},inplace = True)

df1 = df1[df1['Age Group']>0]
df1.head()

df1['total'] = df1.groupby(['Age Group', 'Question'])['count'].transform('sum')
df1 = df1[df1['Age Group'].isin([2,5])]

df1['ratio'] = df1['count']/df1['total']


df2 = df1
df_final = df1.merge(df2, on = ['Question','Answer'], how = 'inner')
df_final.head()

index_to_drop = df_final[df_final['total_x'] == df_final['total_y']].index

df = df_final.drop(index = index_to_drop)

df.head()

df['delta'] = round(df['ratio_y'] - df['ratio_x'],5)

df_positive = df.sort_values(by = 'delta', ascending = False).head(100)
df_positive.head()

df_negative = df.sort_values(by = 'delta', ascending = True).head(100)
df_negative.head()

df_negative.to_csv(r'C:\Users\user\Desktop\tableau\world global quest\negative.csv')

df1 = df.melt(id_vars = cols_age, value_vars = cols_q, value_name = "Answer",var_name = 'Question')
df1=df1[df1['Answer']>-1]

df1 = df1.groupby(list(df1.columns)).size().reset_index(name='count')
df1.rename(columns = {'X003R':'Age Group'},inplace = True)
df1 = df1[df1['Age Group']>0]
df1.head()

df1['total'] = df1.groupby(['Age Group', 'Question'])['count'].transform('sum')
df1 = df1[df1['Age Group'].isin([2,5])]
df1['ratio'] = df1['count']/df1['total']

df1.head()
df1.to_csv(r'C:\Users\user\Desktop\tableau\world global values\all_answers.csv')
```
</details>

<details>
  <summary>Tableau Dashboard, not the best work but anyway</summary>
  [**Dashboard**](https://github.com/sazhirom/Tableau/blob/main/values.png?raw=true)
</details>
---
<br>
<br>

<a id="experience-section"></a>

## 💼 Work Experience & Achievements

- 🏢 **11 years of experience in the petrochemical industry**  
  - **Supply chain management, business analytics, and data analytics**.  
- 🎓 **MBA Graduate from RANEPA**  
  - Accredited by **AMBA** and **AACSB**.  
- 🌍 **Internship in Germany (Deutsche Management Akademie Niedersachsen, Hansa-Flex)**  
- 📊 **IELTS 8.0 (C1 English)**  
- 📜 **IBM Data Engineer Professional Certificate**  
---
<br>
<a id="skills-section"></a>

## 🛠️ Skills

### 👨‍💻 Programming & Scripting
- **Python (Pandas, NumPy, Matplotlib, Seaborn, Selenium, BeautifulSoup, regex)**  
- **SQL (PostgreSQL, ClickHouse, BigQuery)**
- **Bash**

### 📊 Data Visualization Tools
- **Tableau**
- **Power BI**  
- **Metabase**  
- **Grafana**  

### ☁️ Cloud & Other Technologies
- **AWS, GCP**  
- **Docker**  
- **Airflow**  

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
