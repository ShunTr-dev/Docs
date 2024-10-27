# Tomar las 3 últimas imágenes de Instagram con CakePHP

Aquí se presenta una forma de recuperar las tres últimas imágenes de una cuenta de Instagram y mostrarlas en una página web utilizando CakePHP. Este proceso implica realizar una solicitud a la página de perfil de Instagram, analizar el JSON devuelto y extraer la información relevante de las publicaciones.

## Controlador

En el controlador, se llama a la función `retrieveInstagramImages()` para obtener las imágenes y luego se envían a la vista.

```php
$this->set('instagram', $this->retrieveInstagramImages(Configure::read('InstagramAccount'), 3));
```

## Función para recuperar imágenes de Instagram

Esta función toma el nombre de usuario de Instagram y el número de imágenes a recuperar, realiza una solicitud HTTP a la página del perfil de Instagram y analiza el JSON devuelto para extraer la información de las publicaciones.

```php
public function retrieveInstagramImages($username, $image_num) {
    $insta_source = file_get_contents('http://instagram.com/'.$username);
    $shards = explode('window._sharedData = ', $insta_source);
    $insta_json = explode(';</script>', $shards[1]);
    $results_array = json_decode($insta_json[0], TRUE);
    if ($image_num > $results_array['entry_data']['ProfilePage'][0]['graphql']['user']['edge_owner_to_timeline_media']['count']) {
        $image_num = $results_array['entry_data']['ProfilePage'][0]['graphql']['user']['edge_owner_to_timeline_media']['count'];
    }
    for ($i = 0; $i < $image_num; $i++) {
        $url_tmp = null;
        $url_tmp['name_publication'] = $results_array['entry_data']['ProfilePage'][0]['graphql']['user']['edge_owner_to_timeline_media']['edges'][$i]['node']['edge_media_to_caption']['edges'][0]['node']['text'];
        $url_tmp['url_publication'] = $results_array['entry_data']['ProfilePage'][0]['graphql']['user']['edge_owner_to_timeline_media']['edges'][$i]['node']['shortcode'];
        $url_tmp['url_image'] = $results_array['entry_data']['ProfilePage'][0]['graphql']['user']['edge_owner_to_timeline_media']['edges'][$i]['node']['display_url'];
        $url_list[] = $url_tmp;
    }
    return $url_list;
}
```

## Vista HTML

En la vista, se muestra cada imagen recuperada de Instagram.

```html
<div class="instagram-block">
    <h3>
        <i class="fab fa-instagram"></i>
        Instagram / <span><?= __('Fotos del día', 'admin') ?></span> <span class="peq"><a target="_blank" href="http://instagram.com/<?=Configure::read('InstagramAccount')?>">@<?=Configure::read('InstagramAccount')?></a></span>
    </h3>
    <div class="info">
        <?php foreach($instagram as $url): ?>
            <div class="imaxe">
                <a href="http://instagram.com/p/<?= $url['url_publication'] ?>" target="_blank" title="<?// $url['name_publication'] ?>">
                    <img class="instagram-image" src="<?= $url['url_image'] ?>" />
                </a>
            </div>
        <?php endforeach ?>
    </div>
</div>
```

## Estilos CSS

Aquí se proporcionan estilos CSS básicos para dar formato al bloque de Instagram y a las imágenes mostradas.

```css
.instagram-block {
    padding: 25px;
    margin-bottom: 50px;
}

.instagram-block h3 {
    line-height: 1em;
    font-size: 2.2em;
    color: #033565;
    font-family: 'Roboto', sans-serif;
    margin-bottom: 20px;
}

.instagram-block i {
    font-size: 1.8em;
    vertical-align: middle;
}

.instagram-block h3 span {
    font-weight: 300;
}

.instagram-block h3 .peq {
    font-size: .6em;
}

.instagram-block h3 a {
    color: black;
    font-size: 1em !important;
}

.instagram-block .info {
    background: none;
}

.instagram-block .info .imaxe {
    width: 300px;
    height: 300px;
    overflow: hidden;
    display: inline-block;
    vertical-align: top;
    margin-right: 25px;
}

.instagram-block .info .imaxe img {
    min-width: 300px;
    min-height: 300px;
    width: 300px;
}

.instagram-block .info .imaxe:last-child {
    margin-right: 0;
}
```

Estos fragmentos de código te permitirán mostrar las tres últimas imágenes de una cuenta de Instagram específica en tu aplicación CakePHP. Asegúrate de configurar adecuadamente la cuenta de Instagram en tu archivo `app.php` y adaptar el código según tus necesidades específicas.