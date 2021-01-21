The following files are part of the NOAA Weather Data - JFK Airport hosted on IBM Developer Data Asset eXchange.

Homepage: https://developer.ibm.com/exchanges/data/all/jfk-weather-data/
Download link: https://dax-cdn.cdn.appdomain.cloud/dax-noaa-weather-data-jfk-airport/1.1.4/noaa-weather-data-jfk-airport.tar.gz

File list: 
-- jfk_weather.csv : the core dataset as obtained from NOAA.
-- jfk_weather_cleaned.csv : data cleaned for non-numeric data and redundant fields or empty fields. NULLs have been replaced with the closest previous value.
-- LICENSE.txt : a plaintext version of the CLDA-Sharing license that the dataset is licensed under. (https://cdla.io/sharing-1-0/)
-- clean_data.py : the Python script used to clean the data.

If you would like to download data in a similar format for a different time range or United States geographic weather station location, you can follow the steps outlined below: 
1. Access the NOAA Local Climatological Data (LCD) tool here: https://www.ncdc.noaa.gov/cdo-web/datatools/lcd
2. Select a weather station (uniquely identified by its WBAN code) using the Map Tool filters: "Country", "US Territory", "State", "Country", "Zip Code". 
3. Choose a weather station and select "View Full Details". On this page, you can view more details about the weather station and preview the data for a particular day. 
4. When you are ready, select "ADD TO CART", and move to the cart checkout page.
5. From the cart checkout page, select the "LCD CSV" data format, and select the appropriate range of dates for which you would like the data for. 
6. Enter an email address to which you would like NOAA to send you a download link for the data, then click "SUBMIT ORDER". Note, during times of high volume, NOAA may delay sending you a link to your dataset for up to several hours. 
7. For any questions pertaining to the LCD tool, visit NOAA's FAQ page here: ncdc.noaa.gov/cdo-web/faq 

