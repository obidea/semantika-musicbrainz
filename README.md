MusicBrainz-TERMAL/XML
======================

MusicBrainz rdb2rdf mappings for [OBDA Semantika](http://obidea.github.io/semantika-api/) system. Currently we are presenting the native mapping language for Semantika, called [TERMAL/XML](https://github.com/obidea/semantika-api/wiki/2.-Basic-RDB-RDF-Mapping). In the future the system will be able to read R2RML syntax.

The purpose of this project is to show Semantika's capability in exporting data from database tuples to RDF triples; as well as to show the possible option to reuse R2RML mappings for Semantika. I have included a sample dataset that you can use immediately. No import data required.

Credits for Barry Norton who has provided the R2RML mappings in his repository site [LinkedBrainz / MusicBrainz-R2RML](https://github.com/LinkedBrainz/MusicBrainz-R2RML). This work is just a pure translation from those mappings.

**New Tutorial**: [How to create a simple SPARQL endpoint for MusicBrainz database](https://github.com/obidea/semantika-sesame).


## Preparation:

* To run the examples, you will need to use [Semantika CLI](https://github.com/obidea/semantika-cli) project and download the latest release.
* Download it and extract the ZIP file into your local directory.
* Download the mapping files from [termalxml/](https://github.com/obidea/semantika-musicbrainz/tree/master/termalxml) and place them together with the CLI extraction. Notice that you might have downloaded the configuration file as well (mbzdb.cfg.xml).
* Download the sample dataset from [sample-data/](https://github.com/obidea/semantika-musicbrainz/tree/master/sample-data) and extract the ZIP into your local directory. The ZIP file contains a self-contained H2 database.
* Browse the H2 home folder and copy-and-paste a JAR file called h2-1.3.xxx.jar to `jdbc/` in CLI home folder.

## Start Exporting:

* Run the H2 server by executing `h2.sh` (or `h2.bat` if you're in Windows) from its home directory.
```
$ cd $H2_HOME
$ ./h2.sh 
```

* Run Semantika CLI tool from its home directory.
```
$ cd $CLI_HOME
$ ./semantika materialize --config=mbzdb.cfg.xml --output=output.n3 -f N3
```
(Note the other options for the output format, e.g., Turtle, RDF/XML and JSON-LD, see `semantika --help`)


Important Notes
---------------

* All the mappings have been tested using the provided dataset and all passed the run. The total number of triples produced is **1,045,226 Triples**.

* Notice that some mappings are enclosed by comment signs. I have put a comment to explain the reason.

* The dataset is a subset of [MusicBrainz Database](http://musicbrainz.org/doc/MusicBrainz_Database) per March 1, 2014. The dataset contains all US artists/groups from 1970 to 1989 who are still active until now. In summary, the dataset consists of 54 tables with 481,401 tuples (~52 MB). The extraction model is defined as below:
```
artist 
where begin_date_year < 1990 and begin_date_year >= 1970 
  and area = 222 
  and (type = 1 or type = 2)
  and ended = false 
```

* The dataset is released following the parent license which is under the Creative Commons [Attribution-NonCommercial-ShareAlike 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/).



