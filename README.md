# Trabajo Individual
Maribel Choque Medrano
## Clase 1
### ¿Qúe es Git?
Git es un sistema que controla las versiones y guarda archivos pero de manera local.
### ¿Cómo nació GIT?
Fue creado por Linus Torvals porque BitKeeper le retiro la licencia por incumplir la regla de "No usaras ni tu ni tus colaboradores otro ademas de mi", creando git en 2 a 3 semanas.
### ¿Como intalar Git?
Primero escribes en cualquier navegador "Downloads Git" una ves instalado para verificar en la terminal escribes git --version.
#### Las configuraciones basicas
Lo que tienes que escribir en la terminal son estos comandos:
- git config --global user.name "Nuestro Nombre"
- git config --global user.gmail "Nuestro correo"
- git config --global core.autocrlf
### Archivos que todo repositorio debe tener
- Un README.md es una documentacion
- .gitignore es un archivo de texto 

## Clase 2
### States y Commits
Son para gestionar todos los cambios que se hacen.
#### Los estados de GIT
Se divide en tres en tres estados:
##### Directorio de trabajo (Modificado)
Es cuando hemos cambiado un archivo pero aun no esta guardado en nuestro historial.
Aqui Git observa nuestros archivos y los cataloga en dos opciones:
- Untracked: cuando esta sin seguimiento
- Modified: cuando GIT ya tiene la vercion modificada
Para poder pasar de Modificado a nuestro estado original uso (pero tener cuidado porque este eliminada fisicamente todo lo que escribiste):
- git restore "Nuestro archivo"
Si no quieres que GIT vea tu archivo creado lo que tienes que haces es poder tu archivo completo al .gitignore.
##### Stage Area (Preparado)
Es donde elegimos que archivos modificados  se incluiran en el siguiente commit y cual no, usamos:
- git add "Nuestro archivo" : Para agregar uno por uno
- git add . : Para agregar todos los archivos 
Para sacar un archivo del stage area usamos: git restore --staged "Nuestro archivo"
##### Repositorio Local (Confirmado)
Hacemos un punto de guardado para que todo los cambios del preparado sean parte del historial.
Usas : git commit -m "Tu mensaje o descripcion" y para desaser git reset --soft HEAD~1
### Buenas practicas para hacer un commit
Los commits solo tienen que describir un solo cambio pequeño(commits atomicos)
- Usar vervos imperativos como: Add, Change, Fix y Remove.
- No tenemos que usar punto al final y tampoco puntos suspensivos.
- Usar como maximo 50 caracteres
- Usar prefijos para que sea mas legibles como: feat, fix, perf, build, ci, docs, refactor, style y test.
- Poner un contexto despues del commit en su cuerpo pero   solo con informacion necesaria.

## Clase 3
### GITHUB Y SSH
#### ¿Qué es GITHUB?
Es una red social donde gestionamos y colaboramos en proyectos con otros desarrolladores usando GIT.
La diferencia entre GIT y GITHUB es que que el primero contro la las versiones que cre el punto de guardado y el segundo es donde se almacena estos puntos de guardados y se comparte con el mundo.
#### SSH vs HTTPS
HTTPS este nos pide autentificacion cada vez, cuando clonamos y queremos usar el repositorio,
pero el SHH (recomendado usar) se configura con una clave que al ponerla en GITHUB no nos pide mas autentificación.
#### Para configurar SSH
en la terminal ejecutamos (si usas windows haslo desde Git Bash):
- ssh-keygen -t ed25519 -C "Nuestro correo"
- cat ~/.shh/id_ed25519.pub
Copias el contenido y lo pegas en Settings en tu perfil de GITHUB le das un nombre a tu PC y haces click en "Add SHH Key".
- ssh ~T git@github.com
#### Para crear un repositorio en GITHUB
1. Tienes que ir al apartadodo de repositorio de tu cuenta y creas uno nuevo.
2. Pones un nombre y una descripcion y haces clik en "crear repositorio"
#### Conectar tu repositorio local del Git que ya existe a GITHUB
Los comandos son:
- git remote add origin git@github.com:tuUsuario/tuRepo.git.
- git branch -M main
- git push -u origin main (Pero ya tienes que tener tu repositorio inicializado).
#### Para clonar un repositorio en Git
Usa los comandos:
- git clone "git@github.com:TuUser/TuRepo.git"
- Si lo hiciste con HTTPS usa: git clone "https://github.com:TuUser/TuRepo.git"
- Para cambiar de puntero y no te pida autentificacion cada vez usas: git remote set-url origin "git@github.com:TuUser/TuRepo.git"
- Para ver tu repositorio : git remote -v
#### Cambios 
- git push origin <rama> (Empuja los commits al servidor apodado origin a la rama de mi codigo).
- git pull origin <rama> (Traer los commits).

