---
transition: fade-out
hideInToc: true
---
#  Présentation d'OpenTelemetry

<img class="mt-12" src="/images/openTelemetry-pipeline.png" alt="OpenTelemetry Pipeline"/>

<Onea class="absolute left-10 bottom-5"/>


---
transition: fade-out
---

#  Présentation d'OpenTelemetry

<Toc columns="1" min-depth="2" max-depth="3" mode="onlySiblings" />


---
transition: fade-out
level: 2
---
# Un peu d'histoire
<p class="absolute right-5 top-5 text-3xl"> OpenTelemetry </p> 

OpenTelemetry est un projet <b>open-source</b> collaboratif, initié par la Cloud Native Computing Foundation (<b>CNCF</b>)

## Fusion de OpenTracing et OpenCensus

<b>OpenTracing</b> fournissait une API standard pour le traçage distribué.  

<b>OpenCensus</b> offrait des bibliothèques pour la collecte de traces et de métriques.

En 2019, <b>OpenTelemetry</b> a fusionné ces deux projets pour créer une solution <b>unifiée</b> pour l'observabilité des systèmes distribués.

<Onea class="absolute left-10 bottom-5"/>

---
transition: fade-out
level: 2
---
# Quelques caractéristiques 
<p class="absolute right-5 top-5 text-3xl"> OpenTelemetry </p>

### Indépendant des fournisseurs (vendor-neutral)
OpenTelemetry est un projet <b>open-source</b> et <b>indépendant des fournisseurs</b>, ce qui signifie qu'il peut être utilisé avec n'importe quelle technologie ou plateforme.

### Standardisé et unifié
OpenTelemetry fournit un ensemble de composants : des spécifications, un prococol de transport (OTLP), des conventions de nommage, des SDKs, un collecteur et d'autres outils  variés (pour K8s, FaaS , ...)   
Combiner les <b>traces</b>, les <b>métriques</b> et les <b>logs</b> simplifie la configuration de l'observabilité.

### Extensible
OpenTelemetry est conçu pour être <b>extensible</b> et <b>modulaire</b>, permettant aux utilisateurs de personnaliser et d'étendre les fonctionnalités selon leurs besoins.

<Onea class="absolute left-10 bottom-5"/>

<!--
Interopérabilité
Communauté et Support
Facilite la migration entre différentes solutions d'observabilité
-->

---
transition: fade-out
level: 2
title: Les concepts fondamentaux
image: /images/opentelemetry.concept.png
backgroundSize: 70%
layout: image
---

# Concepts fondamentaux

---
transition: fade-out
level: 3
---
# Le contexte de propagation
<p class="absolute right-5 top-5 text-3xl"> OpenTelemetry </p>

Mécanisme utilisé pour transmettre des informations contextuelles (traceId, spanId, ...) à travers les frontières des processus et des réseaux.

> Cette notion est essentielles pour le traçage distribué et la corrélation des signaux.

<br />

### Fonctionnement
- <b>Génération</b>: Un nouveau contexte est généré au début d'une requête (un trace ID et un span ID ...).
- <b>Inejction</b>: Ce contexte est injecté dans les en-têtes des requêtes HTTP ou des messages RPC pour être transmis aux services en aval.
- <b>Extraction</b>: Les services récepteurs extraient le contexte des en-têtes pour continuer la trace.
- <b>Transmission</b>: Les informations de contexte sont propagées tout au long de la chaîne de services, permettant un suivi continu.

<Onea class="absolute left-10 bottom-5"/>

---
transition: fade-out
level: 3
hideInToc: true
---
# Le contexte de propagation
<p class="absolute right-5 top-5 text-3xl"> OpenTelemetry </p>

### Propagateurs
Les propagateurs permettent à chaque service d'une chaîne distribuée de lire et d'écrire les données du contexte et de les propager 

