<h1>Curso XR Plugin 🥽</h1>
<h2>Instalar XR Plugin en tu proyecto 🧩</h2>
<ol>
  <li>Verificar que Android si este instalado desde el Build Settings</li>
  <li>Edit - Project Settings - XR Plugin Management</li>
  <li>Install XR Plugin Management</li>
  <li>Activar Open XR en escritorio y en Android</li>
  <li>Admitir el tipo de dispositivo</li>
  <li>Entrar a la nueva ventana "OpenXR"</li>
  <li>Agregar en "Enabled Interaction Profiles" los mandos deseados, repetir esto en el escritorio como en Android</li>
</ol>
<h2>Kit de herramientas 🔧</h2>
<ul>
  <li>Descargar el ToolKit y started assets (Ruta: Package Manager/+/add package by name) "com.unity.xr.interaction.toolkit"</li>
  <li><strong>Mano Prefab: </strong><a href="https://drive.google.com/file/d/10b39IekUdpBHlcTslZ-BlNRyH5uqPUe1/view">Link de descarga</a></li>
  <li><strong>Pistola Prefab: </strong><a href="https://drive.google.com/file/d/1C5Fn4Yq79yof4X1lkl0MIYzVqY_UBz3M/view">Link de descarga</a></li>
</ul>
<h2>Componentes 📚</h2>
<ul>
  <li><strong>Tracked Pose Driver:</strong> cámara con movimiento en VR</li>
  <li><strong>XR controller:</strong> configurar los controles</li>
  <li><strong>Locomotion System:</strong> Medios que proporciona XR para el movimiento en una escena</li>
  <li><strong>Continuous Move Provider (Action-Based):</strong> Movimiento continuo</li>
  <li><strong>Continuous Turn Provider (Action-based):</strong> Giro continuo</li>
  <li><strong>Snap Turn Provider (Action-based):</strong> Giro quebrado</li>
  <li><strong>Character Controller Driver:</strong> para tener un mejor manejo del character controller</li>
  <li><strong>XR Direct interactor:</strong> Componente para el interactuante</li>
  <li><strong>XR Simple interactable:</strong> Componente para el Interactuable</li>
  <li><strong>XR Grab Interactable:</strong> Componente para agarrar el Interactuable</li>
</ul>
<h2>Configuración Cámara 🎥</h2>
<ol>
  <li>Agregamos al main camara el componente Tracked Pose Driver, con esto ya tenemos la camara lista</li>
  <li>XR trae una camara ya configurada de la mejor manera, para utilizarla en la escena</li>
  <li>Click derecho en jerarquía XR/XR Origin VR</li>
</ol>
<h2>Configuración controles 🕹️</h2>
<ol>
  <li>Creamos dos empty uno será "Left Controller" y "Right Controller"</li>
  <li>Agregamos el componente "XR controller (Action base)" a ambos empty</li>
  <li>Si descargamos los starteds assets podemos configurar rápidamente los controles agregando las propiedades (Ruta: Samples/2.5.3/Starter Assets/Presets) "XR Default Left Controller" y "XR Default Right Controller"</li>
  <li>En el empty "XR Origin (XR rig)" fijarnos que tenga el componente "Input Action Manager" con el action "XR Default Input Actions" de lo contrario se lo debemos agregar</li>
  <li>Si deseamos algún modelo para las manos, podemos ponerlos como hijo del empty previamente creado</li>
</ol>
<h2>Configuración movimiento continuo 🏃</h2>
<ol>
  <li>En el empty "XR origin" agregamos el componente "Locomotion System"</li>
  <li>Este script debemos de pasarle el componente "XR Origin"</li>
  <li>Además agregar el componente "Continuous Move Provider (Action-Based)"</li>
  <li>Este script debemos de pasarle el componente "Locomotion System", ajustar "Gravity application" a "Immediatly", en forward pasar el "Main camara" y por ultimo agregar las entradas de los controles marcando "Use Reference" y seleccionar "XR LeftHand Locomotion/Move"</li>
  <li>Agregar un Character Controller, modificar el center en el eje "Y" a 1</li>
  <li>Por ultimo agregar un "Character Controller Driver" y pasar la referencia del "Continuous Move provider"</li>
