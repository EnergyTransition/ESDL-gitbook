# Data types

ESDL contains several first-class data types that are used in each ESDL-file. This section describes these data types.

#### EnergySystem

This is the entry point of an ESDL-file: every ESDL-file starts with a definition of an Energy System.  
[EnergySystem](energy-system.md). An Energy System contain Instances, EnergySystemInformation, Measures, Parties and Potentials.

#### Area

An area allows for grouping Assets and Buildings and other Area's. Since real Energy Systems have a physical representation, Area scope the given Energy System by this physical boundary. Every Energy System describes at least one Area.  
[Area](areas.md)

#### Items, Assets, EnergyAssets and Services

While Items represent logical things \(both Assets and Services\) in an Energy System, Assets represent physical things of an Energy System. Assets can be specialized into Buildings and in EnergyAssets. The difference between an EnergyAsset and an Item or Building is that Energy Assets contain ports and these ports allow them to connect to other EnergyAssets, allowing to create a network \(graph\) of how the energy system is connected.  
EnergyAssets themselfs are specialized into the five ESDL categories: Producer, Consumer, Storage, Transport and Conversion.

[Items, Assets, EnergyAssets and Services](items-assets-and-energyassets/)  
[Overview of EnergyAssets](items-assets-and-energyassets/overview-of-energyassets.md)

#### Profiles

Profiles are used to model values in ESDL. ESDL suports different types of values, such as single values, time ranges, time series, etd. E.g. the total consumption of energy in a municipality is 50PJ. The price of a HeatPump is 8000 euro. These values can be stored in a profile called 'SingleValue' as they contain only one value.   
In many applications, e.g. simulations, ranges of values are required as input, that are mostly time indexed. These timeseries-based values can be stored in DateTimeProfiles.   
Profiles are used to define information about the energy system as a whole \(e.g. the price-index of 2017, APEX energy prices of 2015-2017\). The Energy System Information part of an EnergySystem can be used for that.  
Profiles can also be used for specifying e.g. the electricity demand of a household. For that a profile with this demand can be attached to a port of the ElectricityDemand class.

* [Profiles](profiles.md)

