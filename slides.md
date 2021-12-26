---
theme: apple-basic
class: "text-center"
highlighter: shiki
download: true
lineNumbers: true
info: |
  # Make it static!
  **Ein Einsteiger-Talk über statische Webseiten, wie man sie erstellt oder auf diese umstellt und dabei seinen bisherigen Workflow beibehält und welche Vor- und Nachteile diese mit sich bringen.**

  "Statische Webseiten, das hat man doch nur zu den Geburtszeiten des Internets benutzt.". Naja, nicht ganz, mittlerweile geht der Trend wieder vom klassischen Backend mit dynamischer Seitengenerierung zurück zu statischen Seiten. Ganz getreu dem Motto "Back to Basics" geht es in diesem Vortrag genau um dieses Thema: "Was sind statisch generierte Webseiten? Und was fange ich damit an?"

  Eine eigene Internetpräsenz zu haben ist mittlerweile keine Seltenheit mehr und wir Wesen beziehen mittlerweile einen Großteil unserer Informationen dorther. Dabei besteht die große Menge dieser Informationsquellen aus Seiten mit einem Backend, welches diese dynamisch generiert. Was auf den ersten Blick unproblematisch klingt kann gerade im Hinblick auf Wartung und Auslastung ein Problem werden. Mit Sicherheit hast du auch schon von Webseiten gehoert, die aufgrund eines veralteten CMS gekapert wurden. Aber muss das wirlich sein? Nein, denn mittlerweile ist das statische Generieren von Webseiten eine echte Alternative und nicht nur eine Sache, die Nerds vorbehalten ist. In diesem Talk erfährst du, was statische Seiten ausmacht, welche Ansätze du wählen kannst, um sie mit Inhalten zu füllen, und wie du trotzdem deinen bisherigen Workflow beibehalten kannst. Außerdem klären wir, was zur Hoelle Hydrierung mit Webseiten zu tun hat und wie du Datenverarbeitung mit einem Hybridansatz ermoeglichen kannst.
drawings:
  persist: false
layout: center
---

# make-it-static

---
class: "text-center"
layout: center
---

# Slides
https://make-it-static.thilo-billerbeck.com
<img src="/qr.png" class="p-4" alt="https://make-it-static.thilo-billerbeck.com" />


---
layout: image-right
image: me.jpg
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
  <img src="/cms-security-risks/article-1.png" class="p-4" alt="Artikel: Drupal Team beseitigt potenziell gefaehrliche Sicherheitsluecke aus dem CMS." />
  <img src="/cms-security-risks/article-2.png" class="p-4" alt="Artikel: Schwere Sicherheitsluecke in Woocommerce: Shopbetreiber sollten dringend updaten." />
  <img src="/cms-security-risks/article-3.png" class="p-4" alt="Artikel: Wordpress: Sicherheitsluecken in beliebtem Plugin betreffen 1 Million Websites" />
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

<p class="text-center mt-8 text-red-300 light:text-red-600"><b><noto-red-exclamation-mark /> EInmal im System kann ein Angreifer die ganze Seite übernehmen <noto-red-exclamation-mark /></b></p>

---

## <noto-newspaper /> CMS und Wartungsaufwand

<noto-wrench /> **Wartung und Sicherheitsupdates**

- Ständige und zeitnahe Updates um Sicherheitslücken zu schliessen
- Wartung des Hostsystems notwendig

<noto-fire-extinguisher />**Feature Breaking und Portierung**

- Updates können Features brechen
- Aufwand der Portierung auf neue Version

<noto-exploding-head />**Plugin Hölle**

- Viele Plugins erzeugen viele Abhänigkeiten
- Wenn ein Plugin bricht, bricht vieles mit

<p class="text-center mt-8 text-red-300 light:text-red-600"><b><noto-red-exclamation-mark /> Dieser Zustand verschlimmert sich in der Regel mit dem Alter der Seite <noto-red-exclamation-mark /></b></p>


---

## Skalierungsprobleme

<noto-satellite-antenna /> **Webserver und Runtime**

- skalieren meistens noch recht gut
- Last kann je nach Komplexität spürbar werden

<noto-file-cabinet /> **Datenbank**
<img src="/qr.png" class="p-4" alt="https://make-it-static.thilo-billerbeck.com" />
layout: center
---

<h1><noto-sparkles /> Static Sites to the rescue! <noto-sparkles /></h1>
<p class="text-center">Nein, natürlich nicht, aber sie lösen einige Probleme.</p>

---

## statische Seiten

<p class="text-yellow-200 light:text-yellow-500 font-bold text-center">
tl:dr; Webseiten ohne das klassische CMS Backend bzw. serverseitige Generierung
</p>

