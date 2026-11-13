# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-1
El diagrama muestra un Modelo Relacional (MR) orientado a la gestión de una biblioteca, compuesto por 6 tablas relacionadas entre sí. A continuación, se detalla la estructura de cada una de ellas, indicando sus campos, claves primarias (PK) y claves foráneas (FK), así como las relaciones que se aprecian visualmente:   1. Tablas y EstructuraUSUARIOID_USUARIO (PK)   NOMBRE   TELEFONO   CORREO   TIPO_USUARIO   PRESTAMOID_PRESTAMO (PK)ID_USUARIO (FK) — Relacionado con la tabla USUARIOFECHA_PRESTAMOCORREOTELEFONODETALLE_PRESTAMOID_PRESTAMO (PK / FK)CODIGO_INVENTARIO (PK / FK)FECHA_DEVOLUCIONFECHA_REAL_DEVOLUCIONNUM_LEGAJOEJEMPLARCODIGO_INVENTARIO (PK)   ISBN (FK) — Relacionado con la tabla LIBRO   ESTADO   LIBROISBN (PK)TITULOEDICIONEDITORIAL.
2. Relaciones PrincipalesUsuario y Préstamo: Un usuario puede realizar múltiples préstamos (relación de uno a muchos representada entre USUARIO y PRESTAMO).Préstamo y Detalle de Préstamo: Un préstamo principal se desglosa en líneas o detalles de préstamo (DETALLE_PRESTAMO), relacionando los ejemplares concretos que se piden.Libro y Ejemplar: Un libro (identificado por su ISBN) puede tener varios ejemplares físicos en la biblioteca (EJEMPLAR).Libro y Autor: Existe una relación de muchos a muchos resuelta por la tabla intermedia LIBRO-AUTOR, lo que permite que un libro tenga varios autores y que un autor escriba varios libros.   
<img width="1427" height="652" alt="EJERCICIO 1-MR drawio" src="https://github.com/user-attachments/assets/11535393-d56e-408d-817e-6786e3969b71" />

La imagen muestra el proceso completo de **normalización de bases de datos** llevado a cabo de manera secuencial, desde una tabla inicial completamente desnormalizada hasta alcanzar la Tercera Forma Normal (3NF).

A continuación, se detalla lo que se realiza en cada fase representada en el esquema:

---

### 1. Fase de Normalización N°0 (Tabla Desnormalizada)

* **Estado inicial:** Se parte de una **única tabla gigante y plana** que contiene todos los datos mezclados (datos de usuarios, préstamos, detalles, libros, editoriales, autores y ejemplares) en un formato repetitivo.
* **Problema:** Presenta redundancia masiva de datos (por ejemplo, el nombre, correo y teléfono de un usuario o los datos de un libro se repiten en cada fila cada vez que realiza un préstamo), lo que genera anomalías de inserción, actualización y borrado.

### 2. Primera Forma Normal (1NF)

* **Condición:** Se busca que todos los atributos contengan valores atómicos (indivisibles) y que cada tabla tenga una clave primaria.
* **Proceso aplicado:** La tabla original se desglosa en tres tablas independientes para eliminar grupos repetitivos:
* **TABLA USUARIO:** Extrae toda la información referente al usuario, utilizando `ID_USUARIO` como Clave Primaria (PK).
* **TABLA EJEMPLAR / LIBRO:** Agrupa los datos correspondientes a los libros, sus ejemplares, editoriales y autores.
* **TABLA PRESTAMO:** Almacena los datos generales de la cabecera de los préstamos vinculados a cada usuario.



### 3. Segunda Forma Normal (2NF)

* **Condición:** Se requiere que la tabla esté en 1NF y que **todos los atributos que no son clave dependan por completo de toda la clave primaria** (se eliminan las dependencias parciales en tablas con claves compuestas).
* **Proceso aplicado:** Se reestructuran las tablas y se separa el detalle operativo:
* **TABLA PRESTAMO:** Conserva los datos generales del préstamo dependiendo exclusivamente de `ID_PRESTAMO`.
* **TABLA DETALLE_PRESTAMO:** Se crea como una tabla intermedia o de detalle con una clave primaria compuesta (`ID_PRESTAMO` y `CODIGO_INVENTARIO`), extrayendo aquellos atributos que dependen de ambos (como la fecha de devolución).



### 4. Tercera Forma Normal (3NF)

* **Condición:** La tabla debe estar en 2NF y **no debe contener dependencias transitivas** (es decir, ningún atributo que no sea clave debe depender de otro atributo que tampoco sea clave; todo debe depender "de la clave, de toda la clave y nada más que de la clave").
* **Proceso aplicado:** Se separan los datos en entidades totalmente normalizadas y especializadas:
* **TABLA EJEMPLAR:** Aísla cada ejemplar físico y su estado, relacionándolo con el libro mediante su `ISBN` (FK).
* **TABLA LIBRO:** Contiene los datos propios de la obra bibliográfica, identificados por su `ISBN` (PK) y separando la editorial.
* **TABLA AUTOR:** Almacena la información de los autores de forma independiente con su `ID_AUTOR` (PK).
* **TABLA LIBRO-AUTOR:** Actúa como una tabla asociativa (muchos a muchos) que vincula el `ISBN` del libro con el `ID_AUTOR`, resolviendo la relación múltiple de forma limpia.
* <img width="2402" height="2239" alt="EJERCICIO 1-FASES DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/6ac56fbe-636d-4519-9d2b-1a9a0e3b245f" />

