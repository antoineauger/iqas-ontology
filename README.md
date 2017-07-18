# iqas-ontology

iQAS platform uses the QoOnto ontology. This repository may be used to setup and configure Apache Jena, the triple data store used for ontology inference.

## The iQAS ecosystem

In total, 5 Github projects form the iQAS ecosystem:
1. [iqas-platform](https://github.com/antoineauger/iqas-platform)<br/>The QoO-aware platform that allows consumers to integrate many observation sources, submit requests with QoO constraints and visualize QoO in real-time.
2. [virtual-sensor-container](https://github.com/antoineauger/virtual-sensor-container) <br/>A shippable Virtual Sensor Container (VSC) Docker image for the iQAS platform. VSCs allow to generate observations at random, from file, or to retrieve them from the Web.
3. [virtual-app-consumer](https://github.com/antoineauger/virtual-app-consumer) <br/>A shippable Virtual Application Consumers (VAC) Docker image for the iQAS platform. VACs allow to emulate fake consumers that submit iQAS requests and consume observations while logging the perceived QoO in real-time.
4. [iqas-ontology](https://github.com/antoineauger/iqas-ontology) (this project)<br/>Ontological model and examples for the QoOonto ontology, the core ontology used by iQAS.
5. [iqas-pipelines](https://github.com/antoineauger/iqas-pipelines) <br/>An example of a custom-developed QoO Pipeline for the iQAS platform.

## System requirements

In order to correctly work, iQAS assumes that the following software have been correctly installed and are currently running. We indicate between parenthesis the software versions used for development and test:
* Java (`1.8`)
* Apache Jena Fuseki (`2.4.1`)

This README describes installation and configuration of the QoOnto ontology for Unix-based operating systems (Mac and Linux).

## Project structure

```
project
│
└───config_fuseki_tdb
│   │   qoo-onto.ttl
│
└───imports
│   │   DUL.rdf
│   │   m3-lite.rdf
│   │   qoo-onto-full-jena.rdf
│   │   qu.owl
│   │   ssn.rdf
│   │   wgs84_pos
│
│   qoo-ontology.rdf
│   iqas_sensors.jsonld
```

## Installation

If it is not already done, you should have downloaded and installed [Apache Jena Fuseki](https://jena.apache.org/documentation/serving_data/).

## Configuration

1. Clone the Github repository:
    ```
    git clone https://github.com/antoineauger/iqas-ontology.git
    ```
2. Edit the file `iqas-ontology/config_fuseki_tdb/qoo-onto.ttl` and choose a location for your ontology store:
    ```
    tdb:location "/your/path/to/your/store" ;
    ```
3. You may want to edit the file `iqas-ontology/iqas_sensors.jsonld` to declare your QoO attributes, sensors, topics, places, etc. Check out the provided minimal example.
4. Run the Fuseki server by passing the previous file in parameter:
    ```
    $FUSEKI_DIR/fuseki-server --config=qoo-onto.ttl
    ```
5. Open a web browser and navigate to Fuseki homepage at [http://localhost:3030](http://localhost:3030)
6. Visualize the `/qoo-onto` dataset and click on "add data".
7. Leave "Destination graph name" blank and click on "select files..."
8. Select the files `qoo-ontology-full.rdf` and `iqas_sensors.jsonld` located at the root of the Github repository. Then, click on "upload all".
9. Click on the query tab and submit the following query:
    ```sql
    SELECT ?p ?v ?k
    WHERE {
        ?p ?v ?k
    }
    LIMIT 10
    ```
    If you see some results, congratulations you have successfully deployed Apache Jena and it is currently able to serve requests on the QoOnto ontology!
10. Please note that all ontology files located in `iqas-ontology/imports` need to be imported by the iQAS platform (see [step 6.1](https://github.com/antoineauger/iqas-platform#configuration))

## Acknowledgments

The iQAS platform have been developed during the PhD thesis of [Antoine Auger](https://personnel.isae-supaero.fr/antoine-auger/?lang=en) at ISAE-SUPAERO (2014-2017).

This research was supported in part by the French Ministry of Defence through financial support of the Direction Générale de l’Armement (DGA).

![banniere](https://github.com/antoineauger/iqas-platform/blob/master/src/main/resources/web/figures/banniere.png?raw=true "Banniere")
