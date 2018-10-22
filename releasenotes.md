# ESDL Release Notes

## Release v1810 \([link](https://github.com/EnergyTransition/ESDL/releases/tag/v1810)\)

* ESDL version has been removed from namespace (was sometimes causing problems with code generation)
* Added MeasuresCollection (e.g. to group different renovation options for buildings)
* Added Sectors (and references from Asset and Party)
* Added ControlStrategy
* Added EnergyMarkets
* Added different Assets: WaterToPower (with types hydro, waves, osmosis, tidal), PVInstallation (with types roof, building integrated, road, field, ...) and WindTurbine types (sea, land, coast, roof), GasConversion, Electrolyzer types (PEM, alkaline, SOEC)
* Changed the way EnergyPotentials are modeled (now grouped per type)
* Restructured the subclasses of Transport
* Renamed KPIList to KPIs

## Release v180901 \([link](https://github.com/EnergyTransition/ESDL/releases/tag/v180901)\)

* Added KPIs to areas
* Added new way of describing Quantities and Units (now only used in profiles, kpis and energy carriers)
* Added possibility to add a DataSource to an asset, profile and so on, without the need for an EnergySystem
* Added ResidualHeatSourcePotential to list of possible Potentials

## Release v1809 \([link](https://github.com/EnergyTransition/ESDL/releases/tag/v1809)\)

* Added assets (GasStorage, Electrolyzer)
* Changed name of asset SinkProducer to SourceProducer
* Added buildingDensity parameter to Area

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

* Initial public release

