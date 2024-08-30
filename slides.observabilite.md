---
Transition: fade-out
hideInToc: true
---
# De la supervision à l'observabilité

![Observabilité vs supervision](/images/observability.png)

<Onea class="absolute left-10 bottom-5"/>

<!--
Compréhension approfondie et détaillée
Amélioration continue
-->

---
transition: fade-out
---

#  De la supervision à l'observabilité

<Toc columns="1" min-depth="2" max-depth="3" mode="onlySiblings" />



---
transition: fade-out
level: 2
---
#  L'observabilité, qu'est-ce que c'est ?
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p> 

L'observabilité nous permet de comprendre l'état et le fonctionnement d'un système complexe en se basant sur ses entrées et ses sorties <b>externes</b>, telles que les <b>journaux</b>, les <b>métriques</b> et les <b>traces</b>.

<div class="flex justify-center  mx-auto mt-8 text-3xl">
  <blockquote class="w-3/4 mt-8">
    <p class="text-2xl p-4 !leading-8 bg-white">
      A system is <b>observable</b>
      if the <b>behaviour</b> of
      the entire system can
      be determined by only
      looking at its <b>inputs
      and outputs</b>*.
    </p>
  </blockquote>
</div>

<br />
*Rudolf Emil Kálmán (1961), On the General Theory of Control Systems

<Onea class="absolute left-10 bottom-5"/>

---
image: /images/signaux.jpg
transition: fade-out
layout: image
backgroundSize: contain
level: 2
---
#  Les signaux
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p> 

  

---
layout: image-right
image: /images/observability-personas.png
transition: fade-out
backgroundSize: contain
level: 2
---

# Quels acteurs ?
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p>
  
  <ul>
    <li>Les équipes <b>support</b>, pour la résolution des problèmes de production </li>
    <li>Les équipes <b>développement</b>, pour le suivi des bugs et des améliorations</li>
    <li>Les <b>responsables métier</b>, pour superviser un périmètre applicatif</li>
    <li>Les <b>administrateurs système</b>, pour s'assurer du bon fonctionnement de l'infrastructure</li>
    <li>Les <b>clients</b>, pour suivre leur signal au travers des services Fournis</li>
    </ul>

<Onea class="absolute left-10 bottom-5"/>


---
transition: fade-out
hideInToc: true
level: 2
---
#  Pourquoi l'Observabilité est-elle cruciale ?
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p> 


## Complexité Croissante 
Les systèmes modernes sont de plus en plus <b>complexes</b> (microservices, architecture distribuée, cloud native, etc.)  

## Visibilité Holistique 
Permet une <b>vue d'ensemble des systèmes</b>, aidant à corréler les données et à identifier les causes profondes des problèmes

## Détection et Résolution Rapide des Problèmes  
Facilite la détection rapide et la résolution des anomalies, réduisant ainsi le <b>temps moyen de détection</b> (MTTD) et le <b>temps moyen de résolution</b> (MTTR)



---
transition: fade-out
level: 2
hideInToc: true
---
#  Pourquoi l'Observabilité est-elle cruciale ?
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p> 

## Amélioration de la Fiabilité
Aide à concevoir des systèmes plus <b>résilients</b> en <b>identifiant</b> les points de défaillance et en permettant la mise en place de mécanismes de récupération appropriés

## Optimisation des Performances  
Permet d'identifier les <b>goulots d'étranglement</b> et d'optimiser les performances des systèmes.  

## Automatisation et IA
Peux être utilisée pour <b>automatiser</b> la surveillance et la gestion des systèmes, et pour alimenter des systèmes d'<b>IA</b>.


---
transition: fade-out
level: 2
---
#  Pourquoi l'Observabilité est-elle cruciale ?
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p> 

## Surveillance Améliorée
Va au-delà de la simple surveillance en offrant une analyse <b>contextuelle</b> et une visualisation des anomalies

## Amélioration de la collaboration
Les outils d'observabilité fournissent un <b>langage commun</b> pour les équipes de <b>développement</b>, d'<b>exploitation et de support</b>, facilitant la collaboration et la résolution de problèmes.

## Support à l'évolutivité et l'innovation  
Simplifie le déploiement de nouvelles fonctionnalités et de nouveaux services, en fournissant une visibilité sur les performances et les interactions des systèmes.


---
transition: fade-out
hideInToc: true
level: 2
---
#  Zoom sur le traçage distribué
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p>

<img src="/images/microservice-architecture.svg" alt="Architecture distribuée" />

---
transition: fade-out
level: 2
---
#  Zoom sur le traçage distribué
<p class="absolute right-5 top-5 text-3xl"> Observabilité </p>

Le traçage distribué est une technique d'observabilité qui permet de suivre le <b>cheminement</b> d'une <b>requête</b> à travers un système distribué, en enregistrant les <b>étapes</b> et les <b>temps</b> de traitement à chaque étape.

## Pourquoi le traçage est-il important ?
Le traçage permet de <b>comprendre</b> et de <b>diagnostiquer</b> les problèmes de performance et de fiabilité, en identifiant les <b>goulots d'étranglement</b> et les <b>points de défaillance</b> dans les systèmes distribués.

## Comment fonctionne le traçage ?
Le traçage est basé sur l'<b>instrumentation</b> des applications, qui enregistre des <b>données de contexte</b> à chaque étape du traitement, et sur la <b>corrélation</b> de ces données pour reconstituer le <b>parcours</b> de la requête.

> Notions clées : Spans, Trace Id


<!--
Span
Trace ID
-->
