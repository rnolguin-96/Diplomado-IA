# Guía de Clase 5: ¿Cómo estructurar un equipo para gestionar un proyecto con IA?
**Diplomado de Inteligencia Artificial - CENIA (Octubre 2026)**
**Relator:** Martín Panza (Líder de Tecnología en Cenia, Cloud DevOps Engineer)

Este repositorio contiene el resumen y la guía de estudio correspondiente a la **Clase 5** del diplomado. A través de la historia evolutiva de una startup hipotética que desarrolla un *Clasificador automático de reclamos de clientes* para una empresa de telecomunicaciones (3.000 emails al día), se exploran los roles esenciales, metodologías de trabajo e hitos de infraestructura necesarios para llevar un proyecto de IA a producción.

---

## 📋 Índice General de la Clase
1. **Idea:** El nacimiento del prototipo monolítico.
2. **Equipo:** La llegada de nuevos desarrolladores y la necesidad de procesos.
3. **Cliente:** Infraestructura cloud, contenedores, bases de datos y ciberseguridad.
4. **Datos:** El verdadero cuello de botella (Pipelines y ETL).
5. **Escala** *(Próximamente)*
6. **Crisis** *(Próximamente)*
7. **Madurez** *(Próximamente)*

---

## 👥 Roles Clave Identificados

### 1. PM / PO (Product Manager / Product Owner)
* **¿Qué hace?:** Representa al negocio dentro del equipo técnico. Es el dueño del *"qué"* se construye, en qué orden y por qué. Evita que el equipo técnico construya soluciones interesantes pero irrelevantes para las necesidades del negocio.
* **En el proyecto:** *Ana* actúa como PM, definiendo que el clasificador ordene por urgencia y validando con clientes.

### 2. Machine Learning Engineer (MLE)
* **¿Qué hace?:** Lleva los modelos del notebook al mundo real combinando ingeniería de software y ML. Productiviza modelos, optimiza infraestructura de inferencia, diseña pipelines de entrenamiento reproducibles y monitorea el rendimiento.
* **En el proyecto:** *Rodrigo* es el MLE inicial que entrenó el clasificador, lo disponibilizó en una API y lo mejora iterativamente.

### 3. Desarrollador Full Stack
* **¿Qué hace?:** Trabaja tanto en el Backend (APIs, lógica, BD) como en el Frontend (interfaces). En equipos de IA es clave para conectar el modelo con aplicaciones del mundo real e integraciones externas.
* **En el proyecto:** *Camila y Diego* se suman para construir la interfaz de gestión de reclamos e integrar los sistemas de correo.

### 4. Administrador de Bases de Datos (DBA)
* **¿Qué hace?:** Diseña, implementa y mantiene las bases de datos de forma eficiente, segura y disponible. Optimiza consultas lentas, gestiona esquemas, backups y accesos.
* **En el proyecto:** Administra la convivencia de tres tipos de BD (PostgreSQL, MongoDB y Vectorial) para que las consultas sean rápidas.

### 5. Ingeniero de Ciberseguridad
* **¿Qué hace?:** Asegura la infraestructura bajo estándares de seguridad y regulaciones vigentes (como la Ley 19.628 en Chile o GDPR en Europa). Audita accesos, realiza pruebas de penetración y gestiona secretos.
* **En el proyecto:** Valida el cumplimiento de seguridad antes de firmar el contrato piloto que involucra emails con datos personales reales.

### 6. Ingeniero de Datos (Data Engineer)
* **¿Qué hace?:** Construye y mantiene los flujos automatizados de datos. No entrena modelos, sino que prepara el terreno limpio, normalizado y a tiempo para el ML Engineer.
* **En el proyecto:** Su incorporación destraba el estancamiento del modelo, automatizando la limpieza de fuentes heterogéneas.

---

## 🧠 Conceptos Técnicos y de Gestión Aprendidos

