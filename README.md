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
    
    tippecanoe -Pf -Z1 -Bg -z14 -pf -o earthquake-tweets.mbtiles earthquake-tweets.geojsonl

    
    
4. To visualize the tweets, recall that you'll need this:

    decodeURIComponent( props.text.replace(/\+/g,' '))