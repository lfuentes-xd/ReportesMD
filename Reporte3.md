<center>

# ¿Podman o Docker?

</center>

para esta parte se nos pidio que investigaramos más acerca de una herramienta que se llama podman muy similar a Docker con algunas diferencias, que realmente, las cuales nos podrian hacer cambiar de opinicon respecto a cual elejir.

pero las mas significativas son...

### Arquitectura.

- Docker

  - Arquitectura.
    - este sigue una arquitectura cliente servidor lo que significa que necesita un daemon para ejecutarse en segundo plano, el cual maneja los contenedores.
  - Rootless
    - Docker tipicamente necesita permisos de root para poder correr contenedores.
  - Compatibilidad con OCI
    - Ambos soportan OCI

- Podman
  - Arquitectura.
    - por otro lado podman es Daemonless, lo que hace que no lo requiera, lo que hgace que este sea más lijero.
  - Rootless
    - Soporta correr contenedores sin la necesidad de correrlos comoroot
  - Compatibilidad con OCI
    - ambos contenedores soportan OCI

<center>

### para una mejor visualzacion...

</center>

<table border="1" cellpadding="10">
  <thead>
    <tr>
      <th>Característica</th>
      <th>Podman</th>
      <th>Docker</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Arquitectura</td>
      <td>Daemonless, no requiere un proceso en segundo plano.</td>
      <td>Cliente-servidor, necesita un daemon (Docker daemon) para gestionar contenedores.</td>
    </tr>
    <tr>
      <td>Rootless (sin privilegios de root)</td>
      <td>Soporte rootless nativo, permite a los usuarios no privilegiados ejecutar contenedores.</td>
      <td>Requiere privilegios de root, lo que puede implicar riesgos de seguridad.</td>
    </tr>
    <tr>
      <td>Compatibilidad con OCI</td>
      <td>Compatible con los estándares OCI de manera estricta.</td>
      <td>También compatible con OCI.</td>
    </tr>
    <tr>
      <td>Docker Compose</td>
      <td>Soporte limitado con Podman Compose.</td>
      <td>Compatibilidad total con Docker Compose.</td>
    </tr>
    <tr>
      <td>Orquestación</td>
      <td>No tiene sistema de orquestación propio, pero es compatible con Kubernetes.</td>
      <td>Incluye Docker Swarm para orquestación, aunque Kubernetes es más común.</td>
    </tr>
    <tr>
      <td>Gestión de imágenes</td>
      <td>Utiliza Skopeo para la gestión y transferencia de imágenes.</td>
      <td>Usa su propio sistema para la gestión de imágenes.</td>
    </tr>
    <tr>
      <td>Compatibilidad de comandos</td>
      <td>Compatible con la mayoría de los comandos de Docker, puedes reemplazar "docker" por "podman".</td>
      <td>Comandos propios de Docker.</td>
    </tr>
    </tbody>
</table>

no solo eso sino que tambien la similitud entre podman y docker son tales que los comandos son los mismos a excepció que Podman usa otro alias en lugar de docker, pero de ahi en más es lo mismo.

para poder instalarlo, es relativamente sencillo necesitamos algo similar como docker, pero al ser nativo para linux, se decidio instalarlo directamente en un linux, en este caso un Ubuntu en su version 24...

dado que se instalo en uno que era anterior a 22.10 se tuve que realizar de nuvo toda la instalación, ¿por que? por que podman no esta disponible para ubuntu en versiones anteriores a 22.10 por lo que se tuvo que reinstalar...

---

<center>

### Proceso de instlacion de Ubuntu

</center>

<table border="1">
    <thead>
        <th>
            materiales
        </th>
    </thead>
    <tbody>
        <tr>
            <td>
            Computador con caracteristicas decentes tal como ram y disco duro con espacio minimo de 120 gb
            </td>
        </tr>
          <tr>
            <td>
            Memoria booteada con el sistema operativo
            </td>
        </tr>
          <tr>
            <td>
            Disco duro con espacio 120gb minimos.
            </td>
        </tr>
          <tr>
            <td>
            RAM minimo 8 gb
            </td>
        </tr>
          <tr>
            <td>
            buena conexion a internet
            </td>
        </tr>
          <tr>
            <td>
            sistema ooerativo a poner 
            </td>
        </tr>
    </tbody>
</table>

# paso 1
Descargar el sistema operativo de Ubuntu desde su pagina oficial. 

