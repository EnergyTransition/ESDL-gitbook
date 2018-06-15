# Energy System

The EnergySystem class will be the place to start if you want to model an energy system for a certain region.

An EnergySystem contains the following information:

* Instances
* Potentials
* Measures
* Parties
* EnergySystemInformation

## Instances

An EnergySystem can contain zero or more Instances. Instances are used to represent different representations of the **same** EnergySystem. Most of the times only one Instance will be used. The primary use case for having more than one Instance is when you have different aggregations of the same EnergySystem in the same model \(e.g. the same region on house level and aggregated on neighbourhood level\).

Instances can contain an Area. The Area is the class to represent a geographical or logical area. An Area contains all assets in that area or can be subdivided into more Areas

## Potentials

Potentials can be used to describe all different kinds of energy potentials. Examples of potentials are:

* GeothermalPotential: to describe the potential for geothermal energy
* WindPotential: to describe the potential for wind turbines
* SolarPotential: to describe the potential for solar PV fields
* LegalArea: to describe for example areas where no aquifers are allowed because the underground water is used for drinking water \(a negative potential\).

## Measures

Measures can be used to describe possible assets that can be installed in the EnergySystem \(e.g. added by a model calculating minimum investments required to match future demands\).

## Parties

Parties can be used if you want to model ownership of assets

## EnergySystemInformation

The EnergySystemInformation class is a container for additional information about the EnergySystem in general.

Currently the following information can be added:

* AvailableEnergyCarriers: list of available energy carriers with information about energy content and CO2 emissions. Power plants typically refer to energy carriers to indicate what the source of their energy is.
* EnergyPrices: prices for gas, electricity

 

