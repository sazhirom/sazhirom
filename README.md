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
- [📈 Smaller Projects](#small)
  - [🏆 Kaggle Competition - Child Mind (*Python: Pandas, SNS, matplotlib, LGBM*)](#kaggle)
  - [📚 World Global Values survey analysis (*Python: Pandas - Tableau*)](#WVS)
  - [🔁 Airflow - Dynamic Dag (*Airflow, Redis*)](#Airflow)
  - [🧠 Sports Odds Modeling (*CatBoost, ClickHouse*)](#Catboost)
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
| ![**Marketing / Funnel Diagram**](https://github.com/sazhirom/Tableau/blob/main/marketing.png?raw=true)  | Marketing Funnel, custom shapes and colours, scatter plots, custom list-based filters, dynamic sets, a lot of conditional formatting and so on.   | [**Link to Tableau Public**](https://public.tableau.com/app/profile/george.romanov/viz/MarketingDashboard_17453783792250/Dashboard1) |
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
  <summary>Tableau Dashboard (not my best work, but still worth sharing)</summary>
  
![Dashboard](https://github.com/sazhirom/Tableau/blob/main/values.png?raw=true)

</details>

--- 
<br>

<a id="Airflow"></a>
### 🔁 Airflow - Dynamic dags
This is part of the legacy code from the ETL betting project.
The idea was simple: if a scraper failed, it would set the corresponding Redis variable to 0.
For example, if scraping from olimpbet.ru failed, the olimpbet variable in Redis would be set to 0.

Then, an Airflow DAG would check these variables every 3 minutes, restart the necessary DAGs if there is 0, and reset the variable to 1 after restarting.

The code is below.
(I eventually removed this part from the main project — it turned out to be easier to just refresh every page every 3 minutes rather than checking whether it needs refreshing.)

<details>
<summary>Dag code</summary>
  
```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from airflow.utils.dates import days_ago
from airflow.operators.trigger_dagrun import TriggerDagRunOperator
from airflow.providers.redis.hooks.redis import RedisHook
from airflow.decorators import dag, task
from datetime import datetime, timedelta
import time

default_args = {
    'owner': 'airflow',
    'retries': 0,
    'start_date': days_ago(1)
}

@dag(
    dag_id="monitor",
    description="Global monitoring DAG",
    schedule="*/3 12-21 * * *", 
    catchup=False,
    start_date=days_ago(1),
    default_args=default_args,
)
def global_dag():
    @task
    def process():
        redis_hook = RedisHook(redis_conn_id="redis")
        redis_client = redis_hook.get_conn()
        current_time = datetime.now().strftime("%H:%M:%S")
        print(f"Checking Redis at {current_time}")
        
        trigger_lists = []
        
        try:
            olimp = redis_client.get("olimp") or b"1"
            pinn = redis_client.get("pinn") or b"1"
            pari = redis_client.get("pari") or b"1"
            
            olimp_val = int(olimp)
            pinn_val = int(pinn)
            pari_val = int(pari)
            
            if olimp_val * pinn_val * pari_val == 0:
                print('Triggering restarts')
                
               
                trigger_lists.append({
                    "trigger_dag_id": "restart_coordinator",
                    "task_id": "trigger_restart_coordinator"
                })
                
                if olimp_val == 0:
                    trigger_lists.append({
                        "trigger_dag_id": "restart_olimp",
                        "task_id": "trigger_restart_olimp"
                    })
                    redis_client.setex("olimp", 600, 1)
                    
                if pari_val == 0:
                    trigger_lists.append({
                        "trigger_dag_id": "restart_pari",
                        "task_id": "trigger_restart_pari"
                    })
                    redis_client.setex("pari", 600, 1)
                    
                if pinn_val == 0:
                    trigger_lists.append({
                        "trigger_dag_id": "restart_pinn",
                        "task_id": "trigger_restart_pinn"
                    })
                    redis_client.setex("pinn", 600, 1)
            else:
                print('All systems operational')
                
        except Exception as e:
            print(f"Redis error: {e}")
            # Consider failing the task here if required
            # raise AirflowException(f"Redis error: {e}")
        
        return trigger_lists

    # Get list of DAGs to trigger from the process task
    trigger_configs = process()

    # Create dynamically mapped TriggerDagRunOperator tasks
    TriggerDagRunOperator.partial(
        task_id="trigger_dag_run",
        wait_for_completion=False
    ).expand_kwargs(trigger_configs)

global_dag_instance = global_dag()
```
</details>

---
<br>

<a id="Catboost"></a>
### 🧠 Sports Odds Modeling (*CatBoost, ClickHouse*)
This project uses historical match odds and results to train a machine learning model that predicts whether a placed bet was successful. The data is pulled from a ClickHouse database, cleaned and enriched with custom features such as odds ratios and team roles (favorite vs underdog). A CatBoost classifier is then trained to identify patterns and estimate bet outcomes, helping to evaluate profitability strategies based on historical data.

<details>
<summary>Catboost code</summary>
  
```python
import clickhouse_connect
import pandas as pd
import matplotlib.pyplot as plt
import shap
import numpy as np
from scipy.stats import skellam
from scipy.optimize import brentq
import math
from catboost import CatBoostClassifier, Pool
from sklearn.model_selection import train_test_split
from sklearn.metrics import log_loss, accuracy_score


# Подключение к ClickHouse
client = clickhouse_connect.get_client(
**************************************
)

# SQL-запрос
query = "SELECT * FROM prematch WHERE timestamp BETWEEN NOW() - INTERVAL '130 days' AND NOW()"


# Выполнение запроса и загрузка в DataFrame
prematch = client.query_df(query)

query = "SELECT * FROM results WHERE date BETWEEN NOW() - INTERVAL '130 days' AND NOW()"

# Выполнение запроса и загрузка в DataFrame
results = client.query_df(query)

prematch = prematch[(~prematch['1'].isna()) & (~prematch['2'].isna())]

prematch['date'] = prematch['timestamp'].dt.date
prematch.drop_duplicates(subset = ['event','date'],inplace = True)
prematch.head()

results['date'] = pd.to_datetime(results['date']).dt.date
results.drop_duplicates(subset = ['event','date'],inplace = True)

df = pd.merge(prematch,results, how = 'inner', on = ['event','date'])

df['has_draw'] = df['X'].notna()  # True — 3 исхода, False — 2 исхода

df = df[df['has_draw']]
df = df.reset_index(drop = True)
df.drop(columns = ['has_draw'], inplace = True)
df = df[(df['F'].notna()) & (df['F1'].notna())]
cols_to_check = ["X", "1", "2",'category_x']
df = df[(df[cols_to_check] != 0).all(axis=1) & df[cols_to_check].notna().all(axis=1)]

# Разбиваем подкатегорию
subcategory_parts = df['subcategory_x'].str.split('.')
max_parts = subcategory_parts.map(len).max()

# Формируем датафрейм из подкатегорий
subcategory_df = subcategory_parts.apply(
    lambda x: pd.Series(x + [None] * (max_parts - len(x)))
)
subcategory_df.columns = [f'subcat_{i}' for i in range(max_parts)]

# Объединяем с исходным df
df = df.join(subcategory_df)
df.drop(
    columns=[
        'category_y', 'subcategory_y', 'f1', 'f2', 'total', 'subcategory_x',
        'score1', 'score2','subcat_3', 'subcat_4', 'subcat_5', 'subcat_6', 'timestamp', 'date'
    ],
    inplace=True,
    errors='ignore'
)

df['odds_A'] = df['1']
df['odds_B'] = df['2']

# Определим команду-андердога
df['underdog_team'] = df.apply(lambda row: row['team1'] if row['odds_A'] > row['odds_B'] else row['team2'], axis=1)

# Также можно сохранить фаворита, если нужно
df['favorite_team'] = df.apply(lambda row: row['team1'] if row['odds_A'] < row['odds_B'] else row['team2'], axis=1)

# Вычислим полезные числовые признаки
df['odds_underdog'] = df[['odds_A', 'odds_B']].max(axis=1)  # чем выше кэф — тем меньше шанс, значит андердог
df['odds_favorite'] = df[['odds_A', 'odds_B']].min(axis=1)
df['odds_ratio'] = df['odds_favorite'] / df['odds_underdog']
df['odds_diff'] = df['odds_favorite'] - df['odds_underdog']

df['odds_underdog'] = 1 / df['odds_underdog']
df['odds_favorite'] = 1 / df['odds_favorite']

df['target'] = (
    ((df['stavka'] == '1') & (df['1'].astype(float) > df['2'].astype(float))) | 
    ((df['stavka'] == '2') & (df['2'].astype(float) > df['1'].astype(float)))
)
df['1'] = 1 / df['1'].astype(float)
df['X'] = 1 / df['X'].astype(float)
df['2'] = 1 / df['2'].astype(float)

df = df[~df['underdog_team'].str.contains('тайм|матч|угловые|хозяева|гости|матчей', case=False, na=False)]
df = df[~df['favorite_team'].str.contains('тайм|матч|угловые|хозяева|гости|матчей', case=False, na=False)]

cols_to_check = ["X", "1", "2"]
df = df[(df[cols_to_check] != 0).all(axis=1) & df[cols_to_check].notna().all(axis=1)]

sports_with_home_matches = [
    'Футбол',
    'Хоккей',
    'Хоккей с мячом',
    'Футзал',
    'Гандбол',
    'Флорбол',
    'Водное поло',
    'Хоккей на траве',
    'Регби',
    'Гэльский спорт',
    'Хоккей на роликах',
    'Пляжный футбол'
]
def home_underdog(row):
    if row['category_x'] not in sports_with_home_matches:
        return 'not applicable'
    if row['team1'] == row['underdog_team']:
        return 'home'
    else:
        return 'away'
df['home_underdog'] = df.apply(home_underdog, axis = 1)


def expected_advantage(f1, f2, f):
    """
    Вычисляет ожидаемое преимущество фаворита (E[G_fav - G_und]) на основе коэффициентов F1, F2 и форы F.
    
    Аргументы:
        f1 (float): Коэффициент на фору для команды 1.
        f2 (float): Коэффициент на фору для команды 2.
        f (float): Значение форы (положительное — команда 1 андердог, отрицательное — команда 2 андердог).
    
    Возвращает:
        float: Ожидаемое преимущество фаворита (неотрицательное).
    """
    # Преобразуем коэффициенты в вероятности
    p1 = 1 / f1
    p2 = 1 / f2
    
    # Нормализуем вероятности
    total = p1 + p2
    p1_normalized = p1 / total
    p2_normalized = p2 / total
    
    # Определяем фаворита по знаку форы
    if f > 0:
        # Команда 2 — фаворит, команда 1 — андердог
        is_team2_favorite = True
        p_fav = p2_normalized  # P(G2 - G1 > f)
        k = math.ceil(f)  # Порог для G2 - G1
    elif f < 0:
        # Команда 1 — фаворит, команда 2 — андердог
        is_team2_favorite = False
        p_fav = p1_normalized  # P(G1 - G2 > |f|)
        k = math.ceil(abs(f))  # Порог для G1 - G2
    else:  # f == 0
        # Определяем фаворита по коэффициентам
        is_team2_favorite = f2 < f1
        p_fav = p2_normalized if is_team2_favorite else p1_normalized
        k = 1  # Порог для победы (G_fav - G_und > 0)
    
    # Для равных коэффициентов и нулевой форы возвращаем 0
    if f == 0 and abs(f1 - f2) < 0.01:
        return 0.0
    
    # Предполагаем общее количество голов
    total_goals = 3.0  # Можно настроить
    
    # Целевая функция для нахождения δ = λ_fav - λ_und
    def objective(delta):
        lambda_und = (total_goals - delta) / 2
        lambda_fav = (total_goals + delta) / 2
        if lambda_und < 0 or lambda_fav < 0:
            return np.inf
        # Вероятность P(G_fav - G_und >= k)
        prob = 1 - skellam.cdf(k - 1, lambda_fav, lambda_und)
        return prob - p_fav
    
    # Численное решение
    try:
        delta = brentq(objective, 0, total_goals - 0.001)
    except ValueError:
        # Приближение: δ пропорционально |f| и p_fav
        delta_approx = abs(f) * (p_fav / (1 - p_fav)) if p_fav < 0.99 else abs(f) * 2
        delta = max(delta_approx, 0)
    
    return delta


# Вычисляем ожидаемое преимущество
df['expected_advantage'] = df.apply(lambda row: expected_advantage(row['F1'], row['F2'], row['F']), axis=1)

df.drop(columns = ['1','2','event','F1','F2','F','Tb','Tm','T'],inplace = True)
df.drop(columns = ['stavka','odds_A','odds_B','team1','team2'],inplace = True)

df.rename(columns={'category_x': 'category'}, inplace=True)

df.reset_index(drop = True)



# Целевая переменная
target = 'target'

# Категориальные фичи
cat_features = [
    'category', 'subcat_0', 'subcat_1',
       'subcat_2', 'home_underdog' # <--- добавлены новые категориальные признаки
]

# Включаем категориальные фичи в обучающие признаки
features = [col for col in df.columns if col not in [target,'underdog_team','favorite_team']]

# Делим на train/test
X_train, X_test, y_train, y_test = train_test_split(
    df[features], df[target], test_size=0.2, random_state=42
)

X_train = X_train.fillna(-999)
X_test = X_test.fillna(-999)

# Фиксим список cat_features (оставляем только те, которые реально есть в X_train)
cat_features_in_data = [col for col in cat_features if col in X_train.columns]

# Обучаем модель
model = CatBoostClassifier(
    iterations=3000,  
    learning_rate=0.02,  
    depth=6,  
    l2_leaf_reg=8,  
    loss_function='Logloss',
    eval_metric='Logloss',
    verbose=200,
    random_seed=42,
    early_stopping_rounds=100,
    bagging_temperature=2,  
    random_strength=3,  
    bootstrap_type='MVS',  
    grow_policy='Lossguide', 
    max_leaves=100,  
    min_data_in_leaf=70,  # Минимальное количество данных в листьях
    subsample=0.85,  # Добавление случайности для предотвращения переобучения
)

model.fit(X_train, y_train, cat_features=cat_features_in_data, eval_set=(X_test, y_test))
```
</details>

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
