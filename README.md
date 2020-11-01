# About
This is an assignment I did as an assignment on Coursera on Data visualizations 
It covers two datasets:
1. Data Science Survey results which is contains results for a survey on different interests of people in different aspects of data science. It is obtained from this link :https://cocl.us/datascience_survey_data. I plotted two bar charts both showing the percentage of interest in three categories of seven different aspects of data science based on the number of respondents. The difference in the bar charts is that one has borders and the other does not
2. SF Neighborhood Crime Data which contains data on different crimes committed on different neighbourhoods in SF on different days of the week. I plotted a map using Folium to show the distribution of total reported crimes per neighbourhood

### Import necessary libraries for data wrangling, analysis and visualizations


```python
import pandas as pd
import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
```

### Data Science Survey Results
Load the survey results


```python
#load the survey results and set first column as index
df_dsurvey = pd.read_csv('https://cocl.us/datascience_survey_data', index_col =0)
```


```python
df_dsurvey
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Very interested</th>
      <th>Somewhat interested</th>
      <th>Not interested</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Big Data (Spark / Hadoop)</th>
      <td>1332</td>
      <td>729</td>
      <td>127</td>
    </tr>
    <tr>
      <th>Data Analysis / Statistics</th>
      <td>1688</td>
      <td>444</td>
      <td>60</td>
    </tr>
    <tr>
      <th>Data Journalism</th>
      <td>429</td>
      <td>1081</td>
      <td>610</td>
    </tr>
    <tr>
      <th>Data Visualization</th>
      <td>1340</td>
      <td>734</td>
      <td>102</td>
    </tr>
    <tr>
      <th>Deep Learning</th>
      <td>1263</td>
      <td>770</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Machine Learning</th>
      <td>1629</td>
      <td>477</td>
      <td>74</td>
    </tr>
  </tbody>
</table>
</div>



#### Bar chart of Percentage of interest
Format the data for data analysis


```python
#sort dataframe in descending order of 'Very Interested column'
df_dsurvey = df_dsurvey.sort_values(by = 'Very interested')
df_dsurvey
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Very interested</th>
      <th>Somewhat interested</th>
      <th>Not interested</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Data Journalism</th>
      <td>429</td>
      <td>1081</td>
      <td>610</td>
    </tr>
    <tr>
      <th>Deep Learning</th>
      <td>1263</td>
      <td>770</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Big Data (Spark / Hadoop)</th>
      <td>1332</td>
      <td>729</td>
      <td>127</td>
    </tr>
    <tr>
      <th>Data Visualization</th>
      <td>1340</td>
      <td>734</td>
      <td>102</td>
    </tr>
    <tr>
      <th>Machine Learning</th>
      <td>1629</td>
      <td>477</td>
      <td>74</td>
    </tr>
    <tr>
      <th>Data Analysis / Statistics</th>
      <td>1688</td>
      <td>444</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```python
#create copy of original dataframe
df_dsurvey1 = df_dsurvey.copy()
df_dsurvey1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Very interested</th>
      <th>Somewhat interested</th>
      <th>Not interested</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Data Journalism</th>
      <td>429</td>
      <td>1081</td>
      <td>610</td>
    </tr>
    <tr>
      <th>Deep Learning</th>
      <td>1263</td>
      <td>770</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Big Data (Spark / Hadoop)</th>
      <td>1332</td>
      <td>729</td>
      <td>127</td>
    </tr>
    <tr>
      <th>Data Visualization</th>
      <td>1340</td>
      <td>734</td>
      <td>102</td>
    </tr>
    <tr>
      <th>Machine Learning</th>
      <td>1629</td>
      <td>477</td>
      <td>74</td>
    </tr>
    <tr>
      <th>Data Analysis / Statistics</th>
      <td>1688</td>
      <td>444</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```python
#convert to percentages of total numbers to 2 decimal places. Know that total number of respondents is 2233
for col in df_dsurvey1:
    df_dsurvey1[col] = round((df_dsurvey1[col]/2233 *100), 2)
df_dsurvey1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Very interested</th>
      <th>Somewhat interested</th>
      <th>Not interested</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Data Journalism</th>
      <td>19.21</td>
      <td>48.41</td>
      <td>27.32</td>
    </tr>
    <tr>
      <th>Deep Learning</th>
      <td>56.56</td>
      <td>34.48</td>
      <td>6.09</td>
    </tr>
    <tr>
      <th>Big Data (Spark / Hadoop)</th>
      <td>59.65</td>
      <td>32.65</td>
      <td>5.69</td>
    </tr>
    <tr>
      <th>Data Visualization</th>
      <td>60.01</td>
      <td>32.87</td>
      <td>4.57</td>
    </tr>
    <tr>
      <th>Machine Learning</th>
      <td>72.95</td>
      <td>21.36</td>
      <td>3.31</td>
    </tr>
    <tr>
      <th>Data Analysis / Statistics</th>
      <td>75.59</td>
      <td>19.88</td>
      <td>2.69</td>
    </tr>
  </tbody>
