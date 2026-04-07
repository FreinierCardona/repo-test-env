# Freinier Steven Cardona Perez - TI: 1077726586 / Analisis y Desarrollo de Software - Ficha: 3145555




# 🏗️ Guía de Despliegue de Base de Datos con Liquibase
Este repositorio contiene la estructura de migraciones para el entorno de base de datos PostgreSQL utilizando Liquibase sobre Docker.

## 🚀 Resumen del Proceso (HU-02: Creación de Tabla Person)
Se ha implementado con éxito la creación de la tabla person siguiendo una arquitectura modular. A continuación, se detallan los pasos técnicos realizados:

### 1. Definición del Objeto (SQL)
Se creó el script de definición de tabla en la ruta:
01_tables/0001_create_table_person.sql

Acción: Creación de tabla con campos id, first_name, last_name, email y timestamps.

### 2. Configuración del ChangeLog Modular
Se vinculó el script SQL dentro de un archivo YAML específico para tablas:
01_tables/00000_changelog.yaml

Etiqueta (Label): HU-02

Rollback: Configurado para apuntar a la carpeta 11_rollbacks/.

### 3. Orquestación Master
El archivo changelog-master.yaml actúa como índice principal, incluyendo el archivo de la HU-02 y manteniendo comentados los módulos vacíos para evitar errores de parseo (Could not find databaseChangeLog node).

## 🛠️ Comandos de Ejecución
Debido a la arquitectura de contenedores, el flujo de ejecución estándar es:

Sincronización de Archivos (Host a Contenedor)
Si se realizan cambios en VS Code, deben enviarse al runner de Liquibase:

PowerShell
docker cp . liquibase_runner:/liquibase/changelog
Aplicación de Cambios
Ejecutar el comando de actualización filtrando por el label de la historia de usuario:

### Bash

liquibase update --labels=HU-02

✅ Resultados Obtenidos
Estado: Exitoso.

Logs de Salida: Update has been successful. Rows affected: 0.

### Persistencia: * Tabla person creada en el esquema public.

Registro de ejecución insertado en la tabla de control databasechangelog.

## 📌 Notas de Mantenimiento

### Nuevos Cambios: No editar los Changesets ya aplicados. Crear siempre un nuevo ID (ej: id: 0002).

### Extensiones: Asegurarse de usar consistentemente .yaml en todas las referencias del Master para evitar errores de "File not found".

### Módulos: Para activar Vistas o Procedimientos, descomentar la línea correspondiente en el changelog-master.yaml una vez que el archivo destino tenga la raíz databaseChangeLog:.

