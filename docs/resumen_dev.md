# Resumen del Estado del Servidor Minecraft Híbrido

Este documento resume el estado actual del proyecto del servidor de Minecraft, las configuraciones aplicadas y el estado final del despliegue.

## 1. Objetivo del Proyecto

El objetivo es desplegar un servidor de Minecraft híbrido (Java/Bedrock) y de alta disponibilidad utilizando Docker. El servidor está diseñado para una **progresión lenta y sostenible**, priorizando la experiencia de los jugadores de Bedrock sin sacrificar la profundidad de contenido que ofrecen los plugins del lado del servidor que emulan a los mods.

## 2. Estado Actual del Servidor: ¡Éxito!

El servidor está **en línea, estable y 100% funcional**. Todos los problemas críticos y menores han sido resueltos.

- **Plataforma:** Docker Compose con 3 servicios principales:
  - `mc`: El servidor de Minecraft.
  - `db`: Una base de datos MariaDB para los plugins.
  - `backups`: Un servicio para copias de seguridad automáticas.
- **Versión de Minecraft:** `PaperMC 1.20.6` (Build 151), que ha demostrado ser la versión estable para el conjunto de plugins actual.
- **Configuraciones Clave Aplicadas:**
  - **Progresión Lenta:** Se ejecutó un script para duplicar el costo de todas las investigaciones en el `Researches.yml` de Slimefun.
  - **Balance Económico:** Se activó la opción `fix-curing-zombie-villager-discount-exploit` en la configuración de Paper para limitar los descuentos de aldeanos.
  - **Optimización:** Se redujeron los `spawn-limits` y `entity-activation-range` en `bukkit.yml` y `spigot.yml` para mejorar el rendimiento.
  - **Conexión Híbrida:** Geyser (manual y auto-instalado), Floodgate (manual y auto-instalado) y ViaVersion (manual) están configurados y funcionales, permitiendo la conexión de clientes de Bedrock (incluyendo v1.21) a la versión Java del servidor sin una cuenta de Java.
  - **Plugins Adicionales Instalados (vía docker-compose.yml o manual):** LuckPerms, Aurelium Skills, EssentialsX, WorldBorder, CoinsSystem.
  - **Plugins Incompatibles:** Se eliminó el plugin `InfinityExpansion` por ser incompatible con la versión actual del servidor, garantizando la estabilidad.

  ### Configuraciones Actuales y Descrepancias con el Roadmap (PDF)

  Se han identificado las siguientes configuraciones que difieren de las recomendaciones del `Roadmap Servidor Minecraft Docker Híbrido.pdf`:
  - **`server.properties - allow-flight`:** Actualmente `false`. El PDF recomienda `true` para evitar kickear a jugadores de Bedrock por "fly hack" en situaciones de lag.
  - **`server.properties - enable-command-block`:** Actualmente `false`. El PDF recomienda `true` para funcionalidades avanzadas de plugins o mapas personalizados.
  - **`plugins/Geyser-Spigot/config.yml - java.auth-type`:** Actualmente `online`. El PDF recomienda `floodgate` para permitir la conexión de jugadores de Bedrock sin cuenta de Java, delegando la autenticación a Floodgate. Esta es una discrepancia crítica que puede afectar la experiencia de usuario.

## 3. Datos de Conexión

- **Dirección para jugadores en internet:** `losmochis-craft.hopto.org`
- **Dirección para jugadores en la red local (LAN):** `192.168.1.59`
- **Puertos (ya configurados en el router):**
  - Java (TCP): `25565`
  - Bedrock (UDP): `19132`

---

## 4. Resolución de Problemas Finales

### **Análisis de Conexión de Jugador (2026-02-02)**

Se revisaron los logs tras un intento de conexión de un jugador. El análisis de los logs del último reinicio muestra un arranque completamente limpio, sin errores de conexión a la base de datos ni de carga de plugins.

- **Estado:** **Conexión Exitosa.** Los logs no muestran ningún error relacionado con el intento de conexión del jugador. El servidor está aceptando jugadores correctamente.

**El servidor está ahora en un estado óptimo y sin errores.**
