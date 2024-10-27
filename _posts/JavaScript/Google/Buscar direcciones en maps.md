```
function searchAddress(address) {
    var geocoder3 = new google.maps.Geocoder();
    geocoder3.geocode({'address': address}, function(results, status) {
    if (status === 'OK') {
        alert(results[0].geometry.location);
    } else {
        alert('Geocode was not successful for the following reason: ' + status);
    }
});
```
