# Écosystème DEX Solana

## 1. Agrégateurs

### Jupiter
- **GitHub**: https://github.com/jup-ag
- **Repos clés**: 
  - jupiter-core: https://github.com/jup-ag/jupiter-core
  - jupiter-sdk: https://github.com/jup-ag/jupiter-sdk
- **Données disponibles**:
  - Routes de swap optimales
  - Prix en temps réel
  - Liquidité par pool
  - Volume de trading
  - Slippage estimé
- **Endpoints utiles**:
  ```
  - /v4/quote : Prix et routes
  - /v3/price : Prix en temps réel
  - /v3/indexed-route-map : Map des routes
  ```

## 2. AMM (Automated Market Makers)

### Raydium
- **GitHub**: https://github.com/raydium-io
- **Repos clés**:
  - raydium-sdk: https://github.com/raydium-io/raydium-sdk
  - raydium-ui: https://github.com/raydium-io/raydium-ui
- **Données disponibles**:
  - État des pools de liquidité
  - TVL (Total Value Locked)
  - APR/APY des farms
  - Volume par pool
  - Prix des tokens
- **Programme principal**: "675kPX9MHTjS2zt1qfr1NYHuzeLXfQM9H24wFSUt1Mp8"

### Orca
- **GitHub**: https://github.com/orca-so
- **Repos clés**:
  - orca-sdk: https://github.com/orca-so/orca-sdk
  - whirlpools: https://github.com/orca-so/whirlpools
- **Données disponibles**:
  - État des Whirlpools (pools concentrés)
    * Prix et liquidité
    * Ticks et spacing
    * Frais et métriques
  - Positions de liquidité
    * Ranges de prix
    * Montants par token
  - Métriques de pool
    * Volume et TVL
    * Statistiques de trading
  - Rendements des pools
    * APR/APY
    * Récompenses
- **Programme principal**: "whirLbMiicVdio4qvUfM5KAg6Ct8VwpYzGff3uctyCc"
- **Parsing des données**:
  ```python
  # Format des données Whirlpool
  {
    "token_a": "...",  # Token mint A
    "token_b": "...",  # Token mint B
    "liquidity": 1000000,  # Liquidité totale
    "price": 1.234,  # Prix actuel
    "fee_rate": 0.003,  # Taux de frais (0.3%)
    "tick_spacing": 1,  # Espacement des ticks
    "tick_current": 100,  # Tick actuel
    "fees": {
      "token_a": 1000,  # Frais collectés token A
      "token_b": 2000   # Frais collectés token B
    }
  }
  ```

## 3. CLOB (Central Limit Order Book)

### Phoenix
- **GitHub**: https://github.com/Ellipsis-Labs/phoenix-v1
- **Repos clés**:
  - phoenix-v1: https://github.com/Ellipsis-Labs/phoenix-v1
  - phoenix-sdk: https://github.com/Ellipsis-Labs/phoenix-sdk
- **Données disponibles**:
  - Carnet d'ordres complet
  - Historique des trades
  - Statistiques de marché
  - État des ordres
- **Programme principal**: "PhoeNiXZ8ByJGLkxNfZRnkUfjvmuYqLR89jjFHGqdXY"

### OpenBook (ex-Serum)
- **GitHub**: https://github.com/openbook-dex
- **Repos clés**:
  - openbook-v2: https://github.com/openbook-dex/openbook-v2
  - program: https://github.com/openbook-dex/program
- **Données disponibles**:
  - Carnet d'ordres
  - Historique des transactions
  - Statistiques de marché
  - État des ordres limites
- **Programme principal**: "opnb2LAfJYbRMAHHvqjCwQxanZn7ReEHp1k81EohpZb"

## 4. Fonctionnalités à Implémenter

### 1. Monitoring des Prix
```python
async def monitor_prices(self, token_pair: str):
    # Jupiter pour les prix agrégés
    # Raydium/Orca pour les prix AMM
    # Phoenix/OpenBook pour les prix CLOB
```

