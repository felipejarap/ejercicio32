1. Crear base de datos
""" CREATE DATABASE Pintagram;
"""

1.1 Acceso a bd
""" \c pintagram """

2 Crear tabla de Users
""" CREATE TABLE users ( id integer PRIMARY KEY, first_name VARCHAR (50) NOT NULL, last_name VARCHAR (50) NOT NULL, email VARCHAR (50) NOT NULL ); """

Agregar 3 usuarios
""" INSERT INTO users (id, first_name, last_name, email) values (1,'Monica','Mambo','mmambo@gmail.com'),(2,'Erica','Number','enumber@gmail.com'),(3,'Rita','Five','rfive@gmail.com'); """

Crear tabla Image
""" CREATE TABLE image ( id INTEGER PRIMARY KEY, name VARCHAR NOT NULL, type VARCHAR NOT NULL, size FLOAT NOT NULL, owner_id INTEGER REFERENCES users(id) ); """

Agregar 3 Imágenes
""" INSERT INTO image (id, name, type, size, owner_id) values (1,'Rain forest','nature',1000,1),(2,'Atacama desert','landscape',10000,2),(3,'Neuschweinstein castle','architecture',20000,3); """

Renombrar tabla Image a Images:
""" ALTER TABLE image RENAME TO images; """

Agregar 3 imágenes más para llegar a dos por usuario:
""" INSERT INTO images (id, name, type, size, owner_id) values (4,'Winter forest','nature',1000,1),(5,'Sky view','wallpaper',10000,2),(6,'Prague castle','architecture',20000,3); """

Crear tabla likes:
""" CREATE TABLE likes( user_id INTEGER REFERENCES users(id), image_id INTEGER REFERENCES images(id), PRIMARY KEY(user_id, image_id) ); """

Ingresar 3 likes por imagen:
""" INSERT INTO likes (user_id, image_id) VALUES (1,1),(1,2),(1,3),(1,4), (1,5),(1,6),(2,1),(2,2), (2,3),(2,4),(2,5),(2,6), (3,1),(3,2),(3,3),(3,4), (3,5),(3,6) ; """

Crear tabla tags:
""" CREATE TABLE tags( id SERIAL PRIMARY KEY, name VARCHAR ); """

Ingresar 8 tags
""" INSERT INTO tags(name) VALUES ('RIP'),('woah'),('nice'),('LOL'),('friends'),('holidays'),('mood'),('hot') ; """

Crear tabla de imágenes con etiqueta (tags)
""" CREATE TABLE images_tags( image_id INTEGER REFERENCES images(id), tag_id INTEGER REFERENCES tags(id), PRIMARY KEY(image_id, tag_id) ); """

Ingresar 3 tags por imagen:
""" INSERT INTO images_tags VALUES (1,1),(1,2),(1,3), (2,4),(2,5),(2,6), (3,1),(3,2),(3,3), (4,4),(4,5),(4,6), (5,1),(5,2),(5,3), (6,4),(6,5),(6,6) ; """

Crear consulta para mostrar nombre de imagen y cantidad de likes
""" SELECT images.name, COUNT(*) FROM images INNER JOIN likes ON (images.id = likes.image_id) GROUP BY images.name ; """

Crear consulta para mostrar nombre de usuario y fotos pertenecientes
""" SELECT first_name, last_name, name FROM users INNER JOIN images ON (users.id = images.owner_id) ; """

Crear consulta para mostrar nombre de etiqueta y cantidad de imágenes con esa etiqueta
""" SELECT tags.name, COUNT(*) FROM tags INNER JOIN images_tags ON (tags.id = images_tags.tag_id) GROUP BY tags.name ; """