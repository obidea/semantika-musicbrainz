MusicBrainz Mappings
====================

MusicBrainz rdb2rdf mappings for [OBDA Semantika](http://obidea.github.io/semantika-api/) system. Currently we are presenting the native mapping language for Semantika, which is [TERMAL/XML](https://github.com/obidea/semantika-api/wiki/2.-Basic-RDB-RDF-Mapping). In the future the system will be able to read R2RML syntax.

The purpose of this project is to show Semantika's capability in exporting data from database to RDF; as well as to show the possible option to reuse R2RML mappings for Semantika. I have included a sample dataset that you can use immediately. No import data required.

Credits for Barry Norton who has provided the R2RML mappings in his repository site [LinkedBrainz / MusicBrainz-R2RML](https://github.com/LinkedBrainz/MusicBrainz-R2RML). This work is just a pure translation from those mappings.


User Guide
==========

Preparation:
------------
1. To run the examples, you will need [Semantika CLI tool](https://github.com/obidea/semantika-cli/releases/download/v1.1/semantika-cli-1.1.zip).
2. Download it and extract the ZIP file into your local directory.
3. Download the mapping files from [termalxml/](https://github.com/obidea/semantika-musicbrainz/tree/master/termalxml) and place them together with the CLI extraction. Notice that you might have downloaded the configuration file as well (mbzdb.cfg.xml).
4. Download the sample dataset from [sample-data/](https://github.com/obidea/semantika-musicbrainz/tree/master/sample-data) and extract the ZIP into your local directory. The ZIP file contains a self-contained H2 database.
5. Copy-and-paste a JAR file called `h2-1.3.xxx.jar` to `jdbc/` in CLI home folder.

Start Exporting:
---------------
1. Run the H2 server by executing `h2.sh` (or `h2.bat` if you're in Windows) from its home directory.
```
$ cd $H2_HOME
$ ./h2.sh
```

2. Run Semantika CLI tool from its home directory.
```
$ cd $CLI_HOME
$ ./semantika materialize --config=mbzdb.cfg.xml --output=output.n3 -f N3
```


Important Notes
===============

1. To be able to try all the mappings, you need to edit the configuration file manually. A list of mapping files are presented there, however the system only accepts one file at a time and therefore you need to remove the comment sign by hand.

2. The dataset is a subset of MusicBrainzDB per March 1, 2014. The dataset contains all US artists/groups from 1970 to 1989 who are still active until now. In summary the dataset consists of 54 tables with 481,401 tuples. The extraction model is defined as below:
```
artist 
where begin_date_year < 1990 and begin_date_year >= 1970 
  and area = 222 
  and (type = 1 or type = 2)
  and ended = false 
```

3. Notice that in the mapping files there are some mappings enclosed by comment signs. These ignored mappings have no support by the current implementation. They are now in my TODO list.

4. All the mappings have performed using the provided dataset and all passed the run.
```
area.tml.xml = 627
artist.tml.xml = 98,486
dbpedia.tml.xml = 0
label.tml.xml = 50,289
medium.tml.xml = 132,069
place.tml.xml = 882
recording.tml.xml = 92,166
release_group.tml.xml = 5,635
release.tml.xml = 18,085
tag.tml.xml = 109,792
track.tml.xml = 312,271
work.tml.xml = 48,246
```