### Capítulos 1 y 2: Prototipado y Colaboración
* **Concepto #1: API (Application Programming Interface):** Pegamento de software que permite a dos sistemas comunicarse sin intervención humana. El sistema de emails envía el correo y la API responde con la urgencia.
* **Concepto #2: Arquitectura Monolítica:** Aplicación donde todo el código (interfaz, modelo, lógica, BD) vive y se despliega junto. Ideal y rápido para validar ideas al inicio; difícil de escalar después.
* **Concepto #3: Git y Control de Versiones:** Estándar de la industria para trabajar simultáneamente en ramas paralelas sin sobreescribir código, manteniendo un historial y usando *Pull Requests*.
* **Concepto #4: Metodologías Ágiles (Scrum):** Organización del trabajo en *sprints* cortos (1-2 semanas) con metas claras, basados en un *Backlog* priorizado por el PM, reuniones *Dailies* (15 min), *Demos* y *Retrospectivas*.
* **Concepto #5: Shape Up:** Alternativa a Scrum desarrollada por Basecamp. Ciclos de 6 semanas de trabajo + 2 de enfriamiento, otorgando mayor autonomía al equipo técnico para definir el "cómo" resolver el problema.
* **Concepto #6: Gestión de Tickets:** Unidades de trabajo (bugs, tareas, features) gestionadas visualmente en tableros de estados (*Todo, En Progreso, Hecho, Bloqueado*) mediante herramientas como Jira o Trello.

### Capítulo 3: El Primer Cliente Piloto e Infraestructura
* **Concepto #7: Cloud vs. On-Premise:** 
  * *Cloud (GCP, AWS, Azure):* Escalabilidad inmediata, sin inversión inicial, costos variables por uso.
  * *On-Premise:* Servidores físicos propios, control total, requiere inversión inicial alta y equipo de IT dedicado.
* **Concepto #8: Containers (Docker):** Empaqueta el código con todas sus dependencias (lenguaje, librerías, configuración). Garantiza que si funciona localmente, funcionará igual en el servidor de la nube.
* **Concepto #9: Bases de Datos SQL (Relacionales):** Datos organizados en tablas con esquemas fijos mediante filas y columnas (ej. PostgreSQL, MySQL). Usado para guardar el historial estructurado de reclamos, estados y tiempos de respuesta.
* **Concepto #10: Bases de Datos NoSQL:** Flexibles y diseñadas para datos no estructurados. Subtipos: Documentos (MongoDB, ideal para emails crudos con distintos encodings), Clave-valor (Redis), Series de tiempo (InfluxDB) o Grafos (Neo4j).
* **Concepto #11: Autenticación vs. Autorización:** 
  * *Autenticación:* Verificar la identidad (¿Eres realmente tú? Ej: Contraseña + MFA).
  * *Autorización:* Verificar permisos (¿Tienes permitido hacer esto? Ej: El ejecutivo ve reclamos pero no modifica el modelo).
* **Concepto #12: Least Privilege (Mínimo Privilegio):** Principio de seguridad donde cada cuenta o proceso tiene acceso estrictamente a lo que necesita para su función, limitando el radio de daño ante incidentes.
* **Concepto #13: Encriptación:** 
  * *En tránsito:* Protege los datos mientras viajan por la red (HTTPS/TLS).
  * *At Rest:* Protege los datos almacenados en discos, bases de datos o backups.
* **Concepto #14: Secret Management:** Almacenamiento centralizado y seguro de credenciales (API keys, tokens, claves de BD) usando herramientas como GCP Secret Manager o HashiCorp Vault, evitando subirlas al código en Git.
* **Concepto #15: Compliance y Datos Personales:** Marcos regulatorios de protección de datos (Ley 19.628 de Chile / GDPR). Exigen la firma de un DPA (Data Processing Agreement), auditorías y políticas de retención.

### Capítulo 4: El Cuello de Botella de los Datos
* **Concepto #16: Pipeline de datos / ETL (Extract, Transform, Load):** Proceso automatizado indispensable bajo la premisa de *"Garbage in, garbage out"*.
  * *Extract:* Extrae datos desde fuentes heterogéneas (correos, CRM).
  * *Transform:* Limpia, normaliza (mismo encoding, formatos de fecha) y valida los datos.
  * *Load:* Carga los datos limpios para el consumo del modelo.

---

## 🏗️ Evolución de la Madurez del Sistema

| Métrica / Estado | Capítulo 1: Idea | Capítulo 2: Equipo Crece | Capítulo 3: Cliente Piloto | Capítulo 4: Datos |
| :--- | :--- | :--- | :--- | :--- |
| **Tamaño del Equipo** | 2 personas | 4 personas | 6 personas | 7 personas |
| **Ubicación del Sistema** | Computador local | Computador local | Google Cloud Platform (GCP) | Google Cloud Platform (GCP) |
| **Arquitectura** | Monolito local | Monolito + Git / Jira | Monolito Dockerizado en VM | Monolito + Pipeline ETL |
| **Precisión del Modelo** | ~80% | ~80% | ~80% | **91% (Gracias a datos limpios)** |
| **Seguridad / Gobierno** | Ninguno | Control de versiones | Encriptación, RBAC, Secret Manager | Pipeline Seguro + Validaciones |
