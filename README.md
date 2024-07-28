<h4>Overview</h4>
<p>
  Filtering Water Depth Sensors in the Huron River Watershed Area
</p>

<h4>Background</h4>
<p>
  
  The Digital Water Lab has deployed over 100 depth sensors in the Michigan area. The goal of this project is to filter out any sensor locations that are outside of the Huron River Watershed. In addition to such, greater filtration steps are taken to remove sensors that are not located on or near the Huron River itself. This filtration algorithm allows one to automatically determine which depth sensors are relevant to be added to the [Huron River Watershed](https://www.huron.digitalwaterlab.org/) with ease.

</p>

<h4>Necessary libraries</h4>

```
pandas
geopandas
shapely.geometry
matplotlib.pyplot
```

<h4>Filtration Methods</h4>

<h5>Initial Filtering of Sensors</h5>
<p>
  Sensor data is initially inputted in the form of a csv file and converted to a pandas dataframe (df). 
  Then, all NaN "Latitude, Longitude" pairs and non-water depth sensors are removed.
  
</p>

<h5>Initial Filtering of Sensors</h5>