Propagateurs maintenus par OpenTelemetry :
- <b>[W3C TraceContext](https://www.w3.org/TR/trace-context)</b>: Standard pour la propagation du contexte de trace
- <b>[W3C Baggage](https://www.w3.org/TR/baggage)</b>: Permet de transmettre des données contextuelles supplémentaires
- <b>[B3](https://github.com/openzipkin/b3-propagation)</b>: Format de propagation de trace utilisé par Zipkin
- <b>[Jaeger](https://www.jaegertracing.io/docs/latest/client-libraries/#propagation-format)</b>: Format de propagation de trace utilisé par Jaeger

<br />

### Zoom : Baggage
Les bagages permettent de transmettre des données contextuelles supplémentaires, telles que des informations de <b>corrélation</b>, des <b>identifiants</b> de session, des <b>informations de sécurité</b>, etc.

[W3C Baggage](https://www.w3.org/TR/baggage)

---
transition: fade-out
level: 3
---
# Les autres concepts
<p class="absolute right-5 top-5 text-3xl"> OpenTelemetry </p>

### Les 3 signaux  

- <b>Trace</b>: Chemin parcouru par une requète
- <b>Métrique</b>: Mesure capturée à l'exécution
- <b>Log</b>: Enregistrement d'un événement 


### Instrumentation  
OpenTelemtry offre la possibilité d'instrumenter le code pour capturer ces signaux, avec une approche zero-code, automatique ou manuelle. 

### Collecteur  
Le collecteur permet de recevoir les signaux, les transformer et les exporter vers un backend comptabile

### Et aussi
SDKs, ressources, baggage, Convention de nommage (Semanyic conventions), Sampling, ...

[Registre OpenTelemetry](https://opentelemetry.io/ecosystem/registry/)

---
transition: fade-out
level: 2
---

# Instrumentation
L'instrumentation est un processus qui permet d'ajouter du code pour capturer les signaux (traces, métriques, logs) de l'application.

### Zero-Code
OpenTelemetry fournit des outils pour capturer automatiquement les signaux, sans nécessiter de modification du code de l'application.
> Utile pour les applications tierces ou les applications existantes.

### Par configuration  
OpenTelemetry fournit des SDKs pour les langages de programmation populaires, qui permettent d'instrumenter automatiquement les applications pour capturer les signaux.

### Manuelle  
OpenTelemetry permet également d'instrumenter manuellement les applications, en ajoutant des points d'instrumentation personnalisés pour capturer des signaux spécifiques.

---
transition: fade-out
level: 3
---

# Les ressources
<p class="absolute right-5 top-5 text-3xl"> Instrumentation </p>

Entité produisant des signaux  
Ex: un service, une application, un conteneur, une machine virtuelle, )

<div class="flex justify-center  mx-auto mt-2 text-3xl">
  <blockquote class="w-3/4 my-4">
    <p class="text-xl p-4 !leading-6">
    La notion de ressource est un élement clé pour l'observabilité. Elle permet de <b>corréler</b> les signaux entre eux et de les <b>associer</b> à des <b>entités</b> du système.
    </p>
  </blockquote>
</div>

### Détection automatique
OpenTelemetry fournit des mécanismes pour détecter <b>automatiquement</b> les ressources, telles que les services, les applications, les conteneurs, les machines virtuelles, etc.

### Personnalisation
OpenTelemetry permet également de <b>personnaliser</b> les ressources, en ajoutant des <b>attributs</b> pour identifier et catégoriser les entités.



---
transition: fade-out
level: 3
hideInToc: true
---
# Les ressourses
<p class="absolute right-5 top-5 text-3xl"> Instrumentation </p>

### Attributs Clés
- <b>service.name</b>: Nom du service
- <b>service.version</b>: Version du service
- <b>service.instance.id</b>: Identifiant de l'instance du service
- <b>service.namespace</b>: Espace de nom du service. 
  > Util pour cartographier le système
- <b>environment.name</b>: Envirronement d'exécution du service (Development, production ...)

<br/>  

### Autres resources importantes (Semantic Conventions 1.26.0): 

- [Host](https://opentelemetry.io/docs/specs/semconv/resource/host/) 
- [Operating System](https://opentelemetry.io/docs/specs/semconv/resource/os/)
- [Process](https://opentelemetry.io/docs/specs/semconv/resource/process/)
- [Telemtry SDK](https://opentelemetry.io/docs/specs/semconv/resource/#telemetry-sdk)

---
transition: fade-out
level: 3
---

# Les Exportateurs 
<p class="absolute right-5 top-5 text-3xl"> Instrumentation </p>

Envoient les données collectées au collecteur OpenTelemtry (ou directement au backend)

Il existe différents types d'exportateurs, par exemple : 
- <b>Console</b> : Pour afficher les données de télémétrie dans la console
- <b>OTLP</b> : Utilise le protocole OpenTelemetry pour exporter les données
- <b>Zipkin</b> : Pour exporter les traces vers Zipkin
- <b>Jaeger</b> : Pour exporter les traces vers Jaeger
- <b>Prometheus</b> : Pour exporter les métriques vers Prometheus

<br />

> Dans certains cas, l'exportateur est préconfiguré pour un backend spécifique.

<Onea class="absolute left-10 bottom-5"/>
