# Overview of EnergyAssets \(TODO\)

All asset classes have a Generic and a Aggregated version, e.g. GenericProducer and AggregatedProducer. The Generic version can be used if no specific class is available or required. This can only be used when no specific parameters are required. In some examples only the presence of the asset is enough information. The Aggregated version can be used when the asset is a reprensentation of more than one physical assets. Aggregated assets also allow to specify the links to the individual assets it represents \(For this purpose more instances within one energysystem can be used, one instance with the individual assets and a second instance with the aggregated versions\).

## Producer Assets

Currently the following producer assets exist:

* PVPanel
* PVParc
* WindTurbine
* WindParc
* GeothermalSource
* SinkProducer

New producer assets will be added in future.

## Consumer Assets

Currently the following consumer assets exist:

* ElectricityDemand
* GasDemand
* HeatingDemand
* CoolingDemand
* Losses
* EVChargingStation
* SinkConsumer

New consumer assets will be added in future.

## Storage Assets

Currently the following storage assets exist:

* Battery
* HeatStorage

New storage assets will be added in future \(aquifer storage\).

## Transport Assets

Currently the following transport assets exist:

* ElectricityNetwork
* EConnection
* ElectricityCable
* Transformer
* HeatNetwork
* HConnection
* HeatExchange
* HeatPipe
* Pump
* Valve
* GasNetwork
* GConnection

New transport assets will be added in future.

## Conversion Assets

Currently the following converion assets exist:

* GasHeater
* HeatPump
* CHP
* FuelCell
* PowerPlant
* Airco

New conversion assets will be added in future.

