Simple Map

```
<div id="map" class="map" style="height: 300px; width: 100%;"></div>
<script>
    var map;

    var myLatLng = {lat: 42.5414227, lng: 1.5821905};

    function initMap() {
            
        map = new google.maps.Map(document.getElementById('map'), {
          zoom: 4
        });

        var bounds = new google.maps.LatLngBounds();

        <?php foreach ($parkings as $parking): ?>
        <?php if($parking->lat != null && $parking->lon != null): ?>
            marker = new google.maps.Marker({
                position: {lat: <?= h($parking->lat) ?>, lng: <?= h($parking->lon) ?>},
                map: map,
                title: "<?= h($parking->name) ?>"
            });
            bounds.extend(marker.position);

            map.fitBounds(bounds);
        <?php endif;?>
    <?php endforeach; ?>
    }

</script>
<script async defer src="https://maps.googleapis.com/maps/api/js?key=<?= $this->Webtext->getText('config_api_google_maps') ?>&callback=initMap"></script>
```