---
transition: fade-out
image: /images/metrics-graphic.jpg
layout: image
backgroundSize: 90%
hideInToc: true
---
# Exporter les métriques

---
transition: fade-out
---

# Exporter les métriques


<Toc columns="1" min-depth="2" max-depth="3" mode="onlySiblings" />


---
transition: fade-out
level: 2
---
# Les métriques
<p class="absolute right-5 top-5 text-3xl"> Les Métriques </p>


## Qu’est ce qu’une métrique ?

<b>Mesures</b> quantitatives qui fournissent des informations sur l'état et la performance d'un système

| <b>timestamp</b> | <b>value</b> | <b>htt_response_status_code</b> | <b>http_request_method</b> |
|-----------|-------|--------------------------|---------------------|
| <span class="text-gray">10</span> | <span class="text-gray">10</span>    | 200                      | GET                 |
| <span class="text-gray">10</span> | <span class="text-gray">2</span>     | 500                      | GET                 |
| <span class="text-gray">15</span> | <span class="text-gray">32</span>    | 200                      | GET                 |

<span class="text-3xl font-bold"> Metric = Timestamp + Valeur + Dimensions (Labels) </span> 

---
transition: fade-out
level: 3
hideInToc: true
layout: image
image: /images/metric_json.png
backgroundSize: contain
---


--- 
transition: fade-out
level: 3
--- 

# Types de métriques OpenTelemetry
- <b>Compteurs</b> : Mesure incrémentale (ex: nb de requetes traitées)
  - Suffixe courant : `_total`
- <b>Jauges</b> : Mesure instantanée (ex: Utilisation de la memoire)
  - Suffixe courant : `_sum`, `_count`
- <b>Histogrammes</b> : Distribution des valeurs (ex: Durée des requetes)
  - Répartition des valeurs dans des plages spécifiques (buckets)
  - Suffixe courant : `_bucket`, `_sum`, `_count`

<br />  

<!--
- Pas de Summary (Prometheus)
- Pas de stockage dans Prometheus du type de métrique
- Asynchrone : La valeur est mise à jour de manière asynchrone : indépendamment du cycle de collecte principal (ex: par un evenement)
- Conventions de nommage : https://prometheus.io/docs/practices/naming/

-->

---
transition: fade-out
level: 3
---

# Instrumentation : synchrone et asynchrone
<p class="absolute right-5 top-5 text-3xl"> Les Métriques </p>

### Instrumentation synchrone
- Collecte à <b>interval régulier</b>
- Impact régulier et prévisible sur les performances
- Vue régulière et cohérente dans le temps
- Exemple : Nombre de reqêtes par seconde, CPU ...  

<br />

### Instrumentation asynchrone
- Collecte basée sur des <b>événements</b>, indépendamment du cycle de collecte principal.
- Impacte plus faible sur les performances, mais irrégulier.
- Utile pour les mesures qui changent moins fréquemment, et qui sont coûteuses à collecter.
- Exemple : Taille d'une file d'attente de message

<!-- 
On se concentre sur Synchrone
-->

---
transition: fade-out
level: 3
---

# Instrumentation : Metrics API
<p class="absolute right-5 top-5 text-3xl"> Les Métriques </p>

## Meter Provider
Fournit une instance de <b>Meter</b> pour la création de métriques.

## Meter
Interface pour la création de métriques (Metric Instruments).

## Metric Instrument
Il enregistre les valeurs des métriques.
Ex: Counter, UpDownCounter, Gauge, Histogram

## Metric Exporter
Exporte les métriques vers un collecteur ou un backend d'observabilité.

---
transition: fade-out
level: 3
layout: image
image: /images/model-event-layer.png
backgroundSize: contain
---

<span class="absolute bottom-5 left-5 text-xl text-black">Spécifications + Conventions de nommage = Données de métriques pré-agrégées 
</span>


---
transition: fade-out
layout: two-cols
level: 2
---

<p class="absolute right-5 top-5 text-3xl "> Les Métriques </p>

# PromQL

### Labels / Filtres
Equivalent à une clause 'where'

```
http_requests_total{method="POST", handler="/api/traces"}
```

### By
Equivalent à un group by

```
sum(http_requests_total) by (method)
```

### Range Vector
Sélectionne les données sur une période donnée

```
http_requests_total[5m]
```

::right::

### Rate
Calcul du taux de variation par seconde

```
rate(http_requests_total[5m])
```

### Opérateurs mathématiques
+, -, *, /, %, ^
```
http_requests_total{method="POST"} +  
  http_requests_total{method="GET"}
```
### Fonctions d'aggération
sum(), count(), avg(), min(), max(), ...

```
sum(http_requests_total) by (method)
```

<!--

Sotckage des données : clé(label)/timestamp/valeur
 Le type de métrique n'est pas stocké dans Prometheus !
-->

---
transition: fade-out
level: 2
---

# Des métriques à partir des traces

Les métriques et les traces sont complémentaires.
Alors que les métriques offrent une vue synthétique de l'ensemble, les traces permettent d'avoir une vue détaillée d'une requête unique.

### OTEL Collector spanmetrics
Le collecteur OpenTelemetry propose un composant spanmetrics qui permet de générer des métriques à partir des traces.

### Quels avantages ? 
- <b>Economie de ressources</b> : Réduit la charge sur les applications !
- <b>Précision</b> : Les métriques sont basées sur des données de traces réelles
- <b>Flexibilité</b> : Possibilité de créer des métriques personnalisées
- <b>Corrélation</b> : Les métriques sont corrélées avec les traces

<p class="absolute right-5 top-5 text-3xl"> Les Métriques </p>

---
transition: fade-out
level: 3
hideInToc: true
layout: image
image: /images/poc.collector.drawio.png
backgroundSize: 80%
---


---
transition: fade-out
level: 2
---

# La méthode RED  

- <b>Rate</b> : Nombre de requêtes par seconde
- <b>Error</b> : Nombre de ces requêtes en erreur
- <b>Duration</b> : Durée moyenne de traitement de ces requêtes


### Pourquoi la méthode RED ?
- <b>Simple</b> : Facile à comprendre et à mettre en oeuvre
- <b>Universelle</b> : Applicable à tous les types de services
- <b>Complémentaire</b> : Combinée avec les traces, elle fournit une vue complète de la performance


### Autres méthodes
- <b>USE</b> : Utilisation, Saturation, Erreurs
- <b>Four Golden Signals</b> : Traffic, Errors, Saturation, Latency


<p class="absolute right-5 top-5 text-3xl"> Les Métriques </p>

---
transition: fade-out
level: 3
hideInToc: true
layout: image
image: /images/red_formula.png
backgroundSize: contain
---
