# Integration with Python and pyEcore

### Introduction

There are currently two ways to create and build Energy Systems with Python. The first is to use the XSD created from the Ecore model and use an XSD to Python class generator to generate python classes. There are a few generators available, but we have useful result with `generateDS`. You can read [here ](https://energytransition.gitbook.io/esdl/tooling-for-esdl/using-esdl-in-models/code-generation-python)more for this approach. 

An alternative is using `pyEcore`. [PyEcore ](https://github.com/pyecore/pyecore)is the python equivalent of the Eclipse EMF Ecore implementation. This means that the ESDL meta-model is at runtime available to you for reading, writing and changing ESDL instances. This section provides some examples to use pyEcore to do just that. PyEcore offers two ways:

* Using a dynamic instance of the model. This means that at runtime the Ecore-model is read and Python classes are dynamically instantiated.
* Using a static instance of the model. This means that you first generate Python classes from the Ecore model \(similar to the XSD-approach\) and import these in your project.

The pyEcore approach provides some benefits above the XSD approach:

* In the transformation from Ecore to XSD, some information is lost, which makes validation more difficult.
* Assigning a value to a cross-reference will automatically set the `eOpposite()` of it, e.g. in the case of the `connectedTo` reference of a `Port`
* Type checking when assigning values to e.g. a reference or a primitive type.
* Since pyEcore is using the ESDL Ecore model as a basis and can create a dynamic instance of the model at runtime, there is no need for generating files/classes before you can use a new version of the core model. Especially during development of the ESDL ecore model this approach is convenient. The downside is that auto completion in the IDE \(e.g. PyCharm\) is not available.
* All Python objects created for ESDL \(both dynamic and static\) inherit from the `EClass` class \(similar to the Java generated files\). This means that you can query the meta model at runtime and get e.g. the contents of the class using `eclass.eContents`. Also notification support is available, if your code needs to know when parts of the model are changed. See the pyEcore documentation at [https://pyecore.readthedocs.io/en/latest/user/quickstart.html](https://pyecore.readthedocs.io/en/latest/user/quickstart.html) for more information and features.

Currently pyEcore support the XMI format for storing models and model instances. As ESDL is currently not using the XMI features, but only the XMLResource in the plugins, you need to register esdl-files with the XMLResource, otherwise the XMI namespace and the XMI version information is added to the ESDL-file when saving, giving errors when loading this file in Eclipse with the ESDL plugins. To use XMLResources you need to download the file attached at the end of this page and import it in your project \(as done in all the examples below\).

## Prerequisites

You can install pyecore and pyecoregen using pip

```text
pip install pyecore
pip install pyecoregen
```

## Using dynamic instances to work with ESDL files

Creating and storing an ESDL file using dynamic instances can then be done as follows.  
_Note_ that there is no need to generated classes first, nor clone the ESDL-repository on github, as the ESDL Ecore model is automatically downloaded from github.

### Creating and storing Energy Systems

```python
from pyecore.resources import ResourceSet, URI
from pyecore.utils import DynamicEPackage
from pyecore.resources.resource import HttpURI
from xmlresource import XMLResource

def main():
    # create a resourceSet that hold the contents of the esdl.ecore model and the instances we use/create
    rset = ResourceSet()
    # Assign files with the .esdl extension to the XMLResource instead of default XMI
    rset.resource_factory['esdl'] = lambda uri: XMLResource(uri)  
    # Read the lastest esdl.ecore from github
    resource = rset.get_resource(HttpURI('https://raw.githubusercontent.com/EnergyTransition/ESDL/master/esdl/model/esdl.ecore'))
    esdl_model = resource.contents[0]    
    rset.metamodel_registry[esdl_model.nsURI] = esdl_model
    # Create a dynamic model from the loaded esdl.ecore model, which we can use to build Energy Systems
    esdl = DynamicEPackage(esdl_model)
    
    es = esdl.EnergySystem(name="Test energy system")
    es.instance.append( esdl.Instance(name="My new instance"))
    es.instance[0].area = esdl.Area(name="My area")
    pvpark = esdl.PVPark(name="PV park")
    ed = esdl.ElectricityDemand(name="E demand")
    es.instance[0].area.asset.append(pvpark)
    es.instance[0].area.asset.append(ed)
    inPort = esdl.InPort(id='inPort1')
    ed.port.append(inPort)
    outPort = esdl.OutPort(id='outPort1')
    outPort.connectedTo.append(inPort)
    pvpark.port.append(outPort)
    
    print("Energy system(name={}), {}".format(es.name, dir(es))) 
    print("OutPort connectedTo: {}".format(outPort.connectedTo))
    print("InPort connectedTo: {}".format(inPort.connectedTo))
    # Create a new resource to hold the Energy System instance we just created, in the context of the previous created resourceSet that holds our ESDL model
    resource = rset.create_resource(URI('Dynamic_instance.esdl'))
    # Append the energy system to the resource
    resource.append(es)
    # Save the resource
    resource.save()

if __name__ == '__main__': 
    main()
```

### Loading ESDL models

Loading an ESDL instance is as follows:

```python
from pyecore.resources import ResourceSet, URI
from pyecore.utils import DynamicEPackage
from pyecore.resources.resource import HttpURI
from xmlresource import XMLResource


def main():
    # create a resourceSet that hold the contents of the esdl.ecore model and the instances we use/create
    rset = ResourceSet()
    # Assign files with the .esdl extension to the XMLResource instead of default XMI
    rset.resource_factory['esdl'] = lambda uri: XMLResource(uri)  

    # Read the lastest esdl.ecore from github
    resource = rset.get_resource(HttpURI('https://raw.githubusercontent.com/EnergyTransition/ESDL/master/esdl/model/esdl.ecore'))
    esdl_model = resource.contents[0]
    print('Namespace: {}'.format(esdl_model.nsURI))
    rset.metamodel_registry[esdl_model.nsURI] = esdl_model
    # Create a dynamic model from the loaded esdl.ecore model, which we can use to build Energy Systems
    esdl = DynamicEPackage(esdl_model)
    resource = rset.get_resource(URI('test.esdl'))
    es = resource.contents[0]
    # At this point, the model instance is loaded!

    # Now the model can be manipulated, e.g. add a PowerToX asset to the area.
    print(es.name)
    print(es.instance[0].area.asset)
    es.instance[0].area.asset.append(esdl.PowerToX(name='Power to Heat', id='powerToH'))
    print(es.instance[0].area.asset)
    # print a list of all the classes of the instance
    for child in es.eAllContents():
        print(attr_to_dict(child))
    # Save the result in the same file
    resource.save()

if __name__ == '__main__': 
    main()

```

## Using the generated classes to create ESDL

To have the Python classes available offline and use auto-completion in your favorite Python Editor, PyEcoreGen can be used to generate the ESDL-classes from the `esdl.ecore` model. On the command line do the following:  
`$ pyecoregen -e https://raw.githubusercontent.com/EnergyTransition/ESDL/master/esdl/model/esdl.ecore -o . --auto-register-package`

This creates an `esdl/`folder and and `esdl.py` that contain all the classes from the ESDL model. More information about pyEcoreGen can be found [here](https://github.com/pyecore/pyecoregen).

There is also an alternative way to generate classes programmatically by executing the following code:

```python
from pyecoregen.ecore import EcoreGenerator
from pyecore.resources import ResourceSet
from pyecore.resources.resource import HttpURI

# Load the ESDL model from GitHub
rset = ResourceSet()
resource = rset.get_resource(HttpURI('https://raw.githubusercontent.com/EnergyTransition/ESDL/master/esdl/model/esdl.ecore'))
esdl_model = resource.contents[0]

# Generate the classes
generator = EcoreGenerator()
generator.generate(esdl_model, ".")
```

### Loading ESDL files using the generated Python classes

Use the following code to use the generated classes in your Python code:

```python
from pyecore.resources import ResourceSet, URI 
from esdl.esdl import * 
import esdl 
from xmlresource import XMLResource

def main():
    # create a resourceSet that hold the contents of the esdl.ecore model and the instances we use/create
    rset = ResourceSet()
    # Assign files with the .esdl extension to the XMLResource instead of default XMI
    rset.resource_factory['esdl'] = lambda uri: XMLResource(uri)  # we register the factory for '.esdl' extension and XML serialization
    # Load the ESDL model in memory
    resource = rset.get_resource(HttpURI('https://raw.githubusercontent.com/EnergyTransition/ESDL/master/esdl/model/esdl.ecore'))
    # and register that model in the meta model registry
    rset.metamodel_registry[esdl.nsURI] = esdl
    # load the ESDL file
    resource = rset.get_resource(HttpURI('https://github.com/EnergyTransition/ESDL-municipality-example/raw/master/ESDL_example_with_municipality_potential_and_measures-new.xmi'))
    # Get the Energy System as root object from the resource
    es = resource.contents[0]
    # EnergySystem is now loaded into 'es' and can be manipulated, e.g. print it.
    print(attr_to_dict(es))
    
if __name__ == '__main__': 
    main()
```

### Show attributes and their values of Python classes

When you try to `print()` e.g. an Energy System, you see something like:  
`print(es)` you get the following information that does not show the attributes of the EnergySystem, but that it is an object of type esdl.esdl.EnergySystem at a certain memory location:  
`<esdl.esdl.EnergySystem object at 0x000002A66FE60390>`   
A convenient method to print the results of an object is the following code. That code creates a dictionary from the EClass with all its attributes and their values. 

```python
def attr_to_dict(eobj):
    d = dict()
    d['eClass'] = eobj.eClass.__name__
    for attr in dir(eobj):
        attr_value = eobj.eGet(attr)
        if attr_value is not None: 
            d[attr] = eobj.eGet(attr)
    return d
```

If you now do a`print(attr_to_dict(es))` you get the following output for the [Municipality Example found here](https://github.com/EnergyTransition/ESDL-municipality-example):

```javascript
{
 'eClass': 'EnergySystem', 
 'description': 'Voorbeeld voor ESDL beschrijving van een gemeente op een redelijk hoog abstractieniveau', 
 'energySystemInformation': <esdl.esdl.EnergySystemInformation object at 0x0000013E54788D68>, 
 'instance': EOrderedSet([<esdl.esdl.Instance object at 0x0000013E5474EF98>]), 
 'measures': <esdl.esdl.Measures object at 0x0000013E5474EDD8>, 
 'name': 'ESDL Voorbeeld Gemeente XXX', 
 'parties': <esdl.esdl.Parties object at 0x0000013E54792E80>, 
 'potentials': <esdl.esdl.Potentials object at 0x0000013E54755978>, 
 'sector': EOrderedSet([GEBOUWDE_OMGEVING=1])
}

```

You can also change the `__repr__` of the classes, e.g. by changing the `__repr__` of the python\_class attribute, e.g. `EnergySystem.python_class.__repr__ = lambda x: 'EnergySystem(name={})'.format(x.name)`

### Manipulating and saving ESDL files

The following example lets you create and save Energy Systems using the generated ESDL classes:

```python
from pyecore.resources import ResourceSet, URI
from esdl.esdl import *
import esdl
from xmlresource import XMLResource
import datetime

# insert attr_to_dict() function from above 

def main():
   # create a resourceSet that hold the contents of the esdl.ecore model and the instances we use/create
   rset = ResourceSet()
   # register the metamodel (available in the generated files)
   rset.metamodel_registry[esdl.nsURI] = esdl
   rset.resource_factory['esdl'] = lambda uri: XMLResource(uri)  # we register the factory for '.esdl' extension and XML serialization
   
   # Create a new EnergySystem
   es = EnergySystem(name="test")
   instance = Instance(name="test instance")
   # example of using an Enum
   instance.aggrType = AggrTypeEnum.PER_COMMODITY
   es.instance.append( instance )
   es.instance[0].area = Area(name="test area")
   pvpark = PVPark(name="PV park")
   pvpark.numberOfPanels = 10
   # Use datatime to set dates and times
   now = datetime.datetime.now()
   pvpark.commissioningDate = now
   ed = ElectricityDemand(name="E demand")
   es.instance[0].area.asset.append(pvpark)
   es.instance[0].area.asset.append(ed)
   inPort = InPort(id='InPort1')
   ed.port.append(inPort)
   outPort = OutPort(id='OutPort1', connectedTo=[inPort])
   pvpark.port.append(outPort)
      
   print("Energy system: {}".format(attr_to_dict(es))) 
   print("OutPort connectedTo: {}".format(outPort.connectedTo))
   print("InPort connectedTo: {}".format(inPort.connectedTo))
   resource = rset.create_resource(URI('Static_model_test.esdl'))
   resource.append(es)
   resource.save()
   
if __name__ == '__main__': 
    main()
```

## XMLResource support for PyEcore

Use the following file to support XMLResources instead of the default XMIResource support of PyEcore

{% code-tabs %}
{% code-tabs-item title="xmlresource.py" %}
```python

from pyecore.resources.xmi import XMIResource, XMIOptions, XMI_URL, XSI_URL, XSI
from lxml.etree import QName, Element, ElementTree
import logging


logger = logging.getLogger(__name__)

"""
Extension of pyecore's XMIResource to support the XMLResource in EMF.
It basically removes the xmi:version stuff from the serialization.
"""
class XMLResource(XMIResource):
    def __init__(self, uri=None, use_uuid=False):
        super().__init__(uri, use_uuid)
        self._later = []
        self.prefixes = {}
        self.reverse_nsmap = {}
        self.parse_information = []

    def get_parse_information(self):
        return self.parse_information

    def save(self, output=None, options=None):
        self.options = options or {}
        output = self.open_out_stream(output)
        self.prefixes.clear()
        self.reverse_nsmap.clear()

        serialize_default = \
            self.options.get(XMIOptions.SERIALIZE_DEFAULT_VALUES,
                             False)
        nsmap = {XSI: XSI_URL} # remove XMI for XML serialization

        if len(self.contents) == 1:
            root = self.contents[0]
            self.register_eobject_epackage(root)
            tmp_xmi_root = self._go_across(root, serialize_default)
        else:
            # this case hasn't been verified for XML serialization
            tag = QName(XMI_URL, 'XMI')
            tmp_xmi_root = Element(tag)
            for root in self.contents:
                root_node = self._go_across(root, serialize_default)
                tmp_xmi_root.append(root_node)

        # update nsmap with prefixes register during the nodes creation
        nsmap.update(self.prefixes)
        xmi_root = Element(tmp_xmi_root.tag, nsmap=nsmap)
        xmi_root[:] = tmp_xmi_root[:]
        xmi_root.attrib.update(tmp_xmi_root.attrib)
        #xmi_version = etree.QName(XMI_URL, 'version') # remove XMI version in XML serialization
        #xmi_root.attrib[xmi_version] = '2.0'
        tree = ElementTree(xmi_root)
        tree.write(output,
                   pretty_print=True,
                   xml_declaration=True,
                   encoding=tree.docinfo.encoding)
        output.flush()
        return self.uri.close_stream()

    """
    This function has been overriden XMIResource, to make it a little more robust for ESDL's that
    are 'older' and do not have a certain feature. By default XMIResource throws an exception when 
    an unknown attribute is found for a class. This version prints a warning and continues.
    """
    def _decode_attribute(self, owner, key, value):
        namespace, att_name = self.extract_namespace(key)
        prefix = self.reverse_nsmap[namespace] if namespace else None
        # This is a special case, we are working with uuids
        if key == self.xmiid:
            owner._internal_id = value
            self.uuid_dict[value] = owner
        elif prefix in ('xsi', 'xmi') and att_name == 'type':
            # type has already been handled
            pass
        # elif namespace:
        #     pass
        elif not namespace:
            if att_name == 'href':
                return
            feature = self._find_feature(owner.eClass, att_name)
            if not feature:
                #raise ValueError('Feature {0} does not exists for type {1}'
                #                 .format(att_name, owner.eClass.name))
                s = 'Attribute {0} does not exists for type {1} and is ignored.'.format(att_name, owner.eClass.name)
                logger.warning(s)
                self.parse_information.append(s)
            return feature
```
{% endcode-tabs-item %}
{% endcode-tabs %}

