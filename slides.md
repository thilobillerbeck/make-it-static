---
# try also 'default' to start simple
theme: apple-basic
# apply any windi css classes to the current slide
class: "text-center"
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
layout: center
---

# make-it-static

---
layout: image-right
image: https://source.unsplash.com/1600x900/?beach
---
# Wer bin ich?

Thilo Billerbeck B.Sc.

Master Informatik Student TU Darmstadt

- <simple-icons-mastodon /> @avocadoom@chaos.social
- <simple-icons-github /> @thilobillerbeck
- <simple-icons-twitter /> @thilobillerbeck
- <simple-icons-matrix /> @avocadoom:avocadoom.de

---

## CMS und Sicherheitsluecken

<!--
- [https://t3n.de/news/wordpress-sicherheitsluecken-1356976/](https://t3n.de/news/wordpress-sicherheitsluecken-1356976/)
- [https://t3n.de/news/woocommerce-sicherheitsluecke-wordpress-shopping-plugin-1392208/](https://t3n.de/news/woocommerce-sicherheitsluecke-wordpress-shopping-plugin-1392208/)
- [https://www.heise.de/news/Drupal-Team-beseitigt-potenziell-gefaehrliche-Sicherheitsluecke-aus-dem-CMS-6145534.html](https://www.heise.de/news/Drupal-Team-beseitigt-potenziell-gefaehrliche-Sicherheitsluecke-aus-dem-CMS-6145534.html)
-->
<div class="w-screen h-screen">
  <img src="/cms-security-risks/article-1.png" class="absolute top-0 left-0 m-40 h-40 rounded" />
  <img src="/cms-security-risks/article-2.png" class="absolute top-24 left-24 m-40 h-40 rounded" />
  <img src="/cms-security-risks/article-3.png" class="absolute top-0 left-48 m-40 h-40 rounded" />
</div>

---

## Generell Backends und Sicherheitsluecken

<noto-hammer-and-wrench /> **Die Fertigloesungen**

- Brauchen regelmaessige Pflege und Updates
- Benoetigen ein sauberes und sicheres Setup
- Was tun wenn die Loesung nicht mehr maintained wird?

<noto-adhesive-bandage /> **Die Eigenbauten**

- Aehnliche Probleme wie bei der Fertigloesung
- Alle Probleme muessen bedacht und abgedeckt werden
- Anfaelligkeit fuer die Breach-Klassiker (SQL-Injection, XSS, ...)

<div class="text-center mt-8"><b><noto-red-exclamation-mark /> EInmal im System kann ein Angreifer die ganze Seite uebernehmen <noto-red-exclamation-mark /></b></div>

---

## CMS und Wartungsaufwand

Wartung und Sicherheitsupdates

- Staendige und zeitnahe Updates um Sicherheitsluecken zu schliessen
- Wartung des Hostsystems notwendig

Feature Breaking und Portierung

- Updates koennen Features brechen
- Aufwand der Portierung auf neue Version

Plugin Hoelle

- Viele Plugins erzeugen viele Abhaenigkeiten
- Wenn ein Plugin bricht, bricht vieles mit

---

## Skalierungsprobleme

Webserver und Runtime

- skalieren meistens noch recht gut
- Last kann je nach Komplexitaet spuerbar werden

Datenbank

- schwer skalierbar
- Last kann auch hier zum Problem werden

<div class="text-center mt-8"><b><noto-red-exclamation-mark /> Grosse Last fuehrt zu Unnereichbarkeit der Seite <noto-red-exclamation-mark /></b></div>

---

## statische Seiten

tl:dr; Webseiten ohne das klassische CMS Backend bzw. serverseitige Generierung

- Bestandteile HTML, CSS, JS
- HTML und JS fuer vorab generierten Inhalt
- JS fuer dynamische Inhalte (bspw. von einer API)
- kein serverseitiges Scripting

---

## Static Site Generatoren - Was ist das?

tl:dr; Tooling, das basierend auf Templates und Daten statische Seiten generiert.

- Strikte Trennung von Inhalt und Template/Frontend
- Seiten werden bereits zur Bereitstellung anstatt zur Auslieferung generiert
- Verschmilzt Templates und Inhalt zu einer Seite
- Generierung von Metadaten
- Meist auch zustaendig fuer das Bundlen von CSS und co.

---

## Bekannte Seiten die mit SSGs gebaut wurden

- [https://gohugo.io/showcase/letsencrypt/](https://gohugo.io/showcase/letsencrypt/)
- [https://gohugo.io/showcase/1password-support/](https://gohugo.io/showcase/1password-support/)
- [https://ionicframework.com/](https://ionicframework.com/)
- [https://www.gatsbyjs.com/showcase/www.nationalgeographic.co.uk](https://www.gatsbyjs.com/showcase/www.nationalgeographic.co.uk)

---

## Vergleich CMS und Wartungsaufwand

**Wartung und Sicherheitsupdates**

- Seite gerendert -> kein Zugriff aufs Backend
- Wenn die Seite einmal online ist, braucht sie keine Updates da kein Rendering
- lediglich Backend benoetigt Wartung

**Feature Breaking und Portierung**

- Inhalte ueber Standards
- Durch Standards in der Generierung Portierung sehr einfach

**Plugin Hoelle**

- Plugins werden meist nicht benoetigt
- koennen relativ gekapselt voneinander verwendet werden

---

## Skalierungsprobleme

**Webserver und Runtime**

- Webserver / CDN als einzige Limitation
- ausrollen sehr einfach

**Datenbank**

- Auch hier APIs als limitierender Faktor
  - Selbst wenn die Last gross ist, kann bereits Content an den Nutzer ausgeliefert werden (s. Hydration)

---

## Bekannte SSGs

<div class="flex flex-wrap">
  <img src="/ssg-logos/hugo.png" class="m-12 h-12" />
  <img src="/ssg-logos/jekyll.png" class="m-12 h-12" />
  <img src="/ssg-logos/eleventy.png" class="m-12 h-12" />
  <img src="/ssg-logos/gatsby.png" class="m-12 h-12" />
  <img src="/ssg-logos/nextjs.png" class="m-12 h-12" />
  <img src="/ssg-logos/astro.png" class="m-12 h-12" />
</div>

---

# Wie funktionieren SSGs?

---

# Beispiel: darmstadt.ccc.de

![Local Image](/darmstadt-ccc-de.jpeg)

---
layout: center
---


<h2 class="text-center">Bausteine</h2>

<div class="flex flex-col">
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Inhalten / Daten</div><div class="text-sm text-gray-300">Markdown, YAML, JSON, ...</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Templates und / oder Themes</div><div class="text-sm text-gray-300">HTML Templates, Partials, ...</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Konfiguration</div><div class="text-sm text-gray-300">Config Files (TOML, YAML, ...</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">statische Assets</div><div class="text-sm text-gray-300">Bilder, Fonts, Scripts, Styles, ...</div></div>
</div>


---
layout: center
---

<h2 class="text-center">Ordnerstruktur Hugo</h2>

<div class="grid grid-cols-[1fr,3fr] width-screen">
<div class="font-bold bg-gray-800 p-2">
<mdi:file/> config.toml
</div>
<div class="w-full p-2">
Konfiguration
</div>

<div class="font-bold bg-gray-800 p-2">
<mdi:folder/> content
</div>
<div class="w-full p-2">
semi- und unstrukturierte Inhalt der Seite bspw. in Markdown
</div>

<div class="font-bold bg-gray-800 p-2">
<mdi:folder/> data
</div>
<div class="w-full p-2">
strukturierte Daten in YAML, JSON, TOML, ...
</div>

<div class="font-bold bg-gray-800 p-2">
<mdi:folder/> static
</div>
<div class="w-full p-2">
statische Assets
</div>

<div class="font-bold bg-gray-800 p-2">
<mdi:folder/> themes
</div>
<div class="w-full p-2">
Themes (meistens separates Repo)
</div>

<div class="font-bold bg-gray-800 p-2">
<mdi:folder/> layouts
</div>
<div class="w-full p-2">
Layouts (ueberschreiben Themes)
</div>

</div>
---
layout: two-cols
---

<template v-slot:default>

```bash
 |-impressum.md
 |-unterstuetzen.md
 |-hackspace.md
 |-freifunk.md
 |-c-radar.md
 |-wizardsofdos.md
 |-posts
 | |-2018-02-01-aktivitätsbericht-2017.md
 | |-2015-12-27-32C3.md
 | |-2018-10-14-hacktoberfest.md
 | |-2020-06-06-are-you-still-there.md
...
 |-kontakt.md
 |-termine.html

```

</template>
<template v-slot:right>

# Inhalte

This shows on the right

</template>

---
layout: two-cols
---

<template v-slot:default>

```markdown
---
layout: page
title: Freifunk
menu:
  left:
    weight: 4
hero: heroes/freifunk.jpg
---

[**Freifunk Darmstadt**](https://darmstadt.freifunk.net/)baut ein freies und
dezentrales WLAN-Netzwerk über Darmstadt auf und bietet darüber anonymen
Internetzugang an. Mittels handelsüblicher WLAN-Accesspoints kann jeder einen
Teil seiner Internet-Bandbreite oder eine tolle Location beitragen. Wenn du dich
schon immer gefragt hast, warum es hier kein öffentliches WLAN gibt, dann ist
Freifunk dein Projekt!
```

</template>
<template v-slot:right>

# Inhalte aus Dateien

This shows on the right

</template>

---

# Weitere Moelgichkeiten

Inhalte aus APIS
INhalte aus strukturierten Daten

---
layout: two-cols
---
<template v-slot:default>
<div class="bg-blue-500 h-100 m-4 p-4 flex flex-col">
<div class="pb-4 text-center">Base</div>
<div class="bg-red-500 p-4 text-center flex flex-col">Header</div>
<div class="bg-orange-500 p-4 text-center flex flex-col flex-1">Main</div>
<div class="bg-green-500 p-4 text-center flex flex-col">Footer</div>

</div>

</template>
<template v-slot:right>

## Themes

- Grundgeruest der Seite.Sc
- Besteht meistens aus einerm Basistempalte
- Template wird befuellt mit Bloecken
- Typische Aufteilung in 3 Bloekce (Header, Main, Foter)

<b class="text-red-300">Header: </b>Metadaten, CSS, JS, Icons, ...

<b class="text-orange-300">Main: </b>Content und Struktur, ...

<b class="text-green-300">Footer: </b>JS, Links, Copyright, ...

</template>

---

## Templates

- Bestimmen Aufbau der Seite
- spezifiziert Content Rendering
- meistens auch Einbindung der Assets und deren Verarbeitung

<b>Beispiel Hugo baseof.html: </b>
```html
<!DOCTYPE html>
<html lang="{{ .Site.LanguageCode }}" dir="{{ .Site.Language.LanguageDirection | default "ltr" }}">
  {{- partial "head.html" . -}}
  <body>
    {{- partial "header.html" . -}} {{- block "main" . }}{{- end }} {{- partial
    "footer.html" . -}} {{- partial "scripts.html" . -}}
  </body>
</html>
```

---

<b>Beispiel Hugo Auszug head.html: </b>

```html
<head>
  ...
  <title>
    {{ if not .Page.IsHome }} {{ .Page.Title }} | {{ end }}{{ .Site.Title }}
  </title>
  <meta name="description" content="{{ .Site.Params.description }}" />
  ...

  {{ $styles := resources.Get "scss/main.scss" | toCSS | minify | fingerprint
  "sha512" }}
  <link
    rel="stylesheet"
    media="screen"
    href="{{ $styles.Permalink }}"
    integrity="{{ $styles.Data.Integrity }}"
    media="screen"
  />
  ...
</head>
```

---

<b>Beispiel Hugo Auszug single.html: </b>

```html
{{ define "main" }}
<div>
  <h1>{{ .Title }}</h1>
</div>
<main>{{ .Content }}</main>
{{ end }}
```

---

## statische Assets

- werden meistens in einem eigenen Ordner abgelegt
- meistens Bilder, Fonts, CSS, Javascript, ...
- meist durch absolute Pfade in Template und Inhalt nutzbar
- Perprocessing durch SSG oft moeglich

---

## Deployen

- relativ einfach da statisch
- meistens CDN, normale Webserver gehen auch
- last nicht gross, da keine Runtime
- viele Anbieter mit integrierter CI, ansonsten CI selbst bauen
- Triggering ueber Webhooks

---

## Umstellung des Workflows am Beispiel Wordpress API

- Wordpress API
  - [REST API Handbook | WordPress Developer Resources](https://developer.wordpress.org/rest-api/)
- Medium
- etc.\
- Converter

---

# Advanced Stuff

## Hydration

[Achieving lazy hydration in Vue 3 from scratch - LogRocket Blog](https://blog.logrocket.com/vue-3-lazy-hydration-from-scratch/)

**Problem:** Wir haben jetzt unsere Seite, aber wir brauchen dynamische Inhalte, wollen dabei aber schnell und durchsuchbar Content fuer alle Content liefern.

**Loesung:** Wir haengen uns in bestimmte Elemente der Seite nach dem Laden ein und fuellen sie mit unseren interaktiven Inhalte. --> Hydration

**Partial Hydration**: Nur einzelne Teile einer Seite werden hydriert, und damit separiert

**Lazy Hydration**: Partial aber mit Entscheidung wann etwas hydriert wird

---

## Partial Server Side Rendering

[Server Side Rendering (SSR) vs. Client Side Rendering (CSR) vs. Pre-Rendering using Static Site Generators (SSG) and client-side hydration. | by Prashant Ram | Oct, 2021 | Medium](https://medium.com/@prashantramnyc/server-side-rendering-ssr-vs-client-side-rendering-csr-vs-pre-rendering-using-static-site-89f2d05182ef)

---

## Hybride CMS

- gut fuer den Einstieg
- oder um alles an einer Stelle zu haben
- verschiedene Systeme implementieren das bereits
- Bspw. Kirby, Grav, Wordpress, ... haben Plugins
- NEOS setzt komplett auf diese Methode

---

# Fazit

---
layout: center
---

# Vielen Dank
