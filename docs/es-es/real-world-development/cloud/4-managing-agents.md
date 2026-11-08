---
title: "Ejercicio 4 - Supervisar y administrar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los dos ejercicios anteriores asignaste al agente de Copilot en la nube tres tareas distintas para mejorar la experiencia de usuario y añadir funcionalidad. Aunque el agente trabaja de forma autónoma y asíncrona, sigue siendo importante poder supervisar esas tareas.

Puedes administrar las tareas desde la [página de agentes][agents-page] de GitHub.com. Este panel muestra las tareas del agente que tienen solicitudes de incorporación de cambios abiertas. Puedes examinar las operaciones realizadas y orientar las sesiones que siguen en curso.

En este ejercicio:

- explorarás la página de agentes para supervisar el trabajo del agente en la nube;
- orientarás una sesión en curso para pedir funcionalidad adicional.

## Escenario

Después de asignar el modo de alto contraste, el equipo decide añadir también un modo claro. Como ya se están actualizando los estilos y se está implementando el selector de modo, quieres orientar al agente para que incluya ambos modos.

## Revisa las tareas del agente en la nube

Comprueba el estado de las tareas asignadas al agente de Copilot en la nube.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Examina las tareas del panel principal y del panel izquierdo. Deberías ver las tareas que asignaste, entre ellas:
   - actualizar la documentación del código;
   - generar API para modificar juegos;
   - añadir un modo de alto contraste al sitio.
3. Selecciona una tarea en curso y revisa las operaciones realizadas por Copilot, que pueden incluir:
   - obtener el código del repositorio;
   - crear el entorno de trabajo;
   - configurar servidores MCP;
   - ejecutar los pasos necesarios para completar la tarea.

> [!NOTE]
> Los pasos concretos varían según el estado del trabajo de Copilot y el enfoque que haya seguido.

4. Observa también el panel de solicitudes de incorporación de cambios de la derecha, donde puedes revisar la PR y los archivos modificados.

## Guía al agente en la nube

Ya has visto las tareas activas. Ahora pide a Copilot que añada el modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título exacto depende de cómo Copilot haya nombrado la tarea y de su estado actual.

    ![Sesión de accesibilidad en el panel de agentes](../../../_images/ex6-accessibility-session.png)

2. Espera unos minutos hasta que termine la configuración y empiece el trabajo. Verás mensajes que indican que el agente ya ha empezado a implementar la tarea.
3. En el cuadro **Steer active session while Copilot is working**, escribe este prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Tarea del agente en la página de agentes con el cuadro para guiar la sesión resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Observa cómo Copilot lo reconoce y lo añade al flujo de trabajo.

## Deja que Copilot trabaje

Copilot incorporará la nueva solicitud cuando termine el paso en curso. El proceso tardará varios minutos; puedes aprovechar ese tiempo para repasar lo que has aprendido.

## Resumen y siguientes pasos

Has explorado la página de agentes de Copilot, el panel central para supervisar y orientar las tareas del agente en la nube. Puedes seguir las tareas activas y completadas, revisar el trabajo y redirigir una sesión en curso para ajustar su alcance.

En este ejercicio:

- has explorado el panel de agentes y supervisado las tareas del agente en la nube;
- has redirigido una sesión en curso para pedir funcionalidad adicional.

Mientras Copilot termina las funciones de accesibilidad, puedes [iterar sobre las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
