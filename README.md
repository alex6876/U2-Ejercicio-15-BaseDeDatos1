# Base de Datos de Gestión de Torneos de Esports y Videojuegos

Proyecto enfocado en la modelación Entidad-Relación (DER / MER) e implementación de base de datos relacional para una plataforma de gestión de deportes electrónicos (esports), administrando videojuegos, torneos, equipos, jugadores, plantillas o nóminas de participación, enfrentamientos/partidos y estadísticas individuales por jugador.

---

## Descripción

El sistema modela una estructura de datos relacional para la organización y seguimiento integral de competencias e-sports. Permite administrar el catálogo de videojuegos competitivos, la organización de torneos o ligas, el registro de los equipos participantes con sus respectivas inscripciones, las plantillas de jugadores que compiten en cada evento, la programación de los partidos disputados y el registro detallado de las métricas o estadísticas de rendimiento individual de cada jugador.

---

## Funcionalidades e Implementación

### Entidades y Atributos

* **Videojuegos:**
* **id_codigo videojuego**: Clave primaria identificadora del videojuego.
* **nombre**: Nombre del título o juego competitivo.
* **género**: Género al que pertenece (ej. MOBA, FPS, Battle Royale).
* **desarrollor**: Empresa desarrolladora o distribuidora del videojuego.


* **Torneo:**
* **id_Torneo**: Clave primaria única identificadora del torneo o campeonato.
* **nombre**: Nombre comercial del torneo.
* **fecha inicio**: Fecha de comienzo de la competición.
* **fecha fin**: Fecha de conclusión de la competencia.
* **id_codigo videojuego**: Clave foránea referenciando al videojuego sobre el cual se disputa el torneo.


* **Equipo:**
* **id_Equipo**: Clave primaria identificadora de la organización o equipo.
* **tag**: Sigla o abreviatura representativa del equipo.
* **razón social**: Nombre legal o denominación del club/organización.
* **pais origen**: País de procedencia o radicación del equipo.
* **fecha fundación**: Fecha de creación de la entidad deportiva.


* **Jugador:**
* **id_Jugador**: Clave primaria identificadora del jugador.
* **nickname**: Apodo o alias competitivo de usuario.
* **nombre real**: Nombre y apellido real del competidor.
* **nacionalidad**: País de origen del jugador.
* **id_Equipo**: Clave foránea del equipo al que pertenece actualmente.


* **Inscripción_equipo:**
* **id_Torneo**: Clave foránea del torneo en el cual se registra el equipo.
* **id_Equipo**: Clave foránea del equipo inscrito para el certamen.


* **Plantilla:**
* **id_Jugador**: Clave foránea del jugador convocado para el torneo.
* **id_Torneo**: Clave foránea del torneo correspondiente.
* **id_Equipo**: Clave foránea del equipo que lo postula en la nómina.


* **Partido:**
* **id_Partido**: Clave primaria única del enfrentamiento.
* **fecha hora**: Marca temporal en que se lleva a cabo el encuentro.
* **id_Torneo**: Clave foránea referenciando al torneo al que pertenece el juego.
* **id_equipo1**: Clave foránea del primer equipo contendiente.
* **id_equipo2**: Clave foránea del segundo equipo contendiente.
* **mapas_set_equipo1**: Puntuación o mapas ganados por el primer equipo.
* **mapas_set_equipo2**: Puntuación o mapas ganados por el segundo equipo.


* **Estadistica jugador:**
* **id_Partido**: Clave foránea del partido donde se registraron las métricas.
* **id_Jugador**: Clave foránea del jugador evaluado.
* **muertes**: Cantidad de veces que el jugador fue eliminado.
* **bajas**: Cantidad de oponentes eliminados por el jugador (kills).
* **daño total**: Cantidad de daño infligido durante la partida.
* **asistencia**: Cantidad de asistencias aportadas a las bajas de su equipo.



---

## Relaciones del Modelo

1. **Videojuegos ↔ Torneo (Relación 1:N):**
* Un videojuego puede ser la disciplina de múltiples torneos, pero cada torneo se juega sobre un único videojuego en particular.


2. **Torneo ↔ Inscripción_equipo ↔ Equipo (Relación N:M):**
* Un torneo agrupa la inscripción de múltiples equipos y un equipo puede inscribirse en múltiples torneos. Esta relación se gestiona mediante la tabla intermedia `Inscripción_equipo`.


3. **Equipo ↔ Jugador (Relación 1:N):**
* Un equipo posee múltiples jugadores en su plantilla institucional, pero cada jugador está contratado o vinculado a un único equipo.


4. **Jugador / Torneo / Equipo ↔ Plantilla (Relación de Asociación):**
* La entidad `Plantilla` define la nómina oficial de jugadores habilitados que representan a un equipo específico dentro de un torneo concreto.


5. **Torneo ↔ Partido (Relación 1:N):**
* Un torneo engloba la disputa de múltiples partidos o mapas, perteneciendo cada partido a un torneo específico.


6. **Equipo ↔ Partido (Relaciones 1:N):**
* Cada partido involucra a dos equipos contendientes (`id_equipo1` e `id_equipo2`).


7. **Partido ↔ Estadistica jugador ↔ Jugador (Relación N:M):**
* Un partido genera métricas estadísticas para múltiples jugadores y un jugador acumula estadísticas a lo largo de múltiples partidos. Se consolida a través de la entidad `Estadistica jugador`.
