Guía de cómo deshacer el último commit con git

Si no has hecho push:

-   Para mantener cambios: git reset --soft HEAD~1
-   Para eliminar cambios: git reset --hard HEAD~1
-   Para arreglar el commit (mensaje o añadir cambios):
    git commit --amend -m "Mensaje corregido"

Ya has hecho push:

-   git revert <hash> para crear un nuevo commit que invierte los cambios. Si hay conflictos, prepárate para manejarlos.
-   git log para recuperar el hash del commit que quieres revertir.

Nivel experto:

-   git rebase -i para modificar tu historial de commits localmente. Puedes cambiar el orden, combinar, editar o eliminar commits.
-   Luego ejecuta "git push --force-with-lease"
-   ⚠️ Aviso: Sólo usa rebase y push forzado en ramas donde seas el único colaborador o en situaciones donde todos los colaboradores estén al tanto y de acuerdo con reescribir la historia.

Te explico los comandos y parámetros que igual no te suenan o no son tan comunes:

git reset: Este comando se usa para restablecer el índice y el directorio de trabajo al estado de un commit específico.

--soft: Indica que el reset no debe alterar el índice (staging area) ni el directorio de trabajo, pero sí mueve el HEAD al commit especificado. Los cambios que estaban en el commit deshecho se quedan en staging, listos para ser recommitidos si se desea.

--hard: Indica que el reset debe cambiar el índice (staging area) y el directorio de trabajo para reflejar el estado del commit especificado. Cualquier cambio en el directorio de trabajo desde el último commit se perderá.

HEAD~1: Se refiere al commit anterior al último. HEAD es un puntero al último commit de la rama actual, y ~1 mueve ese puntero un commit hacia atrás.

--force-with-lease: Una opción más segura que --force, ya que solo forzará el push si tu copia local está actualizada respecto a los cambios en el remoto. Evita sobreescribir el trabajo de otras personas accidentalmente.

Author: [Midudev](https://twitter.com/midudev/status/1757051558443745693)
