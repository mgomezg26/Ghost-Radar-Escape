# Ghost Escape — Juego para nand2tetris (Jack)

**Integrantes del equipo:**
- Juan Antonio Buendía
- Mateo Gómez
- Santiago Salazar

Juego de escape en el que el jugador no ve el mapa y debe guiarse por un
radar que consume energía para esquivar fantasmas y llegar a la salida.

## Archivos

| Archivo          | Rol                                                      |
|------------------|----------------------------------------------------------|
| `Main.jack`      | Punto de entrada. Crea y ejecuta `GhostGame`.            |
| `GhostGame.jack` | Bucle principal, dibujo, HUD, lógica de victoria/derrota.|
| `Player.jack`    | El jugador (posición en la rejilla, movimiento clamp).   |
| `Ghost.jack`     | Un fantasma con movimiento pseudoaleatorio (LCG simple). |
| `Radar.jack`     | Maneja la energía y el costo de cada escaneo.            |

## Cómo compilar y ejecutar

1. Coloca **los 5 archivos `.jack`** en una misma carpeta, por ejemplo
   `projects/9/GhostEscape/`.
2. Compílala con el `JackCompiler` que viene con nand2tetris:

   ```
   JackCompiler.sh projects/9/GhostEscape
   ```

   (en Windows: `JackCompiler.bat projects/9/GhostEscape`)

   Esto genera un `.vm` por cada `.jack`.
3. Abre el **VM Emulator** (`VMEmulator.sh` / `.bat`).
4. `File → Load Program…` y selecciona la carpeta `GhostEscape`.
5. Pon la velocidad al máximo (slider "Speed" a la derecha) y pulsa
   **Run** (▶). Hace falta hacer clic en el área de pantalla del emulador
   para que reciba el teclado.

## Controles

| Tecla         | Acción                              |
|---------------|-------------------------------------|
| Flechas ← ↑ → ↓ | Mover al jugador una casilla       |
| Espacio       | Activar el radar (gasta 1 energía)  |
| Q             | Salir                               |

Cualquier tecla en la pantalla de intro o de fin la cierra.

## Reglas

- Rejilla de **8×8**. Empiezas en la esquina inferior izquierda. La salida
  está en la esquina superior derecha (marcada con una **X** cuando el
  radar la detecta).
- La pantalla está en blanco: **solo ves tu propia casilla**.
- Pulsa **Espacio** para hacer un barrido del radar. Se iluminan
  brevemente las casillas dentro del rango (3 casillas)
  y aparecen como cuadrados rellenos los fantasmas que estén ahí.
- Cada barrido consume **1 energía**. Empiezas con **10**.
- Los **3 fantasmas** se mueven aleatoriamente cada vez que tú te mueves.
  Si uno ocupa tu casilla, **pierdes**.
- Llega a la salida para **ganar**.

## Notas técnicas

- El campo de juego mide 192×192 px (8 casillas de 24 px) centrado
  verticalmente; el HUD ocupa el lateral derecho.
- El generador de azar de cada fantasma es un LCG diminuto que mezcla
  posición + semilla y se mantiene siempre en rango de 16 bits con signo
  (la máquina Hack no tiene enteros más grandes).
- No se usan librerías externas, solo las estándar de Jack OS
  (`Screen`, `Output`, `Keyboard`, `Sys`, `Memory`).

¡Suerte escapando!
