
## Introducción
Este documento presenta las consultas realizadas en MongoDB, incluyendo operaciones básicas, consultas con filtros y operadores, y consultas de agregación con análisis de resultados. El objetivo es documentar el código y explicar su funcionalidad para su uso en entornos de Big Data.

---

## Consultas en MongoDB

### Operaciones Básicas
1. **Inserción de documentos:**
   
db.sensores.insertOne({ sensor_id: 1, tipo: 'temperatura', ubicacion: 'Planta Norte', estado: 'activo' })
```

2. **Selección de documentos:**

db.sensores.find({ estado: 'activo' })
```

3. **Actualización de documentos:**

db.sensores.updateOne({ sensor_id: 1 }, { $set: { estado: 'inactivo' } })
```

4. **Eliminación de documentos:**

db.sensores.deleteOne({ sensor_id: 1 })
```

---

### Consultas con Filtros y Operadores
- Lecturas con valor mayor a 80:

db.lecturas.find({ valor: { $gt: 80 }, unidad: '%' })
```

- Lecturas entre 20 y 30 grados:

db.lecturas.find({ valor: { $gte: 20, $lte: 30 }, unidad: '°C' })
```

- Sensores que no están en Planta Norte:

db.sensores.find({ ubicacion: { $ne: 'Planta Norte' } })
```

- Lecturas de sensores específicos:

db.lecturas.find({ sensor_id: { $in: [1, 3, 5] } })
```

---

### Consultas de Agregación

#### 1. Promedio de valor por unidad
```
db.lecturas.aggregate([
  { $group: { _id: '$unidad', promedio_valor: { $avg: '$valor' } } }
])
```
**Análisis:** Calcula el promedio de lecturas agrupadas por unidad (°C, %, Pa).

#### 2. Máximo y mínimo valor por tipo de sensor
```
db.lecturas.aggregate([
  { $lookup: { from: 'sensores', localField: 'sensor_id', foreignField: 'sensor_id', as: 'sensor_info' } },
  { $unwind: '$sensor_info' },
  { $group: { _id: '$sensor_info.tipo', max_valor: { $max: '$valor' }, min_valor: { $min: '$valor' } } }
])
```
**Análisis:** Permite conocer el rango de valores por tipo de sensor (temperatura, humedad, presión).

#### 3. Cantidad de lecturas por sensor
```
db.lecturas.aggregate([
  { $group: { _id: '$sensor_id', total_lecturas: { $sum: 1 } } },
  { $sort: { total_lecturas: -1 } }
])
```
**Análisis:** Indica cuántas lecturas tiene cada sensor, útil para análisis de actividad.

#### 4. Promedio de temperatura por ubicación
```
db.lecturas.aggregate([
  { $lookup: { from: 'sensores', localField: 'sensor_id', foreignField: 'sensor_id', as: 'sensor_info' } },
  { $unwind: '$sensor_info' },
  { $match: { 'sensor_info.tipo': 'temperatura' } },
  { $group: { _id: '$sensor_info.ubicacion', promedio_temp: { $avg: '$valor' } } }
])
```
**Análisis:** Calcula el promedio de temperatura por ubicación (Planta Norte, Planta Sur, etc.).

#### 5. Promedio, máximo y mínimo por día
```
db.lecturas.aggregate([
  { $group: { _id: { $substr: ['$fecha_hora', 0, 10] }, promedio_valor: { $avg: '$valor' }, max_valor: { $max: '$valor' }, min_valor: { $min: '$valor' } } },
  { $sort: { _id: 1 } }
])
```
**Análisis:** Genera estadísticas diarias (promedio, máximo, mínimo) para monitoreo temporal.





