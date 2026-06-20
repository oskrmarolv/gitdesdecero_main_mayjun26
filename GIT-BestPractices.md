# GIT: Best Practices

## REGLA DE ORO UNIVERSAL (LA MÁS IMPORTANTE)
NUNCA reescribas el historial de una rama que ya haya sido compartida (publicada).
Si ya subiste tus commits a un repositorio remoto (GitHub, GitLab, etc.) y alguien más puede estar basando su trabajo en ellos, NO uses `rebase`, `reset` ni `commit --amend` sobre esa rama.
Reescribir el historial cambia los SHAs (identificadores) de los commits, lo que provocará divergencias y trabajo duplicado en el equipo.

## MERGE
- Usa `merge` en ramas compartidas o en la rama principal.
- `merge` preserva el historial real del trabajo y crea un commit de fusión (merge commit) que deja evidencia explícita de cuándo y cómo se integraron dos ramas.
- Es seguro para ramas publicadas porque NO reescribe commits existentes.
- **REGLA DE ORO:** Prefiere `merge` sobre `rebase` cuando trabajes en equipo en una rama compartida.

## REBASE
- Usa `rebase` SOLO en ramas locales que aún no hayas compartido.
- `rebase` recoloca tus commits sobre otra base, reescribiendo el historial para que se vea lineal y más limpio.
- **REGLA DE ORO:** Nunca hagas `rebase` de una rama que ya haya sido publicada.
- **REGLA DE ORO:** Antes de hacer `rebase`, asegúrate de que tu rama esté limpia (sin cambios sin commit).
- Si durante un `rebase` surge un conflicto, resuélvelo y usa `git rebase --continue`. Si te equivocas, usa `git rebase --abort` para cancelar todo.

## RESET
- Usa `reset` solo en historial LOCAL y NO PUBLICADO.
- `reset` mueve el puntero de la rama a un commit anterior, "deshaciendo" commits.
- **REGLA DE ORO:** `git reset --hard` es DESTRUCTIVO: borra cambios del área de staging y del directorio de trabajo. NUNCA lo uses sin estar seguro.
- Modos de `reset`:
  - `--soft`: mueve el puntero, mantiene los cambios en el área de staging.
  - `--mixed`: (por defecto) mueve el puntero y saca los cambios del staging, pero los mantiene en el directorio de trabajo.
  - `--hard`: mueve el puntero, limpia staging y working directory. ¡Peligro!
- **REGLA DE ORO:** Si ya subiste los commits al remoto, NO uses `reset`. Usa `revert` en su lugar.

## REVERT
- Usa `revert` para deshacer cambios en historial compartido.
- `revert` crea un NUEVO commit que deshace los cambios de un commit anterior, sin reescribir la historia.
- **REGLA DE ORO:** Es la forma SEGURA de deshacer algo que ya fue publicado.

## STASH
- Usa `stash` para guardar cambios temporales sin hacer commit.
- `git stash` guarda tus modificaciones locales y vuelve el working directory al estado del último commit.
- **REGLA DE ORO:** El `stash` es LOCAL a tu repositorio. NO se sube al servidor remoto.
- **REGLA DE ORO:** Siempre que hagas `git stash pop`, verifica que todo esté bien antes de continuar trabajando.

## CHERRY-PICK
- Úsalo con precaución y solo para commits específicos.
- `cherry-pick` aplica un commit específico de otra rama a la rama actual.
- **REGLA DE ORO:** El `cherry-pick` está desaconsejado para uso frecuente porque crea commits duplicados y se pierde trazabilidad del historial original.
- **REGLA DE ORO:** Tu working tree debe estar limpio (sin cambios sin commit) antes de hacer `cherry-pick`.

## REFLOG (SALVADOR DE VIDAS)
- El reflog es tu red de seguridad. Úsalo para recuperar lo "perdido".
- `git reflog` registra TODOS los movimientos de HEAD en tu repositorio local.
- **REGLA DE ORO:** Si "perdiste" commits por un `reset --hard` o un `rebase` mal hecho, `git reflog` te muestra los SHAs anteriores para que puedas recuperarlos.
- **REGLA DE ORO:** El reflog es local y temporal. Los registros caducan después de un tiempo (configurable).

## OTROS COMANDOS Y SUS REGLAS

### git pull
- Por defecto, `git pull` hace un `merge`.
- **REGLA DE ORO:** Si prefieres un historial lineal, usa `git pull --rebase`.

### git push --force
- **REGLA DE ORO:** NUNCA uses `git push --force` en una rama compartida. Si necesitas sobrescribir, usa `git push --force-with-lease`, que es más seguro.

### git commit --amend
- **REGLA DE ORO:** Solo úsalo en commits que NO hayas publicado aún. Si ya lo subiste al remoto, NO lo modifiques.

### git checkout / git switch
- **REGLA DE ORO:** Siempre verifica con `git status` que no tengas cambios sin commit antes de cambiar de rama, o usa `git stash` para guardarlos temporalmente.

## RESUMEN RÁPIDO (TABLA DE REFERENCIA)

| COMANDO | ¿CUÁNDO USARLO? | ¿REESCRIBE HISTORIA? |
|---|---|---|
| `merge` | Ramas compartidas, rama principal | NO |
| `rebase` | Solo en ramas locales NO publicadas | SÍ |
| `reset` | Solo en historial local | SÍ |
| `revert` | Historial compartido (deshacer) | NO |
| `stash` | Guardar cambios temporales | NO |
| `cherry-pick` | Commits específicos (con precaución) | NO (crea nuevos) |
| `reflog` | Recuperar commits "perdidos" | N/A |

Git rastrea silenciosamente todo lo que haces en tu repositorio local a través del reflog.
Si alguna vez cometes un error, respira hondo, revisa `git reflog` y recupera tu trabajo.
Antes de cualquier operación peligrosa, asegúrate de tener un respaldo o de estar en una rama local sin publicar.