</table>
</div>




Plot the graph


```python
#plot the bar chart
ax = df_dsurvey1.plot(kind = 'bar', 
                     figsize = (20,8), 
                     width = 0.8,
                     color = ('#5cb85c', '#5bc0de', '#d9534f'),
                     fontsize = 14
                     )

#annotate the bars with the percentages with axes patches    
for perc in ax.patches:                 
    ax.annotate(round(perc.get_height(),2), 
                (perc.get_x()+perc.get_width()/2., perc.get_height()),
                ha='center', 
                va='center',
                xytext=(0, 5),
                textcoords='offset points')
    
#set the title of the chart
ax.set_title('Percentage of interest', fontsize =16)
```




    Text(0.5, 1.0, 'Percentage of interest')




![png](output_11_1.png)



```python
#plot the bar chart
ax1 = df_dsurvey1.plot(kind = 'bar', 
                       figsize = (20,8), 
                       width = 0.8,
                       color = ('#5cb85c', '#5bc0de', '#d9534f'),
                       fontsize = 14,
                      )
                     
#remove the top, left and right borders
ax1.spines['right'].set_visible(False)
ax1.spines['top'].set_visible(False)
ax1.spines['left'].set_visible(False)

#remove y ticks
ax1.axes.yaxis.set_ticks([])

#annotate the bars with the percentages with axes patches    
for perc in ax.patches:                 
    ax1.annotate(round(perc.get_height(),2), 
                (perc.get_x()+perc.get_width()/2., perc.get_height()),
                ha='center', 
                va='center',
                xytext=(0, 5),
                textcoords='offset points')
    
#set the title of the chart
ax1.set_title('Percentage of interest', fontsize =16)
```




    Text(0.5, 1.0, 'Percentage of interest')




![png](output_12_1.png)


### SF Crime Data: Choropleth
Load the data set


```python
df_sfcrime = pd.read_csv('https://cocl.us/sanfran_crime_dataset')

```


```python
df_sfcrime.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>IncidntNum</th>
      <th>Category</th>
      <th>Descript</th>
      <th>DayOfWeek</th>
      <th>Date</th>
      <th>Time</th>
      <th>PdDistrict</th>
      <th>Resolution</th>
      <th>Address</th>
      <th>X</th>
      <th>Y</th>
      <th>Location</th>
      <th>PdId</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>120058272</td>
      <td>WEAPON LAWS</td>
      <td>POSS OF PROHIBITED WEAPON</td>
      <td>Friday</td>
      <td>01/29/2016 12:00:00 AM</td>
      <td>11:00</td>
      <td>SOUTHERN</td>
      <td>ARREST, BOOKED</td>
      <td>800 Block of BRYANT ST</td>
      <td>-122.403405</td>
      <td>37.775421</td>
      <td>(37.775420706711, -122.403404791479)</td>
      <td>12005827212120</td>
    </tr>
    <tr>
      <th>1</th>
      <td>120058272</td>
      <td>WEAPON LAWS</td>
      <td>FIREARM, LOADED, IN VEHICLE, POSSESSION OR USE</td>
      <td>Friday</td>
      <td>01/29/2016 12:00:00 AM</td>
      <td>11:00</td>
      <td>SOUTHERN</td>
      <td>ARREST, BOOKED</td>
      <td>800 Block of BRYANT ST</td>
      <td>-122.403405</td>
      <td>37.775421</td>
      <td>(37.775420706711, -122.403404791479)</td>
      <td>12005827212168</td>
    </tr>
    <tr>
      <th>2</th>
      <td>141059263</td>
      <td>WARRANTS</td>
      <td>WARRANT ARREST</td>
      <td>Monday</td>
      <td>04/25/2016 12:00:00 AM</td>
      <td>14:59</td>
      <td>BAYVIEW</td>
      <td>ARREST, BOOKED</td>
      <td>KEITH ST / SHAFTER AV</td>
      <td>-122.388856</td>
      <td>37.729981</td>
      <td>(37.7299809672996, -122.388856204292)</td>
      <td>14105926363010</td>
    </tr>
    <tr>
      <th>3</th>
      <td>160013662</td>
      <td>NON-CRIMINAL</td>
      <td>LOST PROPERTY</td>
      <td>Tuesday</td>
      <td>01/05/2016 12:00:00 AM</td>
      <td>23:50</td>
      <td>TENDERLOIN</td>
      <td>NONE</td>
      <td>JONES ST / OFARRELL ST</td>
      <td>-122.412971</td>
      <td>37.785788</td>
      <td>(37.7857883766888, -122.412970537591)</td>
      <td>16001366271000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>160002740</td>
      <td>NON-CRIMINAL</td>
      <td>LOST PROPERTY</td>
      <td>Friday</td>
      <td>01/01/2016 12:00:00 AM</td>
      <td>00:30</td>
      <td>MISSION</td>
      <td>NONE</td>
      <td>16TH ST / MISSION ST</td>
      <td>-122.419672</td>
      <td>37.765050</td>
      <td>(37.7650501214668, -122.419671780296)</td>
      <td>16000274071000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#create new dataframe by grouping the dataset by the district column and counting the number of elements within the groups
df_neighbourhood = df_sfcrime.groupby(['PdDistrict']).count()

#extract one column (as all columns have the same totals) and add it to a new dataframe. The district is currently the index
df_neighbourhood1 = df_neighbourhood[['IncidntNum']]
```


