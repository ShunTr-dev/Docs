---
title: scroll sin JS
date: 2024-10-27 00:00:00 -100
categories: [CSS, code-snippet]
tags: [herramientas]
---

```html
<!--
    @Author: Midudev
    @URL: https://www.youtube.com/watch?v=RwjgfNX41TE
-->

<style type="text/css">
    body {
        font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }

    #progress {
        position: fixed;
        top: 0;
        width: 0%;
        background: #09f;
        height: 1em;

        animation: progress-grow auto linear;

        /* Esta funcionalidad no está disponible en todos los navegadores, en su caso habrá que usar un polyfill (scroll-timeline) */
        animation-timeline: scroll(root block);
    }

    @keyframes progress-grow {
        0% {
            width: 0%;
        }
        100% {
            width: 100%;
        }

    }


    main {
        padding-top: 32px;
    }

</style>

<div id="progress">
</div>



<header>
    <h1>¡Descubre las maravillas de España!</h1>
</header>
<section id="ventajas">
    <h2>Ventajas de viajar a España</h2>
    <ul>
        <li>Una rica historia y patrimonio cultural.</li>
        <li>Gastronomía de clase mundial, desde tapas hasta paella.</li>
        <li>Una diversidad de paisajes, desde playas doradas hasta majestuosas montañas.</li>
        <li>Un clima envidiable durante la mayor parte del año.</li>
        <li>Hospitalidad y calidez de su gente.</li>
        <li>Festivales y celebraciones vibrantes durante todo el año.</li>
        <li>Una excelente red de transporte que facilita el movimiento entre ciudades y regiones.</li>
    </ul>
</section>
<section id="mejores-ciudades">
    <h2>Mejores ciudades para visitar en España</h2>
    <ul>
        <li>
            <h3>Barcelona</h3>
            <p>Qué ver: La Sagrada Familia, Parque Güell, Las Ramblas, Barrio Gótico.</p>
        </li>
        <li>
            <h3>Madrid</h3>
            <p>Qué ver: El Museo del Prado, Palacio Real, Parque del Retiro, Plaza Mayor.</p>
        </li>
        <li>
            <h3>Sevilla</h3>
            <p>Qué ver: La Catedral de Sevilla, la Plaza de España, el Barrio de Santa Cruz, el Real Alcázar.</p>
        </li>
        <li>
            <h3>Granada</h3>
            <p>Qué ver: La Alhambra, el barrio del Albaicín, la Capilla Real, el Generalife.</p>
        </li>
        <li>
            <h3>Valencia</h3>
            <p>Qué ver: La Ciudad de las Artes y las Ciencias, la Lonja de la Seda, la Catedral de Valencia, la Playa de la Malvarrosa.</p>
        </li>
        <li>
            <h3>San Sebastián</h3>
            <p>Qué ver: La Playa de la Concha, el casco antiguo, el Palacio de Miramar, la gastronomía basca.</p>
        </li>
        <li>
            <h3>Córdoba</h3>
            <p>Qué ver: La Mezquita-Catedral, el Puente Romano, el Alcázar de los Reyes Cristianos, los patios cordobeses.</p>
        </li>
        <li>
            <h3>Bilbao</h3>
            <p>Qué ver: El Museo Guggenheim, el Casco Viejo, el Puente Zubizuri, la gastronomía vasca.</p>
        </li>
        <li>
            <h3>Toledo</h3>
            <p>Qué ver: La Catedral de Toledo, el Alcázar de Toledo, la Iglesia de Santo Tomé, el Puente de San Martín.</p>
        </li>
        <li>
            <h3>Málaga</h3>
            <p>Qué ver: La Alcazaba, el Museo Picasso, la Playa de la Malagueta, el Casco Antiguo.</p>
        </li>
        <li>
            <h3>Salamanca</h3>
            <p>Qué ver: La Universidad de Salamanca, la Plaza Mayor, la Catedral Vieja, la Casa de las Conchas.</p>
        </li>
    </ul>
</section>
<footer>
    <p>¡Planifica tu viaje a España y sumérgete en una experiencia inolvidable!</p>
</footer>
</body>
```
