# Actividad 8 — Base de datos agro_campo

**Integrantes:** Annaela Marquez, Camilo Cuadrado.

**Fecha:** 28/10/2026

---

## Resumen del proyecto

La actividad consiste en diseñar y construir la base de datos `agro_campo` para una
empresa agrícola que administra varias fincas, lotes, insumos y aplicaciones de
productos. Se trabaja desde el modelado relacional (DDL), pasando por la integridad
referencial, las consultas de decisión (DML), la normalización de una planilla de campo
y el almacenamiento de detecciones de un modelo de visión artificial (YOLO).

---

## Resumen por punto

### Punto 1 · Modelado y creación de tablas (DDL)

Se creó la base de datos `agro_campo` con las tablas `finca` y `lote`. Se aplicaron las
restricciones PRIMARY KEY, NOT NULL, UNIQUE, CHECK y DEFAULT para garantizar la
calidad de los datos desde el motor y no desde la memoria del programador.

- Se verificó el Ejercicio 0 (versión de MySQL y hora del servidor).
- Se dibujó el modelo entidad-relación con cardinalidad finca–lote (1:N).
- Se probaron los errores generados por las restricciones UNIQUE, CHECK y PRIMARY KEY.
- **RETO 1:** se agregó la columna `tipo_riego` con ALTER TABLE, se creó la tabla
  `operario` (con llave autoincremental, documento único y `certificado_aplicador`
  BOOLEAN por defecto falso) y se insertaron tres operarios.

### Punto 2 · Integridad referencial e insumos con anexo técnico

Se relacionaron las tablas con llaves foráneas (FOREIGN KEY) y se registraron los
productos agrícolas a partir de su anexo técnico.

- Se crearon las tablas `producto` y `aplicacion` (tabla intermedia que resuelve la
  relación muchos a muchos lote–producto).
- Se explicó el significado de `ON DELETE RESTRICT`.
- **RETO 2A:** se registraron los tres productos faltantes (BioLarva WP, RoyaStop 250 EC
  y TizónFin 80 WP) con datos exactos del anexo.
- **RETO 2B:** se registró una aplicación de RoyaStop en el lote POR-L01 calculando la
  cantidad con subconsulta (dosis × área) y se calculó la fecha mínima de cosecha con
  `DATE_ADD`.

### Punto 3 · Consultas para tomar decisiones (DML)

Se respondieron preguntas del negocio combinando tablas con SELECT, WHERE, JOIN,
GROUP BY y HAVING.

- Se identificó qué pregunta del agrónomo responde cada consulta (3.1 a 3.4).
- Se explicó el cálculo del CASE que detecta SOBREDOSIS y SUBDOSIS.
- **RETO 3:** área total por cultivo, fincas con más de 5 ha (HAVING), productos nunca
  aplicados y el responsable con más kilogramos de fertilizante aplicados.

### Punto 4 · Normalización de una planilla de campo

Se detectaron las anomalías de una planilla sin normalizar y se llevó hasta la Tercera
Forma Normal (3FN).

- Se identificaron ejemplos de anomalías de actualización, inserción y borrado.
- Se creó la tabla `operario_n` eliminando la dependencia transitiva
  `documento → teléfono`.
- **RETO 4:** se creó `aplicacion_n` en 3FN, se migraron los datos con
  `INSERT ... SELECT` + JOIN y se reconstruyó la planilla original.

### Punto 5 · Visión artificial con YOLO y MySQL

Se almacenaron en MySQL las detecciones de un modelo YOLO y se convirtieron, con
vistas, triggers y consultas, en una recomendación agronómica.

- Se explicó el modelo `lote → imagen → deteccion` y `clase_objetivo → producto`.
- Se ejecutó YOLO real con una imagen de ejemplo y una foto propia.
- Se explicó línea por línea el trigger `trg_alerta_plaga`.
- **RETO 5:** tendencia por semana (YEARWEEK), densidad por hectárea, calidad del modelo
  por umbrales y diseño para comparar versiones del modelo (yolo11n-agro-v2).

---

## Estructura del repositorio

