erDiagram
  CINE {
    int id_cine PK
    string nombre
    string direccion
    string ciudad
    string telefono
  }

  SALA {
    int id_sala PK
    int id_cine FK
    string nombre
    int capacidad
  }

  PELICULA {
    int id_pelicula PK
    string titulo
    int duracion_min
    string clasificacion
    string genero
  }

  FUNCION {
    int id_funcion PK
    int id_sala FK
    int id_pelicula FK
    datetime fecha_hora
    decimal precio
    string idioma
    string formato
  }

  CLIENTE {
    int id_cliente PK
    string nombres
    string apellidos
    string email
    string telefono
  }

  COMPRA {
    int id_compra PK
    int id_cliente FK
    datetime fecha_compra
    decimal total
    string medio_pago
  }

  BOLETO {
    int id_boleto PK
    int id_compra FK
    int id_funcion FK
    string asiento
    decimal precio_unitario
  }

  CINE ||--o{ SALA : tiene
  SALA ||--o{ FUNCION : programa
  PELICULA ||--o{ FUNCION : se_proyecta_en
  CLIENTE ||--o{ COMPRA : realiza
  COMPRA ||--o{ BOLETO : incluye
  FUNCION ||--o{ BOLETO : genera
