# Comando Publicar

Este comando confirma todos los cambios, los envía al repositorio remoto, crea un Pull Request y lo fusiona con main para publicar el contenido.

## Instrucciones

**IMPORTANTE: Antes de ejecutar CUALQUIERA de los pasos siguientes, DEBES pedir confirmación al usuario.**

Muestra este mensaje al usuario:

---
**CONFIRMACIÓN DE PUBLICACIÓN REQUERIDA**

Estás a punto de publicar tus cambios. Esto hará:
1. Confirmar (commit) todos los cambios actuales
2. Enviar (push) a la rama remota
3. Crear un Pull Request hacia main
4. Fusionar el PR para publicar el contenido

**¿Estás seguro de que deseas continuar?** (sí/no)

---

**Espera la confirmación explícita del usuario antes de proceder.**

## Pasos de Ejecución (Solo después de confirmación)

Si el usuario confirma con "sí", "si", "yes", "y", u otra respuesta afirmativa similar:

1. **Verificar cambios**: Ejecutar `git status` para ver qué cambios existen
2. **Preparar todos los cambios**: Ejecutar `git add -A`
3. **Confirmar cambios**: Crear un commit con mensaje "Publicar: Actualización de contenido [timestamp]"
4. **Enviar al remoto**: Hacer push de la rama actual a origin con `git push -u origin [nombre-rama]`
5. **Crear Pull Request**: Usar `gh pr create --title "Publicar actualización de contenido" --body "Publicación automatizada de actualizaciones de contenido"`
6. **Fusionar PR**: Usar `gh pr merge --merge --auto` para fusionar el PR a main

## Manejo de Errores

- Si no hay cambios para confirmar, informar al usuario y detener
- Si el push falla, reintentar hasta 4 veces con retroceso exponencial
- Si la creación del PR falla, verificar si ya existe un PR y usar ese
- Si la fusión falla, informar al usuario y proporcionar la URL del PR para revisión manual

## Mensaje de Éxito

Después de una ejecución exitosa, mostrar:

---
**PUBLICADO EXITOSAMENTE**

Tus cambios han sido publicados en main.
- Commit: [hash del commit]
- PR: [URL del PR]
- Estado: Fusionado

---
