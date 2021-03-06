# time-zone-server

This is a Node.js server which gives back the local time anywhere in the world, given a Unix Style location
as input, e.g. 'Europe/Zurich'.

A full list of supported time zones is available at: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones



#API:

##GET /getTime/area/location
##GET /getTime/area/location/city

Gets the local time right now for the given TZ style input area and city n the format "yyyymmdd HHMMSS"

    curl http://localhost:3000/GetTime/Europe/Berlin
    2016,04,18,15,56,08


##GET /getTimeZone/area/location
##GET /getTimeZone/area/location/city

Gets the short time zone for the given area/city, e.g.  CET, CEST, EST

    curl http://localhost:3000/GetTimeZone/Europe/Berlin
    CEST


##GET /getTimeOffset/area/location
##GET /getTimeOffset/area/location/city

Gets the current offset to GMT for the given area/city, e.g. GMT+0200

    curl http://localhost:3000/GetTimeOffset/Europe/Berlin
    GMT+0200


##GET /getTimeRaw/area/location
##GET /getTimeRaw/area/location/city

Returns the internal date representation, intended for debugging only

    curl http://localhost:3000/GetTimeRaw/Europe/Berlin
    Tue Apr 19 2016 09:47:30 GMT+0200 (CEST)


#Running on a local server
Install Node.js, there are a lot of references about how to do this. Google it.

Get/build the dependencies

    npm install

Execute

    node time-zone-service.js

#Running on Cloud Foundry
Even easier:

Create the zip file from the root of the repository you cloned:

    zip -r time-zone-service.zip *

Push the service

    cf push time-zone-server -b nodejs_buildpack -m 256m -p time-zone-service.zip -i 1 -c "node time-zone-service.js"
