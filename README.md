
# Sistema de Inventario de Zapatos

**Estudiante:** Santiago Mosquera

## Descripción

Proyecto desarrollado en Python utilizando SQLAlchemy como ORM y SQLite como sistema de almacenamiento.

Permite registrar, consultar, buscar, actualizar y eliminar zapatos mediante un menú en consola.

## Tecnologías utilizadas

- Python
- SQLAlchemy
- SQLite

## Instalación

1. Clonar el repositorio.
2. Abrir la carpeta del proyecto.
3. Instalar las dependencias:

```bash
python -m pip install -r requirements.txt
```

## Ejecución

Ejecutar el siguiente comando:

```bash
python main.py
```

La base de datos `zapateria.db` se crea automáticamente al iniciar el programa.

## Preguntas y respuestas

### 1. ¿Qué clase de Python representa la tabla?

La clase `Zapato` representa la tabla `zapatos`. Hereda de `Base`, que utiliza `DeclarativeBase`.

El atributo `__tablename__` establece el nombre de la tabla y `mapped_column()` define sus columnas: id, modelo, talla y precio.

### 2. ¿Qué ocurre al ejecutar el programa por primera vez?

Se ejecuta `inicializar_bd()` desde `main.py`. Esta función utiliza `Base.metadata.create_all(engine)` para crear la tabla si todavía no existe.

SQLAlchemy crea el archivo `zapateria.db` y la tabla `zapatos` automáticamente.

### 3. ¿Qué recorrido siguen los datos al registrar un zapato?

El usuario selecciona la opción 1 del menú. `main.py` solicita el modelo, la talla y el precio, y llama a `datos.crear_zapato()`.

Esta función crea un objeto `Zapato`, lo agrega a la sesión mediante `session.add()` y guarda los datos permanentemente con `session.commit()`.

### 4. ¿Para qué se utiliza una sesión de SQLAlchemy?

La sesión permite interactuar con la base de datos mediante objetos Python.

Si se agrega o modifica un objeto sin ejecutar `commit()`, los cambios no quedan confirmados ni guardados permanentemente.

### 5. ¿Cómo funciona la búsqueda por ID?

La función `buscar_zapato()` utiliza `session.get(Zapato, id_zapato)` para consultar el registro.

Si encuentra el zapato, devuelve el objeto. Si no existe, devuelve `None`, permitiendo mostrar el mensaje "Zapato no encontrado".

### 6. ¿Cómo se actualiza el precio?

La función `actualizar_precio()` busca el zapato mediante su ID utilizando `session.get()`.

Si existe, modifica el atributo `precio` y ejecuta `session.commit()` para guardar el cambio. Si no existe, devuelve `False`.

### 7. ¿Qué ocurre cuando se elimina un zapato?

La función `eliminar_zapato()` busca el objeto por su ID. Si existe, utiliza `session.delete()` y confirma la operación con `session.commit()`.

La eliminación se comprueba intentando listar los registros o buscar nuevamente el ID eliminado.

### 8. ¿Qué sucede al cerrar y volver a ejecutar el programa?

Los zapatos permanecen almacenados porque SQLite guarda la información en el archivo físico `zapateria.db`.

Al ejecutar nuevamente el programa, SQLAlchemy se conecta a la misma base de datos y permite recuperar los registros existentes.

## Pruebas realizadas

Se realizaron las siguientes pruebas:

1. Registro de zapatos.
2. Consulta de todos los registros.
3. Búsqueda por ID.
4. Actualización de precio.
5. Eliminación por ID.
6. Cierre y reinicio para comprobar la persistencia.

También se probaron entradas numéricas inválidas desde el menú.

## Evidencias

Las capturas de las pruebas se encuentran en la carpeta `evidencias/`.
