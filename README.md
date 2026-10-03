**Reporte Técnico de Configuración de Laboratorio**

**Checkpoint: Mi primer laboratorio seguro de ciberseguridad**



**1\_ Introducción**

El objetivo de esta actividad es crear y configurar una Máquina Virtual (VM) destinada a prácticas de ciberseguridad, aplicando medidas básicas de seguridad antes de comenzar a utilizarla para actividades de laboratorio.

La configuración busca establecer un entorno controlado y separado del sistema principal, utilizando una cuenta de usuario con privilegios limitados, manteniendo el sistema operativo actualizado y creando una instantánea inicial que permita recuperar el estado seguro de la máquina en caso de que una práctica futura provoque algún inconveniente.

Para este laboratorio se utilizó VirtualBox y una máquina virtual con sistema operativo Windows.



**2\_ Fundación: VirtualBox y red aislada**

2.1 Configuración de red

Antes de comenzar las prácticas se configuró la interfaz de red de la máquina virtual utilizando el modo NAT (Network Address Translation).

**Evidencia:**

<img width="819" height="514" alt="5 - Captura de pantalla MV  Windows inicio - configuracion de red NAT" src="https://github.com/user-attachments/assets/e2a01bc4-0adf-4320-8e43-8195a4fcdcb8" />


La configuración se realizó desde:
VirtualBox → Configuración → Red → Adaptador 1 → Conectado a: NAT

**2.2 Justificación**
Se seleccionó el modo NAT porque permite que la máquina virtual tenga acceso a Internet para realizar tareas como descargar actualizaciones y herramientas, sin exponerla directamente como un dispositivo independiente dentro de la red local.
De esta manera, la máquina virtual queda en un entorno más controlado que utilizando el modo Puente (Bridged Adapter), donde la VM podría aparecer en la red local como otro equipo.
Esta configuración constituye una primera medida de aislamiento del laboratorio y reduce la exposición innecesaria del sistema Host frente a las actividades que se realizarán posteriormente dentro de la máquina virtual.

3\_ Capa Windows: usuarios y actualizaciones

3.1 Creación de un usuario estándar
Como medida de seguridad se creó un usuario destinado a las prácticas con permisos estándar, separado de la cuenta administrativa.
**Evidencia:**
<img width="1033" height="469" alt="8- Captura de pantalla MV  Windows inicio - usuario estandart" src="https://github.com/user-attachments/assets/a2ddb220-e185-4cfd-9034-5349291479b6" />

<img width="707" height="568" alt="7 - Captura de pantalla MV  Windows inicio - usuario administrador" src="https://github.com/user-attachments/assets/dab9fe21-89a4-43d9-bdbf-b839c134fa7b" />


El objetivo de utilizar una cuenta sin privilegios administrativos para las actividades habituales es aplicar el principio de mínimo privilegio.
Este principio establece que cada usuario debería disponer únicamente de los permisos necesarios para realizar sus tareas. De esta forma, si una aplicación o actividad realizada durante una práctica se ve comprometida, se limita el nivel de acceso que podría obtener.
La cuenta administrativa queda reservada para tareas que realmente requieran privilegios elevados.

**3.2** Actualización del sistema operativo
Se verificó el estado de actualización del sistema operativo mediante Windows Update.
**Evidencia:**
<img width="751" height="697" alt="11 - Captura de pantalla MV  Windows inicio - windows actualizado" src="https://github.com/user-attachments/assets/f6a7f3d6-906c-4a49-8cf9-12079b1058f4" />

Mantener el sistema operativo actualizado es una medida fundamental de seguridad, ya que las actualizaciones pueden incluir correcciones de vulnerabilidades, errores y problemas de seguridad detectados por el fabricante.
Antes de utilizar la máquina virtual para prácticas de ciberseguridad, se considera importante partir de un sistema actualizado para reducir la exposición a vulnerabilidades conocidas.

4\. Capa Linux: permisos y gestión

4.1 Comprobación de permisos mediante ls -l
Como parte de la práctica se utilizó la terminal para crear un archivo y posteriormente visualizar sus permisos mediante el comando:
ls -l
**Evidencia:**
<img width="716" height="426" alt="2 - Captura de Linux - creacion de archivo y sus privilegios" src="https://github.com/user-attachments/assets/ca81daa3-560d-4f19-9001-72496043a7b8" />

El comando ls -l permite visualizar información detallada sobre los archivos y directorios, incluyendo sus permisos, propietario y grupo.
Los permisos permiten determinar qué usuarios pueden leer, modificar o ejecutar un determinado archivo.
Esta comprobación permite familiarizarse con uno de los mecanismos fundamentales de seguridad de los sistemas Linux: el control de acceso basado en permisos.
Nota: esta evidencia corresponde a la máquina Linux utilizada como parte de las prácticas del laboratorio.

4.2 Gestión de actualizaciones mediante APT
También se utilizó la terminal para consultar la disponibilidad de actualizaciones de los paquetes mediante:
sudo apt update
Evidencia:

<img width="752" height="374" alt="3 - Captura de Linux - sudo apt update verificacion de actualizaciones disponibles" src="https://github.com/user-attachments/assets/143f2866-df00-448b-b9ac-95efc37c55c5" />
El comando sudo apt update actualiza la información disponible sobre los paquetes de los repositorios configurados.
El uso de sudo permite ejecutar la operación con privilegios elevados de manera puntual, sin necesidad de trabajar permanentemente con la cuenta root.
Esta práctica permite reforzar el concepto de utilizar privilegios administrativos únicamente cuando son necesarios.

