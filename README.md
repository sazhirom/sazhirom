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

- [📊 Dashboards](#dashboards)
- [🔥 Complex ETL Projects](#etl)
  - [💰 Betting Analyzer (*Python: BS4, Selenium, Pandas, NumPy → GoogleCloud → Airflow, Redis → Kafka → ClickHouse → Grafana)*](#betting)
  - [🎮 Steam Scraper (*Python: BS4, Selenium, Pandas, NumPy → AWS → PostgreSQL → Metabase)*](#steam-scraper)
- [📈 Smaller Projects](#small)
  - [🏆 Kaggle Competition - Child Mind (*Python: Pandas, SNS, matplotlib, LGBM*)](#kaggle)
- [🎓 About Me](#about-section)
- [🛠️ Skills](#skills-section)
- [💼 Work Experience](#experience-section)
- [📬 Contacts](#contacts-section)

---
<br>
<br>

<a id="Dashboards"></a>
## 📊 Dashboards

Main Showcase for Dashboards is here - ![**Tableau Profile**](https://public.tableau.com/app/profile/george.romanov/vizzes)
<br>
| **Dashboard**         | **Description**                                  | **Link** |
|----------------------|--------------------------------------------------|------------------|
| ![**Hotel Survey/Linker diagram**](https://github.com/sazhirom/Tableau/blob/main/hotel.png?raw=true)  | Dashboard featuring Linker Diagram, custom filters, highlight actions. Based on synthetic data generated in Python Faker  | [**Link Tableau Public**](https://public.tableau.com/app/profile/george.romanov/viz/HotelSurveyLinkerExample/Dashboard1) |

---
<br>
<br>
<a id="ETL"></a>
## 🔥 Complex ETL Projects
---
<a id="betting"></a>
### 💰 Betting Analyzer - Result here: ![Grafana Dashboard](http://138.2.100.167:3000/public-dashboards/5c64055a2d0a432aafe2d29dae512883)

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
 
**Result**  

 Kaggle notebook link: [https://www.kaggle.com/code/georgiiromanov/child-mind-final](https://www.kaggle.com/code/georgiiromanov/child-mind-final) 
 
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
