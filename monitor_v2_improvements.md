# Documentation du Moniteur DEX v2

## Améliorations Majeures

### 1. Architecture Core

#### 1.1 Gestion RPC Améliorée
- Support multi-endpoints avec failover automatique
- Rotation intelligente des endpoints
- Métriques de performance RPC
- Gestion des rate limits

#### 1.2 Détection des Swaps Optimisée
- Support complet de Jupiter, Orca et Phoenix
- Détection précise avec validation multi-niveaux
- Gestion améliorée des décimales
- Support des swaps complexes (routes multiples)

#### 1.3 Monitoring en Temps Réel
- Métriques détaillées par DEX
- Statistiques de trading en temps réel
- Suivi des wallets actifs
- Analyse de la liquidité

### 2. Nouveaux Composants

#### 2.1 Clients DEX Spécialisés
- `JupiterClient`: Support complet de l'API Jupiter v4
- `OrcaClientV2`: Support des Whirlpools
- `PhoenixClient`: Support du CLOB

#### 2.2 Gestion des Ressources
- Gestion asynchrone optimisée
- Nettoyage automatique des ressources
- Cache intelligent
- Rotation des logs

#### 2.3 Système de Métriques
- Métriques détaillées par composant
- Statistiques de performance
- Alertes configurables
- Export Prometheus

## Guide d'Utilisation

### 1. Installation

```bash
# Cloner le repository
git clone <repo_url>
cd dex-monitor

# Configurer l'environnement
cp .env.example .env
# Éditer .env avec vos clés API

# Installer les dépendances
./start_monitor_v2.sh
```

### 2. Configuration

#### 2.1 Configuration RPC (config/rpc_config.json)
```json
{
    "endpoints": {
        "public": [...],
        "premium": {
            "helius": "...",
            "quicknode": "..."
        }
    }
}
```

#### 2.2 Configuration Logging (config/logging.conf)
- Logs séparés par composant
- Rotation automatique
- Niveaux configurables

### 3. Démarrage

```bash
# Démarrer le moniteur
./start_monitor_v2.sh

# Arrêter le moniteur
./stop_monitor_v2.sh

# Exécuter les tests
./test_monitor_v2.sh
```

### 4. Monitoring

#### 4.1 Logs
```bash
# Suivre les logs en temps réel
tail -f logs/dex.log

# Voir les erreurs
tail -f logs/error.log
```

#### 4.2 Métriques
- Accessible via HTTP: `http://localhost:8000/metrics`
- Format Prometheus compatible
- Dashboards Grafana disponibles

### 5. Maintenance

#### 5.1 Nettoyage
```bash
# Nettoyer les anciens logs
find logs -name "*.log" -mtime +7 -delete

# Archiver les logs
tar -czf logs_archive_$(date +%Y%m%d).tar.gz logs/
```

#### 5.2 Mise à Jour
```bash
# Mettre à jour les dépendances
pip install -r requirements.txt --upgrade

# Tester après mise à jour
./test_monitor_v2.sh
```

## Architecture Technique

### 1. Composants Principaux

```
src/
├── dex/                    # Clients DEX
│   ├── jupiter_client.py   # Client Jupiter
│   ├── orca_client_v2.py   # Client Orca
│   └── phoenix_client.py   # Client Phoenix
├── blockchain/             # Interaction blockchain
│   ├── transaction_scanner.py
│   └── swap_detector.py
└── api/                    # API et WebSocket
    ├── server.py
    └── ws_manager.py
```

### 2. Flow de Données

1. RPC Manager reçoit les transactions
2. Transaction Scanner analyse les transactions
3. Swap Detector identifie les swaps
4. DEX Clients récupèrent les informations supplémentaires
5. WebSocket Manager diffuse les mises à jour
6. API expose les données

### 3. Performance

- Traitement asynchrone
- Cache multi-niveaux
- Connection pooling
- Batch processing

## Troubleshooting

### 1. Problèmes Courants

#### RPC Errors
```bash
# Vérifier la santé RPC
./test_rpc.sh

# Voir les logs RPC
tail -f logs/rpc.log
```

#### Memory Usage
```bash
# Monitorer l'utilisation mémoire
ps aux | grep dex_monitor

# Profiler si nécessaire
py-spy record -o profile.svg --pid <PID>
```

### 2. Maintenance

#### Backup
```bash
# Backup configuration
./backup_config.sh

# Backup données
./backup_data.sh
```

#### Restauration
```bash
# Restaurer configuration
./restore_config.sh

# Restaurer données
./restore_data.sh
```

## Roadmap

### Prochaines Améliorations

1. Support de nouveaux DEX
   - Raydium
   - Meteora
   - Drift

2. Analytics Avancés
   - Machine Learning pour la détection des patterns
   - Prédiction de prix
   - Analyse on-chain approfondie

3. Interface Utilisateur
   - Dashboard interactif
   - Alertes personnalisables
   - Rapports automatiques

4. Infrastructure
   - Support multi-cluster
   - Réplication des données
   - Auto-scaling
