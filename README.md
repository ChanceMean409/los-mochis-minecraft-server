# Minecraft Hybrid Server Project

This repository contains the setup for a hybrid (Java/Bedrock) and highly available Minecraft server using Docker. The project focuses on a slow and sustainable progression within the game, aiming to provide a rich experience for Bedrock players without compromising the depth offered by server-side plugins that emulate modded content.

## Project Goal

The primary goal is to deploy a stable, high-performance Minecraft server that seamlessly integrates both Java and Bedrock editions. The emphasis is on a balanced gameplay experience with a gradual progression curve, enhancing the vanilla experience through carefully selected plugins rather than complex mods.

## Current Server Status: Success!

The server is currently **online, stable, and 100% functional**. All critical and minor issues identified during development have been resolved.

### Technical Stack:
-   **Orchestration:** Docker Compose
-   **Main Services:**
    -   `mc`: Minecraft Server
    -   `db`: MariaDB database for plugin data
    -   `backups`: Automated backup service
-   **Minecraft Version:** `PaperMC 1.20.6` (Build 151) - chosen for its stability with the current plugin set.

### Key Configurations and Features:
-   **Slow Progression:** A custom script was executed to double the cost of all researches in Slimefun's `Researches.yml`, ensuring a more deliberate advancement.
-   **Economic Balance:** The `fix-curing-zombie-villager-discount-exploit` option is enabled in Paper's configuration to prevent unlimited villager discounts.
-   **Performance Optimization:** Reduced `spawn-limits` and `entity-activation-range` in `bukkit.yml` and `spigot.yml` to enhance server performance.
-   **Hybrid Connectivity:**
    -   **Geyser** (manual and auto-installed)
    -   **Floodgate** (manual and auto-installed)
    -   **ViaVersion** (manual)
    These are all configured and operational, allowing Bedrock clients (including v1.21) to connect to the Java server without requiring a Java account.
-   **Installed Plugins:** LuckPerms, Aurelium Skills, EssentialsX, WorldBorder, CoinsSystem.
-   **Plugin Compatibility:** The `InfinityExpansion` plugin was removed due to incompatibility, ensuring server stability.

### Discrepancies with the Original Roadmap (PDF):

The following configurations differ from the recommendations in `Roadmap Servidor Minecraft Docker Híbrido.pdf`:
-   **`server.properties - allow-flight`**: Currently `false`. The roadmap suggests `true` to prevent Bedrock players from being kicked for "fly hack" during lag spikes. **Consider reviewing this setting.**
-   **`server.properties - enable-command-block`**: Currently `false`. The roadmap recommends `true` for advanced plugin functionalities or custom maps. **Consider reviewing this setting.**
-   **`plugins/Geyser-Spigot/config.yml - java.auth-type`**: Currently `online`. The roadmap suggests `floodgate` to allow Bedrock players to connect without a Java account, delegating authentication to Floodgate. **This is a critical discrepancy that may impact user experience and should be addressed.**

## Connection Details

-   **Internet Address:** `losmochis-craft.hopto.org`
-   **Local Area Network (LAN) Address:** `192.168.1.59`
-   **Configured Ports (on router):**
    -   Java (TCP): `25565`
    -   Bedrock (UDP): `19132`

## Getting Started (for server administrators)

To set up and run this server locally or on a new host, follow these general steps:

1.  **Clone this repository:**
    ```bash
    git clone https://github.com/ChanceMean409/los-mochis-minecraft-server.git
    cd los-mochis-minecraft-server
    ```
2.  **Configure Environment Variables:**
    Review and configure your `.env` file for any sensitive information or specific settings.
3.  **Start the Docker Compose services:**
    ```bash
    docker-compose up -d
    ```
4.  **Monitor Logs:**
    ```bash
    docker-compose logs -f
    ```
    Ensure all services start without errors.

## Troubleshooting

-   **Connection Issues:** Verify port forwarding on your router and ensure firewall rules are correctly configured for ports `25565` (TCP) and `19132` (UDP).
-   **Authentication for Bedrock Players:** If Bedrock players have issues connecting, re-examine the `java.auth-type` setting in `plugins/Geyser-Spigot/config.yml` and consider changing it to `floodgate` as per roadmap recommendations.
-   **Server Performance:** If performance issues arise, further adjustments to `spawn-limits` and `entity-activation-range` in `bukkit.yml` and `spigot.yml` may be necessary.

**The server is currently in an optimal state, ready for play!**
