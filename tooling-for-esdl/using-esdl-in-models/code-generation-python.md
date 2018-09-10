# Integration with Python

## Introduction

Using the [`generateDS`](https://www.davekuhlman.org/generateDS.html) tool with the XSD generated from the ESDL model, you can generate Python code to work with ESDL. The generated code contains the python classes for each ESDL concept and contains functionality to instantiate a new model, add assets to it, read an ESDL description from disk or save one.

## Generate the XSD from the ESDL model

The ESDL GitHub project contains the XML schema definition \(XSD\) file in the `model` subdirectory.

To generate a new XSD from an updated ESDL model, right click the `esdl.genmodel` file and select the 'Export model...' option from the drop down menu. In the wizard select the 'XML Schema' model exporter and follow the steps in the wizard to create the XSD.

## Create Python classes using GenerateDS

The GenerateDS project provides us with a tool to generate Python data structures and an XML parser from an XML schema definition \(XSD\).

You can find the GenerateDS project [here](https://pypi.org/project/generateDS/).

Install generateDS with `pip install generateDS` to add it to your python libraries

Using the following command, you can create the python code from the XSD file:

```text
generateDS -o esdl.py .\esdl\EsdlXML.xsd
```

## Using the generated Python code

Use the following code to load an ESDL-file:

```python
def load_energy_system(inpath):
    with open(inpath, 'r') as infile:
        # parse esdl file
        es = esdl.parse(infile, silence=False)
        return es
        
es = load_energy_system('Amsterdam.esdl')
# get all assets of an area within the energy system (use 1st instance only)
assets = energy_system.get_instance()[0].get_area().get_asset()
print(assets)


```

