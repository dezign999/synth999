# synth999
Syth999 is a cryptic watch face that is based around the [Absintheric Font](https://www.fontspace.com/absinthelyric-print-font-f30853). With selectable layout styles and colors, it's easy to make this watch face your daily driver. Don't worry, it gets easier to read the time once you realize where to look ;)

## Features
* 24/12 Hour Time - Press the top left button to toggle
* Color Inversion - Press the top right button to toggle a light or dark color scheme
* Layout Style - Press the bottom right button to switch between a clean time-only layout, or a balanced layout with complications
* NTP Time Sync - Time drifting is no longer an issue with 2 daily NTP time syncs, and an initial NTP sync on install
* Live Weather - Updates every 30 minutes by default
* Weather by City Name or City Code - If your city name is not unique, you can fallback to your city code as described in the source comments.
* Ambient Temperature - No WiFi? Watchy will use it's RTC's ability to give you the current ambient temperature (typically on the warmer side)
* Pause Updates - Conserve battery life by pausing weather updates when you're sleeping (user definiable start & end times)
* Battery Meter - Perfectly balanced, the battery meter is nested between the time and weather
* WiFi Scanning - Configure your most used WiFi access points to maintain connectivity, Home, Work, School, etc.

## Configuration
Admittedly, there's quite a bit to configure with this (and future) watch face(s). These required configurations have comment descriptions in the source code. Below are the most critical settings that need to be configured in order to run this watch face:

### Weather
##### API KEY
In order for the watchy to receive weather upates, you'll need an API Key from [OpenWeatherMap.org](https://openweathermap.org/appid) which is completely free. I've included SQFMI's key which is enabled by default. Using this key is not recommended as it will cease to function when minute/daily limits are reached, or if SQFMI simply deletes it. Add your API Key to the `APIKEY` definition.

#### City Name or ID
Weather for your location is limited to one area and is defined by entering your city name where defined in the source code under `CITY`. If your city name is used in other states or provinces, you can also use your city code by looking up a city on openweathermap.org, it'll take you to a page like "https://openweathermap.org/city/4574324". Copy those numbers (ex 4574324) on the end and put them into `CITY_ID` between the quotes. You'll also have to define `COUNTRY` and `TEMP`. `TEMP` is used to determine if Imperial temperature is displayed.

#### Pausing Weather Updates
It's possible to pause weather updates when the watch is not in use, i.e. when you're sleeping. By default, its set to pause 30 minutes after midnight, and resume updates at 5:30am. These can be changed by modifying the `pauseStart` and `pauseEnd` strings. Setting both strings to the same time will disable the pause updates feature. Pause start and end times must be written in the 24 hour format.

When updates are paused, the weather icon will be represented by a sleeping RTC icon and ambient temperature will be used instead of live weather.

## NTP
#### Timezone
NTP syncs require that you define your timezone, `TIMEZONE_STRING` which can be found [using this resource link](https://github.com/nayarsystems/posix_tz_db/blob/master/zones.json). Use the example in the source to determine what is required. 

#### NTP Servers
By default, the NTP server tried first is a pool of servers that should automatically find the best match based on your location. You can leave `NTP_SERVER_1` as-is, or specify NTP servers. `NTP_SERVER_2` and `NTP_SERVER_3` are US based and should be changed to a local server if outside of the US.

#### Syncing
NTP Syncs happen twice a day, once at Noon and once at Midnight. This can be changed by modifying `NTP_TIMER`.
