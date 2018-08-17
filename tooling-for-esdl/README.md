---
description: Which software tools can be used to use and edit ESDL
---

# Tooling for ESDL

## Modelling

The concepts and the relations among the concepts in ESDL are defined in a structured model: the ESDL model. A modelling language is subsequently used to model the ESDL model. This modelling language is called the [Unified Modelling Language](https://en.wikipedia.org/wiki/Unified_Modelling_Language) \(UML\). But to make ESDL more accessible to both modelers, developers and end-users, ESDL is based on a dialect of UML called ECore. Therefore ESDL is modelled in [ECore](https://en.wikipedia.org/wiki/Eclipse_Modelling_Framework#Ecore).

ECore is part of the [Eclipse Modelling Framework ](https://www.eclipse.org/modelling/emf/)\(EMF\). [Eclipse ](https://www.eclipse.org/)is a well-known open-source Integrated Development Environment \(IDE\) that supports developers with all kinds of tools to develop software programs.

The EMF gives us several tools for free compared to using UML:

* Code generation. It can automatically generate Java-classes, XSD schema's and UML models from the ECore model.
* Provide semantics for modelling concepts. These semantics are geared towards generating tools to read, visualize and edit your ESDL files. EMF provides two ways for these semantics: \(1\) a static version \(using the code generation facility, creating actual files on disk\), and \(2\) a dynamic version that is in real-time created from the concepts you are modelling. This allows for direct feedback on the changes you make to the model as editors are instantly updated with these changes.
* A graphical editor to manipulate the model.

These properties make it easier to adopt ESDL, as this project not only provides an XML Schema for usage in energy transitions tools, letting the developers write XML-based ESDL-files themselves, but also provide rich editors to manipulate ESDL-files.

The tools can be spilt up in two categories:

1. Tools to edit the ESDL model instances \(the ESDL-files\)
2. Tools to edit the ESDL model itself and contribute the ESDL specification


