# minemeld-covid-feeds
Minemeld prototypes and configuration to consume IoC feeds from multiple sources. Each source here has a subfolder

* cybersaiyan.it
* www.cyberthreatcoalition.org

A colleague handed me some COVID-19 (novel coronavirus) IoC feed information and I made a MineMeld configuration to aggregate these into feeds by IoC type (url, domain, ipv4) for consumption in Palo Alto Networks NGFW External Dynamic Lists. 


## Installation

There are two parts to the installation: prototypes and configuration

For the purposes of lazy documentation, I'm going to use the filename `minemeld-covid-prototypes.yml` here. For other feeds, substitute the name of the prototype yml file. (for example for cyberthreatacoalition use `minemeld-cti-prototypes.yml` )



### Part 1: Prototypes

Note: This process needs to be done for each feed (folder) on this repo that you want to consume feeds from.

First, install the prototypes by copying the contents of the `minemeld-covid-prototypes.yml` file to `/opt/minemeld/local/prototypes/minemeldlocal.yml`

If the file already exists, be sure to merge only the relevant lines and not duplicate the header of the file.

edit: It likely also works to just place the `minemeld-covid-prototypes.yml` file in the folder `/opt/minemeld/local/prototypes`

Then restart the minemeld engine.


### Part 2a: use canned configuration

If this is the only configuration you plan to use with Minemeld, you can just import the contents of `minemeld-covid-config.txt`

This is done by navigating in the WebGUI to Configuration and clicking **Import**. Copy the contents of the `minemeld-covid-config.txt` file to clipboard, and paste them into the dialog box that appears.

Click **Commit** once you're out of the dialog box, and the engine will restart.

Navigate to the Nodes screen and you will see the configuration begin to download IoC's.


## Part 2b: merge with your existing minemeld configuration

If you already use MineMeld for other feeds, you can create your own instances of the prototypes and connect them to your already-in-place aggregators and output feeds. 

Navigate in the WebGUI to Configuration and choose the triple-bar icon at the bottom. For simplicity, type 'cov' in the text box to filter the prototypes to just these. Click on the desired prototype (start with miners) and click **clone** to create a new instance of this prototype. From there, name it and click ok. 

Miners need to connect to aggregators, which then connect to output feeds. Note the type of the indictor must match the type of the aggregator; if not it will not pass any IOC's. The configuration is valid, but it won't work. :)

See the file `minemeld-covid-config.txt` for an example.

Note you must commit your configuration for it to take effect.

