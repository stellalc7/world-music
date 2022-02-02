## <a href="https://beatconnection.herokuapp.com" target="_blank">Beat Connection</a>
```
Behold, our beat connections (っ˘з(˘⌣˘ ) ♡
Listen to popular streams around the world.
```

https://user-images.githubusercontent.com/17345270/152177744-b3266537-11dd-4386-ad20-0c6132b154fc.mov

## Functionalities
- An interactive globe connects cities (from user input) with bezier curves.
- Listen to streams on-site.
- Current stream location propogates rings.
- Current stream location's local time, and weather conditions are available.

## Technologies
- NodeJS, ExpressJS, HTML, CSS
- <s>Spotify API</s>
- Mixcloud API for streams
- OpenWeatherMap API for coordinates, timezone, weather
- Globe.GL for connecting beats

## Code snippet
Initially, I opted for the Spotify API as it sounded the most robust and reliable to allow users to input an artist they enjoy listening to. From their input, a related artist was fetched. The original goal was to discover similar artists to listen to around the world.
artist name (i.e. user input) => artist id
```
// SPOTIFY API CALL
const urlStart = 'https://api.spotify.com/v1/search';
const artistName = req.query.artistName;
const url = `${urlStart}?q=${artistName}&type=artist`;
const getArtistID = await fetch(url, { method: 'GET', headers: { 'Authorization': 'Bearer ' + token }, json: true })
  .then(apiResponse => apiResponse.json())
```  
artist id => related artist
```
// SPOTIFY API CALL
const relatedUrlStart = 'https://api.spotify.com/v1/artists';
const artistID = getArtistID.artists.items[0].id;
const relatedUrl = `${relatedUrlStart}/${artistID}/related-artists`;
const relatedArtist = await fetch(relatedUrl, { method: 'GET', headers: { 'Authorization': 'Bearer ' + token }, json: true })
  .then(apiResponse => apiResponse.json())
  .then(data => resp.send(data))
  .catch(error => resp.send(error));
```
I realized Spotify made artist location data obselete a few years ago. So, I thought I could inherently search for countries with a genre through playlists, to get 1 track from playlists, and map the track/artist over the country - i.e. 'Bolivian rap'. This equation would probably require a lot of testing - obscure genres, coupled with specific countries, etc.

I discovered the Mixcloud API, which offers streams posted by users around the world - live shows, DJ sets, rave recordings, etc. I modified my concept to 'streams around the world' and allow users to input cities instead. I added the OpenWeatherMap API to display coordinates, local weather conditions, and local time.


## Sources
https://globe.gl/<br>
https://gist.github.com/tadast/8827699<br>
https://www.last.fm/api/show/geo.getTopArtists<br>
https://www.mixcloud.com/developers/#connections-lists<br>
https://www.mixcloud.com/developers/widget/#methods<br>
https://developer.spotify.com/console/get-search-item/<br>
https://developer.spotify.com/console/get-artist-related-artists/<br>
https://developer.spotify.com/documentation/general/guides/track-relinking-guide/


## Shout outs
Big hugs to everyone who gave me coding wisdom + inspiration.
