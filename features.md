# Principales funcionalidades de un ITSM

Un sistema de **Gestión de Servicios de TI (ITSM)** es una plataforma integral diseñada para gestionar, entregar y mejorar los servicios tecnológicos de una organización, alineándolos con las necesidades del negocio. 
A continuación, se detallan las funcionalidades principales que conformarán el proyecto.

---

## Gestión de incidencias

La gestión de incidencias es el núcleo operativo de cualquier plataforma ITSM, enfocándose en restaurar el servicio normal lo más rápido posible tras una interrupción no planificada.  
Incluye registro, categorización, priorización, asignación y resolución de incidentes.

Las plataformas modernas incorporan **colas inteligentes** que integran solicitudes desde múltiples canales (correo electrónico, chat, portal de autoservicio) y utilizan **aprendizaje automático** para agrupar tickets similares, facilitando la categorización automática.

Los sistemas avanzados también incluyen **escalación automática** basada en prioridad empresarial y SLAs, permitiendo asignar recursos donde más se necesitan para garantizar resoluciones rápidas y efectivas.

Para esta primera versión de la plataforma, nos vamos a concentrar en el canal "portal de autoservicio", los demás canales no se implementarán.

---

## Gestión de problemas

Mientras que la gestión de incidentes aborda los síntomas, la **gestión de problemas** identifica y elimina las causas raíz que originan múltiples incidentes recurrentes.  
Su objetivo es minimizar el impacto de las interrupciones desarrollando soluciones permanentes o temporales.

Incluye análisis de causa raíz, documentación de soluciones conocidas y medidas proactivas para prevenir futuros problemas.

---

## Gestión de cambios

La **gestión de cambios** supervisa y controla la transición o modificación de procedimientos y tecnologías organizacionales, asegurando la implementación controlada de cambios con riesgo mínimo.

Incluye procesos de **aprobación**, **evaluación de impacto**, **planificación de rollback** y **documentación completa** de todos los cambios realizados.

---

## Gestión de activos de TI (ITAM) y CMDB

La **Base de Datos de Gestión de Configuración (CMDB)** actúa como un repositorio centralizado de todos los componentes del sistema de TI (hardware, software, redes, instalaciones, personal, etc.).  
No solo cataloga activos, sino que **mapea sus relaciones e interdependencias**.

Permite realizar análisis de impacto, gestión eficiente del cambio y cumplimiento normativo, ayudando a comprender cómo los CIs se conectan a los resultados empresariales.

---

## Gestión de solicitudes de servicio y catálogo de servicios

El **catálogo de servicios** es un repositorio centralizado que contiene todos los servicios de TI disponibles para los usuarios, con descripciones, plazos, aprobaciones y relaciones entre servicios.

Los usuarios interactúan con el catálogo mediante un **portal intuitivo**, activando flujos de trabajo automatizados para solicitudes como restablecimiento de contraseñas, adquisición de equipos o instalación de software.

---

## Portal de autoservicio

Los **portales de autoservicio** empoderan a los usuarios para resolver problemas comunes de forma independiente, reduciendo la carga del equipo de TI.

Ofrecen acceso 24/7 a recursos de TI, **bases de conocimiento**, **FAQs**, seguimiento de tickets y chat con soporte.  
Sus capacidades clave incluyen formularios dinámicos, sugerencias automáticas de artículos y seguimiento en tiempo real.

---

## Gestión del conocimiento

La **gestión del conocimiento** captura, organiza y comparte información de forma sistemática dentro de la organización.

Una **base de conocimiento centralizada** ofrece acceso rápido a FAQs, guías, procedimientos y mejores prácticas.  
Soporta los demás procesos ITSM sacando el conocimiento de silos organizacionales y poniéndolo a disposición de todos los agentes.

---

## Gestión de niveles de servicio (SLA)

Los **Acuerdos de Nivel de Servicio (SLAs)** son contratos documentados que definen el nivel de servicio esperado.

Incluyen métricas medibles, responsabilidades y objetivos de nivel de servicio (SLOs).  
Permiten monitoreo continuo, informes de rendimiento y acciones de mejora basadas en los resultados.

Los SLAs modernos gestionan **tiempos de respuesta**, **resolución**, **disponibilidad** y **procedimientos de escalación**.

---

## Reporting, dashboards y analíticas

Los **dashboards ITSM** ofrecen visibilidad en tiempo real del estado de los servicios de TI, mostrando métricas como volumen de tickets, cumplimiento de SLAs, MTTR, y tendencias.

Los **reportes ITSM** complementan los dashboards con análisis detallados, métricas de negocio y seguimiento ejecutivo.

Las **analíticas avanzadas** permiten identificar cuellos de botella, predecir tendencias y demostrar el valor del departamento de TI.

---

## Automatización y workflows

La **automatización ITSM** reduce tareas repetitivas (enrutamiento de tickets, categorización, restablecimientos de contraseña, etc.).  
Los **workflows condicionales** permiten crear sistemas inteligentes que reaccionan según ciertas condiciones, como escalar incidentes o activar solicitudes de cambio.

Las plataformas avanzadas incorporan **constructores visuales sin código** e integraciones con sistemas HRIS, IAM, MDM y herramientas empresariales como **Slack** o **Microsoft Teams**.

---

## Inteligencia artificial y chatbots

Los **agentes virtuales basados en IA** automatizan interacciones de soporte desde plataformas de chat, ofreciendo asistencia inmediata y escalable.

Emplean **procesamiento de lenguaje natural (NLP)** y **aprendizaje automático** para entender solicitudes, ejecutar workflows y enrutar tickets inteligentemente.  
En casos complejos, transfieren al usuario a un agente humano.

