# Especificación de Requisitos de Software (ERS)
## Proyecto: Plataforma de Apuntes Compartidos Universitarios

### 1. Requerimientos Funcionales (RF)

Los requerimientos funcionales definen las acciones específicas, comportamientos y operaciones que el sistema debe ejecutar.

*   **RF-01 Gestión de Usuarios y Autenticación:** El sistema debe permitir el registro y autenticación de usuarios utilizando exclusivamente el dominio de correo institucional de la Universidad Distrital.
*   **RF-02 Roles y Permisos:** El sistema debe manejar tres roles de usuario: 
    *   *Estudiante (Lector/Contribuidor):* Puede buscar, descargar, subir apuntes y calificar.
    *   *Moderador:* Puede ocultar publicaciones reportadas y gestionar etiquetas.
    *   *Administrador:* Acceso total al panel de control y gestión de usuarios.
*   **RF-03 Publicación de Material:** El sistema debe permitir a los usuarios subir material académico proporcionando: Título, Descripción, Facultad, Proyecto Curricular (ej. Ingeniería de Sistemas), Semestre, Materia y el recurso (URL externa o archivo PDF).
*   **RF-04 Motor de Búsqueda y Filtrado:** El sistema debe incluir una barra de búsqueda por palabras clave en el título y descripción, y permitir aplicar filtros combinados por: Semestre, Materia y Tipo de Documento (Taller, Parcial, Código, Resumen).
*   **RF-05 Sistema de Valoración (Rating):** El sistema debe permitir a los usuarios autenticados calificar un apunte de 1 a 5 estrellas. Un usuario no puede calificar su propio material.
*   **RF-06 Gestión de Favoritos:** El sistema debe permitir a los usuarios guardar apuntes en una colección personal de "Guardados para después".
*   **RF-07 Moderación y Reportes:** El sistema debe permitir a los usuarios reportar un documento (por plagio, error técnico, o spam). Al acumular 3 reportes, el sistema debe cambiar automáticamente el estado del apunte a "En Revisión" y ocultarlo del feed público.
*   **RF-08 Sistema de Reputación (Gamificación básica):** El sistema debe calcular y mostrar un nivel de reputación en el perfil del usuario, sumando puntos por cada valoración positiva recibida en sus aportes.

### 2. Requerimientos No Funcionales (RNF)

Los requerimientos no funcionales definen los atributos de calidad, rendimiento, seguridad y arquitectura del sistema.

*   **RNF-01 Arquitectura:** El sistema debe estar construido bajo un patrón de Arquitectura por Capas (N-Tier) garantizando la separación estricta entre la capa de presentación, la lógica de negocio y el acceso a datos.
*   **RNF-02 Rendimiento (Tiempo de Respuesta):** Las consultas realizadas a través del motor de búsqueda y filtros no deben exceder los 2.5 segundos de tiempo de respuesta bajo condiciones de carga normal.
*   **RNF-03 Seguridad de Datos:** Las contraseñas de los usuarios deben almacenarse utilizando algoritmos de encriptación y hashing seguro (ej. bcrypt o Argon2). Nunca en texto plano.
*   **RNF-04 Escalabilidad de Almacenamiento:** Los archivos físicos (PDFs) no deben almacenarse como BLOBs en la base de datos relacional. Deben alojarse en un sistema de archivos local del servidor o almacenamiento en la nube, guardando solo la ruta lógica (URL) en la base de datos SQL.
*   **RNF-05 Usabilidad (Diseño Responsivo):** La interfaz de usuario debe ser completamente responsiva, garantizando una correcta visualización y operatividad en dispositivos móviles, tablets y monitores de escritorio (Mobile First).
*   **RNF-06 Disponibilidad:** El sistema debe garantizar una disponibilidad del 99% durante los periodos de mayor tráfico académico (semanas de parciales).
*   **RNF-07 Prevención de Inyecciones:** Todas las consultas a la base de datos SQL deben realizarse a través de consultas preparadas (Prepared Statements) o un ORM para prevenir ataques de inyección SQL.