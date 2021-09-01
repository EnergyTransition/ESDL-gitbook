# Integration with Java

There are a few ways to integrate with Java-based technology and obtain the ESDL Java source code. This can be obtained manually using option 1, but we also provide a external maven repository and maven tools to generate the source code on the command line.



    
### 1. Use our maven repository
- Add the following repository entry to your `pom.xml` file:
   ```xml
    <repository>
           <id>hesi-releases</id>
           <name>HESI release artifactory</name>
           <url>https://ci.hesi.energy/artifactory/libs-release-local</url>
           <snapshots>
                 <enabled>false</enabled>
           </snapshots>
           <releases>
                 <enabled>true</enabled>
           </releases>
    </repository>
    ```
- You can then add the ESDL dependencies like so again in the pom.xml file:
   ```xml 
    <dependency>
           <groupId>nl.tno.esdl</groupId>
           <artifactId>esdl</artifactId>
           <version>2.21.6</version>
    </dependency>
   ```

**Add the required EMF dependencies**  
You need the following dependencies in your `pom.xml` when using EMF-based ESDL:

```xml
<dependency>
       <groupId>org.eclipse.emf</groupId>
       <artifactId>org.eclipse.emf.ecore</artifactId>
       <version>2.25.0</version>
</dependency>
<dependency>
       <groupId>org.eclipse.emf</groupId>
       <artifactId>org.eclipse.emf.common</artifactId>
       <version>2.23.0</version>
</dependency>
<dependency>
       <groupId>org.eclipse.emf</groupId>
       <artifactId>org.eclipse.emf.ecore.xmi</artifactId>
       <version>2.16.0</version>
</dependency>
```

You can also manually extract the main EMF-jar files from your local P2 Eclipse repository and add them to your classpath. You require the following EMF-jars:

   ```text
   org.eclipse.emf.common_2.23.0.v21xxyyzz.jar
   org.eclipse.emf.ecore_2.25.0.v21xxyyzz.jar
   org.eclipse.emf.ecore.xmi_2.16.0.v21xxyyzz.jar
   ```
If these dependencies are added to your application, ESDL can be used in the Java code.

### 2. Command line code generation
    
 - Clone the https://github.com/EnergyTransition/ESDL.git repository locally.
     Then execute: 
  ```bash
  mvn -f ESDL/esdl.parent/pom.xml install -pl ../esdl.buildtools -am
  mvn -f ESDL/esdl.parent/pom.xml generate-sources
  ```
   (Optional) If you want to be able to extend the ESDLPackage to create your own implementations for the ESDL classes, please manually add this constructor definition…

   ```java
   protected EsdlPackageImpl(String ensUri, EsdlFactory einstance) {
      super(ensUri, einstance);
   }
   ```
   … to the `EsdlPackageImpl.java` class in `ESDL/esdl/src-gen/esdl/impl/EsdlPackageImpl.java`

 - You can then add the folder ESDL/esdl/src-gen to the build path of your code in your IDE.
 - Don't forget to add the EMF dependencies mentioned above.

### 3. Use the Eclipse platform for code generation (and application creation)
When loading the ESDL project into Eclipse, you can right-click the `esdl.genmodel` file to generate the ESDL model Java code. Then use this project in other Eclipse based plugins.

This is currently used for the Edit, Editor and Designer plugins: they are Eclipse plugins that leverage the feature-rich Eclipse platform. Explaining how to do this can be read elsewhere on the internet. Options include using [Sirius ](https://www.eclipse.org/sirius/overview.html)to create the Designer plugin, using [EMF Forms](https://www.eclipse.org/ecp/emfforms/) to create attractive UIs to edit model instances, or creating a stand-alone ESDL-based application using [Eclipse RCP](https://wiki.eclipse.org/Rich_Client_Platform).

_Note: this approach is outdated now and hasn't been tested recently, we mostly create stand-alone Java applications outside of the Eclipse environment using the maven repository and dependencies._


   
# Examples

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

