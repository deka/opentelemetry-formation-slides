---
layoutClass: gap-16
---

# Introduction

<Toc columns="1" min-depth="2" max-depth="3" mode="onlySiblings" />


---
transition: fade-out
layout: image
level: 2
title: Sparks
image: /images/welcome-sparks.png
---

<Onea class="absolute left-10 bottom-5"/>

---
transition: fade-out
layout: image
hideInToc: true
level: 2
image: /images/intro-sparks.png
backgroundSize: contain
---


---
transition: fade-out
level: 2
title: Fil rouge 
---

# Fil rouge 
Quelques éléments clefs

<h3 class="mb-2">Objectif: Mettre en place une solution d'observabilité pour une application distribuée.</h3>
 
Mise en avant de l'importance de la <b>corrélation</b> de données.  

Construction d'un tableau de board de supervision utilisant les <b>indicateurs RED</b> (Rate, Error, Duration).

<h3>Une application distribuée simple</h3>

Périmètre fonctionnel : une application qui retourne des unités de transport, avec un un voyage associé.
   
- Une <b>API Front</b> en .Net  
- Une <b>API Business</b> en .Net  
- Une <b>base de données SQLite</b> qui stocke les unités de transport.  


<Onea class="absolute left-10 bottom-5"/>

---
transition: fade-out
level: 3
---

# Utilisation de la pile OpenTelemetry

<p class="absolute right-5 top-5 text-3xl"> Fil rouge </p> 


Protocole OTLP pour la communication  
Instrumentation automatique et manuelle   
Collecteur OTEL  
   
Un backend de visualisation basée sur la pile LGTM (Loki, Grafana, Tempo, Mimir)
  - Loki pour la gestion des logs 
  - Tempo pour la gestion des traces.
  - Mimir pour la gestion des métriques.
  - Grafana pour la visualisation des données.


---
transition: fade-out
image: /images/demo.collecte.drawio.png
backgroundSize: 80%
layout: image
level: 3
title: C4 Model
---
<p class="absolute right-5 top-5 text-3xl"> Fil rouge </p> 

<!--
Démo
-->