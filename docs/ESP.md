

APP-full

Presentación del proyecto
Implementación de una aplicación completamente del lado del servidor, incluyendo el renderizado de la vista también.

La aplicación accederá a una base de datos SQL utilizando mysql2.
La vista (el HTML que el servidor envía al navegador) será generada con EJS.
Las rutas (es decir, las URLs y las acciones que estas ejecutan) serán gestionadas con express, que es un framework de Node.js para manejar servidores web.

Habrá un sistema de autenticación de usuarios. Para proteger las contraseñas, se usará bcrypt, que es una librería que permite cifrar (hash) las contraseñas, evitando que se almacenen en texto plano.
El mantenimiento de las sesiones de los usuarios (es decir, la información que indica si un usuario está conectado o no) se gestionará con express-session, que permite almacenar la sesión en el servidor. Además, se usará un almacenamiento SQL para estas sesiones (store sql), lo que significa que las sesiones se guardarán en la base de datos.
Para manejar datos sensibles, como claves de API o configuraciones del servidor, se usará dotenv, que permite guardar estas variables en un archivo .env fuera del código fuente. Esto mejora la seguridad.

Durante el desarrollo de la aplicación, se usará nodemon, una herramienta que reinicia el servidor automáticamente cada vez que detecta cambios en el código, lo que facilita las pruebas y el desarrollo.

La temática de la aplicación será un blog.
La arquitectura será MVC (Modelo, Vista, Controlador), que es una forma de organizar el código separando la lógica de negocio (Modelo), la lógica de presentación (Vista) y el control de las interacciones entre ambos (Controlador). Esta arquitectura facilita la organización y el mantenimiento del código.

Reglas del blog:
Solo el administrador podrá publicar artículos.
Los artículos:
Solo podrán ser comentados por usuarios que hayan iniciado sesión.
Tendrán una imagen asociada.
Mostrará el nombre del autor que lo escribió.
Mostrará la fecha y hora de publicación.
Tendrán un título.
Contendrán el texto o contenido del artículo.
Estarán vinculados a una única categoría.
Sobre los comentarios:
Mostrará el nombre del usuario que escribió el comentario.
Mostrará la fecha y la hora en la que se publicó.
Incluirá el mensaje o contenido del comentario.
Requisitos para que un usuario pueda iniciar sesión:
Un alias o nombre de usuario (username).
Una contraseña (password).
Esquema de la base de datos
Modelo Conceptual de Datos (MCD)
Entidades (tablas principales del sistema):

user (usuarios)
story (historias o artículos del blog)
comment (comentarios)
Cardinalidades (relaciones entre las entidades):

Un user puede comentar una o varias stories (artículos). 0..N

Una story puede tener comentarios de uno o varios users. 0..N

Una story estará relacionada con una sola category (categoría). 1..1

Una category puede estar relacionada con una o varias stories. 0..N

Relaciones:

user N <-----> N story
(Un usuario puede comentar varias historias, y una historia puede tener comentarios de varios usuarios).

story 1 <-----> N category
(Cada historia pertenece a una única categoría, pero una categoría puede tener varias historias).

Modelo Lógico de Datos (MLD)
Tablas y sus campos en la base de datos:

User: (id, username, password)

Aquí se guardarán los usuarios registrados, con su nombre de usuario y contraseña cifrada.
User_Story: (#user_id, #story_id, message, publishDate)

Esta tabla representará los comentarios, con el ID del usuario, el ID de la historia comentada, el mensaje del comentario y la fecha de publicación.
Story: (id, title, content, publishDate, author, img, #category_id)

Esta tabla contendrá las historias del blog, con su título, contenido, fecha de publicación, autor, imagen asociada y el ID de la categoría.
Category: (id, label)

Tabla que contiene las categorías de los artículos, con un campo para el nombre o etiqueta de la categoría.
Panel de Administración (Back-Office)
Un panel de administración simple que permitirá al administrador (propietario del sitio) gestionar los artículos del blog:

Crear un nuevo artículo.
Leer o visualizar un artículo.
Actualizar o editar un artículo.
Eliminar un artículo.
Funcionalidad adicional (BONUS)
Se incluirá la posibilidad de gestionar (CRUD) las categorías del blog:

Crear, Leer, Actualizar y Eliminar categorías.
Esto permitirá un CRUD completo en la aplicación, lo que significa que todas las entidades principales podrán ser creadas, leídas, actualizadas y eliminadas.