---
transition: fade-out
image: /images/otel-baggage-2.svg
layout: image
backgroundSize: 70%
---
# Baggage

---
transition: fade-out
level: 2
---

# Définition
Mécanisme de propagation de paires <b>clé-valeur</b> à travers les services dans un système distribué. 

> Les données du baggage appartiennent au context de propagation et sont accessibles pour tous les signaux (traces, logs, métriques) 

<br/> 

## Baggage HTTP

Exemple pour une propagation du contexte utilisant les entêtes HTTP

```plaintext
baggage: key1=value1,key2=value2,key3=value3
```

<br />

## Caractéristiques principales
- Propagation transparente à travers les limites des services
- Stockage de données sous forme de paires clé-valeur
- Accessibilité depuis n'importe quel point du parcours d'une requête

<p class="absolute right-5 top-5 text-3xl "> Baggage </p>


---
transition: fade-out
layout: two-cols
level: 2
---

# Utilisation

- Ajout d'informations métier (ID client, type de compte, etc.)
- Transmission de paramètres de configuration
- Partage de données de débogage

<div style="padding:0.5rem; margin-right: 1rem; background-color: #f5f5f5; border-radius: 0.5rem;">
    <p>🚨 Attention 🚨</p>
    <p>Les données du baggage doivent-être utilisées exclusivement pour enrichir les signaux.</p>
    <p>Ne pas utiliser pour des données métiers !</p>
</div>

<br />

### Bonnes pratiques
    - Limiter la taille et le nombre d'éléments de bagage
    - N'inclure que des informations pertinentes et non sensibles
    - Nettoyer le bagage lorsqu'il n'est plus nécessaire


::right::

### Exemple

Pour ajouter une paire clé-valeur dans le contexte de propagation
```csharp
Tracer.CurrentSpan?.SetBaggageItem("key", "value");
```

Pour récupérer une paire clé-valeur dans le contexte de propagation
```csharp
var value = Tracer.CurrentSpan?.GetBaggageItem("key");
```

<p class="absolute right-5 top-5 text-3xl "> Baggage </p>

