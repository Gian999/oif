# oif — paquete `oi` para Octave (Métodos Numéricos)

## Instalar (una línea)

En Octave:

    pkg install "https://github.com/Gian999/oif/raw/main/oif.tar.gz"
    pkg load oi

Desde PowerShell/CMD:

    octave-cli --eval "pkg install 'https://github.com/Gian999/oif/raw/main/oif.tar.gz'"

Si no sigue la redirección: `irm https://github.com/Gian999/oif/raw/main/oif.tar.gz -OutFile oif.tar.gz` y luego `pkg install oif.tar.gz`.

## `h`: lista de métodos, te pide los datos y te los escribe (sin IA)

`h` muestra todos los métodos de la Unidad 2. Eliges uno (`h` o `h('seidel')`, `h('lagrange')`...), ves la chuleta y luego:

- **Enter**: te pide los datos (la matriz `A` y `b` **o las ecuaciones escritas** como `2x-y+z=-1; x+y+3z=0`, `X0`, iteraciones o tolerancia, tablas `x` e `y`; también `excel datos.xlsx B4:D9`). Después escribe el código con tus teclas, igual que `octavei`, y guarda el Excel donde el método lo tiene.
- **g**: el modo guiado de antes (todo de golpe).
- **n**: solo la chuleta.

Con Excel: Jacobi, Gauss-Seidel, punto fijo, Newton de sistemas, regresión (recta, parábola, ambas, múltiple de 2 variables), Lagrange y Newton de interpolación. Solo código: Gauss-Jordan, inversa, LU, Cholesky, normas, reordenar, Cramer / eliminación / sustitución y ajuste con `polyfit`. No usa IA ni clave.

## Motor de IA para `octavei`

- Codex: `codex login` (por defecto si no hay claves).
- Claude (API Console), en Windows CMD: `setx ANTHROPIC_API_KEY "sk-ant-..."` y reiniciar Octave. Para forzarlo: `setenv("OCT_IA_PROVIDER","anthropic")`.

## Clave de Claude (una vez)

La primera vez que uses `octavei` o `haz` aparece una sola línea `  > ` y escribes la contraseña (no se ve nada mientras tecleas; al dar Enter la línea desaparece). Enter solo = omitir y usar Codex. Si te equivocas sale `no` y puedes reintentar (3 veces). Se guarda en tu usuario (`~/.oif`), no en el paquete. Para cambiarla o borrarla: `oifs` (o `octavei setup`); para borrarla: `oifs("borrar")`.

## Si algo se ve raro: repensar

Después de `haz examen.pdf` y `ss2`, si el ejercicio 2 quedó extraño: `repensar 2` (o `repensar 2 solo pedía la parábola`). La IA vuelve a leer el enunciado, revisa qué falló y lo rehace o lo resuelve por otro camino; luego `ss2` reemplaza su hoja. También funciona con `otra 2` y `rehacer 2`. Sin número rehace la última pregunta suelta de `octavei("...")`.

## Analizar de nuevo y resolver de una vez: anss

Después de `haz examen.pdf`, escribe `anss2` seguido de lo que quieres o falta, por ejemplo `anss2 creo que me pide gráfico` o `anss4 solo pedía la parábola y el error`. La IA vuelve a analizar el ejercicio 2 con tu nota y escribe los comandos de una vez (es `repensar 2` + `ss2` en un solo paso; también `anss 2 ...`, hasta `anss12`). Si el ejercicio no cambia no lo ejecuta. `ss2 creo que me pide gráfico` hace lo mismo; `ss 2 e` / `ss 2 o` siguen forzando solo Excel / con Octave. Si tu nota lleva paréntesis o comillas, escríbela como texto: `anss2("me pide (b) gráfico")`.

## Historial de comandos limpio

Los comandos del paquete (`haz`, `ss2`, `anss2`, `octavei`, `exportar`, `repensar`, `h`, `oifs`) **no se guardan** en el historial (flecha arriba, panel Command History, archivo de historial): solo quedan las líneas de código que el programa teclea. Eso también evita que una clave escrita como `oifs("sk-ant-...")` se quede guardada. Para limpiar lo que ya estaba guardado de antes: `oifs limpiar`. Octave no trae "borrar una línea" del historial (solo `history -c`, que lo borra todo); el paquete lo hace vaciando el historial y volviendo a cargar las demás líneas.

## Excel y LibreOffice

Cada ejercicio se guarda como `.xlsx` (principal: abre igual en Excel y en LibreOffice) y, si LibreOffice está instalado, también como `.ods` en la misma carpeta. Para no generar el `.ods`: `setenv("OCT_IA_ODS","0")`.

## El código de Octave sale de los mismos datos que el Excel

Para Jacobi, Gauss-Seidel, punto fijo, Newton de sistemas y los exámenes con esos métodos, la IA solo lee el enunciado y manda los **datos** (sistema `A`, `b`, ecuaciones `F`, funciones `g`, `X0`, iteraciones o tolerancia). El programa, no la IA:

- reordena el sistema para E.D.D. una sola vez y escribe el despeje en papel (`-3x - z = 2  ->  x = (-2 - z)/3`),
- arma `BJ`, `C` con fracciones exactas (`BJ=[0 0 -1/3; 1/4 0 1/2; 0 1/2 0]`), o `BGS` para Gauss-Seidel,
- deriva el jacobiano de `F` y corrige el de la IA si no coincide, avisa si `J(X0)` es singular o si un `g` no sale de las ecuaciones,
- escribe el código en el estilo de tu clase (`X1=BJ*X0+C`, `E1=norm(X1-X0,inf)`, `jacobian`, `subs`...), igual que lo que ves en el Excel.

Antes de teclear cualquier código, `octavei` lo **ejecuta en un espacio aislado** (no toca tu sesión ni tus archivos): si da error, matriz singular o NaN, se lo pide a la IA otra vez con el mensaje real de Octave (hasta 2 intentos). Para apagar la comprobación: `setenv("OCT_IA_VALIDAR","0")`.