### 2. Surveillance des Pools
```python
async def monitor_pools(self, pool_address: str):
    # TVL
    # Volume
    # APR/APY
    # Composition du pool
```

### 3. Carnet d'Ordres
```python
async def monitor_orderbook(self, market_address: str):
    # Profondeur du marché
    # Spread
    # Volume par niveau de prix
```

### 4. Analyse des Routes
```python
async def analyze_routes(self, input_token: str, output_token: str):
    # Meilleures routes
    # Prix sur chaque DEX
    # Slippage estimé
```

### 5. Statistiques Globales
```python
async def get_global_stats(self):
    # Volume total
    # TVL total
    # Nombre de trades
    # Tokens les plus tradés
```

## 5. Structure des Données

### Prix
```json
{
  "token_pair": "SOL/USDC",
  "price": 100.50,
  "timestamp": "2024-01-18T01:23:45Z",
  "source": "Jupiter",
  "volume_24h": 1000000,
  "price_change_24h": 2.5
}
```

### Pool
```json
{
  "address": "pool_address",
  "type": "AMM",
  "tvl": 1000000,
  "volume_24h": 500000,
  "apr": 15.5,
  "tokens": [
    {
      "address": "token_address",
      "amount": 1000,
      "weight": 0.5
    }
  ]
}
```

### Carnet d'Ordres
```json
{
  "market": "market_address",
  "timestamp": "2024-01-18T01:23:45Z",
  "bids": [
    {
      "price": 100.45,
      "size": 10.5
    }
  ],
  "asks": [
    {
      "price": 100.55,
      "size": 8.2
    }
  ]
}
```

## 6. Endpoints WebSocket

### Jupiter
```
wss://phoenix.jup.ag/phoenix/socket/websocket
```

### Raydium
```
wss://api.raydium.io/v2/main/ws
```

### Orca
```
wss://api.orca.so/v1/ws
```

### Phoenix
```
wss://phoenix-ws.hellomoon.io/v1/ws
```

## 7. Métriques à Surveiller

1. Performance
   - Latence des routes
   - Taux de succès des swaps
   - Temps d'exécution des ordres

2. Liquidité
   - Profondeur du marché
   - Concentration de la liquidité
   - Stabilité des pools

3. Prix
   - Volatilité
   - Arbitrage opportunities
   - Prix cross-DEX

4. Activité
   - Volume par DEX
   - Nombre de transactions
   - Wallets actifs

## 8. Dashboard API et WebSocket

### API REST
```
# Base URL: http://localhost:8000/api/v1

# Prix et Métriques
GET /metrics/prices
GET /metrics/volume
GET /metrics/tvl

# Données Historiques
GET /history/trades
GET /history/liquidity
GET /history/volume

# Configuration
GET /config/alerts
POST /config/alerts
```

### Protocol WebSocket
```json
// Connection
ws://localhost:8000/ws

// Souscription
{
  "type": "subscribe",
  "channel": "prices",
  "pairs": ["SOL/USDC", "RAY/USDC"]
}

// Message de Prix
{
  "type": "price_update",
  "data": {
    "pair": "SOL/USDC",
    "price": 100.50,
    "timestamp": "2024-01-18T01:23:45Z",
    "source": "Jupiter"
  }
}

// Message de Volume
{
  "type": "volume_update",
  "data": {
    "pair": "SOL/USDC",
    "volume_24h": 1000000,
    "timestamp": "2024-01-18T01:23:45Z"
  }
}
```

## 9. Alertes à Implémenter

1. Prix
   - Variations importantes
   - Opportunités d'arbitrage
   - Divergence entre DEX

2. Liquidité
   - Changements soudains de TVL
   - Déséquilibre des pools
   - Concentration excessive

3. Transactions
   - Grands swaps
   - Activité suspecte
   - Erreurs de transaction

4. Technique
   - Latence élevée
   - Erreurs RPC
   - Problèmes de connexion
