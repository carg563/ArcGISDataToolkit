# ArcGIS Data Toolkit

The ArcGIS Data Toolkit contains a number of tools and scripts to update and convert data from a varierty of different sources. The following tools are available:

#### WFS Download
Downloads a dataset from a WFS feed. Downloads data from the LINZ data service by either downloading the entire dataset for WFS or downloading the changeset and updating the data. Parameters required: 

* URL TO WFS Server - e.g. "http://Servername/geoserver/wfs?key=xxx"
* WFS Server Version (optional) e.g. "2.0.0", "1.1.0" or "1.0.0"
* Layer/table ID - e.g. "layer-319" or "layer-319-changeset"
* Data type - e.g. "Layer" or "Table"
* Dataset of extent of data to download (optional) e.g.  "C:\Temp\Scratch.gdb\FeatureClass"
* Last update file (optional) e.g. "C:\Development\Python for ArcGIS Tools\ArcGIS Data Toolkit\Configuration\WFSDownload-LINZDataServiceRail.json"
* Changeset Dataset ID (optional) e.g. "id"
* Output Dataset ID (optional) e.g. "id"
* WFS download type - e.g. "Shape-Zip", "CSV" or "JSON"
* Output workspace - e.g. "C:\Temp\Scratch.gdb"
* Dataset name - e.g. "FeatureClass"

#### Geodatabase Maintenance
Will compress geodatabase, update statistics and rebuild tables indexes. Optionally stops connections to the geodatabase while the tool runs.

#### Runtime Data to File Geodatabase
Converts all runtime data used in ArcGIS Runtime products (.geodatabase extension) to a file geodatabase.

#### Map Service Download
Downloads the data used in a map service layer by querying the json and converting to a feature class.

#### FTP Upload
Uploads a file to an FTP site.

#### Remote Server Data Update
This combines two of the above tools to update data on a remote web server. It consists of two geoporcessing tasks (one to be
setup on the server and one to be setup where the data is located).

* WebDataUpload will zip up datasets and upload them to the server via FTP
* DataUpdateFromZip will unzip datasets and load them into the database on the server
* WebDataUpload is the main script to be run and will call the DataUpdateFromZip tool via a geoprocessing service

#### Web Data Upload
Copies data to be replicated into geodatabase and zips this up. Zip file is then uploaded to FTP site 
for loading into a geodatabase.

#### Update from Link
Downloads a zipped up file geodatabase from a download link. Updates data in a geodatabase from the zip file and 
will update the datasets with the same name in the specified geodatabase.

#### Update from Zip
Updates data in a geodatabase from a zip file containing a geodatabase. Will get the latest zip file from update folder and 
update the datasets with the same name in the specified geodatabase. If dataset doesn't exist will copy it over.

#### Update from CSV
Updates data in a geodatabase from a CSV file. Will get the latest zip CSV from update folder and 
updates the dataset with the same name in the specified geodatabase.

#### Geodatabase Documentation
Documents a geodatabase by exporting feature class, table and domain information to a CSV file.

#### Google Drive Upload
Uploads a specified file or folder to Google Drive account. 
Need to generate keys first from here: 
* https://cloud.google.com/console/project 
Then need authorisation code from here: 
* https://accounts.google.com/o/oauth2/auth?scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&response_type=code&client_id={CLIENTID}&access_type=offline 
There are then two options - Generate Credentials File or not. You will need to generate the credentials file the first time this is run.

#### Convert to CSV
Converts a table or feature class to a CSV file. Optionally adds in header and footer records also.

#### Database Replication
Copies data from one geodatabase to another using a CSV file to map dataset names. Two update options:
   
        
* Existing Mode - Will delete and append records, so field names need to be the same.
             
* New Mode - Copies data over (including archive datasets if needed). Requires no locks on geodatabase datasets being overwritten.  

#### Database Contents To CSV
Exports out the names of datasets in a geodatabase to a CSV file.

#### Remove Duplicate Domains
Gets a list of used domains in the database then removes those not being used. Also looks at configuration file to find duplicate domains, then re-assigns a domain and removes the unused duplicate domain.

#### Map Document Summary
Creates a summary for each map document in a folder, stating description information about the map document as well as a list of data sources used in the map documents.

#### Setup Data for Replication
Prepares the datasets specified for replication to another local or remote geodatabase. This will version all the datasets and add GlobalIDs. Locks will be removed from the datasets, so this can take place.

#### Syncronise Datasets
Runs the syncronise changes gp tool to update dataset changes from one geodatabase to another.

#### Wellington Water Data Upload
Updates services data for Wellington Water, packages this data up and uploads to an FTP site for download.

#### Assign Permissions on Datasets
Updates permissions for datasets specified in a CSV file. This will go through CSV file and make sure datasets have the permissions specified for the relevant groups and users.

