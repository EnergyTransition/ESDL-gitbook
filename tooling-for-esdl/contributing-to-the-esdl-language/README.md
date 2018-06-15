# Contributing to the ESDL language

To contribute to the ESDL language you have to install Eclipse and the Eclipse Modeling Tools which contain the Eclipse Modeling Framework.

These can be downloaded from the eclipse.org website. Easiest is downloading the modeling package directly with a new Eclipse installation, but alternatively you could also install these modeling tools as plugins in your existing Eclipse installation. Since EMF is still under active development, and ESDL is using new features from these latest releases, it is required to use the lastest version of Eclipse.

Currently Oxygen 3a is the latest stable release of Eclipse. The complete package can be downloaded [here](https://www.eclipse.org/downloads/packages/eclipse-modeling-tools/oxygen3a).

## Setting up Eclipse Modeling Tools

After downloading and installing Eclipse and Eclipse Modeling Tools, you start Eclipse Modeling Oxygen by doubleclicking on the created icon on the Deskop \(if you are using Windows...\). If will ask you where you want to place your workspace files. Select a logical location and you end up with a welcome screen.

 If you did not clone the repository yet, now is a good moment with your preferred GIT tool or use Eclipse to import the repository directly.

![](../../.gitbook/assets/import.png)

Next step is importing the ESDL git repository by using File -&gt; Import... If you already cloned the repository locally, use _Existing Project into Workspace_ and the project will be imported. If you want to directly import the project from Git, use Git-&gt;Projects from Git.



After importing, the _Package explorer_ will show the following files and directories:

![](../../.gitbook/assets/package-explorer.PNG)

In the model folder you see several files:

* esdl.aird - In this file the graphical representation of the ESDL concepts are documented, such as the \(x,y\) location of the classes, the color of the classes, the font, etc. It allows us to visually modify the contents of the ESDL model. If you double click you can open the ESDL model diagram editor and manipulate the model.
* esdl.ecore - This is ESDL. The UML-based model describing all ESDL concepts: the vocabulary and grammar of an Energy System. If you double click you can edit the ESDL model using a tree-based structure \(less convienent than the diagram editor\)
* esdl.genmodel - This file describes how to generate Java-files and XSD Schemas from a ecore-file. It contains a dozen configuration options.
* esdlXML.xsd - this is the XML Schema file for ESDL
* esdlXML.xsd2ecore - maps the XSD to the Ecore model.

Double clicking on the aird-file opens the following dialog:

![](../../.gitbook/assets/aird.png)

The AIRD file shows the model dependencies and representation. The Design-&gt;Entities in a Class Diagram is the most interesting. Double click on 'esdl' to open this representation.

There is also a Review representation that shows all the documentation in the model. \(although this is work in progress\).

