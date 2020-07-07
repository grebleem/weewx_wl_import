## Description
This program will import data from Davis WeatherLink into the weewx database.
The data is retrieved using the v2 api from WeatherLink. More information on the [WeatherLink Developer Portal](https://weatherlink.github.io/v2-api/).

A cvs file is created and that file is automatically imported using wee_import. Using wee_import will assure no double records are added in the database and al the conversions are made and
all the daily summaries are calculated.

### Usage
* First enter weewx directory in the in `davis-csv.conf`. 
* Next copy the API Key v2 details from [https://www.weatherlink.com/account](https://www.weatherlink.com/account)  
* If only one station is registerd the `station_id` is not needed. If there are more stations the program will show all the stations associated to the api details.
```
[weatherlink]
    # weewx directory
    WEEWX_ROOT = /home/weewx
    
    # Copy the API Key v2 and API Secrect from WeatherLink: https://www.weatherlink.com/account
    API_KEY = v2_api_key
    API_SECRET = v2_api_secret
    
    # Only Needed with multiple Stations
    # If you have multiple stations fill in the ID of the required station
    # The program will give all the Station associated with the given API Key
    station_id = default
```
### UV and Solar data
If the data has no UV and Solar data set the folowing stanza to `false`
```
    UV_sensor = False
    solar_sensor = False
```
## Starting the import
There is no limit of the amount of data that is imported, however take the following [warning](http://www.weewx.com/docs/utilities.htm#Importing_from_CSV_files) from weewx into considerations:

**_Warning!_
Running WeeWX during a `wee_import` session can lead to abnormal termination of the import. 
If WeeWX must remain running (e.g., so that live data is not lost) run the `wee_import` session on another machine or to a second database 
and merge the in-use and second database once the import is complete.**

To import a single day use
```
weewx_weatherlink --date=YYYY-mm-dd
```
Or importing a range
```
weewx_weatherlink --startdate=YYYY-MM-DD[THH:MM] --enddate=YYYY-MM-DD[THH:MM]
```

### Python modules
The folowing python modules need to be installed:
``` 
pip install requests
```