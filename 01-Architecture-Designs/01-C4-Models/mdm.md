# Arquitectura de Acceso a Smallworld
**Flujo de Conexión y Ejecución**

```mermaid
graph TD
    %% Definición de Estilos (Colores C4)
    classDef person fill:#08427b,stroke:#073b6e,color:#ffffff,font-weight:bold;
    classDef system fill:#1168bd,stroke:#0b4884,color:#ffffff,font-weight:bold;
    classDef boundary fill:white,stroke:#444,stroke-dasharray: 5 5,color:#444;

    %% Nodos
    User((Usuario Externo)):::person

    subgraph DMZ ["Zona Pública (Internet)"]
        BN["Bastión ($BN)<br/>Windows Server<br/>137.131.177.182"]:::system
    end

    subgraph Internal ["Red Interna (LAN)"]
        TS["Terminal Server ($TS)<br/>Windows Server<br/>10.164.97.210"]:::system
        SB["Samba & DB ($SB)<br/>Linux Server<br/>10.164.98.100"]:::system
        SL["Servidor Licencias ($SL)<br/>IP: 10.164.65.250"]:::system
    end

    %% Conexiones con etiquetas claras
    User -- "1. Inicia RDP" --> BN
    BN -- "2. Salto RDP" --> TS
    
    TS -- "3. Carga .exe / 5. Datos" --> SB
    TS -- "4. Valida Licencia" --> SL

    %% Ajustes visuales de las cajas
    style DMZ font-weight:bold
    style Internal font-weight:bold
