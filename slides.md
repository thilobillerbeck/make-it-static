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
---

# make-it-static

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

## Typischer Aufbau einer Seite

Eine statische Seite besteht meistens aus:

- Inhalten / Daten (Markdown, YAML, JSON, ...)
- Templates und / oder Themes (HTML Templates, Partials, ...)
- Konfiguration (Wie soll was funktonieren?)
- Binaries / statischen Assets (Bilder, Fonts, Scripts, ...)

Beispiel Hugo:

├── config.toml // Konfiguration
├── content // semi- und unstrukturierte Inhalt der Seite bspw. in Markdown
├── data // strukturierte Daten in YAML, JSON, TOML, ...
├── static // statische Assets
└── themes // Themes (meistens separates Repo)
├── layouts // Layouts (ueberschreiben Themes)

---

## Wie funktioniert ein SSG?

Idee schrittweise zeigen

1. Initiales Tempalte
2. Befuellen von Head, Footer, Main
3. Befuellen von Head und Fotter mit Metatags und Assets
4. Rendern Inhalt

- Wo kommt was hin?
  - Content
  - Assets
  - Kontext (globaler Kontext, Meta)
  - Zusammenbau der Seite

---

## Workflow

---

## SSG ausschen

Faktoren

- Technische Vorknenntnisse / Vorlieben
- Kompatibilitaet
- Plugins

---

## Template

entweder schreiben oder sich eins raussuchen

- Aussuchen
- Portieren

---

## Mit Content fuellen API oder lokal

Methoden von API nehmen

- Lokal (Markdown, JSON, YAML, ...)
- API REST / GraphQL

---

## Deployen

Netlify, Vercel, Pages, nginx

CI und git

---

## Umstellung des Workflows am Beispiel Wordpress API

- Wordpress API
  - [REST API Handbook | WordPress Developer Resources](https://developer.wordpress.org/rest-api/)
- Medium
- etc.\

---

# Advanced Stuff

## Hydration

[Achieving lazy hydration in Vue 3 from scratch - LogRocket Blog](https://blog.logrocket.com/vue-3-lazy-hydration-from-scratch/)

---

## Partial Server Side Rendering

[Server Side Rendering (SSR) vs. Client Side Rendering (CSR) vs. Pre-Rendering using Static Site Generators (SSG) and client-side hydration. | by Prashant Ram | Oct, 2021 | Medium](https://medium.com/@prashantramnyc/server-side-rendering-ssr-vs-client-side-rendering-csr-vs-pre-rendering-using-static-site-89f2d05182ef)

---

## Hybride CMS

Moeglichkeiten der SSG wie etwa Grav oder Kirby

static HTML CMS wie NEOS

---

# Fazit

---

# Vielen Dank