```python
#reset the index so that we have the district column as it's own column and not index label
df_neighbourhood1 = df_neighbourhood1.reset_index()
```


```python
#rename the column names to something that makes more sense
df_neighbourhood1 = df_neighbourhood1.rename(columns = {'PdDistrict': 'Neighbourhood', 'IncidntNum': 'Count'})
df_neighbourhood1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighbourhood</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BAYVIEW</td>
      <td>14303</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CENTRAL</td>
      <td>17666</td>
    </tr>
    <tr>
      <th>2</th>
      <td>INGLESIDE</td>
      <td>11594</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MISSION</td>
      <td>19503</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NORTHERN</td>
      <td>20100</td>
    </tr>
    <tr>
      <th>5</th>
      <td>PARK</td>
      <td>8699</td>
    </tr>
    <tr>
      <th>6</th>
      <td>RICHMOND</td>
      <td>8922</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SOUTHERN</td>
      <td>28445</td>
    </tr>
    <tr>
      <th>8</th>
      <td>TARAVAL</td>
      <td>11325</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TENDERLOIN</td>
      <td>9942</td>
    </tr>
  </tbody>
</table>
</div>



### SF Crime on a Map


```python
#install folium for geomap plotting
!pip install folium
import folium
```

    Requirement already satisfied: folium in c:\users\hp\anaconda3\lib\site-packages (0.11.0)
    Requirement already satisfied: jinja2>=2.9 in c:\users\hp\anaconda3\lib\site-packages (from folium) (2.11.1)
    Requirement already satisfied: numpy in c:\users\hp\anaconda3\lib\site-packages (from folium) (1.18.1)
    Requirement already satisfied: branca>=0.3.0 in c:\users\hp\anaconda3\lib\site-packages (from folium) (0.4.1)
    Requirement already satisfied: requests in c:\users\hp\anaconda3\lib\site-packages (from folium) (2.22.0)
    Requirement already satisfied: MarkupSafe>=0.23 in c:\users\hp\anaconda3\lib\site-packages (from jinja2>=2.9->folium) (1.1.1)
    Requirement already satisfied: idna<2.9,>=2.5 in c:\users\hp\anaconda3\lib\site-packages (from requests->folium) (2.8)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in c:\users\hp\anaconda3\lib\site-packages (from requests->folium) (1.25.8)
    Requirement already satisfied: certifi>=2017.4.17 in c:\users\hp\anaconda3\lib\site-packages (from requests->folium) (2019.11.28)
    Requirement already satisfied: chardet<3.1.0,>=3.0.2 in c:\users\hp\anaconda3\lib\site-packages (from requests->folium) (3.0.4)
    


```python
import folium
```


```python
#read the geojson file for the neighborhoods
sanfran = r'https://cocl.us/sanfran_geojson' # geojson file

# create a plain sf map
sf_map = folium.Map(location=[37.7749, -122.4194], zoom_start=12, tiles='OpenStreetMap')
```


```python
folium.Choropleth(geo_data=sanfran, 
                  data = df_neighbourhood1,
                  columns = ['Neighbourhood', 'Count'],
                  key_on = 'feature.properties.DISTRICT',
                  fill_color='YlOrRd',
                  fill_opacity=0.7, 
                  line_opacity=0.2,
                  legend_name='Crime Rate in San Francisco'
                 ).add_to(sf_map)

#sf_map
```




    <folium.features.Choropleth at 0x200dc814e48>



The map could not be rendered in markdown. Check the Jupyter notebook to see the output


```python

```