## Clase 4
### Remote, SSH multiple y checkout
#### Git remote
Este comando nos ayuda a gestionar nuestras conexiones con repositorios remotos, los comandos que puedes usar son:
- git remote -v : Para ver las URLs de donde apunta nuestro repositorio.
- git remote add <apodo> "url" : para vincular nuestro repositorio local con uno en la nuve.
- git remote set-url <apodo> "url" : para cambiar la url de donde apunta nuestro repsitorio.
#### Multiples SSH
Cuando tenemos otras cuentas en github o simplemente necesitamos más cuentas tenemos que tener mas de una llave SSH.
Para configurar los multiples SSH seguimos estos pasos:
1. Generamos el ssh key con otro nombre: 
        ssh-keygen -t ed25519 -C
        "nuestroCorreo" -f~/.ssh/id_miname
2. Creamos un archivo config para que las llaves no choquen:
        # Nuestra cuenta personal
            Host github.com (Host: es el apodo que se le pone a la conexión)
            HostName github.com (HostName: es la direccion real del servidor)
            User git (User: nombre de usuario del sistema remoto)
            IdentityFile~/.ssh/id_ed25519 (IdentifyFile: es la ruta exacta a la llave privada)
        # La cuenta de otro correo
            Host github-miname
            HostName github.com
            User git
            IdentityFile~/.ssh/id_miname
3. Para ver si funciona
        ssh-T git@github-miname
Para hacer configuraciones por repositorio (locales) es lo mismo que hacer como las globales pero sin --global los comados son:
- git config user.name "Nuevo nombre"
- git config user.email "Mi correo"
Algo importante es hacer git clone solo con el host correcto de tu cuenta.
- git clone git@github-miname:usuario/repo.gti
#### Git Checkout
Es para desplazar el HEAD hacia un punto especifico del historia o una rama distinta. Esto nos sirve para inspeccionar como era el contenido
de un commitantiguo, recuperar los archivos borrados o cambiados, probar cambios sin llegar ha arruinar la rama principal y para saltar d una rama a otra.
El estado "Detached HEAD" aqui lo normal es que el HEADapunte a una rama en movimiento pero en su lugar apunta a un commit fijo.
Para ir y volver de commit usamos: git checkout <hash_antiguo> y git checkout <rama>. Cuidado porque si hiciste un commit aqui va ha 
desaparecer amenos que hagas: git checkout <hash_commit_creado> y git checkout -b rama_nueva.
##### Buenas practicas del Checkout
1. No trabajes por largo tiempo en "Detached HEAD", si ecribes mas de una linea trabaja en otra rama.
2. Siempre limpia tu directorio de trabajo, siempre has commit de lo que estas haciendo en el presente.
3. Usalo para aprender para entender como crecieron.

## Clase 5
### Ramas y GitFlow Basico
Las ramas y GitFlow es lo mas importante en para trabajar en equipo.
### ¿Qué son las ramas?
Las ramas son las principales utilidades para poder tener un mejor control del codigo que escribimos. Esto trata de dividir la rama principal (main o marter) para que podamos trabajar en nuevas caracteristicas y correcciones.
Para usar usar ramas usamos el comando "git branch" que nos ayuda a gestionar las ramas que tenemos o tendremos, los comados son:
- git branch : lista las ramas que tenemos y ver el posicionamiento actual del HEAD.
- git branch <rama> : es para crear una rama apartir de la rama que estamos posicionando.
- git branch -D <rama> : es para eliminar la rama.
#### Git Checkout enfocado en ramas
Se usa esencialmente para ver los archivos pasados mediante los commits, pero tambien puede usarse junto a las ramas para:
- Para cambiar de rama pero sin tener nada en modified/untracked o staged, el comando es: git checkout <rama>.
- Para crear la rama y movernos directamente a ella, el comado es: git checkout -b <rama>.
#### Git checkout vs git switch
Git checkout es multiproposito y te puede dejar en Detached HEAD facilmente ademas estaba sobrecargado. Por esta razon en 2019  se introdujo git switch para solo especializarse en ramas y evitar errores accidentales al moverse.
###  Gitflow Basico
Es un flujo de trabajo que nos permite trabajar ordenadamente con las ramas, versiones y con cualquier persona que quiera aportar en nuestro proyecto.
La forma en que funciona es:
- main.- Por defecto tenemos la rama main (o master) al crear el repositorio que contiene el codigo que se encuentra en producción.
- develop.- Esta es la rama de pre-producción esta tiene las caracteristicas que se estan probando que se lanzarán a producion pronto.
- Ramas de apoyo.- son las que nos permiten escribir nuestro codigo y son:
        feature/*: Esta nace de develop y es para realizar una tarea especifica.
        release/*: Esta nace de develop y muere en develop y main, es donde hacemos pruebas (QA).
        hotflix/*: Esta nace en main y es donde se arreglan los bugs o un problema en producción.











