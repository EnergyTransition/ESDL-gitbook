# Energy Data Modelling

In order to fully understand how an energy system operates and how it can evolve, multiple types of information needs to be combined.  Information on how and where the energy system is installed, what the installed base is, what the evolution potential is and how the energy system is used all form a part of the puzzle. This chapter describes these different types of data, a description on how they can be combined and modelled in ESDL follows in the next chapters.

## Energy System Registration

The first type of information is named the ‘energy system registration’, this is geo-oriented data that contains information such as: buildings characteristics, installed base of energy consuming/producing/converting appliances and topologies and other characteristics of energy transportation networks.

## Energy System Potential

The second type of information is the ‘energy system potential’.  This information is also typically geo-oriented and describes the potential and constraints of the energy system to evolve. For example information about: areas where wind turbines can be installed, areas where geothermal sources can be found and areas that are suitable for district heating \(heat networks\).

![](Images/Dutch%20Geo%20Potential.JPG)

## Energy System Usage

The third type of information is ‘energy system usage’. This type of information is providing insight on how the energy system is used over time. Typically this results in profiles or measurements for a certain duration of time. Examples of this information are: yearly energy consumption of a building, a profile of the production of a PV panel and a profile of the usage of a heat pump. This information describes the dynamic behaviour of the energy system.

![](Images/Repository%20Data.JPG)

## Combining data

To fully understand how a certain energy system is functioning and can evolve, the 3 types of information states in the sections above should be combined. Typically a source of energy data provides information within the scope of one of the types.  ESDL provides the means to model these three aspects of the energy system in one common language and reason more powerful on the combined data.