5_ Red de seguridad: Snapshot inicial
Una vez finalizada la configuración inicial y aplicadas las medidas básicas de seguridad, se creó una instantánea de la máquina virtual utilizando VirtualBox.
El Snapshot fue denominado:
Clean Install - Hardening applied
Evidencia:

<img width="1913" height="273" alt="4 - Captura de Linux - Snapshot" src="https://github.com/user-attachments/assets/8f791642-09d2-4af3-8c62-d987bd0c71c3" />
<img width="1178" height="228" alt="5- Captura de Linux - Snapshot" src="https://github.com/user-attachments/assets/2f5cfaf4-5802-44f2-9c3f-b82f7caf259e" />
La instantánea funciona como un punto de recuperación del laboratorio. Si durante una práctica futura se modifica accidentalmente la configuración, se instala una herramienta problemática o el sistema queda en un estado no deseado, será posible regresar al estado previamente guardado.
Por este motivo, el Snapshot representa una medida importante para mantener un entorno de pruebas controlado y facilitar la recuperación del laboratorio.


6\. Medidas de seguridad aplicadas

A través de la configuración realizada se implementaron diferentes medidas básicas de seguridad:

Medida	Objetivo

Red NAT	Reducir la exposición directa de la máquina virtual en la red local

Usuario estándar	Aplicar el principio de mínimo privilegio

Actualizaciones de Windows	Mantener el sistema protegido frente a vulnerabilidades conocidas

Permisos Linux	Comprender y controlar el acceso a archivos

sudo	Utilizar privilegios elevados únicamente cuando sean necesarios

Snapshot	Permitir la recuperación del estado seguro del laboratorio



Estas medidas no convierten a la máquina virtual en un sistema completamente seguro, pero establecen una configuración inicial adecuada para comenzar prácticas de ciberseguridad en un entorno controlado.
**7\_ CONCLUSIÓN**
La actividad permitió construir una primera máquina de prácticas aplicando diferentes capas básicas de seguridad.
La configuración de red mediante NAT proporciona un nivel inicial de aislamiento, mientras que el uso de una cuenta estándar permite aplicar el principio de mínimo privilegio. La instalación de actualizaciones contribuye a mantener el sistema actualizado y la utilización de permisos en Linux permite comprender cómo se controla el acceso a los recursos.
Finalmente, la creación de una instantánea establece un punto de recuperación que permitirá experimentar con diferentes herramientas y configuraciones durante futuras prácticas sin perder fácilmente el estado inicial del laboratorio.
De esta manera, la máquina virtual queda preparada como un entorno controlado para continuar desarrollando actividades de aprendizaje en ciberseguridad.
**8\_ Evidencias**

Evidencia 01 — Configuración de red NAT
<img width="827" height="575" alt="6- Captura de Linux - Configuracion de Red NAT" src="https://github.com/user-attachments/assets/26d90af9-f1a0-4c0f-b409-e844161be043" />
Descripción: Configuración del adaptador de red de la máquina virtual utilizando el modo NAT.

Evidencia 02 — Usuario estándar

Descripción: Usuario destinado a las prácticas configurado con permisos estándar.
<img width="1033" height="469" alt="8- Captura de pantalla MV  Windows inicio - usuario estandart" src="https://github.com/user-attachments/assets/a0b8a088-ab15-4bb5-b06c-69a316f1fc7f" />

Evidencia 03 — Windows Update

<img width="751" height="697" alt="11 - Captura de pantalla MV  Windows inicio - windows actualizado" src="https://github.com/user-attachments/assets/7d0a92ca-6cbc-4da3-9164-7acb4187b09e" />

Descripción: Verificación del estado de actualización del sistema operativo.

Evidencia 04 — Permisos Linux

<img width="716" height="426" alt="2 - Captura de Linux - creacion de archivo y sus privilegios" src="https://github.com/user-attachments/assets/7103fbd7-68c1-415c-9f08-ff94595c4956" />

Descripción: Ejecución de ls -l para visualizar los permisos del archivo creado.
Evidencia 05 — Actualización de paquetes Linux

<img width="752" height="374" alt="3 - Captura de Linux - sudo apt update verificacion de actualizaciones disponibles" src="https://github.com/user-attachments/assets/12d4404e-3efb-4c8c-a05c-77dc80397c68" />

Descripción: Ejecución de sudo apt update para consultar la información actualizada de los repositorios.

Evidencia 06 — Snapshot

<img width="752" height="374" alt="3 - Captura de Linux - sudo apt update verificacion de actualizaciones disponibles" src="https://github.com/user-attachments/assets/192964f3-f534-4ae5-8d11-6beaafdfe453" />

Descripción: Snapshot inicial del laboratorio denominado Clean Install - Hardening applied.

<img width="1913" height="273" alt="4 - Captura de Linux - Snapshot" src="https://github.com/user-attachments/assets/161b73fd-bf13-48d1-90ac-03f8e0b1eb52" />

<img width="1178" height="228" alt="5- Captura de Linux - Snapshot" src="https://github.com/user-attachments/assets/33890e2c-18d8-47fb-b6f3-b3d151b139f1" />


