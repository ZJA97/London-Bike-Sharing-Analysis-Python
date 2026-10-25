# London Bike Sharing Analysis

Exploratory data analysis of 17,000+ hourly bike rentals in London, looking at how time of day, season and weather shape demand, and what that means for fleet planning and redistribution.

Built in Python (Pandas, Matplotlib, Seaborn) in a Jupyter notebook.

## Key Findings

- **Two commuter peaks.** Demand spikes at **08:00 (~2,880 rentals/hr)** and **17:00 (~2,830 rentals/hr)**, roughly **twice the midday rate** (10:00–15:00 averages ~1,365/hr).
- **Weekdays beat weekends.** Average hourly demand is **23.7% higher on weekdays** (1,209 vs 977 rentals/hr), consistent with commuting being the main driver. Thursday is the busiest day (1,259) and Sunday the quietest (960).
- **Strong seasonality.** Summer averages 1,464 rentals/hr against 822 in winter. July is the peak month (1,544) and January the lowest (785).
- **Weather matters.** Demand rises steeply with temperature, peaking at **25–30°C (~2,784 rentals/hr)**, and falls to ~630 rentals/hr below 5°C. Humidity has a negative correlation with demand (-0.46).
- **Bad weather suppresses demand.** Rain (713), thunderstorms (583) and snow (251) all sit well below the fair-weather averages.

### Charts

![Average bike rentals by hour of the day](images/Rentals-by-Hour.png)

![Average bike rentals by season](images/Rentals-by-Season.png)

### Detail

| Season | Avg rentals/hr |
|---|---|
| Spring | 1,103.8 |
| Summer | 1,464.5 |
| Autumn | 1,179.0 |
| Winter | 821.7 |

| Weather condition | Avg rentals/hr | Hours in data |
|---|---|---|
| Few clouds | 1,496 | 4,034 |
| Broken clouds | 1,195 | 3,551 |
| Clear / mostly clear | 1,162 | 6,150 |
| Rain / light rain | 713 | 2,141 |
| Cloudy | 635 | 1,464 |
| Thunderstorm | 583 | 14 |
| Snowfall | 251 | 60 |

> Thunderstorm and snowfall are based on very few hours, so treat those averages with caution.

## Recommendations

1. **Rebalance around the peaks.** Concentrate bike redistribution on weekdays in the hours before the morning peak (06:00–08:00) and before the evening peak (15:00–17:00).
2. **Schedule maintenance in quiet periods.** Overnight (roughly 02:00–04:00, when demand is around 200 rentals/hr or fewer) and during winter (Dec–Feb) are the lowest-demand windows.
3. **Scale the active fleet for summer.** June–August demand averages about 33% above spring and 78% above winter, so capacity should be increased ahead of the summer months.

## Dataset

[London Bike Sharing Dataset](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset) on Kaggle: hourly bike rental counts combined with weather data.

- **Rows:** 17,414 hourly records
- **Period:** 4 January 2015 to 3 January 2017
- **File used:** `df.csv`

| Column | Description |
|---|---|
| `timestamp` | Date and hour of the record |
| `cnt` | Number of bikes rented in that hour |
| `t1` | Air temperature (°C) |
| `t2` | "Feels like" temperature (°C) |
| `hum` | Humidity (%) |
| `wind_speed` | Wind speed |
| `weather_code` | Weather category (clear, few clouds, broken clouds, cloudy, rain, thunderstorm, snowfall) |
| `is_holiday` | 1 if a holiday, else 0 |
| `is_weekend` | 1 if a weekend, else 0 |
| `season` | 0 = spring, 1 = summer, 2 = autumn, 3 = winter |

## Methodology

1. **Data checks:** checked for missing values and duplicate rows (none found) and converted `timestamp` to a datetime type.
2. **Feature engineering:** extracted year, month, day of week and hour from the timestamp, and binned temperature into 5°C ranges.
3. **Exploratory analysis:** compared average hourly demand (`cnt`) by hour, day of week, month, season, weekday vs weekend, holiday vs non-holiday, temperature, humidity and weather condition.
4. **Correlation analysis:** built a correlation heatmap across demand, weather variables and time features.
5. **Visualisation and recommendations:** summarised the patterns as charts and turned them into operational recommendations.

## Tools

- Python
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook

## Limitations & Interpretation Notes

This is a descriptive exploratory analysis, so the findings show patterns in the data rather than proven causes.

- **Commuting as the main driver:** the sharp peaks at 08:00 and 17:00, and the 23.7% higher weekday demand, are consistent with commuter use. The hourly pattern has not yet been split by weekday vs weekend, which would confirm it.
- **Weather and time of day overlap:** afternoons are warmer and mornings are more humid, so part of the temperature and humidity effect may reflect the hourly pattern. The correlations are moderate (temperature +0.39, humidity -0.46) rather than strong, and temperature and humidity are the strongest of the weather variables only.
- **Temperature trend:** demand rises steeply with temperature up to 25-30°C and then levels off slightly at 30-35°C. The exact shape of this relationship was not modelled.
- **Small samples:** thunderstorm (14 hours) and snowfall (60 hours) averages are based on very few observations and should be treated with caution.
- **Unexplained results:** "cloudy" hours average fewer rentals (~635/hr) than rain (~713/hr), which was not investigated further. Holidays also show much lower demand (~770 vs ~1,152 rentals/hr), but this was not analysed in depth.
- **Scope of the data:** two years of system-wide hourly totals, with no station-level or user-type detail, so the recommendations are high-level.

### Possible Next Steps

- Compare hourly demand on weekdays vs weekends to test the commuter explanation directly.
- Build a regression model that controls for hour, season and weather together, to separate their effects.
- Investigate why cloudy conditions show lower demand than rain.

## Repository Structure
