---
title: "Ejercicio 2 - Agente de GitHub Copilot en la nube"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Es probable que muchas organizaciones tengan problemas con la deuda técnica: incidencias de seguridad pendientes, código heredado que hay que actualizar o solicitudes de funcionalidad relegadas en el backlog por falta de tiempo. El agente de GitHub Copilot en la nube puede actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, genera una solicitud de incorporación de cambios (PR) en borrador para que la revise un desarrollador. Así puedes delegar tareas tediosas, acelerar el desarrollo y centrarte en trabajos de mayor alcance.

Explorarás cómo usar el agente en la nube para:

- personalizar el entorno de generación de código;
- garantizar que las operaciones se realicen de forma segura;
- comprender la importancia de delimitar bien las incidencias;
- asignar incidencias a Copilot.

## Escenarios

Tailspin Toys tiene deuda técnica. Los contratistas que crearon la primera versión del sitio no añadieron documentación. Como primer paso, el equipo quiere que se añadan comentarios TSDoc a todas las funciones exportadas.

Además, el equipo de diseño quiere mejorar el descubrimiento de juegos. Quiere mostrar en la página de detalles de cada juego otros títulos de la misma categoría para que los usuarios puedan seguir explorando. No necesita una implementación pulida todavía; quiere probar y aceptar la experiencia de usuario. Aunque esta solicitud está actualmente bloqueada, hay incidencias de mayor prioridad.

Son tareas que suelen posponerse y que pueden asignarse al agente en la nube. El agente trabaja de forma asíncrona mientras tú te ocupas de otras tareas y, cuando termina, puedes revisar el resultado.

## Introducción al agente de GitHub Copilot en la nube

