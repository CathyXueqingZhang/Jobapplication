## Wind Vector Map in R
library used: dplyr,  ggplot2,  plotly,  maps

### Downloading data
Download data from http://coastwatch.pfeg.noaa.gov/erddap/tabledap/ndbcSosWind.html. For this I will need at least longitude, latitude, station_id, time, wind_from_direction, and wind_speed.

```
setwd('~/Downloads/')

# read in dataset
df <- read.csv('windData.csv')
# set up usa map df
usa <- map_data('state')
```
The first step in aggregation is to specify what I want the aggregation to be grouped by: in this case, it’s the station_id, longitude, and latitude.
```
df_mean <- df %>% group_by(station_id, longitude, latitude)
df_mean <- df %>% 
  group_by(station_id, longitude, latitude) %>% 
  summarize(speed_mean = mean(wind_speed, na.rm=T),
            direction_mean = mean(wind_from_direction, na.rm=T)) %>% 
  mutate(u_wnd = speed_mean*cos(pi*direction_mean/180),
          v_wnd = speed_mean*sin(pi*direction_mean/180))
```
Here’s what the output df looks like:

```
head(df_mean)
## # A tibble: 6 x 7
## # Groups:   station_id, longitude [6]
##                   station_id longitude latitude speed_mean direction_mean
##                       <fctr>     <dbl>    <dbl>      <dbl>          <dbl>
## 1 urn:ioos:station:wmo:32st0   -85.074  -19.430   6.970060       124.6108
## 2 urn:ioos:station:wmo:34002   -90.000  -55.000  10.919568       103.0381
## 3 urn:ioos:station:wmo:41002   -74.840   31.760   6.815476       177.6786
## 4 urn:ioos:station:wmo:41004   -79.099   32.501   7.505429       142.4186
## 5 urn:ioos:station:wmo:41008   -80.868   31.400   6.349693       137.4233
## 6 urn:ioos:station:wmo:41009   -80.184   28.501   5.607108       215.7270
## # ... with 2 more variables: u_wnd <dbl>, v_wnd <dbl>
```
Now, setting up the map of the US with ggplot. The dataframe called is the usa dataframe that we created earlier. A couple arguments that I add are fill, color, coord_fixed(), and theme_bw(). Fill changes the state’s colors, color changes the map outline color, coord_fixed() is used to make sure that the aspect ratio of the map remains consistent if the size of the map is changed, and theme_bw() gives a nice minimal theme that works well with this graphic.
```
df_usa <- df_mean %>% 
  filter(latitude <= max(usa$lat) &
          latitude >= min(usa$lat) &
          longitude <= max(usa$lon) &
          longitude >= min(usa$lon))
          
#Set up Map of USA
usa_plot <- ggplot() + 
  geom_polygon(data = usa, aes(x=long, y=lat, group=group), fill = NA, color = "grey60") + 
  coord_fixed(1.3) +
  theme_bw()

usa_plot
```
<img src="https://github.com/CathyXueqingZhang/Jobapplication/blob/master/R/picture/Screen%20Shot%202022-02-06%20at%2019.41.27.png" width="600" height="400" /><br/>

Adding the wind speed data as a scalar quantity onto the map.
```
# Scalar Plot
usa_plot +
  geom_point(data = df_usa, aes(x=longitude, y=latitude, color=speed_mean)) +
  scale_color_gradient(low="light blue", high="dark blue")
```
<img src="https://github.com/CathyXueqingZhang/Jobapplication/blob/master/R/picture/Screen%20Shot%202022-02-06%20at%2019.41.34.png" width="600" height="400" /><br/>

Plot the wind vectors. 
```
# vector plot
usa_plot +
  geom_segment(data = df_usa, aes(x=longitude, y=latitude, xend=longitude+u_wnd/10, yend=latitude+v_wnd/10),
               arrow = arrow(length = unit(0.1, 'cm')), size=0.3)
```
Here is the final result!
<img src="https://github.com/CathyXueqingZhang/Jobapplication/blob/master/R/picture/Screen%20Shot%202022-02-06%20at%2019.41.42.png" width="600" height="400" /><br/>

