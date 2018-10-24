# Comma Separated Values repo


## CAP (postcodes) of Italy
More info: https://www.openstreetmap.org/user/Cascafico/diary/44859

- cap.csv italian postcodes
- cap_addr.csv italian postodes and sample addresses

Licence Open Data (read, download, copy, reuse allowed)
https://indicepa.gov.it/documentale/n-opendata.php

### CAP geocoding
$ sudo npm install -g csvgeocode
$ cat cap_addr.csv | awk -F "," '{print $3","$2","$1}' > captogeocode.csv
check/add headers accordingly
$ csvgeocode captogeocode.csv capgeocoded.csv --handler osm --delay 1000 --verbose --url "http://nominatim.openstreetmap.org/search?q={{street}},{{postcode}} {{comune}}&format=json"

