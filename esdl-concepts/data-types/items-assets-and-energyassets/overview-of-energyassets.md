# Overview of EnergyAssets

All asset classes have a Generic and a Aggregated version, e.g. GenericProducer and AggregatedProducer. The Generic version can be used if no specific class is available or required. This can only be used when no specific parameters are required. In some examples only the presence of the asset is enough information. The Aggregated version can be used when the asset is a reprensentation of more than one physical assets. Aggregated assets also allow to specify the links to the individual assets it represents \(For this purpose more instances within one energysystem can be used, one instance with the individual assets and a second instance with the aggregated versions\).

## Producer Assets

Currently the following producer assets exist:

* PVPanel: Represents an individual PV panel
* PVInstallation: Represents an installation of PV panels on a roof, road, water, or building-integrated.
* PVParc: Represents a PV parc.
* SolarCollector: Represents an individual solar collector or an installation of solar collector panels.
* WindTurbine: Represents an individual windturbinbe.
* WindParc: Represents a Wind parc \(on sea or on land\).
* GeothermalSource: Represents a geothermal source producing heat or electricity.
* SourceProducer: Represents an unlimited source of energy, that can be used to represent the network outside the scope of the energysystem being described.
* ResidualHeatSource: Represents residual heat sources from data centers, industry or cooling houses.
* WaterToPower: Represents an installation that generates energy from water using different techniques \(hydro power, wave power, tidal power, or osmotic power\)

New producer assets will be added in future.

## Consumer Assets

Currently the following consumer assets exist:

* ElectricityDemand: Represents the electricity demand of a house, group of buildings, sector, area or country.
* GasDemand: Represents the gas demand of a house, group of buildings, sector, area or country.
* HeatingDemand: Represents the heating demand of a house, group of buildings, sector, area or country.
* CoolingDemand: Represents the cooling demand of a house, group of buildings, sector, area or country.
* EnergyDemand: Represents the energy demand of a house, group of buildings, sector, area or country. It can be used in describing the energybalance of a region for example.
* Losses: Represents the losses in an energy system. 
* EVChargingStation: Represents the electricity consumption of an EV charging station.
* SinkConsumer: Represents an unlimited sink of energy, that can be used to represent the network outside the scope of the energysystem being described.
* MobilityDemand: Represents the energy demand of the mobility sector. Can be used to represent total demand or specify a demand per vehicle type and/or fuel type.

New consumer assets will be added in future.

## Storage Assets

Currently the following storage assets exist:

* Battery: Represents an electrical battery to store electricity.
* HeatStorage: Represents a water buffer to store heat \(or cold\).
* GasStorage: Represents a tank to store gas.

New storage assets will be added in future \(aquifer storage\).

## Transport Assets

Currently the following transport assets exist:

* ElectricityNetwork: Represents an electricity network \(on any scale, from an inhouse network, to the national scale electricity network.
* EConnection: Represents the connection to a electricity network \(including the electricity meter\).
* ElectricityCable: Represents an individual cable in a network \(if you want to describe a detailed topology\).
* Transformer: Represents a electric transformer \(station\) to connect two networks with different voltage levels.
* CircuitBraker: Represents a electric circuit braker \(switch\)
* HeatNetwork: Represents a \(district\) heat network.
* HConnection: Represents the connection to a heat network.
* HeatExchange: Represents a heat exchange to connect two heat networks.
* HeatPipe: Represents an indivual pipe \(if you want to describe a detailed topology\).
* Pump: Represents a pump to generate a flow of water in a pipe or network.
* Valve: Represents a valve to control water flow.
* GasNetwork: Represents a gas network.
* GConnection: Represents the connection to a gas network \(including the gas meter\).
* EnergyNetwork: Represents an \(abstract\) energy network \(for describing energy balance\).

New transport assets will be added in future.

## Conversion Assets

Currently the following converion assets exist:

* GasHeater: Represents a gas heater.
* HeatPump: Represents a heat pump \(e.g. air-water, connected to an aquifer, using surface water, as a booster pump\)
* CHP: Represents a CHP \(Combined Heat and Power\) to generate electricity and useful heat simultaneously.
* FuelCell: Represents a fuel cell, that generates electricity \(and possibly heat\) using a certain fuel \(H2 for example\).
* PowerPlant: Represents a power plant, using for example coal, gas or uranium to produce electricity \(residual heat can be delieverd to a heat network\). 
* Airco: Represents an airconditioner. 
* FermentationPlant: Represents a fermentation plant.
* BiomassHeater: Represents a heating installation that is using biomass.
* GasConversion: Represents an installation that converts one gas to another \(e.g. H2 generation from methane\).
* PowerToX: Represents a generic power-to-X installation \(can be used when no specific option exists\).
* XToPower: Represents a generic X-to-power installation \(can be used when no specific option exists\).
* Electrolyzer: Represents an electrolyzer generating H2 from electricity.

New conversion assets will be added in future.

