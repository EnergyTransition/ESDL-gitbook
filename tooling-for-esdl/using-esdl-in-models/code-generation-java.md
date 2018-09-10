# Integration with Java

There are two ways to integrate with Java-based technology:

1. **Use the Eclipse platform** This is currently used for the Edit, Editor and Designer plugins: they are Eclipse plugins that leverage the feature-rich Eclipse platform. Explaining how to do this can be read elsewhere on the internet. Options include using [Sirius ](https://www.eclipse.org/sirius/overview.html)to create the Designer plugin, using [EMF Forms](https://www.eclipse.org/ecp/emfforms/) to create attractive UIs to edit model instances, or creating a stand-alone ESDL-based application using [Eclipse RCP](https://wiki.eclipse.org/Rich_Client_Platform).
2. **Use the main EMF-jars in your stand-alone Java application**  
   If you extract the main EMF-jar files from the EMF plugins or use the Maven repo to download these dependencies into your Maven-project. You require the following EMF-jars:

   ```text
   org.eclipse.emf.common_2.14.0.v20xxyyzz.jar
   org.eclipse.emf.ecore_2.14.0.v20xxyyzz.jar
   org.eclipse.emf.ecore.xmi_2.14.0.v20xxyyzz.jar
   ```

The maven repo is currenly a little behind the lastest EMF-versions, but you need the following dependencies in your `pom.xml`:

{% code-tabs %}
{% code-tabs-item title="pom.xml" %}
```markup
         <dependency>
                <groupId>org.eclipse.emf</groupId>
                <artifactId>org.eclipse.emf.ecore</artifactId>
                <version>2.12.0</version>
        </dependency>
        <dependency>
                <groupId>org.eclipse.emf</groupId>
                <artifactId>org.eclipse.emf.common</artifactId>
                <version>2.12.0</version>
        </dependency>
        <dependency>
                <groupId>org.eclipse.emf</groupId>
                <artifactId>org.eclipse.emf.ecore.xmi</artifactId>
                <version>2.12.0</version>
        </dependency>

```
{% endcode-tabs-item %}
{% endcode-tabs %}

If these dependencies are added to your application, ESDL can be used in the Java code.

E.g. creating an Energy System with an Area programmatically:

```java
EnergySystem energySystem = EsdlFactory.eINSTANCE.createEnergySystem();
energySystem.setName("My First EnergySystem");
energySystem.setId("firstEnergySystem");
Area area = EsdlFactory.eINSTANCE.createArea();
area.setId("Test");
area.setName("Amsterdam municipality")
energySystem.getArea().add(area);
```



The following code allows you to load and save ESDL-model instances:

## Loading of an ESDL-file

```java
public static EnergySystem loadESDLModel(String fileName) throws IOException {
		// Initialize the model
		EsdlPackage.eINSTANCE.eClass();
		XMIResource resource = new XMIResourceImpl(URI.createURI(fileName));
		resource.load(null);
		return (EnergySystem) resource.getContents().get(0);
}
```

If the models grow large with a lot of internal references, add the following lines to speed up the loading of the files:

```java
public static EnergySystem loadESDLModel(String fileName) throws IOException {
		// Initialize the model
		EsdlPackage.eINSTANCE.eClass();
		XMIResource resource = new XMIResourceImpl(URI.createURI(fileName));
		// speed up loading of large files by defering ID references lookup.
		resource.getDefaultLoadOptions().put(XMIResource.OPTION_DEFER_IDREF_RESOLUTION, Boolean.TRUE);
		resource.setIntrinsicIDToEObjectMap(new HashMap<String, EObject>());
		// load the resource
		resource.load(null);
		return (EnergySystem) resource.getContents().get(0);
}
```

## Saving an ESDL-file

Saving to an ESDL-file is as follows:

```java
public static XMIResource saveESDLModel(EnergySystem energySystem, String fileName) throws IOException {
		XMIResource resource = new XMIResourceImpl(URI.createURI(fileName));
		resource.getContents().add(energySystem);
		HashMap<String, Object> opts = new HashMap<String, Object>();
		// Produce an xsi:schemaLocation in the resource
		opts.put(XMIResource.OPTION_SCHEMA_LOCATION, true);
		resource.save(opts);
		return resource;
	}
```

