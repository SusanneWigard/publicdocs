# Public Documents
The Regulation on Public Documents (http://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R1191) foresees the use of multilingual standard forms suitable for electronic exchange in order to facilitate the translation of the public documents to which they are attached.
The objective of this task is to create the technical representations of the standardised forms for the Regulation on Public Documents as XML schema files (xsd).
In order to maximize semantic and technical interoperability, the XML schemas will use existing standards or results from previous projects where possible, and will have - at the core - a common subset of each form while additional elements will be included, if needed, for each MS.
# Standards used
The XML schemas generated contain the following standards: 
* Core Vocabularies (https://joinup.ec.europa.eu/community/semic/og_page/core-vocabularies)
* UBL (http://docs.oasis-open.org/ubl/UBL-2.1.html) 

# Tools used
* Modelling: Papyrus: https://eclipse.org/papyrus/ 
* Transformation: Acceleo: http://www.eclipse.org/acceleo/
* XSD validation: 
	* SQC (http://xml.coverpages.org/IBM-SQC211-CommandUse.html)
	* XSV (http://www.ltg.ed.ac.uk/~ht/xsv-status.html)
	* JAXB (http://www.oracle.com/technetwork/articles/javase/index-140168.html - check is performed only if the Java objects are generated)

# File structure
* model: contains the UML models (class diagrams) created via Papyrus
* src: contains the Acceleo templates that perform the transformation
* config.properties: contains all the variables used by Acceleo to perform the transformation of the model into XML schemas
* lib: libraries used by the Acceleo modules
* generated: contains the XML schemas and html documentation generated by Acceleo templates

# Setup
* Download Eclipse JEE Neon from (the JEE version includes the XML editor and it requires Java 8): https://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon3
* Unzip the folder and run eclipse.exe (choose any folder as workspace)
* Go on menu "Help" -> "Install New Software..."
* In the "work with" dropdown menu select: "Neon - http://download.eclipse.org/releases/neon"
* Wait that the list of plugins appears and search for the "Modeling" section
* Expand the "Modeling" section, select "Acceleo" and "Papyrus UML" plugins
* click on "Next", click on "Next" again, accept the licence and click on "Finish"
* Wait that the plugins are downloaded and restart Eclipse if requested
* Go on menu "File" -> "Import..." -> Expand "Git" -> Select "Projects from Git" -> click "Next"
* Select "Clone URI" -> click "Next"
* in URI paste the URL: https://github.com/e-documents-isa/publicdocs.git -> click "Next"
* Make sure you select only the branch "origin/master", click "Next, click "Next"
* In the import wizard make sure that "Import exisint Eclipse project" is selected, click "Next" and click "Finish"
* You can close the welcome page (if it appears) and in "Project Explorer" you should be able to see the project

# Run Acceleo
* In "Project Explorer" right click on the project folder "publicdocs"
* From the contextual menu select "Run As" -> "Launch Acceleo Application"
* From the drop down selection, select the "Generate" class and click "OK"
* Browse the model (with *.uml), you should find the /publicdocs/model/pd.uml
* Browse the target and select the folder /publicdocs/generated
* Click Run
* In the console you might see different debug messages (in black)

If you experience the error:
"Error: Could not find or load main class org.eclipse.acceleo.module.publicdocs.main.Generate"
* In "Project Explorer" right click on the project folder "publicdocs"
* From the contextual menu select "Properties" and search for "Java Build Path"
* Select "Library" tab and you should see an error next to JRE System Library [JavaSE-1.8] (unbound)
* Select the JRE System Library and click "Edit" and select "Workspace default JRE"
* In the menu "Window" -> "Preferences", search for "Java" -> "Compiler"
* In compiler compliance level select 1.5 (at least)
* Repeat the launch of Acceleo as explained before

If you experience the error:
"Caused by: org.eclipse.emf.ecore.xmi.PackageNotFoundException: Package with uri 'http://www.omg.org/spec/ALF/20120827/ActionLanguage-Profile' not found."
* In "Project Explorer" right click on the pd.uml file and open with "Text Editor"
* Delete the following tags:
* "xmlns:ActionLanguage="http://www.omg.org/spec/ALF/20120827/ActionLanguage-Profile" on line 2
* "<ActionLanguage:TextualRepresentation .../>" at the end of the file
* Save the file and rerun Acceleo

# Model
The model is composed by 2 parts:
* isa.uml, used as profile containing stereotypes
* pd.uml, the class diagram containing all the classes of the Regulation and MS










# Licence
* The XML schemas are released under ISA Open Metadata Licence v1.1 (https://joinup.ec.europa.eu/category/licence/isa-open-metadata-licence-v11)
* The code is released under EUPL v1.1 (https://joinup.ec.europa.eu/community/eupl/og_page/european-union-public-licence-eupl-v11)