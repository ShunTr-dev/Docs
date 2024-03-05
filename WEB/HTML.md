HTML - Hypertext Markup Language

De qué se encarga HTML?

NO: La presentación -> CSS
NO: La interactividad -> JavaScript
SI: Describir el contenido

Los archivos con HTML tienen extenión .html, el archivo raíz es el index.html

HTML  funciona con etiquetas. Por ejemplo. los títulos se ponen con la etiqueta h1, h2, h3,...

<h1> HTML básico </h1>

'h1': es la etiqueta.
'<h1> HTML básico </h1>': es el elemento (HTML)

Todas las etiquetas deben de tener una etiqueta de apertura y de cierre. Puede ser en la misma línea o en otra.
Excepto los elementos reemplazables que no tienen por qué cerrarse como img o input

Para poder ver el archivo creado en el navegador, se puede navegar con el explorador de archivos hasta él y abrirlo con el navegador.

El atributo hidden (que es global) oculta el elemento, es un atributo booleano, lo que quiere decir que si está presente se ocultará el elemento. Si no,no. Da igual que le pongas hidden="true" o hidden="false" mientras esté presente el elemento se ocultará.

El atributo id="" funciona como un identificador. Y debe de ser único.
El atributo class="" funciona como una referencia y puede ser múltiple.

La etiqueta de b está deprecated, por que hace referencia a la presentación (los estilos) del documento. Sin embargo tenemos etiquetas que sí hacen referencia a los estilos, como h1, esto es por que los navegadores tienen una serie de estilos por defecto. Se llaman USER AGENT STYLESHEET.





Página mínima

El módulo doctype es necesario por que algunos navegadores si no lo pones entran en otro modo de HTML, pero la gran mayoría de ellos no tienen problema o lo añaden ellos.

En el head ponemos metadatos y otros archivos, es un lugar donde lo que pongamos no se va a renderizar.
En el body ponemos nuestro contenido

<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8"> <!-- codificación -->
        <meta name="viewport" content="width=device-width"> <!-- Le decimos que el ancho del contenido es el ancho de la pantalla -->
        <title>Title</title> <!-- Título de la pestaña, tiene MUCHO peso en SEO, es el título que aparece en el buscador -->
        <meta name="description" content="Descripción del contenido de la página"> <!-- SUPER importante para el SEO, es lo que puede aparecer en la entradilla en el buscador -->
        <meta name="author" content="name">
        <meta name="keywords" content="keywords">
        <!-- OPEN GRAPH -->
        <!-- Conjunto de etiquetas creadas por Facebook para que cuando se comparte un contenido se vea bien -->
        <!-- Puedes ir a https://www.opengraph.xyz para ver como ses vería compartido un elemento -->
        <!-- Facebook Meta Tags -->
        <meta property="og:url" content="https://tuURL/">
        <meta property="og:type" content="website">
        <meta property="og:title" content="Título que queremos que aparezca en la caja">
        <meta property="og:description" content="Descripción que aparece debajo del título">
        <meta property="og:image" content="https://tuUrl/img/tuIMG.jpg">
        <meta property="og:image:alt" content="Descripción de la imagen">
        <!-- Twitter Meta Tags -->
        <meta name="twitter:card" content="summary_large_image">
        <meta property="twitter:domain" content="tuURL.es">
        <meta property="twitter:url" content="https://www.tuURL.es/">
        <meta name="twitter:title" content="Título que queremos que aparezca en la caja">
        <meta name="twitter:description" content="Descripción que aparece debajo del título">
        <meta name="twitter:image" content="https://tuUrl/img/tuIMG.jpg">
        <meta name="robots" content="index, follow"> <!-- Le decimos a los buscadores si tienen que indexar la página y si tienen que seguir los enlaces -->
        <meta name="theme-color" content="#09f"> <!-- Cambia la parte de arriba del navegador, haciendo la página más amigable y corporativa -->
        <link rel="icon" type="image/jpg" href="/img/favicon.jpg"> <!-- Favicon, por defecto suele intentar cargar el favicon.ico -->
        <link rel="alternate" href="https://tuUrl/en" hreflang="en-GB"> <!-- Enlazar a un link alternativo (Por ejemplo la página pero en otro idioma), MUY importante para el SEO, si no se pone puede advertir como contenido duplicado -->
        <link rel="canonical" href="https://tuUrl/"> <!-- Indicamos la página principal del sitio, importante para el SEO -->
        <link href="style.css" rel="stylesheet" type="text/css" />
        <style type="text/css">
            body {
                background: #09f;
            }
        </style>
        <script src="script.js"></script>
        <script>
            // Javascript code
        </script>
    </head>
    <body>
        <!-- content here -->
    </body>
