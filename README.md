# Insights-from-a-real-air-bnb-data-set
### https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz 
I’ve completed all the calculations using data from Paris. Once you visit the website, you can click on calendar.csv.gz, and it will download directly!
If you’re working with Google Colab, the .gz file format won’t cause you any issues.
```python
import pandas as pd
calendar = pd.read_csv('https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz')
```
![image](https://github.com/user-attachments/assets/05b15fe2-66f5-4b90-9cc2-a986eef9f48f)
![image](https://github.com/user-attachments/assets/5a8c1ef4-83db-409f-a7f4-a829bf1222fb)

# Questions
## 1. Want to know the number of available and unavailable rooms

```python
calendar.available.value_counts()
```
![image](https://github.com/user-attachments/assets/9d7764f9-d60a-4773-ac16-096a779ae55a)
