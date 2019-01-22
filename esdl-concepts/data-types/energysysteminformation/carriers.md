## Carriers

ESDL allows you to describe a list of carriers with parameters that are used inside your model

There are two types of carriers:
- Commodities
- Energy carriers

They serve different purposes but can be combined in the same model if required. Choices depend on the scope of the model.

The `Carriers` class is a collection of the abstract class `Carrier`. The `Carrier` class can have the following parameters:
- an `id` paramater that is used for referring to carriers.
- a `name` parameter to describe the name of the carrier.
- a `cost` paramater of type GenericProfile (allows both a fixed value as a profile that changes over time).
- a `dataSource` parameter to document the origin of the information you're using

The `Commodity` and `EnergyCarrier` classes are subclasses of `Carrier`.

# Commodity

The `Commodity` class is an abstract class, with the following subclasses:
- ElectricityCommodity: can be used for electricity. If required a distinction between different voltage levels can be made (LV, MV, HV, ...). A `voltage` parameter can be specified.
- GasCommodity: can be used for natural gas, biogas, carbon dioxide (CO2), hydrogen (H2), and so on. Distinction is done based on the `name` parameter.
- HeatCommodity: can be used for heat. If required a distinction between different temperature levels can be made (LT, MT, HT, ...). A `temperature` parameter can be specified. 
- EnergyCommodity: can be used for describing energy balances (expressed in Joules, independent of the specific commodity).

# EnergyCarrier

This class is based on the [list of energy carriers](https://www.rvo.nl/sites/default/files/2018/03/Nederlandse%20energiedragerlijst%202018.pdf) as published by RVO

The `EnergyCarrier` class has the following parameters:
- an `energyContent` parameter: allows the specification of the energy content of the energy carrier
- an `energyContentUnit` parameter: the unit of the `energyContent` paramater
- an `emission` parameter: allows the specification of emission values per energy content
- an `emissionUnit` parameter: the unit of the `emission` parameter
- an `energyCarrierType` parameter: an enumeration with options `UNDEFINED`, `RENEWABLE`, `FOSSIL`
- a `stateOfMatter` parameter: an enumeration with options `UNDEFINED`, `SOLID`, `LIQUID`, `GASEOUS`
