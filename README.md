PiSensor
=============
NodeJS server for the DS18B20 temperature sensors on the Raspberry Pi.

Description
-----------
* A NodeJS server for the DS18B20 GPIO temperature sensor on the Raspberry Pi.
* The sensor is accessed using the w1-gpio and w1-therm kernel modules in the Raspbian distro.
* The server parses data from the sensor and returns the temperature and a Unix time-stamp in JSON format, this is then written to an SQLite database on the Pi.
* Simple front-end is included and served using node-static, which performs ajax calls to the server/database and plots temperature in real time or from a time-series, using the highcharts JavaScript library.

Files
-----
* load_gpio.sh - bash commands to load kernel modules
* server.js - NodeJS server, returns temperature as JSON, logs to database and serves other static files
* temperature_plot.htm - example client front-end showing live temperatures
* temperature_log.htm - example client front-end showing time-series from database records
* build_database.sh - shell script to create database schema
* sample_database.db - example database with real world data from the Pi recorded in UK Jan-Feb 2013

Dependencies
------------
* NodeJS
* SQLite3
* node-sqlite3
* node-static

Install/Setup
-------------
1. Run `npm install` in this directory
2. Run `load_gpio.sh` script as root to load kernel modules for the sensor
3. Run the `build_database.sh` script to create "piTemps.db". Note this wil drop any existing database of the same name in the directory
4. Open "server.js" and edit line 35 to read the serial number of your sensor in /sys/bus.
5. In a terminal run "node server.js" to start the server.
6. Open a web browser on the Pi and go to http://localhost:8000/temperature_plot.htm to see a plot of current temperature. Go to http://localhost:8000/temperature_log.htm to see a plot of logged temperature. 

References
----------
* [RaspberryPi DS tutorial](http://www.cl.cam.ac.uk/freshers/raspberrypi/tutorials/temperature/)
* [PiThermServer](https://github.com/talltom/PiThermServer)


