# WordPress-Code-Schnipsel

Code-Schnipsel die so anfallen wenn man ein **neues WordPress-Theme** erstellt...

## header.php

Hier ein paar Schnipsel, die in den Kopf des Dokumentes kommen.

Wenn man ein Theme für internationales Publikum erstellt, dann kommt am Anfang, nach Angabe des Doctypes, die Berücksichtigung der **Sprache des Inhalts**:

``` php
<html <?php language_attributes(); ?>>
```

Ist das Theme nur z.B. für den Einsatz im deutschsprachigen Raum gedacht, dann kann man stattdessen auch folgendes notieren:

``` html
<html lang="de">
```

Die nächste variable Angabe betrifft den **benutzen Zeichensatz**, dynamische Notierung schaut so aus:

``` php
<meta charset="<?php bloginfo('charset'); ?>" />
```

In der Regel sollte allerdings für Europa UTF-8 ausreichen:

``` html
<meta charset="utf-8" />
```
Hier die einfache Angabe um den **Seitentitel** zu generieren:

``` php
<title><?php wp_title('|', true, 'right'); ?></title>
```

Eine etwas ausgefeiltere Variante:

``` php
<?php if (is_home() or is_front_page()) { ?>
<title><?php bloginfo('name'); ?> - <?php bloginfo('description'); ?></title>
<?php }
elseif(is_category() or is_archive() or is_page() or is_single()) { ?>
<title><?php wp_title(''); ?> &raquo; <?php bloginfo('name'); ?></title>
<?php } else { ?>
    <title><?php bloginfo('name'); ?><?php wp_title(); ?> - <?php bloginfo('description'); ?> | <?php bloginfo(); ?></title>
<?php } ?>
```

Falls die Einbindung der **CSS-Datei** nicht in der functions.php definiert wurde kann man sie auch so einbinden:

``` php
<link rel="stylesheet" type="text/css" media="all" href="<?php bloginfo('stylesheet_url'); ?>" />
```

Falls man **Pingbacks** zulassen möchte:

``` php
<link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>" />
```
Und als letzte Angabe vor `</head>` folgt der **Header-Hook**, der z.B. Angaben aus Plugins oder Funktionen zwischen `<head>` und `</head>` einfügt. Deswegen sollte er auf jeden Fall vorhanden sein:

```php
<?php wp_head(); ?>
```

Je nach Unterseite bekommt durch folgende Angaben, dass öffnende `body`-Tag **zusätzliche Klassenwerte**, was eine leichtere Ansprache durch CSS-Regeln ermöglicht:

```php
<body <?php body_class(); ?>>
```