# vaidal-footlab
Football sandbox and match simulator
# Football Lab — formato de datos v1

Utiliza esta especificación cuando solicites a ChatGPT una plantilla, un equipo, una liga o una base de datos compatible con Football Lab v0.1.

## Estructura

Un archivo JSON UTF-8 contiene un objeto con `schemaVersion: 1` y tres listas: `ligas`, `clubes`, `jugadores`. Las listas pueden estar vacías u omitirse. También se admite un objeto jugador individual o una lista de jugadores.

- Liga: `id`, `nombre`, `pais`.
- Club: `id`, `nombre`, `liga` (ID de liga o cadena vacía), `pais`.
- Jugador: `id`, `nombre`, `posicion`, `equipo` (ID de club o cadena vacía), `nacionalidad`, `fechaNacimiento` (YYYY-MM-DD o cadena vacía), `pie` (Derecho, Izquierdo, Ambidiestro o cadena vacía), `posicionesSecundarias` (lista), `atributos` (objeto), `rasgos` (lista de textos).

Los ID, nombres, posición y atributos de los jugadores son obligatorios. Los demás campos se pueden omitir. Los identificadores deben ser únicos dentro de cada tipo y estables entre exportaciones. Incluye los clubes y las ligas necesarios si todavía no existen en la base de destino. No incluyas valoraciones globales o posicionales: las calcula Football Lab.

Posiciones: POR, DFC, LI, LD, MCD, MC, MCO, EI, ED, DC. Un portero no puede tener posiciones secundarias de campo y viceversa.

## Atributos exactos (enteros 0–10)

Campo (20):
- Técnica: `control`, `regate`, `pase`, `vision`.
- Remate: `definicion`, `cabezazo`, `tiroLejano`, `potenciaTiro`.
- Físico: `fuerza`, `resistencia`, `salto`, `equilibrio`.
- Defensa: `marcaje`, `intercepciones`, `entradas`.
- Velocidad: `aceleracion`, `velocidad`, `agilidad`.
- Mental: `tactica`, `compostura`.

Portero (10):
- Paradas: `reflejos`, `estirada`, `blocaje`.
- Dominio del área: `colocacion`, `juegoAereo`, `salidas`.
- Distribución: `juegoBalon`.
- Mental: `concentracion`, `fortalezaMental`, `liderazgo`.

Escala: 0 nulo; 1 extremadamente deficiente; 2 muy deficiente; 3 deficiente; 4 limitado; 5 aceptable; 6 bueno; 7 notable; 8 sobresaliente; 9 élite mundial; 10 excepcional a nivel histórico. Las valoraciones de jugadores reales son estimaciones de diseño, no mediciones oficiales.

## Cálculo vigente

Global campo = suma de atributos / 2. Global portero = suma de atributos. Posicional campo = media ponderada de los grupos, normalizados a 100. Los atributos de cada grupo pesan igual, de momento. Posicional portero = global.

| Posición | TEC | REM | FIS | DEF | VEL | MEN |
|---|---:|---:|---:|---:|---:|---:|
| DFC | 10 | 5 | 25 | 35 | 10 | 15 |
| LI/LD | 20 | 5 | 15 | 25 | 25 | 10 |
| MCD | 25 | 5 | 15 | 25 | 10 | 20 |
| MC | 35 | 10 | 15 | 10 | 10 | 20 |
| MCO | 35 | 20 | 5 | 5 | 15 | 20 |
| EI/ED | 30 | 20 | 5 | 5 | 30 | 10 |
| DC | 15 | 40 | 15 | 0 | 15 | 15 |

## Importación

1. Abre FootballLab.html en un navegador.
2. Ve a Importar / exportar, elige un JSON o pega su contenido.
3. Selecciona añadir (mantener IDs existentes), actualizar (reemplazar registros con mismo ID) o reemplazar toda la base.
4. Revisa el resumen de validación y aplica la importación.

Exporta periódicamente una copia de la base. El guardado local depende del navegador y de la ubicación del archivo HTML. Los datos y el motor de la aplicación son independientes.
