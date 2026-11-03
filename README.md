# solar_resource_assesment_group15
poster session project something



Project description
For the forecasting assignment, you will compare different forecast models and evaluate how forecast accuracy changes with forecast horizon.

Groups
For the assignment, you have to pair up in groups of two. Please self-enroll in a group on DTU Learn. If you cannot find a group member, please email arajen@dtu.dk.

Each group will be assigned a different weather station, where you will assess the forecast. The weather stations are all located in Denmark and operated by the Danish Meteorological Institute (DMI). The station assigned to each group can be found here. See this page for metadata for the different stations (such as the location and station name).

Measurement data
The accuracy of a forecast model can be assessed by comparing forecasts with actual measured ground-measured irradiance. Most solar irradiance forecasting models output global horizontal irradiance (GHI), which is what we will assess in this project.

As the first step, you should retrieve measurements of solar irradiance measurements from DMI using the solarpy Python package. The package is not on PyPI, so you have to run the following command to install the package:

pip install git+https://github.com/assessingsolar/solarpy.git
The function for retrieving historical observations from DMI is solarpy.iotools.get_dmi_metobs. 

Once you have retrieved measurement data, you should quality control the data. The quality control procedures should include checking if the maximum and minimum values are within the BSRN QC checks. You should also generate plots of the data and visually inspect the data quality (e.g., check for shading and time shifts). You may consider using the solarpy plotting module.

The DMI measurements have a 10-minute frequency, whereas the forecast data are hourly. You will therefore need to resample the measurement data to 1-hour average values to match the forecast timestamps. The measurement data is in UTC and right-labeled, meaning the timestamp 10:20 corresponds to the average value from 10:11 to 10:20. When resampling, ensure that you select the correct options for the label and closed parameters!

Forecast data
Forecasts of GHI have been retrieved for each DMI station at each hour of the day starting on 2026-11-03. Forecasts have been retrieved from 8 different NWP models from open-meteo.com. The forecast files are available in the folder called "Forecast data". Additional forecast files will be uploaded continuously until 2026-11-27.

The forecast file name indicates the station and the time at which the forecast was retrieved. For example, the file "06031_20261109T0600.csv" contains the forecast for station 06031 (Tylstrup) and was retrieved at 6:00 am UTC on November 9th 2026. The forecast timestamps are in UTC, and the values are right-binned, meaning that the data point with the timestamp 02:00 is the average value for the period 01:01 to 02:00.

Each forecast file contains hourly forecasts of GHI for the next 7 days. Each column corresponds to a different NWP model. Note that the different models have different forecast horizons. Regional NWP models usually have shorter time horizons than global models. For example, the DMI Harmonie Arome model has a forecast horizon of 54 hours, whereas ECMWF's global IFS models have a forecast horizon of up to 10 days. The models denoted "_seamless" combine multiple forecast models; e.g., "dmi_seamless" uses the DMI forecast models for short forecast horizons (2-3 days) and ECMWF data for longer forecast horizons.

Once you've retrieved the measurement data, you should load the forecast data into Python or your preferred data analytics tool. Make sure to visually inspect the forecast and measured data. Do the forecasts look good? Do some models look better than others?

Quantifying forecast accuracy
Once you have parsed the forecast data files and the measurements data, you can then begin quantifying the accuracy of the forecasting models. Several metrics can be used to quantify forecast error, each with its own strengths and limitations. In this assignment, we will evaluate forecast accuracy using two metrics: Root Mean Square Error (RMSE) and Bias.

You will calculate these error metrics for each forecast model and for every forecast horizon (e.g., forecast horizons of 1 hour, 2 hours, and so on). To do this, you have to compare the measured values from your DMI station with the forecasted values from the NWP models.

For example, when assessing the 1-hour forecast horizon, use the first hour from each forecast file to compute RMSE and Bias. Repeat this process for 2-hour, 3-hour forecasts, and so on. For each metric, you will need to use forecast data from all forecast files corresponding to your station.

 

Forecast metrics as a function of forecast horizon.

Poster presentation
The results from your forecast comparison will be presented at the poster session on December 1st from 1:00 to 5:00 p.m. Each group will give a 5-minute presentation of their poster, with the time split evenly between the two group members. It is mandatory to attend the poster session.

Your poster should include the following:

Figures showing quality control of the measurement data 
Comparison metrics of the different forecast models as a function of forecast horizon
One or more figures showing the forecasted and measured irradiance for one or more days
Discussion about why some models perform better than others (is it as you would expect)? Are some types of days easier to forecast than others (e.g., clear sky, cloudy, or broken clouds)?
Each group will need to print their poster in size A0, which can be done at the DTU Library.

The poster should be uploaded to DTU Learn before the poster presentation.

Forecast competition
As mentioned in the lecture notes, it is possible to make a better forecast by blending/combining different forecasts. Make an attempt to combine different forecasts (e.g., 80% Model A and 20% Model B) to improve the forecast scores. Based on the best method you derived, you will make your own blended forecast 4 days ahead for DTU for the period from the 28th of November to the 1st of December.

You will need to submit this blended forecast on Learn before Friday, the 27th at 23:59. The forecast files for DTU will be provided to you, meaning you will only need to apply your blending method and submit the forecast on DTU Learn.

The forecast should be submitted in the CSV format with the first column corresponding to the date/time in the format of (2025-11-29 02:00+00:00). The file name should be your group number, e.g., "Group3.csv".

Grading
Your final grade for the course will be a combination of your mid-term quiz score (66%) and the poster presentation (34%). For the poster presentation, the grading will focus on your communication (presentation, poster design, etc.), how well you assessed the forecasts, as well as your ability to reflect on the project (e.g., did the forecast rank as expected, what would you have done differently?). You will not be graded on how well you perform in the forecast competition, but it is mandatory to submit a forecast.