# Documentación de Acceso: Entorno Smallworld SGNM

Este documento describe la arquitectura de red, el flujo de pasos técnicos y los tiempos de respuesta requeridos para iniciar la aplicación **SGNM 5.3.5 - PLUZ**.

## 1. Inventario de Servidores

| Sigla | Nombre del Servidor | IP / Host | Sistema Operativo | Función |
|:---:|:---|:---|:---|:---|
| **$BN** | Bastión | `137.131.177.182` | Windows | Puerta de enlace (Gateway) |
| **$TS** | Terminal Server | `10.164.97.210` | Windows | Ejecución de aplicación |
| **$SB** | Samba & DB | `10.164.98.100` | Linux | Binarios, Compilación y Datos |
| **$SL** | Servidor Licencias | `10.164.65.250` | Linux | Gestión de tokens de licencia |

## 2. Flujo de Conexión (Step-by-Step)

### Paso 1: Acceso Externo
Conectarse vía **RDP (Remote Desktop Protocol)** a la dirección pública del Bastión:
- **IP:** `137.131.177.182`

### Paso 2: Conexión Interna
Desde el escritorio del Bastión, iniciar una nueva sesión de RDP hacia el servidor de trabajo:
- **IP:** `10.164.97.210` ($TS)

### Paso 3: Ejecución de Smallworld
Dentro del Terminal Server ($TS), seguir estos pasos:
1. Presionar las teclas `Win + R` para abrir la ventana de **Ejecutar**.
2. Ingresar la ruta compartida del servidor Linux: `\\10.164.98.100\GNM`.
3. Ubicar y ejecutar el archivo: `SGNM 5.3.5 - PLUZ.exe`.

### Paso 4: Compilación y Licenciamiento
Al iniciar el ejecutable, el sistema realiza los siguientes procesos automáticos:
1. El servidor **$SB** compila internamente los recursos `.jar` y archivos `.magik`.
2. El servidor **$SB** establece conexión con el servidor de licencias (`10.164.65.250`) para validar el acceso.

---

## 3. Tiempos de Respuesta y Ejecución (Benchmarks)
*Medición realizada el: **27/02/2026 - 02:15 PM***

| Proceso | Duración (min:seg.ms) |
|:---|:---:|
| Ingreso al servidor Bastión mediante RDP | `00:33.99` |
| Ingreso al servidor Terminal Server mediante RDP | `00:18.77` |
| Apertura de credenciales hacia servicio Samba (vía Run) | `03:10.66` |
| Acceso a la carpeta compartida en el servicio Samba | `00:03.79` |
| Ejecución de SGNM hasta Inicio de Sesión (Core Spatial Tech) | `07:42.50` |
| Carga y vista del panel Smallworld Applications | `00:24.14` |
| Apertura total de plataforma SGNM Electricidad - PLUZ | `01:35.55` |

---

## 4. Diagrama de Arquitectura

```mermaid
graph TD
    %% Definición de Estilos (Colores C4)
    classDef person fill:#08427b,stroke:#073b6e,color:#ffffff,font-weight:bold;
    classDef system fill:#1168bd,stroke:#0b4884,color:#ffffff,font-weight:bold;
    classDef internal fill:#ffffff,stroke:#444,stroke-dasharray: 5 5,color:#444;

    %% Nodos
    User((Usuario Externo)):::person

    subgraph DMZ ["Zona Pública (Internet)"]
        BN["Bastión ($BN)<br/>137.131.177.182"]:::system
    end

    subgraph Internal ["Red Interna (LAN)"]
        TS["Terminal Server ($TS)<br/>10.164.97.210"]:::system
        SB["Samba & DB ($SB)<br/>10.164.98.100"]:::system
        SL["Licencias ($SL)<br/>10.164.65.250"]:::system
    end

    %% Conexiones
    User -- "1. Conexión RDP" --> BN
    BN -- "2. Salto RDP" --> TS
    
    TS -- "3. Ejecución Run:<br/>\\10.164.98.100\GNM" --> SB
    
    %% Flujo interno en SB
    SB -. "4. Compila .jar / .magik" .-> SB
    
    %% SB es quien pide la licencia
    SB -- "5. Valida Licencia" --> SL
    
    %% Retorno de apertura
    SB -- "6. Abre DB / Login" --> TS

    %% Estilos de los subgrafos
    style DMZ font-weight:bold
    style Internal font-weight:bold
