```mermaid
erDiagram
  PELICULA {
    int id_pelicula PK
    string titulo_distribucion
    string titulo_original
    string genero
    string idioma_original
    boolean subtitulos_espanol
    int anio_produccion
    string url_sitio_web
    int duracion_horas
    int duracion_minutos
    string calificacion_edad  "ATP|+9|+15|+18"
    date fecha_estreno
    string resumen
  }

  PAIS {
    int id_pais PK
    string nombre
  }

  PERSONA {
    int id_persona PK
    string nombre  "UNIQUE"
    string nacionalidad
  }

  PERSONA_PELICULA_ROL {
    int id_pelicula FK
    int id_persona FK
    string rol  "DIRECTOR|ACTOR"
    %% PK compuesta sugerida: (id_pelicula, id_persona, rol)
  }

  PERSONA_PERSONAJE {
    int id_pelicula FK
    int id_persona FK
    string personaje
    %% PK compuesta sugerida: (id_pelicula, id_persona, personaje)
  }

  CINE {
    int id_cine PK
    string nombre  "UNIQUE"
    string direccion
    string telefono
  }

  SALA {
    int id_sala PK
    int id_cine FK
    int numero_en_cine
    string nombre
    int cantidad_butacas
  }

  FUNCION {
    int id_funcion PK
    int id_sala FK
    int id_pelicula FK
    string dia_semana
    time hora_comienzo
    date semana_inicio  "opcional (para cartelera semanal)"
  }

  PROMOCION {
    int id_promocion PK
    string descripcion
    decimal descuento
  }

  FUNCION_PROMOCION {
    int id_funcion FK
    int id_promocion FK
    %% PK compuesta sugerida: (id_funcion, id_promocion)
  }

  OPINION {
    int id_opinion PK
    int id_funcion FK
    string nombre_persona
    int edad
    date fecha_opinion
    string calificacion  "ObraMaestra|MuyBuena|Buena|Regular|Mala"
    string comentario
  }

  PELICULA }o--o{ PAIS : "origen"
  PELICULA ||--o{ FUNCION : "se_exhibe_en"
  CINE ||--o{ SALA : "tiene"
  SALA ||--o{ FUNCION : "programa"

  FUNCION }o--o{ PROMOCION : "tiene"
  FUNCION ||--o{ OPINION : "recibe"

  PELICULA ||--o{ PERSONA_PELICULA_ROL : "creditos"
  PERSONA ||--o{ PERSONA_PELICULA_ROL : "participa"

  PELICULA ||--o{ PERSONA_PERSONAJE : "reparto"
  PERSONA ||--o{ PERSONA_PERSONAJE : "interpreta"
