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

#### paso 1
descargar el sistema operativo de Ubuntu desde su pagina oficial. 

[Ubuntu](https://ubuntu.com/download/desktop)

tambien el programa para bootear memorias con sistemas operativos rufus. 

[rufus](https://rufus.ie/es/)

> [!NOTE]
> This is a note.
