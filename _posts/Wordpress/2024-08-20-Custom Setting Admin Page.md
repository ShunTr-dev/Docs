---
title: Custom Setting Admin Page
date: 2024-08-20 00:00:00 -100
categories: [Wordpress]
tags: [herramientas]
---

# Página de Administrador Personalizada en WordPress

En el post anterior sobre páginas de administrador personalizadas de WordPress, definimos una página de administrador personalizada y explicamos cómo agregar una nueva página de administrador a WordPress.

Uno de los usos más importantes de las páginas de administrador personalizadas de WordPress son las páginas de configuración. Casi todos los plugins tienen páginas de configuración personalizadas, lo que permite a los desarrolladores tener una página de opciones para su plugin. Algunos plugins como Akismet solicitan códigos de integración y otros tienen la opción de habilitar o deshabilitar sus funciones. WooCommerce tiene varias opciones para personalizar la tienda, y todas ellas se implementan utilizando la API de Configuración.

En este post, profundizaremos en cómo crear una página de configuración personalizada en WordPress para lo que creamos en el post anterior. También agregaremos una nueva configuración y la interfaz de usuario requerida para ella. Luego guardaremos y usaremos este valor guardado en el sitio. Agregar una nueva configuración en WordPress

Para agregar nuevas configuraciones a WordPress, debemos usar la API de Configuración de WordPress. La API de Configuración es una API central que permite a los desarrolladores agregar una nueva página de configuración personalizada en WordPress.

Esto incluye funciones para registrar configuraciones, configurar la sección de configuración y los campos de configuración, renderizar el formulario y manejar errores. Antes de agregar configuraciones

Para el primer paso, necesitamos asegurarnos de tener un formulario y que esté configurado para funcionar con options.php. En el siguiente código que tenemos una función de devolución de llamada para generar el encabezado, necesitamos cargar las configuraciones para que las funciones de la API nos permitan que nuestras configuraciones personalizadas funcionen con WordPress.

El código del post anterior sobre cómo tener una página de administrador personalizada se puede acceder aquí.

Necesitamos cambiar la función my_admin_page_contents a lo siguiente:

```php
function my_admin_page_contents() {
    ?>
    <h1> <?php esc_html_e( 'Bienvenido a mi página de administración personalizada.', 'my-plugin-textdomain' ); ?> </h1>
    <form method="POST" action="options.php">
    <?php
    settings_fields( 'sample-page' );
    do_settings_sections( 'sample-page' );
    submit_button();
    ?>
    </form>
    <?php
}
```

Acabamos de cargar los campos de configuración y las secciones de configuración (que crearemos) y agregamos un botón de enviar para guardarlos. Sección de configuración

Una sección de configuración es parte de la API de configuración de WordPress que permite a los desarrolladores tener un grupo de configuraciones bajo un encabezado. Es posible agregar una sección de configuración a una página de administrador de WordPress existente o a una nueva página de administrador personalizada.

Aquí, vamos a agregar una nueva sección de configuración a nuestra página de administrador personalizada. Agregar una nueva sección de configuración

Ahora, procederemos a utilizar la función add_settings_section para tener una nueva sección de configuración en nuestra página de administrador personalizada que tenga sample-page como el slug.

```php
add_settings_section(
    'sample_page_setting_section',
    __( 'Configuraciones personalizadas', 'my-textdomain' ),
    'my_setting_section_callback_function',
    'sample-page'
);
```

En el código anterior, hemos agregado una nueva sección de configuración y los argumentos son:

```php
<?php add_settings_section( $id, $title, $callback, $page ); ?>
```

-   id Un slug personalizado para la sección de configuración.
-   title Título de la sección de configuración. Asegúrate de que sea traducible.
-   callback Una función que agrega marcados a la sección de configuración.
-   page El slug de la página en la que queremos agregar nuestra sección de configuración.

Como hemos usado una función de devolución de llamada (my_setting_section_callback_function), definámosla.

```php
function my_setting_section_callback_function( $args ) {
    echo '<p>Texto introductorio para nuestra sección de configuraciones</p>';
}
```

