# Trabajo Individual

Roger Eric Saldivar Rojas

## Clase 1
### ¿Qué es Git?
Git es un Sistema de control de versiones distribuido, gratuito y de codigo abierto. 

En términos sencillos, es una herramienta que registra los cambios realizados en los archivos de un proyecto a lo largo del tiempo, permitiéndote "viajar al pasado" para recuperar versiones anteriores o comparar modificaciones

### ¿Como instalar Git en: ?
### Linux
Si usas alguna distribucion basada en debian como Ubuntu usa el siguiente comando 
```bash
# apt-get install git
```
Para mas informacion acerca de la instalacion de git en otros Sistemas operativos consulta: [Descargar Git](https://git-scm.com/install/).

### Curiosidades sobre Git
#### ¿sSabes quien creo Git?
LO creo Linus GOAT Torvalds
#### Sabes como y porque se creo git

Todo comenzo cuando Linus Torvalds y el equipo de que desarrollaba el nucleo (kernel) de linux perdio su licencia gratuita de BitKeeper debido a que uno de los desarrolladores de linux trato de hacer ingenieria inversa al software, provocando la ruptura de la relacion entre la empresa y la comunidad de Linux.

Despues de eso Linus Torvalds busco alternativas pero ninguno terminaba de agradarle y al no encontrar nada util, Torvals frustado aplico su filosofia de: "Si quieres algo bien hecho, hazlo tú mismo". Lo que lo llevo a encerrarse durante 10 dias para desarrollar git y que al decimo dia, el software resulto ser tan funcional **que Git ya se usaba para gestionar el propio código de Git** XD. 

## Clase 2 
### Estados de Git

* **Working Directory:** Archivos         modificados (Modified) o nuevos (Untracked) que aún no están bajo el control de versiones.
* **Staging Area:** El área de preparación técnica donde se seleccionan los cambios específicos mediante un index antes de ser confirmados.
* **Local Repository:** El historial definitivo donde los cambios reciben un identificador único (**SHA-1 hash**).

### Comandos de Recuperacion y Gestion
Git permite manipular el estado de los archivos y gestionar qué elementos deben ser ignorados por el sistema.
 * **Restoring:** Uso de git restore `<file>` para descartar cambios en el directorio de trabajo o git restore --staged `<file>` para sacar archivos del área de preparación.
 * **Ignored Files:** Configuración del archivo `.gitignore` para excluir artefactos del sistema, dependencias o variables de entorno del seguimiento de Git.
### Buenas Practicas
La calidad del historial depende de seguir estándares de mensajes claros y cambios con un único propósito lógico.
 * **Atomic Commits:** Cada confirmación debe representar un cambio pequeño, completo y funcional, evitando "bloques" masivos de cambios no relacionados.
 * **Structure:** Los mensajes deben usar el modo imperativo (ej. "Add" en lugar de "Added"), no exceder los 50 caracteres y utilizar prefijos como feat, fix, docs, refactor, etc..

## Clase 3

### GitHub: El hogar de nuestro código
Git es la herramienta que crea los puntos de guardado en nuestra PC, pero GitHub es como la "nube" o red social donde guardamos y compartimos esos puntos con otros.

### Llaves SSH: Entrada sin contraseñas
Usar *HTTPS* es pesado porque te pide contraseña a cada rato. Configurar una llave SSH es como darle a GitHub una "llave digital" de tu casa (tu PC) para que te deje pasar automáticamente sin preguntar quién eres cada vez que subes algo.

+ **Configuracion SSH**: En la terminal ejecutamos los siguientes comandos desde tu terminal si estas en Linux o desde Git Bash si estas en Windows
```bash
~ ssh-keygen -t ed25519 -C “tu-correo@email.com”

~ cat ~/.ssh/id_ed25519.pub

#Copias el contenido del anteroir comando y te diriges a github donde te diriges a tu perfil → Settings y luego SSH y GPG Keys y luego “New SSH Key” (1) y pegas tu key, le das un nombre para tu PC y click en “Add SSH Key”. (2)

~ ssh -T git@github.com
```

### Conectar un repositorio local de Git existente con uno en Github
```bash
git remote add origin git@github.com:TuUser/TuRepo.git 

# Remote es la URL que apunta al servidor externo es decir a tu repositorio externo creado en Github y Origin es simplemente el apodo(nickname) que git le da por defecto a esa URL

git branch -M main

git push -u origin main
```
 
NOTA: PARA ESTO YA TIENES QUE HABER INICIALIZADO EL REPO. LOCAL `git init` Y TENER UN COMMIT INICIAL AL MENOS `git add . + git commit -m “Initial commit”`
### Comandos para "Viajar" a la nube (Push & Pull)

Para mover código usamos dos movimientos: push es para "empujar" tus cambios desde tu compu hacia GitHub, y pull es para "traer" o bajar lo que está en la nube a tu carpeta local. Es como subir y bajar archivos de un Drive, pero con esteroides.

+ **Subir mis cambios:**
```bash
git push origin <rama>
```
+ **Bajar los cambios hechos:**
```bash
git pull origin <rama>
```

### Gestión de Remotos y Visualización
Antes de mover archivos, es vital saber a dónde apuntan nuestros "túneles" de conexión. El comando `git remote` nos permite administrar estas direcciones, verificar las URLs configuradas con el modo *verbose* (-v) y corregirlas si cometimos algún error al escribirlas inicialmente

### Multi-SSH y Seguridad de Cuentas
Si manejas varias cuentas (ej. personal y de la UMSS), necesitas una llave para cada "puerta". Configurar múltiples llaves SSH evita conflictos de identidad. Esto se logra generando archivos de llave con nombres distintos y organizándolos en un archivo config para que Git sepa qué identidad usar en cada repositorio automáticamente

+ Paso 1. Generamos el sshkey en con
otro nombre:
```bash
ssh-keygen -t ed25519 -C
"micorreo@gmail.com" -f ~/.ssh/id_miname
```
+ Paso 2. Creamos un archivo config
para que no choquen las key:
```bash
# Cuenta Personal (la de siempre)
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_ed25519
# Cuenta del otro correo
Host github-miname
HostName github.com
User git
IdentityFile ~/.ssh/id_miname
```
### Navegación en el Tiempo y Estado Desacoplado
El comando checkout es nuestro "viajero del tiempo". Nos permite saltar entre ramas o incluso visitar un punto exacto del pasado usando un *hash*. Cuando viajamos a un commit específico sin una rama, entramos en estado **Detached HEAD**; aquí somos "espectadores" y cualquier cambio se perderá si no creamos una nueva rama para "encarnar" esos avances.

Para ir atras debes hacer:
`git checkout <hash_antiguo>`

Y para volver al ultimo hash de la rama
`git checkout <rama>`

Si hiciste algo aca (como un commit) desaparece
salvo que hagas:
```bash
git checkout <hash_commit_creado>
git checkout -b rama_nueva
```