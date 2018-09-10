# ESDL Release Notes

## Release v1808 \([link](https://github.com/EnergyTransition/ESDL/releases/tag/v1808)\)

* Merged Commodities and EnergyCarriers lists into Carriers list
* Removed commodities enumeration from ports
* Added mobility concepts to ESDL \(Mobility demand per vehicle type and fuel type, fuel efficiency per vehicle type, number of vehicles per area\)
* Improved the Geometry classes \(added MultiPolygon\)
* Added assets \(ResidualHeatSource, MobilityDemand, SolarCollector, FermentationPlant\)
* Added residual heat source potential
* Added Parties class to model ownership
* Added DataSources class to list sources of used data in an ESDL model
* Added Profiles class and ReferenceProfile class to enable reuse of profiles
* Measures is an Asset collection instead of an Item collection \(to ease development of ESDL designer\)

## Release v1807a \([link](https://github.com/EnergyTransition/ESDL/releases/tag/v1807a)\)

* Generated proper XSD, the v1807 release still contained the v1806 XSD

## Release v1807 \([link](https://github.com/EnergyTransition/ESDL/releases/tag/v1807)\)

* Added 'UNDEFINED' and 'ENERGY' to CommodityEnum
* Renamed some assets:
  * HeatPipe --&gt; Pipe
  * HeatDemand --&gt; HeatingDemand
  * CoolDemand --&gt; CoolingDemand

## Release v1806 \([link](https://github.com/EnergyTransition/ESDL/releases/tag/v1806)\)

* Initial release