</html>

HTML Semántico

Hacer que las etiquetas tengan un significado



<body>
    <header>
        <h1>A como etiqueta de enlace</h1>
        <nav>
            <a href="#subtitulo"> <!-- Enlace interno-->
            <a href="https://tuUrl.es" target="_blank" rel="noreferer"> <!-- Enlace externo en una página nueva, no envía la cabeceza de referido -->
        </nav>
    </header>
    <main> <!-- La etiqueta main sólo puede estar UNA vez en todo el contenido y es el que marca el contenido principal de la página-->
        <p>
            Párrafo con el contenido de la página
            <strong>Elemento con peso importante dentro del párrafo (En negrita)</strong>
        </p>
        <h2 id="subtitulo">Subtitulo</h2>
        <ul>
            <li class="list-item">Elemento de la lista</li>
            <li class="list-item">Elemento de la lista</li>
            <li class="list-item">Elemento de la lista</li>
        </ul>
    </main>
    <footer>
        Copyright today
    </footer>
</body>








<h1>Main heading</h1> Para poner los títulos, van de h1 a h6 
<!-- etc -->
<h6>Level-6 heading</h6>

tag 	element
h1 	main heading
h6 	least important heading
Paragraphs

<p>Paragraph.<br/> 
Other line.</p>
<p>Other paragraph.</p>
<hr/>
<p>See the line above.</p>

tag 	element
p 	paragraph
br 	line break
hr 	horizontal line
Formatting

<em>Formatting</em> is <strong>important</strong> !
(a+b)<sup>2</sup> = a<sup>2</sup> + b<sup>2</sup> + 2ab

tag 	element
sub 	subscript
sup 	superscript
em 	emphasize
strong 	important
mark 	highlighted
small 	small
i 	italic
b 	bold
Quotes

<cite>This book</cite> was written by this author.
<q cite="url">quotation</q>
<blockquote cite="url">
Lorem ipsum<br/>
Lorem ipsum
</blockquote>

tag 	element
cite 	title of a work
q 	inline quotation
blockquote 	quotation
Content
Links

<a href="url">link</a>
<a href="url" target=_blank>open in a new window</a>

<a href="#comments">watch comments</a>
<h2 id="comments">comments</h2>

tag 	element
a 	hyperlink
Images

<img src="image.png" alt="description" width="300" height="200" title="información relacionada con la imagen, aparece con un tooltip"/>

El atributo de alt es muy importante para el SEO
tag 	element
img 	image
Blocks

<div>block</div>
<span>inline</span>

tag 	element
div 	block-level element
span 	inline element
Lists
Unordered list

<ul>
    <li>item</li>
    <li>item</li>
    <li>item</li>
</ul>

tag 	element
ul 	unordered list
li 	list item
Ordored list

<ol>
    <li>first</li>
    <li>second</li>
    <li>third</li>
</ol>

tag 	element
ol 	ordered list
li 	list item
Definition list

<dl>
    <dt>term</dt><dd>definition</dd>
    <dt>term</dt><dd>definition</dd>
    <dt>term</dt><dd>definition</dd>
</dl>

tag 	element
dl 	definition list
dt 	term
dd 	definition
Tables
Basic table

