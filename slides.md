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
layout: center
---

# Aktuelle Situation

---

## CMS und Sicherheitslücken

<!--
- [https://t3n.de/news/wordpress-sicherheitsluecken-1356976/](https://t3n.de/news/wordpress-sicherheitsluecken-1356976/)
- [https://t3n.de/news/woocommerce-sicherheitsluecke-wordpress-shopping-plugin-1392208/](https://t3n.de/news/woocommerce-sicherheitsluecke-wordpress-shopping-plugin-1392208/)
- [https://www.heise.de/news/Drupal-Team-beseitigt-potenziell-gefaehrliche-Sicherheitsluecke-aus-dem-CMS-6145534.html](https://www.heise.de/news/Drupal-Team-beseitigt-potenziell-gefaehrliche-Sicherheitsluecke-aus-dem-CMS-6145534.html)
-->
<div class="grid grid-cols-[1fr,1fr]">
  <img src="/cms-security-risks/article-1.png" class="p-4" />
  <img src="/cms-security-risks/article-2.png" class="p-4" />
  <img src="/cms-security-risks/article-3.png" class="p-4" />
</div>

---

## <noto-control-knobs /> Backends und Sicherheitslücken

<noto-hammer-and-wrench /> **Die Fertiglösungen**

- Brauchen regelmässige Pflege und Updates
- Benötigen ein sauberes und sicheres Setup
- Was tun wenn die Lösung nicht mehr maintained wird?

<noto-adhesive-bandage /> **Die Eigenbauten**

- ähnliche Probleme wie bei der Fertiglösung
- Alle Probleme müssen bedacht und abgedeckt werden
- Anfälligkeit für die Breach-Klassiker (SQL-Injection, XSS, ...)

<p class="text-center mt-8 text-red-300"><b><noto-red-exclamation-mark /> EInmal im System kann ein Angreifer die ganze Seite übernehmen <noto-red-exclamation-mark /></b></p>

---

## <noto-newspaper /> CMS und Wartungsaufwand

<noto-wrench /> **Wartung und Sicherheitsupdates**

- Ständige und zeitnahe Updates um Sicherheitslücken zu schliessen
- Wartung des Hostsystems notwendig

<noto-fire-extinguisher />**Feature Breaking und Portierung**

- Updates können Features brechen
- Aufwand der Portierung auf neü Version

<noto-exploding-head />**Plugin Hölle**

- Viele Plugins erzeugen viele Abhänigkeiten
- Wenn ein Plugin bricht, bricht vieles mit

<p class="text-center mt-8 text-red-300"><b><noto-red-exclamation-mark /> Dieser Zustand verschlimmert sich in der Regel mit dem Alter der Seite <noto-red-exclamation-mark /></b></p>

---

## Skalierungsprobleme

<noto-satellite-antenna /> **Webserver und Runtime**

- skalieren meistens noch recht gut
- Last kann je nach Komplexität spürbar werden

<noto-file-cabinet /> **Datenbank**

- schwer skalierbar
- Last kann auch hier zum Problem werden

<p class="text-center mt-8 text-red-300"><b><noto-red-exclamation-mark /> Grosse Last führt zu Unnereichbarkeit der Seite <noto-red-exclamation-mark /></b></p>

---
layout: center
---

<h1><noto-sparkles /> Static Sites to the rescü! <noto-sparkles /></h1>
<p class="text-center">Nein, natürlich nicht, aber sie lösen einige Probleme.</p>

---

## statische Seiten

<p class="text-yellow-200 font-bold text-center">
tl:dr; Webseiten ohne das klassische CMS Backend bzw. serverseitige Generierung
</p>

<div class="flex flex-col">
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">HTML</div><div class="text-sm text-gray-300">Gibt Struktur und Inhalt vor</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">CSS</div><div class="text-sm text-gray-300">Bestimmt das Aussehen der Seite</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Javascript und co.</div><div class="text-sm text-gray-300">Fügt <b>dynamische</b> Elemente zur Seite hinzu</div></div>
</div>

<div class="text-center mt-8"><b><noto-red-exclamation-mark /> Keine serverseitige Generierung <noto-red-exclamation-mark /></b></div>

---

## Static Site Generatoren - Was ist das?

<p class="text-yellow-200 font-bold text-center">
tl:dr; Tooling, das basierend auf Templates und Daten statische Seiten generiert
</p>

- Quasi der Werkzeugkasten der statischen Seite
- Strikte Trennung von Inhalt und Template/Frontend
- Generierung bei Deployment, nicht erst bei Aufruf
- Templates und Inhalt werden "verschmolzen"
- Generierung von Metadaten
- Zusätzliche Features
  - JS / CSS Bundling
  - Hashgenerierung
  - Bildverarbeitung
  - ...

---

## Beispiele für statische Seiten

<div class="grid grid-cols-[1fr,1fr] width-screen">
  <img src="/example-sites/site-1.png" class="p-4" />
  <img src="/example-sites/site-2.png" class="p-4" />
  <img src="/example-sites/site-3.png" class="p-4" />
  <img src="/example-sites/site-4.png" class="p-4" />
</div>

---
layout: center
---
## Bekannte SSGs

<div class="flex flex-wrap">
  <img src="/ssg-logos/hugo.png" class="m-12 h-12" />
  <img src="/ssg-logos/jekyll.png" class="m-12 h-12" />
  <img src="/ssg-logos/eleventy.png" class="m-12 h-12" />
  <img src="/ssg-logos/gatsby.png" class="m-12 h-12" />
  <img src="/ssg-logos/astro.png" class="m-12 h-12" />
</div>

---
layout: center
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

<h2 class="text-center pb-4">Ordnerstruktur Hugo</h2>

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
Layouts (überschreiben Themes)
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

- Daten mit denen die Seite gefüllt werden soll
- strukturiert und/oder semi strukturiert
- meist verschiedene Formate und Qüllen möglich
- Beispiel rechts: Inhalt darmstadt.ccc.de 

</template>

---

## Inhalte aus unstrukturierten Dateien

- Hauptsächlich Inhalt (hier Markdown)
- Metadaten
  - Allgemeins (Titel, Datum, ...)
  - SSG spezifisches (Menüposition, Template, ...)
  - eigenes wie etwa ein Headerbild (hier Hero)


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

---
layout: two-cols
---

<template v-slot:default>

## strukturierte Daten aus Dateien

- CSV, JSON, YAML, TOML
- eignet sich gut für Datensätze
- Layouting über Template
- Vermeidet Inkonsistenz

</template>
<template v-slot:right>

## strukturierte Daten aus APIs

- Daten werden beim Rendering aus API abgerufen
- bspw. gut mit Headless CMS oder bestehendem CMS
- REST / GraphQL
- Layouting über Template
- Vermeidet Inkonsistenz

</template>

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

- Grundgerüst der Seite.Sc
- Besteht meistens aus einerm Basistempalte
- Template wird befüllt mit Blöcken
- Typische Aufteilung in 3 Blökce (Header, Main, Foter)

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
- Perprocessing durch SSG oft möglich

---

## Deployment

- relativ einfach da statisch
- meistens CDN, normale Webserver gehen auch
- last nicht gross, da keine Runtime
- viele Anbieter mit integrierter CI, ansonsten CI selbst baün
- Triggering über Webhooks

---

## Vergleich CMS und Wartungsaufwand

**Wartung und Sicherheitsupdates**

- Seite gerendert -> kein Zugriff aufs Backend
- Wenn die Seite einmal online ist, braucht sie keine Updates da kein Rendering
- lediglich Backend benötigt Wartung

**Feature Breaking und Portierung**

- Inhalte über Standards
- Durch Standards in der Generierung Portierung sehr einfach

**Plugin Hölle**

- Plugins werden meist nicht benötigt
- können relativ gekapselt voneinander verwendet werden

---

## Skalierungsprobleme

**Webserver und Runtime**

- Webserver / CDN als einzige Limitation
- ausrollen sehr einfach

**Datenbank**

- Auch hier APIs als limitierender Faktor
  - Selbst wenn die Last gross ist, kann bereits Content an den Nutzer ausgeliefert werden (s. Hydration)

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

<!-- [Achieving lazy hydration in Vue 3 from scratch - LogRocket Blog](https://blog.logrocket.com/vue-3-lazy-hydration-from-scratch/) -->

**Problem:** Wir haben jetzt unsere Seite, aber wir brauchen dynamische Inhalte, wollen dabei aber schnell und durchsuchbar Content für alle liefern.

**Lösung:** Wir hängen uns in bestimmte Elemente der Seite nach dem Laden ein und füllen sie mit unseren interaktiven Inhalte. --> Hydration

**Partial Hydration**: Nur einzelne Teile einer Seite werden hydriert, und damit separiert

**Lazy Hydration**: Partial aber mit Entscheidung wann etwas hydriert wird

---

## DSG (Defered Site Generation)

<!-- >
[Server Side Rendering (SSR) vs. Client Side Rendering (CSR) vs. Pre-Rendering using Static Site Generators (SSG) and client-side hydration. | by Prashant Ram | Oct, 2021 | Medium](https://medium.com/@prashantramnyc/server-side-rendering-ssr-vs-client-side-rendering-csr-vs-pre-rendering-using-static-site-89f2d05182ef)
-->

- viele SSGs bieten alternative Rendering Optionen
- ermöglicht Flexibilität
- birgt aber auch Downsides
- Seiten bei Aufruf generiert
- So lange im Cache bis sich der Content ändert

---

## Hybride CMS

- gut für den Einstieg
- oder um alles an einer Stelle zu haben
- verschiedene Systeme implementieren das bereits
- Bspw. Kirby, Grav, Wordpress, ... haben Plugins
- NEOS setzt komplett auf diese Methode

---

# Fazit

- Sind SSGs die Antwort auf alles?
- Nein, aber sie lösen viele Probleme
- hohe Flexibilität
- geringer Wartungsaufwand
- hohe Geschwindigkeit

---
layout: center
---

# Vielen Dank