[Ubuntu](https://ubuntu.com/download/desktop)

También el programa para bootear memorias con sistemas operativos:  rufus. 

[rufus](https://rufus.ie/es/)

> [!WARNING]
> Se necesita instalar una version superior a Ubuntu 22.10 para que podman funcione correctamente de lo contrario este no funcionara. 

con estos dos puntos podemos comenzar a instalar ubuntu en nuestro disco duro, en este caso es un ssd externo conectado por medio de USB por lo que necesitamos meternos a nuestro BIOS 


> [!WARNING]
> si no sabe como configurar la Bios es mejor que revise un tutorial para realizar dicha operación. 

en el caso de este equipo se necesita presionar f10 para entrar en las opciones de la BIOS y asi ajustar el arranque seguro, que por defecto esta en habilitado lo pasamos a deshabilitado para que podamos correr nuestro proceso de instalacion desde la memoria booteada. 

una vez hecho lo anterior apagamos/ reinciamos la computadora y conectamos el USB mientras el sistema aun no arranca. 

>[!TIP]
>si el instalador no arranca es probable que el orden de arranque este mal, por lo que dependiendo el caso, usted deberá presionar otra tecla, en caso mio es F2 para seleccionar la memoria y que esta empiece el proceso. 

una vez lo anterior comenzamos con el proceso de instalacion de ubuntu que es en teoria sencillo. es sumamente guiado y en la opcion para seleccionar el disco seleccionamos la opcion numero 2, que es par aborrar todo lo que tiene el disco y empezar desde cero


> [!CAUTION]
> Asegurese de seleccionar el disco correcto, no seleccione otro. 

una vez lo anterior y terminado el proceso de instalacion (que dependiendo la velocidad de su maquina) tarda de 10- 30 mn la instalacion, el sistema le pedirá que reinicie el equipo, y en un momento le pedirá que desconecte su unidad booteada, cuando llegue ese momento lo hace y presiona enter, y deja que el proceso continue. 

> [!NOTE]  
> SI por alguna razon queda trabado este proceso sera necesario revisar el orden de arranque y poner arriba el ubuntu antes que windows y se solucionará. 


![Instalacion de ubuntu 24](../ReportesMD/Imagenes/instalacion.png)

en ocasiones puede que la instalacion se haya hecho sin errores pero el arrancador se puso en uno de nuestros discos del sistema. 

nos dira algo asi ...

***MInimal BASH-Like line editing is suported. FOt the first word, TAB list possible command completions. Anywhere else TAB list posible device or file completions.***

en ese caso el arrancador se puso en otra ubicacion diferente a la de nuestro dusco duro externo (eso si se eligio otra instalacion diferente a la dicha)

en dado caso solo tendremos que escribir exit, para que continue a nuestro sistema operativo. 

---

una vez hecho eso... necesitamos instalar todo lo necesario para poder trabajar. 

¿que necesitamos? 

1. Visual Studio Code
2. Postman
3. Git
4. Podman/ CLI
5. Python
6. NVM

las aplicaicones de Vscode se encuentran en la tienda de Ubuntu...


![Instalacion de ubuntu 22.04](../ReportesMD/Imagenes/Aplications.png)

[para la instalacion de Podman se siguio la documentacion](https://podman-desktop.io/docs/installation/linux-install)

instalando Flatpak bundle. [Flatpak](https://flatpak.org/setup/Ubuntu)

y seguimos los pasos tal cual nos marca la pagina. 

para la interfaz grafica descargamos la aplicacion desde su pagina oficial. 


![descarga de podman](../Reportes/Imagenes/podman.png)

y si todo se hizo correcto podremos ver una vista asi. 

![finalizada](../Reportes/Imagenes/instalacion_Podman.png)

una vez hecho lo anterior, necesitamos comprobar que tengamos lo necesario para poder poner nuestra app en un contenedor. 

en este caso nos falta. python por lo que se instala y ya, (en ocasiones ya viene instalado lo revisa poniendo el comando python3 --version)

<center>

![comprobación](../Reportes/Imagenes/comprobacion.png)

</center>

por lo demás, necesitamos instalar Git, para hacer eso se baso en su documentación. [Git](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Instalaci%C3%B3n-de-Git)

y configuramos el usuario y correo.

```Git
git config --global user.name "Tu Nombre de Usuario"
git config --global user.email "tuemail@example.com"
```

y asi podremos empezar a usar git ...

en nuestro caso clonamos la aplicacion de flask para echart. para asi poder empezar a usar podman. 

### ¿cuales son los pasos? 

1. Clonar el repositorio

```Git
git clone Tu_link_Aqui
```

2. crear el ambiente virtual. 
```Linux
python3 -m venv .venv
```

> [!NOTE]  
> En ubuntu no se soporta ese comando amenos que se tenga instalado el paquete para ambientes virtuales. dicho comando lo arroja la terminal, una vez hecho eso podremos correr el comando normalmente. 

3. habilitamos el ambiente virtual. 
```Linux
. .venv/bin/activate
```
4. instalamos las dependencias. 
```Python
pip install -r Requirements.txt
```
5. corremos el programa. 
```Python
python3 main.py
```

una vez lo verificamos que si corre, es momento de usar podman. 

6. generar archivo para podman. 

creamos un archivo en la raiz de nuestro proyecto, con el nombre de 
**Dockerfile**

con una estructura como esta. 

```Dockerfile
# Usar una imagen base oficial de Python
FROM python:3.12-slim

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /main

# Copiar los archivos de tu proyecto al directorio de trabajo
COPY . /main

# Instalar las dependencias de Python
RUN pip install --no-cache-dir -r Requirements.txt

# Exponer el puerto en el que correrá la aplicación
EXPOSE 5000

# Comando para ejecutar la aplicación
CMD ["python", "main.py"]

```
una vez lo anterior , y asegurados de que el archivo esta correcto, hacemos lo siguiente. 

Abriendo una nueva terminal ponemos el siguiente comando. 

para generar la imagen. 
```Linux
podman build -t flask-app .
```

este para correrlo. 
```Linux
podman run -d -p 5000:5000 flask-app
```

> [!NOTE]  
> Si no tiene un archivo Requiremtns en su proyecto, el contenedor no funcionara, lo necesita crear. 

y una vez que este corra lo puede ver asi ...

<center>

![contenedor en podman](../Reportes/Imagenes/ContenedorCorriendo.png)

</center>

y un navegador asi ...


<center>

![comprobación del contenedor](../Reportes/Imagenes/contenedorFuncionando.png)

</center>

