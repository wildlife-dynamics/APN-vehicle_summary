# Vehicle Summary

Fleet-wide vehicle activity report for Argentina's national parks (Administración de Parques Nacionales — APN). It pulls every "Libro Diario Vehicular" (Vehicle Daily Log) event from EarthRanger over a time range, extracts the per-journey details recorded in the field (plate, odometer readings, fuel loaded, fuel type, occupants, purpose, origin/destination), and rolls them up into fleet-level statistics, a per-journey table, and usage trend charts.

## Dashboard widgets

| Widget | Description |
|--------|-------------|
| Nro. de Vehículos utilizados | Count of distinct vehicles (by licence plate) with at least one logged journey |
| Total de desplazamientos | Total number of logged journeys |
| Total de km recorridos | Sum of distance travelled across all journeys (arrival odometer − departure odometer) |
| Total de combustible utilizado | Total fuel loaded across all journeys, in litres |
| Total de diesel utilizado | Total fuel loaded on journeys where fuel type is "Diesel comun", in litres |
| Total de nafta utilizada | Total fuel loaded on all non-diesel journeys, in litres |
| Promedio de ocupantes por viaje | Average number of occupants per journey |
| Resumen de Viajes por Vehículo | Per-journey table: plate, start/end date, fuel loaded, fuel type, purpose, origin, destination, distance. Sortable, filterable, downloadable |
| Distancia recorrida por mes (km) | Grouped bar chart of monthly distance travelled, one colour per vehicle |
| Nro. de Viajes por Vehículo | Bar chart of total trip count per vehicle |

This workflow has no groupers — all widgets show fleet-wide totals for the configured time range in a single dashboard view.

## Data extraction

Each `libro_diario_vehicular_v2` event stores its details as free-form fields (in Spanish) inside `event_details`. The workflow extracts each field into its own column: `Patente` (plate), `KM_de_salida`/`Km_de_llegada` (departure/arrival odometer), `Litros_cargados` (fuel loaded), `Tipo_de_combustible` (fuel type), `Pasajeros` (occupant list, reduced to a count), `Motivo_del_desplazamiento` (trip purpose), `Origen_del_desplazamiento`/`Destino` (origin/destination), and `Regreso` (return time). Distance per journey is computed as arrival odometer minus departure odometer.

## Requirements

[pixi](https://pixi.sh) is required for environment and dependency management. You will also need an EarthRanger connection configured for the `apn` data source.
