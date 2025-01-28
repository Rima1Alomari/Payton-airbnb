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
<img src="https://github.com/user-attachments/assets/9d7764f9-d60a-4773-ac16-096a779ae55a" width="600"/>


## 2. Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
#### Explanation:
value_counts(normalize=True) gives proportions.

Multiplying by 100 converts the proportions into percentages
```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
<img src="https://github.com/user-attachments/assets/932c9bb6-6288-41d5-bda0-fb901729417a" width="600"/>



# 3. Let`s Count the busiest day! 🚩
### Hint: We will be counting the most unavailable days (given by f)

```python
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
<img src="https://github.com/user-attachments/assets/d48db258-db5c-4540-8bed-fea72e6e4799" alt="Value Counts Output" width="600"/>


## 4. Plot a bar graph to show availability percentage
```python
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green', 'red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
<img src="https://github.com/user-attachments/assets/842a5c3a-1290-4d28-88a3-533e2ad4a4ac" alt="Value Counts Output" width="600"/>

# 5. Plot the busiest day
```python
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img src="https://github.com/user-attachments/assets/057f0077-9595-45af-822f-ef871dd92c17" alt="Value Counts Output" width="600"/>

# 📄 Download listings dataset of Paris from 
https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/visualisations/listings.csv
```python
import pandas as pd
listings = pd.read_csv('/content/listings (1).csv')
```
<img src="https://github.com/user-attachments/assets/dbcd1059-5919-4ebd-811b-16301377c45a" alt="Value Counts Output" width="600"/>
<img src="https://github.com/user-attachments/assets/57fd9f4d-fb5b-4610-b334-d8f01315a12d" alt="Value Counts Output" width="600"/>

## listings.columns
<img src="https://github.com/user-attachments/assets/f5ca7a9b-e37d-4e54-9952-baa8f12fa393" alt="Value Counts Output" width="600"/>





