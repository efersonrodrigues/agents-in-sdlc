---
title: "Lección 1 - Instalar la aplicación GitHub Copilot"
description: "Instala la aplicación GitHub Copilot, conecta el repositorio creado a partir de la plantilla, conoce el espacio de trabajo y prueba un chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La **[aplicación GitHub Copilot][about-copilot-app]** es una aplicación de escritorio para el desarrollo dirigido por agentes. Se basa en GitHub Copilot CLI y se integra de forma nativa con GitHub, por lo que los repositorios, las ramas y las canalizaciones de CI funcionan sin configuración adicional. Está diseñada para flujos de trabajo en los que diriges varios agentes en paralelo, cada uno en su propio espacio de trabajo aislado, y automatizas tareas repetitivas. Como ya tienes Node.js y una copia del proyecto, ahora instalarás la aplicación y conectarás el repositorio.

En esta lección:

- instalarás la aplicación GitHub Copilot e iniciarás sesión;
- añadirás el proyecto a la aplicación desde su repositorio de GitHub;
- te familiarizarás con el espacio de trabajo, incluido el backlog inicial de la plantilla;
- probarás un chat rápido para conocer la propia aplicación.

## Escenario

Tu equipo está adoptando agentes de IA para abordar un backlog cada vez mayor. La aplicación Copilot ofrece un único lugar desde el que dirigir ese trabajo: seleccionar incidencias, ejecutar agentes, revisar cambios y combinar solicitudes de incorporación de cambios. En esta lección instalarás y conectarás la aplicación y aprenderás a iniciar una conversación sobre el proyecto.

> [!NOTE]
> Necesitas un plan de Copilot apto: Copilot Free, Copilot Student o cualquier plan de pago (Pro, Pro+, Business o Enterprise). Si utilizas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva **GitHub Copilot app**.

## Instala y configura la aplicación GitHub Copilot

La aplicación tiene versiones para Windows, macOS y Linux. Instálala, autentícate y añade el repositorio de Tailspin Toys.

1. En un navegador, abre la [página de inicio de la aplicación GitHub Copilot][download-app].
2. Descarga la aplicación para tu plataforma e instálala siguiendo las instrucciones de la página.
3. Abre la aplicación después de instalarla.
4. Selecciona **Sign in to GitHub** y sigue las instrucciones para autenticarte. Si usas GitHub Enterprise Cloud con residencia de datos, selecciona **Use GitHub Enterprise** e introduce el nombre de host `*.ghe.com` cuando se te solicite. GitHub Enterprise Server no es compatible.
5. Si la configuración inicial permite elegir un repositorio, selecciona el repositorio Tailspin Toys que creaste a partir de la plantilla. También puedes omitir ese paso y añadirlo después.
6. Cuando se te solicite, elige un tema y completa la configuración inicial.
7. Busca el repositorio en **Sessions**, en la barra lateral. Si ya aparece, no hace falta que lo añadas de nuevo.
8. Si todavía no está conectado, selecciona **+** junto a **Sessions** para crear una sesión y, después, **Add GitHub repository**. Usa el propietario y el nombre del repositorio que anotaste en la lección de requisitos previos.
9. Comprueba que el repositorio aparece en la barra lateral. En esta organización, carpetas como `tailspin-toys` se agrupan bajo **Sessions**, con sus sesiones individuales debajo.

## Familiarízate con el espacio de trabajo

Con el proyecto conectado, explora las áreas de la barra lateral:

- **New**: inicia una nueva sesión de chat con Copilot.
- **Pull requests**: accede a tus solicitudes de incorporación de cambios mediante la integración nativa con GitHub. Puedes explorarlas, filtrarlas, comprobar el estado de CI y revisarlas sin salir de la aplicación.
- **Issues**: accede a tus incidencias. Puedes explorarlas, filtrarlas e iniciar una sesión a partir de una incidencia.
- **Automations**: consulta las tareas de agente guardadas que se ejecutan según una programación o bajo demanda. Son útiles para listas de tareas, mantenimiento periódico y tareas repetitivas. El repaso las enlaza como siguiente paso, no como ejercicio del taller.
- **Customize**: añade funciones a la aplicación mediante servidores MCP, plugins, habilidades y otros componentes. Lo usarás para configurar Playwright MCP.
- **Chats**: mantén conversaciones breves para preguntas y lluvias de ideas que no necesitan rama ni espacio de trabajo. Esta sección aparece después del primer chat. Si no está visible, selecciona **+** junto a **Sessions** para iniciar un chat.
- **Sessions**: agrupa las carpetas de repositorio y las sesiones de agente. Selecciona un repositorio, como `tailspin-toys`, para abrir su vista o una sesión para volver a la conversación. Cada sesión se ejecuta en un espacio de trabajo aislado, por lo que puedes ejecutar varias sin que sus cambios entren en conflicto. Iniciarás la primera sesión al añadir las clasificaciones por estrellas.

Explorarás el espacio de trabajo durante el taller.

> [!TIP]
> Si tienes dudas, pregunta a Copilot. Si no sabes cómo hacer algo o si es posible, puede ayudarte.

### Busca el backlog inicial

Tailspin Toys tiene un backlog de incidencias que se creó al generar el repositorio a partir de la plantilla.

1. En la barra lateral, selecciona la carpeta del repositorio Tailspin Toys bajo **Sessions**, no una sesión individual. Después, selecciona **Issues** en la navegación superior del repositorio.
2. Busca estas incidencias por su título, no por el número:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecciona una incidencia para leer los detalles. Cada una sirve también para iniciar una sesión de agente. Después de un primer cambio rápido, empezarás por la incidencia de filtrado.

> [!NOTE]
> Las listas de **Issues** y **Pull requests** se filtran automáticamente para mostrar los elementos de los repositorios que has añadido a la aplicación Copilot. Para ver elementos de otros repositorios, añádelos a la aplicación.

## Prueba un chat rápido

Un **chat rápido** te permite preguntar o intercambiar ideas sin crear una rama ni un árbol de trabajo. Es ideal para preguntas breves que no necesitan una sesión.

1. En la barra lateral, selecciona **+** junto a **Chats** para abrir un chat. Si **Chats** todavía no aparece, selecciona **+** junto a **Sessions** para iniciar el primer chat; después aparecerá la sección **Chats**.
2. Pregunta cómo funcionan las sesiones de la aplicación:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. Lee la respuesta en la vista de conversación. Cada sesión se ejecuta en su propio árbol de trabajo aislado de Git; así puedes ejecutar varios agentes en paralelo sin que sus cambios entren en conflicto. Puedes continuar la conversación o iniciar otra cuando quieras.

## Resumen y siguientes pasos

Has instalado la aplicación GitHub Copilot, conectado el proyecto y explorado el espacio de trabajo. Has aprendido a:

- instalar la aplicación e iniciar sesión en GitHub;
- añadir un proyecto desde su repositorio de GitHub;
- conocer el espacio de trabajo y encontrar el backlog inicial en **Issues**;
- usar un chat rápido para hacer una pregunta breve.

A continuación, [iniciarás tu primera sesión de agente][next-lesson] y mostrarás las clasificaciones por estrellas en las tarjetas de juegos.

## Recursos

- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Introducción a la aplicación GitHub Copilot][getting-started]
- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
