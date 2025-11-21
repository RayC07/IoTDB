# Proyecto: Consultas en MongoDB para Big Data

Este repositorio contiene la documentación y ejemplos prácticos de consultas en **MongoDB**, incluyendo:
- Operaciones básicas (CRUD)
- Consultas con filtros y operadores
- Consultas de agregación con análisis de resultados

## 📌 Descripción
El objetivo es aplicar técnicas de almacenamiento y consulta en MongoDB para entornos de **Big Data**, documentando el código y explicando su funcionalidad.

---

## 📂 Estructura del repositorio
- `Consultas_MongoDB_RayCadena.docx` → Documento académico con consultas y análisis.
- `Consultas_MongoDB_RayCadena.md` → Versión en Markdown para visualización en GitHub.
- `README.md` → Este archivo con instrucciones y guía del proyecto.

---

## ✅ Requisitos previos
- **MongoDB** instalado y en ejecución.
- **MongoDB Shell** o **Compass** para ejecutar consultas.
- Opcional: **Python 3** con la librería `pymongo` para ejecutar consultas desde scripts.

Instalación de PyMongo:
```bash
pip install pymongo
```

---

## ▶️ Cómo ejecutar las consultas
### En MongoDB Shell
1. Conéctate a tu base de datos:
```bash
mongosh
use nombre_base_datos
```
2. Copia y pega las consultas desde el archivo `.md` o `.docx`.

### Con Python y PyMongo
Ejemplo de conexión:
```python
from pymongo import MongoClient
client = MongoClient('mongodb://localhost:27017/')
db = client['nombre_base_datos']
```
Luego ejecuta las consultas usando métodos como `find()`, `insert_one()`, `aggregate()`, etc.

---

## 📊 Consultas incluidas
- **CRUD básico**: inserción, selección, actualización, eliminación.
- **Filtros y operadores**: `$gt`, `$lt`, `$in`, `$and`, `$or`.
- **Agregaciones**: promedio, máximo, mínimo, conteo, agrupación por fecha y ubicación.

---

## 👨‍🎓 Autor
Ray Cadena González  
Curso: Big Data  
Universidad Nacional Abierta y a Distancia - CEAD Ibagué  
Año: 2025

---

¡Explora, aprende y contribuye! 🚀
