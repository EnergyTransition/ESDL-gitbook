# How to use ESDL

The possible applications of ESDL are endless. This chapter gives some guidelines of how to use the ESDL language.

## Models and descriptions \(TODO\)

...

## Different levels of abstraction and scopes

ESDL is a very generic energy modelling language. It can be used to describe energy related systems with very different abstration levels or scopes:

* describe an individual house or a street of houses with their interconnection. For each house the electricity, heating and/or cooling demand can be described and the present assets \(heatpump, gasheater, in house battery, rooftop PV, EV charging stations\). Also different house parameters can be described \(insulation parameters, energy label, areas of walls/windows/roofs, type of roof \(slanted or flat roof\)\).
* describe a city with different districts, where buildings are clustered as aggregated buildings. Each district has its own characteristics \(type of houses, building periods\) and possible renewable energy solutions. Some districts are suited for a district heating network solution, others are suited for an all-electric approach.
* describe a region with the energy demand of different sectors \(e.g. industry, agriculture, residential, businesses\), including the installed production assets, and available renewable production and energy storage options.
* describe the energy balance of a country, indicating imports and exports of energy.
* describe the electricy production facilities in the country including the flow of 'supply materials' \(coal, gas, oil\).

It can also be used to describe all kinds of energy related \(open\) data, either to publish data for use by others or to document assumptions taken into account in a model or calculation. The following list provides some example applications:

* standard energy profiles \(with consumption levels for every 5 minutes\).
* CO2 emission data for different energy carriers.
* historic, current or predicted fuel prices.
* yearly profile for solar irradiance \(or wind speeds\) for a certain region.
* data sheets for different components in the energysystem \(with specific parameter values\).
* expected prices for energy assets for the coming 30 years \(what will a heat pump cost in 2040\).
* geographic data: potential geothermal energy in the underground, total electricity consumption per municipality for a whole country.
* distribution of energy labels over all houses in the city.

## Geographic and non-geographic models

ESDL can be used for geographic models and non-geographic models. Geographic models contain physical shapes and locations for all assets in the energysystem. It will mostly be used for describing a specific actual existing region and its future \(or historic\) developments. Non-geographic models do not contain locations and can be used to describe some commonly available configurations of energysystems without denoting a specific one, e.g. city centers with mainly old houses or an energy neutral house that is fully self sufficient.

## Start with \(TODO\):

Depending on the application, you can start your ESDL model with:

* EnergySystem
* Carriers
* Profiles
* House
* an Asset template

