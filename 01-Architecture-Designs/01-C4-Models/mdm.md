Aquí tienes el contenido completo listo para ser guardado en un archivo con extensión `.md` (por ejemplo: `flujo_acceso_servidores.md`). 

He utilizado la sintaxis **C4Container** que es la más estándar y compatible de Mermaid para el modelo C4, y he incluido una tabla descriptiva para mayor claridad.

---

```markdown
# Documentación de Flujo de Acceso - Sistema Smallworld

Este documento detalla el procedimiento técnico y la arquitectura de red para el ingreso a los servidores de la infraestructura y la ejecución de la aplicación Smallworld.

## 1. Diagrama de Arquitectura (C4 Model)

El siguiente diagrama representa los contenedores y el flujo lógico de la sesión.

```mermaid
C4Container
    title Diagrama de Flujo de Ingreso y Ejecución Smallworld

    Person(user, "Usuario Externo", "Personal autorizado para operar Smallworld.")

    System_Boundary(c1, "Infraestructura de Red") {
        
        Container(bn, "Bastion ($BN)", "Windows Server", "IP: 137.131.177.182", "Puerta de entrada desde internet. Recibe tráfico RDP.")
        
        System_Boundary(c2, "Red Interna (LAN)") {
            Container(ts, "Terminal Server ($TS)", "Windows Server", "IP: 10.164.97.210", "Servidor donde el usuario trabaja y ejecuta la aplicación.")
            Container(sb, "Samba & DB ($SB)", "Linux Server", "IP: 10.164.98.100", "Almacena el binario (.exe) en ruta compartida.")
            Container(sl, "Licencias ($SL)", "Servidor de Licencias", "IP: 10.164.65.250", "Valida las licencias activas al ejecutar el software.")
        }
    }

    Rel(user, bn, "1. Acceso RDP", "RDP/TCP 3389")
    Rel(bn, ts, "2. Salto RDP", "RDP/TCP 3389")
    Rel(ts, sb, "3. Acceso a ruta / Ejecución .exe", "SMB/CIFS")
    Rel(ts, sl, "4. Petición de Licencia", "Protocolo de Licencias")
```

## 2. Detalle de Servidores

| Identificador | Nombre del Servidor | Dirección IP | Sistema Operativo | Función |
| :--- | :--- | :--- | :--- | :--- |
| **$BN** | Bastion | 137.131.177.182 | Windows | Punto de entrada único desde Internet. |
| **$TS** | Terminal Server | 10.164.97.210 | Windows | Host donde se inicia la sesión de usuario final. |
| **$SB** | Samba y Base de Datos | 10.164.98.100 | Linux | Repositorio de archivos del sistema y datos. |
| **$SL** | Servidor de Licencias | 10.164.65.250 | - | Gestión de tokens de software. |

## 3. Flujo de Inicio de Sesión Paso a Paso

1.  **Conexión Inicial:** El usuario inicia una conexión de Escritorio Remoto (RDP) hacia el **Bastion ($BN)** utilizando la IP pública `137.131.177.182`.
2.  **Segundo Salto:** Una vez dentro del escritorio del Bastion, se abre una nueva sesión de RDP interna hacia el **Terminal Server ($TS)** en la IP `10.164.97.210`.
3.  **Localización del Ejecutable:** En el Terminal Server, se debe navegar hacia la ruta de red compartida ubicada en el servidor Linux **$SB** (`10.164.98.100`).
4.  **Ejecución de Smallworld:** Se localiza el archivo `.exe` en la ruta Samba y se ejecuta con doble clic.
5.  **Validación de Licencia:** Al iniciar, el sistema Smallworld en el Terminal Server contacta automáticamente al **Servidor de Licencias ($SL)** en la IP `10.164.65.250`. Si hay una licencia disponible, el sistema se abre correctamente.

---
*Nota: Este flujo garantiza que el tráfico interno nunca esté expuesto directamente a internet, utilizando el Bastion como único punto de inspección.*
```

---

### ¿Cómo visualizarlo?
1.  **VS Code:** Instala la extensión "Markdown Preview Mermaid Support".
2.  **GitHub/GitLab:** Copia el código en un archivo `.md` y súbelo; se renderizará automáticamente.
3.  **Obsidian:** Simplemente pega el código en una nota.
4.  **Navegador:** Puedes pegar el código de Mermaid en el [Mermaid Live Editor](https://mermaid.live/) para exportarlo como imagen si lo necesitas.
