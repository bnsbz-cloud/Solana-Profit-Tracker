# Client Solana Unifié

## Dernières Mises à Jour

### Améliorations du Typage (2024-01-03)
- Correction du typage de la méthode `get_multiple_accounts`
- Passage de `Optional[GetMultipleAccountsResp]` à `List[Optional[Dict[str, Any]]]`
- Meilleure représentation du comportement réel de la méthode
- Support explicite des comptes non-existants dans la liste de retour

## Fonctionnalités Principales

### Gestion des Comptes
- `get_account_info`: Récupération des informations d'un compte unique
- `get_multiple_accounts`: Récupération en batch des informations de plusieurs comptes
  - Support des comptes non-existants (retourne None)
  - Préservation de l'ordre des comptes dans la réponse
  - Validation des clés publiques en amont
- `get_program_accounts`: Récupération des comptes associés à un programme

### WebSocket
- Connexions WebSocket avec gestion de pool
- Surveillance de la santé des connexions
- Reconnexion automatique
- Support des subscriptions aux programmes

### Gestion RPC
- Failover automatique
- Validation des endpoints
- Retry avec backoff exponentiel
- Monitoring de la santé des connexions

## Utilisation

### Récupération Multiple de Comptes
```python
# Exemple d'utilisation de get_multiple_accounts
accounts = await client.get_multiple_accounts([
    "account1_pubkey",  # Compte existant
    "account2_pubkey"   # Compte potentiellement non-existant
])

# Traitement des résultats
for account in accounts:
    if account:
        print(f"Compte trouvé: {account['owner']}")
    else:
        print("Compte non trouvé")
```

### Gestion des Erreurs
- Validation des clés publiques
- Gestion des timeouts
- Reconnexion automatique
- Logging détaillé

## Tests

### Tests Unitaires
- Validation des types de retour
- Gestion des cas d'erreur
- Vérification des comptes non-existants
- Tests de connexion WebSocket

## Prochaines Étapes
- [ ] Optimisation du pooling de connexions
- [ ] Cache intelligent des données
- [ ] Métriques détaillées de performance
- [ ] Support de nouveaux types de filtres