El [agente de GitHub Copilot en la nube](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano de forma similar a un desarrollador. Por ejemplo, puedes [asignar una incidencia de GitHub a Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Una vez asignada, Copilot crea una PR en borrador para registrar el progreso, configura un entorno y empieza a trabajar. Puedes inspeccionar la sesión durante el proceso o después. Cuando la solución esté lista para revisarla, Copilot te mencionará en la PR.

## La importancia de unas instrucciones bien delimitadas

GitHub Copilot no es magia: no elimina la necesidad de pensar. Incluso las tareas aparentemente sencillas pueden ser complejas, así que [delimita bien el trabajo que asignas al agente en la nube][cloud-agent-best-practices]. Trátalo como a un programador colaborador con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian al añadir IA generativa.

## Instrucciones personalizadas de este repositorio

Los ejercicios anteriores presentaron las instrucciones personalizadas. Si ya completaste esa práctica, habrás visto cómo funciona `.github/copilot-instructions.md`; si no, revísalo ahora. Antes de asignar trabajo al agente, lee los archivos de instrucciones que incluye el repositorio para reconocer su influencia más adelante.

Abre estos archivos en la interfaz web de GitHub o en un Codespace:

- `.github/copilot-instructions.md`: revisa **Code standards**, especialmente las convenciones de TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: fíjate en el frontmatter `applyTo`, que aplica las instrucciones a `**/*.test.ts`.

Cuando asignes al agente la incidencia `Code lacks documentation`, observa en la PR los comentarios TSDoc, las convenciones de TypeScript y los encabezados de comentario. Estas directrices proceden de los archivos de instrucciones. Volveremos a revisarlas en un ejercicio posterior.

## Configura el entorno de desarrollo del agente

La creación de código suele requerir herramientas y dependencias concretas. Esto también se aplica al agente, que trabaja de forma similar a un ingeniero de software.

El agente utiliza [GitHub Actions][github-actions] para configurar su entorno. Puedes personalizarlo con un flujo de trabajo de preparación, definido en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que empiece el trabajo. Este flujo, preparado para el taller, instala Node.js, las dependencias, los navegadores de Playwright y la base de datos SQLite migrada y con datos iniciales:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio.
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Define los permisos mínimos necesarios para *estos pasos*. Copilot recibirá su propio token para sus operaciones.
    permissions:
      # Si quieres clonar el repositorio como parte de los pasos de configuración, por ejemplo, para instalar dependencias, necesitarás el permiso `contents: read`. Si no clonas el repositorio en estos pasos, Copilot lo hará automáticamente cuando terminen.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración de frontend y aplicación: Node.js (toda la aplicación usa Astro y Drizzle/libSQL).
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y carga datos iniciales en SQLite local para que la compilación y las pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

El archivo se parece a cualquier flujo de trabajo de GitHub, pero hay dos detalles importantes:

- Incluye un solo trabajo, `copilot-setup-steps`, que se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la PR.
- El desencadenador `workflow_dispatch` permite ejecutar manualmente el flujo desde la pestaña **Actions** del repositorio. Así puedes comprobar que funciona sin esperar a que Copilot lo inicie.

## Añade documentación

Muchos proyectos tienen información obsoleta o carecen de documentación. Esta deuda técnica ralentiza el trabajo y dificulta mantener el código o incorporar a nuevos desarrolladores. Copilot puede ayudar a crear documentación; asígnale esta incidencia y, en un ejercicio posterior, revisarás el resultado.

1. Abre tu repositorio en github.com en una pestaña nueva.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de incidencias.
4. Selecciona **Blank issue**.
5. Escribe `Code lacks documentation` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecciona **Create**.
8. En el lado derecho, selecciona **Assign to Copilot**.

  ![Asignar una incidencia a Copilot](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.
10. Selecciona la pestaña **Pull Requests**.
11. Abre la PR que Copilot acaba de crear, cuyo título será similar a `[WIP]: Code lacks documentation`. Si todavía no aparece, espera un momento y actualiza la página.
12. Al cabo de unos minutos, Copilot debería crear una lista de tareas.

> [!NOTE]
> La lista puede tardar varios minutos en aparecer. Copilot está configurando el entorno mediante el flujo de trabajo descrito antes, analizando el proyecto y planificando la tarea.

13. Revisa la lista y las tareas previstas.
14. Desplázate por la cronología de la PR hasta ver que Copilot ha empezado a trabajar.
15. Selecciona **View session**.

  ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la página para ver el indicador actualizado.

16. Observa la sesión en directo y cómo Copilot explora el código, analiza la situación, decide un plan y crea código.

El proceso puede tardar varios minutos. Una ventaja del agente en la nube es que trabaja de forma asíncrona, por lo que puedes asignarle otra tarea mientras te ocupas de otras tareas de la aplicación.

## Añade una sección de juegos relacionados

Una ventaja del agente en la nube es que puede trabajar en paralelo mientras tú te ocupas de otras tareas. Asigna también la solicitud del equipo de diseño para mostrar juegos relacionados:

1. Vuelve al repositorio en github.com.
2. Selecciona la pestaña **Issues** y, después, **New issue**.
3. Selecciona **Blank issue**.
4. Escribe `Show related games on the game details page` en **Title**.
5. Escribe lo siguiente en **Description**:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

6. Selecciona **Create**.
7. A la derecha, selecciona **Assign to Copilot** y, después, **Assign**.

Poco después, aparecerá un emoji 👀 en el primer comentario de la incidencia para indicar que Copilot está trabajando en ella. El agente funciona de forma similar a un ingeniero de software: no hace falta supervisar cada paso; puedes revisar el resultado cuando termine. Ahora explorarás los agentes personalizados.

## Resumen y siguientes pasos

Has explorado el [agente de GitHub Copilot en la nube][copilot-agents], al que puedes asignar incidencias para que trabaje de forma asíncrona en deuda técnica, funcionalidades o migraciones. En esta lección:

- has personalizado el entorno de generación de código;
- has aprendido a realizar operaciones de forma segura;
- has explorado la importancia de delimitar bien las incidencias;
- has asignado incidencias a Copilot.

Mientras Copilot trabaja en segundo plano, puedes explorar los agentes personalizados. El agente en la nube también puede usar [servidores MCP][cloud-agent-mcp] y las instrucciones personalizadas que has revisado en los ejercicios anteriores.

## Recursos

- [Acerca del agente de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de preparación del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
