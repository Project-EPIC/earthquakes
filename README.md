## Earthquake Tweets


Note: The design of this repo is to be easily replicable to other collections local to Epic-Analytics


### Process:

1. Run `epic_utils/parallel_get/get_geo.rb` for the earthquake collection, like this:

    `ruby get_geo "Earthquake" 24`
    
   This will create 24 `.json` files of the form `tweets_<process>.json`.
   
   Next, put these files together with: `cat *.json > ../../earthquakes/raw-geo-earthquake-tweets.jsonl`
   
2. Use the EarthquakeTweets Jupyter Notebook to process this massive file of tweets

3. Now use tippecanoe to tile objects

    tippecanoe -Pf -o epic-earthquake-tweets.mbtiles earthquake-tweets.geojsonl
    
With some trial and error, this one seems to work okay:
    
    tippecanoe -Pf -Z1 -z16 -B5 -m4 -as -o earthquake-tweets.mbtiles earthquake-tweets.geojsonl

4. Upload the tileset to Mapbox:

    ~/upload-tiles.js earthquake-tweets.mbtiles
    
5. The `docs` folder in this repository contains the webpage to view these tweets interactively.

6. TODO: ^ This could be much better.