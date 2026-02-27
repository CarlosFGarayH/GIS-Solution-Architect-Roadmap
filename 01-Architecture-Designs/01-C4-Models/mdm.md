# Arquitectura de Acceso a Smallworld
*Flujo de Conexión y Ejecución*

## Diagrama de Infraestructura

```mermaid
C4Context
    %% No usamos 'title' interno para evitar que se corte arriba
    
    Person(user, "Usuario Externo", "Acceso vía RDP")

    Boundary(dmz, "Zona Pública (Internet)") {
        System(bn, "Bastión ($BN)", "Windows Server<br/>137.131.177.182")
    }

    Boundary(internal, "Red Interna (LAN)") {
        System(ts, "Terminal Server ($TS)", "Windows Server<br/>10.164.97.210")
        
        %% Separamos los sistemas para que las flechas tengan espacio
        System(sb, "Samba & DB ($SB)", "Linux Server<br/>10.164.98.100")
        System(sl, "Licencias ($SL)", "Servidor Licencias<br/>10.164.65.250")
    }

    %% Relaciones claras y con espacio
    Rel(user, bn, "1. Inicia RDP")
    Rel(bn, ts, "2. Salto RDP")
    
    %% Unificamos el paso 3 y 5 para evitar que las letras se superpongan
    Rel_L(ts, sb, "3. Carga .exe / 5. Datos", "SMB & SQL")
    
    %% El paso 4 va hacia el otro lado
    Rel_R(ts, sl, "4. Valida Licencia", "FlexLM")

    %% Ajuste de diseño para dar más ancho
    UpdateLayoutConfig($c4ShapeInRow="2", $c4BoundaryInRow="1")