<table>
<tr>
    <th>heading 1</th>
    <th>heading 2</th>
</tr>
<tr>
    <td>line 1, column 1</td>
    <td>line 1, column 2</td>
</tr>
<tr>
    <td>line 2, column 1</td>
    <td>line 2, column 2</td>
</tr>
</table>

tag 	element
table 	table
tr 	table row
th 	table heading
td 	table cell
Advanced table

<table>
<caption>caption</caption>
<colgroup>
    <col span="2" style="..." />
    <col style="..." />
</colgroup>
<thead>
    <tr>
        <th>heading 1</th>
        <th>heading 2</th>
        <th>heading 3</th>
    </tr>
</thead>
<tfoot>
    <tr>
        <th>footer 1</th>
        <th>footer 2</th>
        <th>footer 3</th>
    </tr>
</tfoot>
<tbody>
    <tr>
        <td>line 1, column 1</td>
        <td>line 1, column 2</td>
        <td>line 1, column 3</td>
    </tr>
    <tr>
        <td>line 2, column 1</td>
        <td>line 2, column 2</td>
        <td>line 2, column 3</td>
    </tr>
</tbody>
</table>

tag 	element
caption 	caption
colgroup 	defines groups of columns
col 	defines column's properties
thead 	groups headings together
tfoot 	groups footers together
tbody 	groups other rows
Forms

<form action="url" method="post">
    <fieldset>
        <legend>Who are you ?</legend>
        <label>Login :<input type="text" name="login" /></label><br/>
        <label for="pswd">Password :</label><input type="password" name="password" id="pswd" /><br/>
        <input type="radio" name="sex" value="male" />Male<br/>
        <input type="radio" name="sex" value="female" />Female<br/>
    </fieldset>
    
    <label>Your favorite color : <select name="color">
        <option>red</option>
        <option>green</option>
        <option>blue</option>
    </select></label>
    
    <input type="checkbox" name="available" value="monday" />Monday<br/>
    <input type="checkbox" name="available" value="tuesday" />Tuesday<br/>
    
    <textarea name="comments" rows="10" cols="30" placeholder="Write your comments here"><textarea/>
    
    <input type="submit" value="Button text">
</form>

tag 	element
form 	form
label 	label for input
fieldset 	group inputs together
legend 	legend for fieldset
input type="text" 	text input
input type="password" 	password input
input type="radio" 	radio button
input type="checkbox" 	checkbox
input type="submit" 	send form
select 	drop-down list
option 	drop-down list item
optgroup 	group of drop-down list items
datalist 	autocompletion list
textarea 	large text input
HTML5 Semantic
Page layout

<header>My website</header>
<nav>
    <a href="page1">Page 1</a>
    <a href="page2">Page 2</a>
    <a href="page3">Page 3</a>
</nav>

<section>
    Hello everybody, Welcome to my website !
</section>

<article>
    <header>
        <h2>Title</h2>
    </header>
    <p>
        My article
    </p>
</article>

<aside>
    Writen by me
</aside>

<section id="comments">
    <article>Comment 1</article>
    <article>Comment 2</article>
</section>

<footer>
Copyright notice
</footer>

tag 	element
header 	header of document or section
footer 	footer of document or section
section 	section
article 	article, forum post, blog post, comment
aside 	aside content related to surrounding content
nav 	navigation links
New elements

<figure>
    <img src="image.png" alt="figure 1" />
    <figcaption>Figure 1</figcaption>
</figure>

<details>
    <summary>Declaration of M. X on <time datetime="2013-12-25">Christmas day</time></summary>
    <p>M. X said...</p>
</details>

Downloading progress : <progress value="53" max="100"></progress>
Disk space : <meter value="62" min="10" max="350"></meter>

tag 	element
figure 	an illustration
figcaption 	caption of a figure element
details 	details that can be shown or hidden
summary 	visible heading of a details element
progress 	progress of a task
meter 	display a gauge
time 	machine-readable time indication