#### Export Metadata
Exports all metadata in a geodatabase out to a text file.

#### Restore Geodatabase History
Re-attachs an orphaned history dataset to its base dataset, by re-enabling archiving and loading in the orphaned archived dataset records in a SQL Server database.  

#### Field Aliases Export and Import
Exports field aliases for datasets specified to a CSV file. Can also use a configuration CSV file to import field aliases to datasets.

#### LINZ Mortgage Data Update
Creates a mortgage feature class by parcel and suburb based of LINZ title parcels and memorial data including title owners.
Input datasets from LINZ needed as input:

* Memorials table - https://data.linz.govt.nz/table/1695-nz-title-memorials-list-including-mortgages-leases-easements
* Property Titles (Including Owners) - https://data.linz.govt.nz/layer/805-nz-property-titles-including-owners

#### MapInfo Data Import
Imports all MapInfo data to a selected geodatabase. Takes a folder as input and will find all MapInfo files in this folder and subfolders. Requires data interoperability extension.

#### Stats Property Data Import
Imports data from Census NZ stats relating to property and aggregates this data by meshblock and suburb.

#### Summit Forests Data Clean
Cleans the Summit Forests GIS data by merging datasets and fixing up any issues.

#### NZAA ArchSite Data Download
Downloads archaeological data from the NZAA ArchSite and loads it into a database. 

#### Livestock Improvement Corporation Datawarehouse Sync
Syncronises data between the LIC data warehouse and GIS database, producing error and change reports.      


## Features

* Automate the data update process.
* Get data from zip or CSV and import into database.
* Easy way to update data on web server.
* Two options - New or existing.
* Backup data to Google Drive
* Download data from a map service or WFS layer.
* Replicate datasets
* Create mortgage datasets from LINZ.


## Requirements

* ArcGIS for Desktop 10.0/Python 2.6+
	* Update from Zip
	* Google Drive Upload
	* Database Migration

* ArcGIS for Desktop 10.1/Python 2.7+
	* Update from Link
	* Update from CSV
	* Web Data Upload
	* Map Service Download
	* WFS Layer Download
	
* ArcGIS for Desktop 10.3/Python 2.7+ or ArcGIS Pro 1.1/Python 3.4+ (Need to be signed into a portal site)
	* LINZ Mortgage Data Import

* Remote Server Data Update Requirements
	* ArcGIS for Server 10.1/Python 2.7+
	* FTP server setup on server
	* Setup DataUpdateFromZip tool as Geoprocessing service with these parameters:
		* Log File is a constant (defined when publishing tool)
		* Database is a constant (defined when publishing tool)
		* Update folder is a constant (defined when publishing tool)
		* Update mode can be existing or new (defined when running)


## Installation Instructions

* Google Drive Upload
	* Install Google API python library
		* Download library from [here](https://code.google.com/p/google-api-python-client) 
	* Setup a Google project [here](https://cloud.google.com/console/project)
	* Create new client ID to get the client ID and client secret
	* Go to this link and replace {CLIENTID} with the ID generated in the above step - https://accounts.google.com/o/oauth2/auth?scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&response_type=code&client_id={CLIENTID}&access_type=offline

* Setup Replication Process
	* All datasets to be replicated need to be versioned and have global IDs - Run the "Setup data for replication" script.
	* These datasets then need to be copied to the replication database.
	* Setup MXD with all datasets to be replicated.
	* Open up the Distributed Geodatabase toolbar and go through the Create Replica wizard for each database. e.g.
        	* One Way - Parent to Child
     		* Select the geodatabase where the datasets have been copied to
     		* Select Register Existing Data Only
       		* Give the replica a name
	* Go Next and Finish and this will register all the datasets in these two databases together, so any changes in the parent database will be recorded, then when the "Syncronise Datasets" tool is run, these will be pushed to the child geodatabase.

* Setup a script to run as a scheduled task
	* Fork and then clone the repository or download the .zip file. 
	* Edit the [batch file](/Examples) to be automated and change the parameters to suit your environment.
	* Open Windows Task Scheduler and setup a new basic task.
	* Set the task to execute the batch file at a specified time.


## Resources

* [LinkedIn](http://www.linkedin.com/in/sfweston)
* [GitHub](https://github.com/WestonSF)
* [Twitter](https://twitter.com/Westonelli)
* [Blog](http://westonelli.wordpress.com)
* [Python for ArcGIS](http://resources.arcgis.com/en/communities/python)
* [Google Drive SDK](https://developers.google.com/drive/web)
* [LINZ Data Service](https://data.linz.govt.nz)


## Issues

Find a bug or want to request a new feature?  Please let me know by submitting an issue.


## Contributing

Anyone and everyone is welcome to contribute. 


## Licensing
Copyright 2016 - Shaun Weston

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.