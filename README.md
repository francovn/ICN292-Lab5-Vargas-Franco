# ICN292-Lab5-Vargas-Franco
 
Laboratorio 5 de **ICN-292 Sistemas de Información para la Gestión**.
 
El laboratorio crea y carga la base `andesbike` de Andes Bike, una cadena de tiendas de bicicletas, y resuelve diez consultas SQL sobre ella.
 
## Archivos
 
| Archivo | Contenido |
|---|---|
| `ICN292-Lab5-Vargas-Franco.sql` | Creación de las cuatro tablas, carga oficial y las diez consultas, en ese orden |
| `ICN292-Lab5-Vargas-Franco.pdf` | Informe: código de cada consulta y captura de su resultado |
| `ICN292-Lab5-Vargas-Franco.docx`| Informe en formato Word|
| `ICN292-Lab5-Vargas-Franco.png` | Modelo entidad-relación de la base ya construida (MySQL Workbench) |
| `Consultas/` | Capturas de las consultas que usan en el informe |
 
## Modelo de datos
 
- `tiendas` (`id_tienda`, `nombre`, `comuna`)
- `vendedores` (`id_vendedor`, `nombre`, `id_tienda`, `fecha_ingreso`)
- `bicicletas` (`id_bicicleta`, `modelo`, `categoria`, `precio`)
- `ventas` (`id_venta`, `id_vendedor`, `id_bicicleta`, `fecha`, `unidades`)
Relaciones: cada vendedor pertenece a una tienda (puede no tener), y cada venta la registra un vendedor y corresponde a un modelo del catálogo. `categoria` solo admite `'Eléctrica'`, `'Infantil'`, `'Montaña'`, `'Ruta'` y `'Urbana'`.
 
## Cómo ejecutarlo
 
1. Abrir `ICN292-Lab5-Vargas-Franco.sql` en MySQL Workbench, conectado a un servidor MySQL 8.
2. Ejecutar todo el script (rayo). Corre de principio a fin sobre una base vacía.
3. El script parte con `DROP DATABASE IF EXISTS andesbike;`, así que borra y vuelve a crear esa base si ya existía.
Ninguna consulta modifica datos, por lo que se pueden correr en cualquier orden.
 
## Carga oficial
 
4 tiendas, 8 vendedores, 8 modelos y 18 ventas. Las ventas suman 35 unidades y un monto de 16.969.650 (monto de una venta = `unidades * precio`).
 
## Consultas
 
| N.º | Qué responde | Técnica |
|---|---|---|
| 1 | Todos los vendedores con su cantidad de ventas, incluidos los que no tienen | `LEFT JOIN`, `COUNT(columna)` |
| 2 | Ventas y unidades por tienda, incluidas las tiendas sin vendedores | `LEFT JOIN` encadenado |
| 3 | Tiendas sin ningún vendedor | anti-join |
| 4 | Modelos que no se vendieron en junio de 2025 | condición del mes en el `ON` |
| 5 | Vendedores sin ventas, con el nombre de su tienda | `LEFT JOIN` encadenado, anti-join |
| 6 | Pares de vendedores de la misma tienda, el que ingresó antes primero | autojoin |
| 7 | Monto en bicicletas de Montaña y Ruta por tienda, solo si supera 2.000.000 | `JOIN` encadenado, `HAVING` |
| 8 | Modelos con precio sobre el promedio del catálogo | subconsulta escalar en el `WHERE` |
| 9 | Vendedores con promedio de unidades por venta sobre el de la cadena | `HAVING`, subconsulta escalar |
| 10 | Monto total por vendedor, incluidos los que no vendieron | `LEFT JOIN` encadenado |
 
## Compilar el informe
 
Con LaTeX instalado (o en Overleaf), compilar `ICN292-Lab5-Vargas-Franco.tex` dos veces con `pdflatex`. Necesita los logos y la carpeta `fig/` junto al `.tex`.
 
