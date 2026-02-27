# Arquitectura de Acceso a Smallworld

Este documento describe el flujo de conexión desde el internet público hasta la ejecución de la aplicación Smallworld en la red interna.

## Diagrama C4 Model - Nivel 2 (Contenedores)

```mermaid
C4Container
    title Diagrama de Contenedores - Acceso a Aplicación Smallworld

    Person(user, "Usuario Externo", "Personal con acceso remoto.")

    System_Boundary(dmz, "Zona de Entrada (Public)") {
        Container(bastion, "Bastion ($BN)", "Windows Server", "IP: 137.131.177.182. Punto de entrada seguro desde internet.")
    }

    System_Boundary(internal_net, "Red Interna") {
        Container(ts, "Terminal Server ($TS)", "Windows Server", "IP: 10.164.97.210. Servidor de ejecución de aplicaciones.")
        Container(sb, "Samba & DB ($SB)", "Linux", "IP: 10.164.98.100. Almacena el binario (.exe) y la base de datos.")
        Container(sl, "Servidor de Licencias ($SL)", "Software Licenser", "IP: 10.164.65.250. Gestiona los tokens de Smallworld.")
    }

    Rel(user, bastion, "1. Inicia sesión RDP", "RDP/3389")
    Rel(bastion, ts, "2. Salta vía RDP", "RDP/3389")
    Rel(ts, sb, "3. Accede a ruta de red (SMB) para ejecutar .exe", "SMB/445")
    Rel(ts, sl, "4. Valida licencia al iniciar el sistema", "FlexLM/TCP")
    Rel(ts, sb, "5. Conexión de datos", "SQL/Proprietary")

    UpdateLayoutConfig($c4ShapeInRow="2", $c4BoundaryInRow="1")
