# Insights-from-a-real-air-bnb-data-set
### https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz 
I’ve completed all the calculations using data from Paris. Once you visit the website, you can click on calendar.csv.gz, and it will download directly!
If you’re working with Google Colab, the .gz file format won’t cause you any issues.
```python
import pandas as pd
calendar = pd.read_csv('https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz')
```
<img src="https://github.com/user-attachments/assets/05b15fe2-66f5-4b90-9cc2-a986eef9f48f" width="600"/>
<img src="https://github.com/user-attachments/assets/5a8c1ef4-83db-409f-a7f4-a829bf1222fb" width="600"/>


# Questions
## 1. Want to know the number of available and unavailable rooms

```python
calendar.available.value_counts()
```
<img src="(https://github.com/user-attachments/assets/9d7764f9-d60a-4773-ac16-096a779ae55a" width="600"/>


## 2. Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
#### Explanation:
value_counts(normalize=True) gives proportions.

Multiplying by 100 converts the proportions into percentages
```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
<img src="https://github.com/user-attachments/assets/932c9bb6-6288-41d5-bda0-fb901729417a" width="600"/>



# 3 Let`s Count the busiest day! 🚩
### Hint: We will be counting the most unavailable days (given by f)

```python
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
<img src="https://github.com/user-attachments/assets/d48db258-db5c-4540-8bed-fea72e6e4799" alt="Value Counts Output" width="600"/>


## 4.Plot a bar graph to show availability percentage
```python
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green', 'red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
<img src="https://github.com/user-attachments/assets/842a5c3a-1290-4d28-88a3-533e2ad4a4ac" alt="Value Counts Output" width="600"/>




