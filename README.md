# Comma Separated Values repo


## CAP (postcodes) of Italy
More info: https://www.openstreetmap.org/user/Cascafico/diary/44859

Get amministrazioni.txt file at https://indicepa.gov.it/documentale/n-opendata.php
Licence Open Data (read, download, copy and reuse allowed)

manually parsed files:
- cap.csv (municipality,postcode)
- cap_addr.csv italian postodes with sample addresses (Abbiate Grasso,04128,Via Roma 41)

alternatively, use OpenRefine
- amministrazioni.operations file
- export tabular data Indirizzo,Comune,Cap
- apply sort -u -t, -k1,2 openrefinetabularoutput.csv > > tobegeocoded.csv (remember put headers)


### CAP geocoding
$ sudo npm install -g csvgeocode
geocoder documentation: https://github.com/veltman/csvgeocode

$ cat cap_addr.csv | awk -F "," '{print $3","$2","$1}' > captogeocode.csv
check/add headers accordingly
alternatively, use OpenRefine to remove apostrophes, trim spaces, remove comma in Indirizzo and Comune, etc.

NOMINATIM
$ csvgeocode captogeocode.csv capgeocoded.csv --handler osm --delay 1000 --verbose --url "http://nominatim.openstreetmap.org/search?q={{street}},{{postcode}} {{comune}}&format=json&viewvbox=6,47,15,47"

MAPBOX (more flexible in matches)
$ csvgeocode captogeocode.csv capgeocoded.csv --handler mapbox --delay 1000 --verbose --url "http://api.tiles.mapbox.com/v4/geocode/mapbox.places/{{street}},{{postcode}} {{city}}.json?access_token=<token>"
search problem for streets with  apostrophe char (ie: "Via D'Azeglio")
some coords out of continent (insert Italy in search?)



## Highway names of Italy
more info: https://www.openstreetmap.org/user/Cascafico/diary/44214

- ???_names.csv where ??? is province code

Licence CC-BY (read, download, copy and reuse allowed; attribution)
