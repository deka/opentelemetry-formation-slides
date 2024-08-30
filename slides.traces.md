---
transition: fade-out
---

# Exporter les traces d'une application distribuée


<Toc columns="1" min-depth="2" max-depth="3" mode="onlySiblings" />

---
transition: fade-out
layout: image-left
image: /images/k6-icon.svg
backgroundSize: 50%
level: 2
---

# Générer du traffic (Grafana K6)

Grafana k6 est une solution de <b>test de charge</b> et de performance <b>open-source</b>  
Grafana k6 permet de simuler des charges réalistes 

[Documentation](https://k6.io/docs/)

<Onea class="absolute left-10 bottom-5"/>

---
transition: fade-out
image: /images/demo.collecte.drawio.png
backgroundSize: 60%
layout: image
level: 2 
title: Architecture distribuée
---

# Architecture distribuée



---
transition: fade-out
layout: image
image: /images/traces-spans.png
backgroundSize: 90%
level: 2
---
# Les Traces
<p class="absolute right-5 top-5 text-3xl"> Les Signaux </p>

<Onea class="absolute left-10 bottom-5"/>


---
transition: fade-out
level: 3
---

# Modèle de données
<p class="absolute right-5 top-5 text-3xl"> Les Traces </p>

### Span Context
Portion du span qui contient les données du contexte distribué ([W3C TraceContext](https://www.w3.org/TR/trace-context/)). On y retrouve : 
- <b>TraceID</b> : Identifiant unique de la trace
- <b>SpanID</b> : Identifiant unique du span
- TraceFlags : Drapeaux de trace. (1 seul supporté : `sampled`)
- TraceState : Etat de la trace ()
- IsRemote : Indique si le span est un span distant

<br />



---
transition: fade-out
level: 3
---

# Span Events

- Points temporels spécifiques dans une span -> timestamp
- Utiles pour capturer des actions ponctuelles
- Contiennent un nom et un timestamp
- Peuvent avoir leurs propres attributs

<br />

```csharp	
Tracer.CurrentSpan?.AddEvent("Custom Event");
```

## Cas d'usage : 
Les exceptions : C'est une pratique standardisée par OTEL
https://opentelemetry.io/docs/specs/semconv/exceptions/exceptions-spans/

## Point d'attention :
Ne pas surcharger les spans avec trop d'événements. Les événements sont des données supplémentaires qui peuvent être coûteuses à traiter.

---
transition: fade-out
level: 3
layout: two-cols
---

# Autres informations


## Span links
Les liens sont des références à d'autres spans. Ils peuvent être utilisés pour relier des spans entre eux.

## Span kind
Indique le type de span. Il peut être :
- <b>Server</b> : Span qui représente un serveur
- <b>Client</b> : Span qui représente un client
- <b>Producer</b> : Span qui représente un producteur
- <b>Consumer</b> : Span qui représente un consommateur

::right::

<br />

## Span status
Indique le statut du span. Il peut être :
- <b>OK</b> : Le span s'est terminé avec succès
- <b>ERROR</b> : Le span s'est terminé avec une erreur
- <b>UNSET</b> : Le statut n'est pas défini

## Et aussi ... 
Chaque span contient également des informations sur le <b>nom</b>, la <b>durée</b>, le <b>début</b>, la <b>fin</b>, les <b>attributs</b>.


---
transition: fade-out
level: 3
---

# Instrumentation
Trace API

### Trace Provider
Fournit une instance de <b>Tracer</b> pour la création de traces. 

### Tracer
Interface pour la création de traces (Spans)

### Trace Exporters
Exporte les traces vers un collecteur ou un backend d'observabilité.



---
transition: fade-out
level: 2
---

# Echantillonnage

L'échantillonnage est une technique qui consiste à décider si une trace doit être enregistrée ou non.

### Pourquoi échantillonner ?
- Réduire le volume de données et les coûts de stockage
- Diminuer la charge sur le système de collecte et d'analyse
- Maintenir les performances des applications instrumentées

## Types d'échantillonnage

Deux types d'échantillonnage principaux :
- Head-based sampling (échantillonnage en tête)
- Tail-based sampling (échantillonnage en queue)

---
transition: fade-out
level: 3
---

# Head-based sampling (échantillonnage en tête)
<p class="absolute right-5 top-5 text-3xl"> Echantillonnage </p>

- Décide de l'échantillonnage au début de la trace
- Simple et rapide
- Risque de perdre des informations importantes

## Exemples de stratégies :
- Always-on : Collecte toutes les traces
- Probabilistic : Échantillonne un pourcentage fixe de traces
- Rate-limiting : Limite le nombre de traces par unité de temps



---
transition: fade-out
level: 3
---

# Tail-based sampling (échantillonnage en queue)
<p class="absolute right-5 top-5 text-3xl"> Echantillonnage </p>

- Décision prise après que la trace soit complète
- Avantages : Peut sélectionner les traces les plus pertinentes
- Inconvénients : Nécessite plus de ressources, introduit une latence

## Critères de sélection possibles :
- Durée de la trace
- Présence d'erreurs
- Attributs spécifiques

> Plus difficile à mettre en place que l'échantillonnage en tête.

---
transition: fade-out
level: 3
---

# Bonnes pratiques
<p class="absolute right-5 top-5 text-3xl"> Echantillonnage </p>

- Commencez avec un taux d'échantillonnage élevé et ajustez progressivement
- Utilisez de préférence le head-based sampling.
- Combinez différentes stratégies d'échantillonnage si nécessaire.
- Assurez-vous de toujours conserver les traces contenant des erreurs.