<div class="flex flex-col">
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">HTML</div><div class="text-sm text-gray-300 light:text-gray-500">Gibt Struktur und Inhalt vor</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">CSS</div><div class="text-sm text-gray-300 light:text-gray-500">Bestimmt das Aussehen der Seite</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Javascript und co.</div><div class="text-sm text-gray-300 light:text-gray-500">Fügt <b>dynamische</b> Elemente zur Seite hinzu</div></div>
</div>
todo
<p class="text-yellow-200 light:text-yellow-500 font-bold text-center">
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
  <img src="/example-sites/site-1.png" class="p-4" alt="Screenshot: National Geographic Website" />
  <img src="/example-sites/site-2.png" class="p-4" alt="Screenshot: ionic Website" />
  <img src="/example-sites/site-3.png" class="p-4" alt="Screenshot: 1Password Hilfe Website" />
  <img src="/example-sites/site-4.png" class="p-4" alt="Screenshot: Let's Encrypt Website" />
</div>

---
layout: center
---
## Bekannte SSGs

<div class="flex flex-wrap light:bg-gray-800 rounded ">
  <img src="/ssg-logos/hugo.png" class="m-12 h-12" alt="Logo: Hugo" />
  <img src="/ssg-logos/jekyll.png" class="m-12 h-12" alt="Logo: Jekyll" />
  <img src="/ssg-logos/eleventy.png" class="m-12 h-12" alt="Logo: Eleventy" />
  <img src="/ssg-logos/gatsby.png" class="m-12 h-12" alt="Logo: Gatsby" />
  <img src="/ssg-logos/astro.png" class="m-12 h-12" alt="Logo: Astro" />
</div>

---
layout: center
---
# Wie funktionieren SSGs?

---

# Beispiel: darmstadt.ccc.de

![Screenshot: darmstadt.ccc.de](/darmstadt-ccc-de.jpeg)

---
layout: center
---


<h2 class="text-center">Bausteine</h2>

<div class="flex flex-col">
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Inhalten / Daten</div><div class="text-sm text-gray-300 light:text-gray-500">Markdown, YAML, JSON, ...</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Templates und / oder Themes</div><div class="text-sm text-gray-300 light:text-gray-500">HTML Templates, Partials, ...</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">Konfiguration</div><div class="text-sm text-gray-300 light:text-gray-500">Config Files (TOML, YAML, ...</div></div>
<div class="p-4 border border-gray-500 m-2"><div class="font-bold">statische Assets</div><div class="text-sm text-gray-300 light:text-gray-500">Bilder, Fonts, Scripts, Styles, ...</div></div>
</div>


---
layout: center
---

<h2 class="text-center pb-4">Ordnerstruktur Hugo</h2>

<div class="grid grid-cols-[1fr,3fr] width-screen">
<div class="font-bold bg-gray-800 p-2 text-gray-100">
<mdi:file/> config.toml
</div>
<div class="w-full p-2">
Konfiguration
</div>

<div class="font-bold bg-gray-800 p-2 text-gray-100">
<mdi:folder/> content
</div>
<div class="w-full p-2">
semi- und unstrukturierte Inhalt der Seite bspw. in Markdown
</div>

<div class="font-bold bg-gray-800 p-2 text-gray-100">
<mdi:folder/> data
</div>
<div class="w-full p-2">
strukturierte Daten in YAML, JSON, TOML, ...
</div>

<div class="font-bold bg-gray-800 p-2 text-gray-100">
<mdi:folder/> static
</div>
<div class="w-full p-2">
statische Assets
</div>

<div class="font-bold bg-gray-800 p-2 text-gray-100">
<mdi:folder/> themes
</div>
<div class="w-full p-2">
Themes (meistens separates Repo)
</div>

<div class="font-bold bg-gray-800 p-2 text-gray-100">
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

- Grundgerüst der Seite
- Besteht meistens aus einerm Basistempalte
- Template wird befüllt mit Blöcken
- Typische Aufteilung in 3 Blöcke (Header, Main, Foter)

<b class="text-red-300">Header: </b>Metadaten, CSS, JS, Icons, ...

<b class="text-orange-300">Main: </b>Content und Struktur, ...

<b class="text-green-300">Footer: </b>JS, Links, Copyright, ...

</template>

---
layout: two-cols
---

<template v-slot:default>
<div class="h-100 m-4 p-4 flex flex-col font-mono">
<div class="p-2 text-gray-400 light:text-gray-600">{ extend "template42" }</div>
<div class="p-2">{{ "<article>" }}</div>
<div class="p-2">
{{ "<h1>" }}
<span class="bg-red-800 light:bg-red-200">Titelvariable</span>
{{ "</h1>" }}
</div>
<div class="p-2">{{ "<div class='rc3-is-awesome'>" }}</div>