</ol>
<h2>Configuración movimiento teletransporte 🕴️</h2>
<ol>
  <li>Click derecho en la jerarquia y agregamos "Ray interactor (Action-Based)" como hijo de Camara offset</li>
  <li>Click en las propiedades de "XR Controller (Action-Based)" y añadimos "XR Default Right Controller"</li>
  <li>En el empty "XR origin" agregamos el componente "Teleportation Provider"</li>
  <li>Este script debemos pasarle la referencia a "locomotation system"</li>
  <strong>Teletransporte en area:</strong>
  <ol>
    <li>En el empty del suelo agregamos el componente "Teleportation Area"</li>
    <li>En el script pasamos en collider el "Mesh collider" del suelo</li>
    <li>Creamos un empty como hijo del Ray Interactor (esta será la forma del lugar indicativo al que nos teletransportaremos)</li>
    <li>En el Ray interactor en el componente "XR Ray Interactor" / "Raycast configuration" cambiamos el Line type a "Bezier Curve" y ponemos estos valores 5, -7, 3, -0.3</li>
    <li>Por ultimo modificamos en el componente "XR Interactor Line Visual" pasamos la referencia del objeto previamente creado en "reticle"</li>
  </ol>
  <strong>Teletransporte en anchor:</strong>
  <ol>
    <li>Creamos un lugar indicativo para el teletransporte</li>
    <li>Agregamos el componente "Teleportation Anchor"</li>
    <li>En intereaction manager pasamos la referencia a "XR interaction manager", en collider pasamos el collider del objeto indicativo y en teleport anchor transform pasamos la referencia del objeto indicativo</li>
  </ol>
</ol>
<h2>Activar botón teletransporte 🎯</h2>
<p>Al momento de configurar el movimiento por medio de teletransporte, veras que el rayo siempre queda activado y esto es bastante incomodo cuando no deseas utilizarlo, para solucionar esto es bastante sencillo:</p>
<ul>
  <li>Crear un nuevo script por ejem: "ActivateTeleport"</li>
  <li>Agregar estas líneas de código:</li>
  <img src="https://github.com/TatoDesign/Repositorios-Imagenes/blob/main/XRPlugin/image.png">
  <li>Básicamente este script lo que hace es: una referencia al objeto del rayo el cual se activa si el botón se está presionando</li>
  <li>Agregamos el Script al empty "XR Origin"</li>
</ul>
<h2>Configuración rotación continua 🤸‍♂️</h2>
<ul>
  <li>En el empty "XR origin" agregamos el componente "Continuous Turn Provider (Action-based)"</li>
  <li>Este script debemos de pasarle el componente "Locomotion System"</li>
  <li>Por ultimo agregar las entradas de los controles, marcar "Use Reference" y seleccionar "XR RightHand Locomotion/Turn"</li>
</ul>
<h2>Configuración rotación quebrada 🛫</h2>
<ul>
  <li>En el empty "XR origin" agregamos el componente "Snap Turn Provider (Action-based)"</li>
  <li>Este script debemos de pasarle el componente "Locomotion System"</li>
  <li>por ultimo agregar las entradas de los controles, marcar "Use Reference" y seleccionar "XR RightHand Locomotion/Snap Turn"</li>
</ul>
<h2>Configuración interacción con objetos 📦</h2>
<p><strong>Interactuante:</strong> Establece el tipo de interacción que se desea y es interrumpible.</p>
<p><strong>Interactuable:</strong> Como responde el objeto a esta interacción.</p>
<ul>
  <strong>Interactuante:</strong>
  <ol>
    <li>En el empty de los controles agregar el componente "XR Direct Interactor"</li>
    <li>Asignar la referencia en Interaction Manager a "XR interaction manager"</li>
    <li>Agregar un sphere collider y marcarla como trigger</li>
  </ol>
  <strong>Interactuable:</strong>
  <ul>
    <strong>Interactuable simple:</strong>
    <ol>
      <li>Creamos un objeto al cual le agregaremos un rigidbody</li>
      <li>Agregamos el componente "XR Simple interactable"</li>
      <li>En "Interactable Events" encontraremos los diferentes eventos que podemos modificar</li>
    </ol>
    <strong>Interactuable agarrar:</strong>
    <ol>
      <li>Agregar al objeto que deseamos agarrar el componente "XR Grab Interactable"</li>
      <li>Agregar un "Rigidbody"</li>
      <li>Modificar el "Movement Type" a lo que se necesite, la mejor es "velocity tracking"</li>
      <li>Si desea que el objeto se agarrado desde un punto en específico, crea un empty y ubícalo en el lugar correspondiente</li>
      <li>En el script "XR Grab interactable" agregar en Attach transform la referencia del punto de ubicación</li>
      <li>Si desea que el objeto sea agarrado desde cualquier punto, en el script marcar la opción "Use Dynamic Attach"</li>
    </ol>
  </ul>
</ul>
<h2>Configuración de interfaces 🖥️</h2>
<ol>
  <li>Crear un canvas con todos los elementos que deseamos agregar</li>
  <li>En el canvas cambiar el "Render Mode" por "World Space" y cambiar la escala en "X,Y,Z" por "0.001" y ajustarlo a la posición deseada</li>
  <li>Eliminar el componente "Graphic Raycaster" y agregar el componente "Tracked Device Graphic Raycaster"</li>
  <li>En el empty "EventSystem" eliminar el componente "Standalone Input Module" y agregar el componente "XR UI Input Module"</li>
</ol>
