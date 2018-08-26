# Profiles

ESDL support many different types of profiles. Next to this ESDL uses profiles for different applications.

Currently ESDL uses profiles for:
- describing energy consumption and production at ports of EnergyAssets
- Describing solar irradiance or wind speeds over time
- Describing historic, current and expexted costs for EnergyCarriers or Commodities (e.g. expected electricity price developments)
- Describing costs for EnergyAssets (cost developments of a HeatPump for the coming 30 years). These costs are divided into investment costs, installation costs and operation and maintenance costs)

ESDL supports the following types of profiles:
- `DateTimeProfile`: Allows to specify a range of values with timestamps.
- `SingleValue`: Allows to specify a single value for a parameter
- `Range`: Allows to specify a range of possible values between minValue and maxValue.
- `URIProfile`: Allows to refer to a URI for a profile 
- `InfluxDBProfile`: Allows to refer to a profile in an InfluxDB database
- `ReferenceProfile`: Allows to refer to a profile in the `Profile` collection class.

## DateTimeProfile

The `DateTimeProfile` is a collection of values each annotated with a starting time (`from`) and optionally an end time (`to`). When only a starting time is specified, the value is valid until the starting time of the next value in the profile. 
So, the value of the last item in the profile, is valid for the rest of the time (basically forever). If you want to specify a value for a certain bounded time period, you must specify the `end` time.

## InfluxDBProfile

The `InfluxDBProfile` allows to refer to a profile in an InfluxDB database. 

It requires the following parameters:
- `host`: the hostname of the database server
- `port`: the port on which the InfluxDB server is running
- `database`: the name of the database that contains the profiles
- `measurement`: the name of the measurement that contains the profile data
- `field`: the name of the field that contains the profile values
