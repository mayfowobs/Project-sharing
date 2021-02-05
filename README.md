# Project-sharing
This is my data engineering project 

# Data Engineering test

We have IoT devices collecting some metrics across the world. We have experienced that a lot of devices are failing lately. We know that the devices are sensible to temperature, so we have downloaded some weather data from the locations of the devices.  

## Part 1. Data manipulation  

We have the list of the position of the devices in a json file like this `devices.json`:  

``` json
{'id': 15126, 'name': 'device-BE-17', 'lat': 35.7721, 'lon': -78.63861} 
{'id': 12526, 'name': 'device-US-11', 'lat': 36.7721, 'lon': -71.1561} 
... 
```

We have another dataset downloaded in json the of the weather data for the last week with hourly granularity for the positions of the devices ([API](https://www.weatherbit.io/api/swaggerui/weather-api-v2#!/Hourly32Historical32Weather32Data/get_history_hourly_lat_lat_lon_lon)). As we want you to have up to date data, we provide a python script that downloads the last month of data from the API, see at the end for instructions on how to use it.

Apart from that, we have csv dataset with extra information about the weather stations that collect the weather. This csv has a column with a metric that contains the measurement reliability of each station. The data look like this:  

```csv
station_id,lat,lon,source,reports,country,measurement_reliability 
0011W82.82,15.16,madis,subhourly,SJ,0.5 
00000,17.03,-42.97,madis,subhourly,GF,0.56 
0001W,30.436,-84.122,madis,subhourly,US,0.93 
0002W,30.538,-84.224,madis,subhourly,US,0.85 
... 
```

We would like to gather all the relevant information in a single table and provide it to the device expert to enable them to find some insight on what the problem with the devices could be.

Summarize the results to have daily granularity, use average to aggregate the measurements. This table would have the following schema:

```csv
device_id, device_name, lat, lon, date, avg_temp, meassurement_reliability_score
```

Take into consideration that each weather measurement can come from multiple stations (`source` field). When a measurement comes from multiple stations, use the [Harmonic mean](https://en.wikipedia.org/wiki/Harmonic_mean).

You can use any programing language or technology to complete it, if it is a supported language in Azure. Take into consideration that in a future iteration we might need to add more measurements to the result table.