<div class="p-2">
<span class="bg-blue-800 light:bg-blue-200">Inhaltsvariable</span>
</div>

<div class="p-2">{{ "</div>" }}</div>
<div class="p-2">{{ "</article>" }}</div>

<div class="p-2 text-gray-400 light:text-gray-600">{ end }</div>

</div>

</template>
<template v-slot:right>

## Templates

- Bestimmen Aufbau der Seite
- spezifiziert Content Rendering
- meistens auch Einbindung der Assets und deren Verarbeitung

</template>

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

## statische Assets

- werden meistens in einem eigenen Ordner abgelegt
- meistens Bilder, Fonts, CSS, Javascript, ...
- meist durch absolute Pfade in Template und Inhalt nutzbar
- Preprocessing durch SSG oft möglich

---

## Deployment

- relativ einfach da statisch
- meistens CDN, normale Webserver gehen auch
- Last gering, da keine Runtime
- viele Anbieter mit integrierter CI, ansonsten CI selbst baün
- Triggering über Webhooks

---

## Vergleich CMS und Wartungsaufwand

<noto-wrench /> **Wartung und Sicherheitsupdates**

- ein Zugriff aufs Backend
- wenn die Seite einmal online ist, braucht sie keine Updates da kein Rendering
- lediglich Backend benötigt Wartung

<noto-fire-extinguisher />**Feature Breaking und Portierung**

- Inhalte über Standards
- Durch Standards in der Generierung Portierung sehr einfach

<noto-exploding-head />**Plugin Hölle**

- Plugins werden meist nicht benötigt
- können relativ gekapselt voneinander verwendet werden

---

## Skalierungsprobleme

<noto-satellite-antenna /> **Webserver und Runtime**

- Webserver / CDN als einzige Limitation
- ausrollen sehr einfach

<noto-file-cabinet /> **Datenbank**

- Auch hier APIs als limitierender Faktor
  - Selbst wenn die Last gross ist, kann bereits Content an den Nutzer ausgeliefert werden (s. Hydration)

---

## Umstellung des Workflows am Beispiel Wordpress API

- viele CMS bieten APIs (Wordpress, Medium, ...)
- alternative Konverter / Exporter
- Vorteil APIs, Workflow von Autor*innen beibehalten
- CMS holt sich bei Rendering Content von API
- Build Server braucht Internetverbindung!

<div class="text-4xl text-center mt-8 grid grid-cols-5 w-max gap-4">
<div/><div/><mdi-wordpress /><div/><div/>
<div/><div/><mdi-arrow-up /><div/><div/>
<mdi-language-html5 /> <mdi-arrow-right /> <mdi-server /> <mdi-arrow-right /> <mdi-server-network /> 
</div>
---

# Advanced Stuff

## Hydration

<!-- [Achieving lazy hydration in Vue 3 from scratch - LogRocket Blog](https://blog.logrocket.com/vue-3-lazy-hydration-from-scratch/) -->

**Problem:** Wir haben jetzt unsere Seite, aber wir brauchen dynamische Inhalte, wollen dabei aber schnell und durchsuchbar Content für alle liefern.

**Lösung:** Wir hängen uns in bestimmte Elemente der Seite nach dem Laden ein und füllen sie mit unseren interaktiven Inhalte. --> Hydration

**Partial Hydration**: Nur einzelne Teile einer Seite werden hydriert, und damit separiert

**Lazy Hydration**: Partial aber mit Entscheidung wann etwas hydriert wird

<div class="text-sm justify-center content-center flex flex-row">

<div class="border p-4 justify-center content-center flex flex-col">
<div>Loading</div>
</div>

<mdi-arrow-right class="text-2xl m-4" />

<div class="border p-4 justify-center content-center flex flex-col">
<b>Title</b>
<div class="bg-orange-800 light:bg-orange-200">
<div>Entry-1</div>
<div>Entry-2</div>
</div>
</div>


<mdi-arrow-right class="text-2xl m-4" />

<div class="border p-4 justify-center content-center flex flex-col">
<b>Title</b>
<div class="bg-green-800 light:bg-green-200">
<div>Entry-1</div>
<div>Entry-2</div>
<div>Entry-3</div>
</div>
</div>
</div>

---

## DSG (Defered Site Generation)

- viele SSGs bieten alternative Rendering Optionen
- ermöglicht Flexibilität
- birgt aber auch Downsides
- Seiten bei Aufruf generiert
- So lange im Cache bis sich der Content ändert

<img src="/dsg.webp" class="h-xs" alt="https://make-it-static.thilo-billerbeck.com" />
<small class="text-gray-400">Quelle: https://www.gatsbyjs.com/blog/deferred-static-generation-guide/</small>


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
