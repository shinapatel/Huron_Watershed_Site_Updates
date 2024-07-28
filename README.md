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

<h4>Water Depth Sensor Filtration</h4>
<p>
  Sensor data is initially inputted in the form of a csv file and converted to a pandas dataframe (df).
  Then, all NaN "Latitude, Longitude" pairs and non-water depth sensors are removed.

  In order to remove water depth sensors located outside of the Huron River Watershed, shapely.geometry is used to store the Huron River Watershed as a polygon and to create Point objects of sensor coordinate pair.

  <p align="center">
    <img src="https://github.com/shinapatel/Huron_Watershed_Site_Updates/blob/main/huron_river_watershed_sensors.png" width=325px>
  </p>

  ```
  sensors_geometry = [Point(xy) for xy in zip(sensors_df.lon, sensors_df.lat)]
  sensors_gdf = gpd.GeoDataFrame(sensors_df, crs='EPSG:4326', geometry=sensors_geometry)
  huron_watershed_polygon = shape(watershed_gdf.geometry.iloc[0])
  sensors_within_watershed = sensors_gdf[sensors_gdf.geometry.apply(lambda x: x.intersects(huron_watershed_polygon))]
  ```

  In order to remove water depth sensors located far away from the Huron River System, shapely.geometry is used to develop a buffer surrounding the Huron River which demonstrates the margin of acceptable distance between a sensor location and the river.

  <p align="center">
    <img src="https://github.com/shinapatel/Huron_Watershed_Site_Updates/blob/main/final_sensor_filtration_plot.png" width=325px>
  </p>

  ```
  sensors_geometry = [Point(xy) for xy in zip(sensors_df.lon, sensors_df.lat)]
  sensors_gdf = gpd.GeoDataFrame(sensors_df, crs='EPSG:4326', geometry=sensors_geometry)
  buffer_distance = 0.01
  river_gdf['geometry'] = river_gdf.geometry.buffer(buffer_distance)
  sensors_near_river = gpd.sjoin(sensors_gdf, river_gdf, how='inner', predicate='intersects')
  ```
</p>



