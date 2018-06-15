# Items, Assets, EnergyAssets and Services

## Items

The Item class represents an abstract item. Items can have an id, a name, a short name and a description.  The following classes are derived from the item class:

* Assets: an Asset is an Item with a physical representation. 
* Services: A Service is a logical Item.

## Assets

Assets are all physical items in the EnergySystem. Assets can have a location, a geometry, commisioning and decommissioning dates, cost information \(investment, installation and operation and maintenance costs\).

Assets are contained by Areas.

## EnergyAssets

An EnergyAsset is an Asset with one or more ports allowing to model connections between assets.

The EnergyAsset class is subdivided into 5 categories:

* ProductionAsset: e.g. wind turbine, solar panel, geothermal source
* ConsumptionAsset: e.g. electricity demand, heat demand, gas demand
* StorageAsset: e.g. battery, buffer
* TransportAsset: e.g. electricity network, gas network, cable, pipe, transformer, heat exchange
* ConversionAsset: e.g. gasheater, heatpump, power plant, CHP, fuel cell

## Services

Example Services are demand response services and aggregator services.

