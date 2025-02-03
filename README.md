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

## Room type and price is given seperately
#### Let`s Combine and visualize them
```python
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='cyan')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
<img src="https://github.com/user-attachments/assets/2ca14676-60ad-4511-9dfa-d3629d87d4b7" alt="Value Counts Output" width="600"/>
## Which are the top 10 neighborhoods with the most listings?

```python
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img src="https://github.com/user-attachments/assets/47e49026-6c2e-429e-b7ed-8c65c97492cc" alt="Value Counts Output" width="600"/>


## Geographical Distribution of Listings (Price Colored)
```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img src="https://github.com/user-attachments/assets/d0c0d38b-ce34-4db9-a414-866ea958d325" alt="Value Counts Output" width="600"/>

## Let us see the listings on a real map
##### 
* Hotter Areas (Red/Yellow):
High Density: The areas that appear in red or yellow (the "hot" colors) indicate higher density or concentration of listings. This means there are more listings in these areas.
Popular Locations: These regions might be more popular or in high demand. It could be near tourist attractions, popular neighborhoods, or central areas in Paris where people tend to stay more often.

* Colder Areas (Green/Blue):
Low Density: Areas with blue or green (the "cold" colors) indicate a lower concentration of listings. These regions have fewer listings available.
Less Popular Locations: These areas might be less popular or further from key attractions. If you're looking at pricing or other factors, lower density could imply less competition in these regions, which might indicate more affordable areas or less tourist traffic.

* Density Patterns:
Clustered Areas: If you notice clusters of heatmap intensity, they represent hotspots. These might correspond to high-traffic areas like resorts, beaches, or urban centers.
Spread-Out Listings: If the heatmap shows a more uniform distribution, it could suggest that listings are more evenly spread across the region, which may reflect a more balanced demand for rentals across different areas of Paris.

```python
import folium
from folium.plugins import HeatMap
import pandas as pd

# Example dataset for Paris coordinates (replace with your actual data)
paris_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Paris
m = folium.Map(location=[48.8566, 2.3522], zoom_start=12)  # Paris coordinates

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in paris_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('paris_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m

```
<img src="https://github.com/user-attachments/assets/a0cc5ce2-a117-4ba9-bdee-a3be69baa0f0" alt="Value Counts Output" width="600"/>

## How do I find location for my city?
#####
* Type your city name on google maps
* Click on What`s here

<img src="https://github.com/user-attachments/assets/2913a415-43ca-4ddc-8f24-f06e23f94eaf" alt="Value Counts Output" width="600"/>

<img src="https://github.com/user-attachments/assets/6403ebaf-b6b5-4706-a070-ae2bc50465a6" alt="Value Counts Output" width="600"/>

<img src="https://github.com/user-attachments/assets/b13460b5-fc19-4555-a000-97c364d0e8d7" alt="Value Counts Output" width="600"/>

