# Minecraft Server Deployment

This repository contains the Helm chart for our Minecraft Paper server running on our Raspberry Pi 5 k3s Kubernetes cluster, automatically synchronized and deployed via ArgoCD.

## Connecting to the Server

* **Server Address / IP**: `192.168.100.33` (default Minecraft port: `25565`)
* **Edition**: Java Edition (PaperMC)
* **Default Game Mode**: Survival
* **Difficulty**: Normal

## Customizing the Server

All server settings can be adjusted in [`minecraft/values.yaml`](minecraft/values.yaml):

```yaml
minecraft:
  env:
    motd: "Welcome to our Minecraft Server!"
    difficulty: "normal"     # peaceful, easy, normal, hard
    mode: "survival"          # survival, creative, adventure, spectator
    pvp: "true"
    viewDistance: "10"
    maxPlayers: "10"
    ops: ""                  # Comma-separated list of Minecraft usernames to grant operator rights
    whitelist: ""            # Comma-separated list of allowed players (if whitelisting is needed)
```

Whenever you push changes to the `dev` branch, ArgoCD will automatically synchronize and update the Minecraft server.

## Data & World Storage
World data, player inventories, and server configs are stored on a persistent volume backed by `longhorn-ssd` (retained across restarts and pod updates).
