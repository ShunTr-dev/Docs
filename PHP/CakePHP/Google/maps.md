## Google Maps en CakePHP

### Simple Map

```html
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
            var marker = new google.maps.Marker({
                position: {lat: <?= h($parking->lat) ?>, lng: <?= h($parking->lon) ?>},
                map: map,
                title: "<?= h($parking->name) ?>"
            });
            bounds.extend(marker.position);
        <?php endif;?>
        <?php endforeach; ?>
        
        map.fitBounds(bounds);
    }
</script>
<script async defer src="https://maps.googleapis.com/maps/api/js?key=<?= $this->Webtext->getText('config_api_google_maps') ?>&callback=initMap"></script>
```

Este documento muestra cómo integrar Google Maps en una aplicación CakePHP. La sección proporciona un mapa simple con marcadores para los parkings especificados. La función `initMap()` inicializa el mapa y agrega marcadores para cada parking válido. Se utiliza un bucle `foreach` para iterar sobre los parkings y crear marcadores para aquellos con coordenadas válidas. La API de Google Maps se carga de manera asíncrona y deferida al final del documento.