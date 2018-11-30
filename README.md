# Mapcrafter Configuration

Configuration and setup files for [Mapcrafter](https://mapcrafter.org/),
used for generating a map for the [Minecraft](https://minecraft.net/) server
[Lompemakeriet](http://minecraft.tomlin.no/maps/new/).

#### Build
- `git clone https://github.com/mapcrafter/mapcrafter.git`
- `brew install boost libpng cmake libjpeg-turbo`
- `cd mapcrafter`
- `cmake . -DJPEG_INCLUDE_DIR=/usr/local/opt/jpeg-turbo/include/ -DJPEG_LIBRARY=/usr/local/opt/jpeg-turbo/lib/libjpeg.dylib`
- `make`

#### Run
- `./src/mapcrafter -c src/config.conf -j 8`
- `./src/mapcrafter -c src/config.conf -j 8 -F` (force rerender)

#### Upload
- `tar -zcf map.tar.gz worlds/map_world_*`
- `scp map.tar.gz xxxxx@xxx.tomlin.no:/www/lompemakeriet/maps/new/`
- `ssh xxxxx@xxx.tomlin.no`
- `cd /www/lompemakeriet/maps/new/`
- `tar zxvf map.tar.gz &`

#### Modifications
- Copy `leaflet.label.js/css` to `static/leaflet`
- Add `leaflet.label.js/css` to `index.html`
- Replace in `static/handler/markers.js`:
  `marker.bindPopup(markerInfo.text ? markerInfo.text : markerInfo.title);` with
  `marker.bindLabel(markerInfo.title, { noHide: true, direction: 'right', offset: [-20, -5] });`
- Copy markers from `markers.js`