Y envolvamos nuestros códigos en una nueva función para llamarla en admin_init.

```php
add_action( 'admin_init', 'my_settings_init' );

function my_settings_init() {
    add_settings_section(
        'sample_page_setting_section',
        __( 'Configuraciones personalizadas', 'my-textdomain' ),
        'my_setting_section_callback_function',
        'sample-page'
    );
}

function my_setting_section_callback_function( $args ) {
    echo '<p>Texto introductorio para nuestra sección de configuraciones</p>';
}
```

El resultado será como el siguiente: Página de Configuración Personalizada en WordPress 1

Ten en cuenta que WordPress agrega automáticamente un botón Guardar cambios. Campos de configuración

Después de tener una sección para nuestras configuraciones, que incluye un título, marcado personalizado y botón de guardar, es hora de tener algunas configuraciones reales que nos permitirán obtener algunas entradas. Para hacerlo, usaremos la función settings_fields.

La función settings_fields no solo es para tener configuraciones y marcados de entrada, sino que también agrega nonce y se encarga de la seguridad, así como agrega las acciones y funcionalidades requeridas para asegurar que nuestras configuraciones funcionen. Agregar un nuevo campo de configuración

El uso

de la función settings_fields es como:

```php
add_settings_field(
   'my_setting_field',
   __( 'Mi campo de configuración personalizado', 'my-textdomain' ),
   'my_setting_markup',
   'sample-page',
   'sample_page_setting_section'
);
```

que es en realidad

```php
<?php add_settings_field( $id, $title, $callback, $page, $section, $args ); ?>
```

y los argumentos son:

-   id Un slug personalizado para el campo de configuración.
-   title Título del campo de configuración.
-   page El slug de la página en la que queremos mostrar el campo de configuración.
-   section La sección en la que queremos mostrar el campo de configuración.
-   $args Argumentos adicionales. Ver más aquí.

Al igual que al agregar una sección de configuración, tenemos una función de devolución de llamada que genera el marcado.

```php
function my_setting_markup() {
    ?>
    <label for="my_setting_field"><?php _e( 'Mi entrada', 'my-textdomain' ); ?></label>
    <input type="text" id="my_setting_field" name="my_setting_field" value="<?php echo get_option( 'my_setting_field' ); ?>">
    <?php
}
```

Deberíamos envolver la función settings_fields en nuestra función my_settings_init. Entonces nuestro código será:

```php
add_action( 'admin_init', 'my_settings_init' );

function my_settings_init() {
    add_settings_section(
        'sample_page_setting_section',
        __( 'Configuraciones personalizadas', 'my-textdomain' ),
        'my_setting_section_callback_function',
        'sample-page'
    );

    add_settings_field(
       'my_setting_field',
       __( 'Mi campo de configuración personalizado', 'my-textdomain' ),
       'my_setting_markup',
       'sample-page',
       'sample_page_setting_section'
    );

    register_setting( 'sample-page', 'my_setting_field' );
}

function my_setting_section_callback_function() {
    echo '<p>Texto introductorio para nuestra sección de configuraciones</p>';
}

function my_setting_markup() {
    ?>
    <label for="my_setting_field"><?php _e( 'Mi entrada', 'my-textdomain' ); ?></label>
    <input type="text" id="my_setting_field" name="my_setting_field" value="<?php echo get_option( 'my_setting_field' ); ?>">
    <?php
}
```

Y la salida será Página de Configuración Personalizada en WordPress 2

Si intentas guardar las configuraciones, es posible que veas algunos errores como opción de página no encontrada. La razón es que acabamos de agregar marcas, pero nuestras configuraciones aún no están registradas en WordPress, y no estamos listos para guardar valores en la base de datos de WordPress. Registrar configuraciones personalizadas en WordPress y guardar valores

La API de configuración de WordPress tiene la funcionalidad necesaria para obtener y guardar valores de una configuración. Por lo tanto, debemos usar la función register_setting. Con el siguiente código, registraremos nuestras configuraciones en WordPress.

```php
register_setting( 'sample-page', 'my_setting_field' );
```

Nuevamente, necesitamos usar eso en init. Entonces nuestro código será:

```php
add_action( 'admin_init', 'my_settings_init' );

function my_settings_init() {
    add_settings_section(
        'sample_page_setting_section',
        __( 'Configuraciones personalizadas', 'my-textdomain' ),
        'my_setting_section_callback_function',
        'sample-page'
    );

    add_settings_field(
       'my_setting_field',
       __( 'Mi campo de configuración personalizado', 'my-textdomain' ),
       'my_setting_markup',
       'sample-page',
       'sample_page_setting_section'
    );

    register_setting( 'sample-page', 'my_setting_field' );
}

function my_setting_section_callback_function() {
    echo '<p>Texto introductorio para nuestra sección de configuraciones</p>';
}

function my_setting_markup() {
    ?>
    <label for="my_setting_field"><?php _e( 'Mi entrada', 'my-textdomain' ); ?></label>
    <input type="text" id="my_setting_field" name="my_setting_field" value="<?php echo get_option( 'my_setting_field' ); ?>">
    <?php
}
```

Como paso final, necesitamos asegurarnos de que estamos mostrando el valor guardado en el formulario después de regresar a nuestra página de configuración personalizada en WordPress.

Agreguemos el siguiente código a la función my_setting_markup

```php
value="<?php echo get_option( 'my_setting_field' ); ?>"
```

Y será

```php
function my_setting_markup() {
    ?>
    <label for="my_setting_field"><?php _e( 'Mi entrada', 'my-textdomain' ); ?></label>
    <input type="text" id="my_setting_field" name="my_setting_field" value="<?php echo get_option( 'my_setting_field' ); ?>">
    <?php
}
```

Resumiendo, tendremos nuestro plugin:

```php
<?php

/*
 * Plugin Name: Mi página de administración personalizada
 * Description: Agrega páginas de administrador personalizadas con estilos y scripts de muestra.
 * Version: 1.0.0
 * Author: Artbees
 * Author URI: http://artbees.net
 * Text Domain: my-custom-admin-page
*/

function my_admin_menu() {
    add_menu_page(
        __( 'Página de muestra', 'my-textdomain' ),
        __( 'Menú de muestra', 'my-textdomain' ),
        'manage_options',
        'sample-page',
        'my_admin_page_contents',
        'dashicons-schedule',
        3
    );
}
add_action( 'admin_menu', 'my_admin

_menu' );

function my_admin_page_contents() {
    ?>
    <h1> <?php esc_html_e( 'Bienvenido a mi página de administración personalizada.', 'my-plugin-textdomain' ); ?> </h1>
    <form method="POST" action="options.php">
    <?php
    settings_fields( 'sample-page' );
    do_settings_sections( 'sample-page' );
    submit_button();
    ?>
    </form>
    <?php
}

add_action( 'admin_init', 'my_settings_init' );

function my_settings_init() {
    add_settings_section(
        'sample_page_setting_section',
        __( 'Configuraciones personalizadas', 'my-textdomain' ),
        'my_setting_section_callback_function',
        'sample-page'
    );

    add_settings_field(
       'my_setting_field',
       __( 'Mi campo de configuración personalizado', 'my-textdomain' ),
       'my_setting_markup',
       'sample-page',
       'sample_page_setting_section'
    );

    register_setting( 'sample-page', 'my_setting_field' );
}

function my_setting_section_callback_function() {
    echo '<p>Texto introductorio para nuestra sección de configuraciones</p>';
}

function my_setting_markup() {
    ?>
    <label for="my-input"><?php _e( 'Mi entrada' ); ?></label>
    <input type="text" id="my_setting_field" name="my_setting_field" value="<?php echo get_option( 'my_setting_field' ); ?>">
    <?php
}

?>
```

Ahora, tenemos una página de administrador personalizada que incluye una página de configuración personalizada en WordPress. Podemos guardar opciones en la base de datos y recuperarlas y usarlas para implementar funcionalidades complejas en nuestros plugins.

Para obtener el valor guardado de la configuración agregada, podemos usar la función get_option. El siguiente código devolverá el valor guardado para la configuración que hemos agregado en este post:

```php
get_option( 'my_setting_field' );
```
