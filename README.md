# oif — paquete `oi` para Octave (Métodos Numéricos)

## Instalar (una línea)

En Octave:

    pkg install "https://github.com/Gian999/oif/raw/main/oif.tar.gz"
    pkg load oi

Desde PowerShell/CMD:

    octave-cli --eval "pkg install 'https://github.com/Gian999/oif/raw/main/oif.tar.gz'"

Si no sigue la redirección: `irm https://github.com/Gian999/oif/raw/main/oif.tar.gz -OutFile oif.tar.gz` y luego `pkg install oif.tar.gz`.

## Motor de IA para `octavei`

- Codex: `codex login` (por defecto si no hay claves).
- Claude (API Console), en Windows CMD: `setx ANTHROPIC_API_KEY "sk-ant-..."` y reiniciar Octave. Para forzarlo: `setenv("OCT_IA_PROVIDER","anthropic")`.

## Clave de Claude (una vez)

La primera vez que corras `octavei` te pide la clave (Enter = omitir y usar Codex). Se guarda en tu usuario (`~/.oif`), no en el paquete. Para cambiarla o borrarla: `octavei setup` o `oif_setup("borrar")`.
