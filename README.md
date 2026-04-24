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
