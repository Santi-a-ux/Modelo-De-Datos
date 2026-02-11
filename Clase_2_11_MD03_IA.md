```mermaid
erDiagram
    EMPLEADO ||--o{ SOLICITUD_COMPRA : realiza
    EMPLEADO ||--o{ CENTRO_COSTO : adscrito_a
    EMPLEADO ||--o{ RESPONSABLE_BIEN : es
    CENTRO_COSTO ||--o{ SOLICITUD_COMPRA : "carga a"
    RUBRO_PRESUPUESTAL ||--o{ SOLICITUD_COMPRA : "descarga"
    SOLICITUD_COMPRA ||--o{ ITEM_SOLICITUD : contiene
    SOLICITUD_COMPRA ||--o{ AUTORIZACION : "autorizada por"
    BIEN ||--o{ ITEM_SOLICITUD : "identificado en"
    ITEM_SOLICITUD ||--o{ ITEM_ORDEN_COMPRA : "asociado a"
    PROVEEDOR ||--o{ COTIZACION : realiza
    SOLICITUD_COMPRA ||--o{ COTIZACION : "cotizada de"
    PROVEEDOR ||--o{ ORDEN_COMPRA : "realiza compra a"
    COTIZACION ||--o{ ORDEN_COMPRA : "genera"
    ORDEN_COMPRA ||--o{ ITEM_ORDEN_COMPRA : contiene
    ORDEN_COMPRA ||--o{ ENTRADA_ALMACEN : "recibida en"
    PROVEEDOR ||--o{ ENTRADA_ALMACEN : entrega
    ENTRADA_ALMACEN ||--o{ ITEM_ENTRADA_ALMACEN : detalla
    BIEN ||--o{ ITEM_ENTRADA_ALMACEN : "recibido en"
    ENTRADA_ALMACEN ||--o{ SALIDA_ALMACEN : genera
    SALIDA_ALMACEN ||--o{ ITEM_SALIDA_ALMACEN : detalla
    BIEN ||--o{ ITEM_SALIDA_ALMACEN : "despachado en"
    EMPLEADO ||--o{ SALIDA_ALMACEN : responsable_entrega
    BIEN ||--o{ UBICACION_BIEN : "ubicado en"
    EMPLEADO ||--o{ UBICACION_BIEN : responsable
    CENTRO_COSTO ||--o{ RESPONSABLE_BIEN : "recibe en"

    EMPLEADO {
        string cedula PK
        string nombre
        string cargo
    }

    CENTRO_COSTO {
        string codigo PK
        string nombre
        string descripcion
    }

    RUBRO_PRESUPUESTAL {
        string codigo PK
        string nombre
        decimal presupuesto
    }

    SOLICITUD_COMPRA {
        string numero PK
        date fecha
        string cedula_responsable FK
        string centro_costo FK
        string rubro_presupuestal FK
        decimal valor_total
        string estado
    }

    ITEM_SOLICITUD {
        string numero_solicitud FK
        int item PK
        string codigo_bien FK
        string nombre
        int cantidad
        string unidad_medida
        decimal valor_unitario
        decimal valor_total
    }

    AUTORIZACION {
        string numero_solicitud FK
        string cedula_jefe_area FK
        date fecha_autorizacion_jefe
        string cedula_director_financiero FK
        date fecha_autorizacion_director
        string estado
    }

    BIEN {
        string codigo PK
        string nombre
        string tipo
        string caracteristica
    }

    PROVEEDOR {
        string nit PK
        string nombre
        string direccion
        string telefono
        string email
    }

    COTIZACION {
        string numero PK
        string numero_solicitud FK
        string nit_proveedor FK
        date fecha_cotizacion
        decimal valor_total
        string estado
    }

    ORDEN_COMPRA {
        string numero PK
        string nit_proveedor FK
        date fecha_orden
        decimal monto_total
        date fecha_entrega_esperada
        string cedula_director_financiero FK
        string estado
    }

    ITEM_ORDEN_COMPRA {
        string numero_orden FK
        int item PK
        string codigo_bien FK
        string nombre
        int cantidad_solicitada
        int cantidad_despachada
        string unidad_medida
        decimal valor_unitario
        decimal valor_total
    }

    ENTRADA_ALMACEN {
        string numero PK
        date fecha
        string numero_factura
        string nit_proveedor FK
        int total_bienes
        decimal valor_total
        date fecha_recepcion
    }

    ITEM_ENTRADA_ALMACEN {
        string numero_entrada FK
        int item PK
        string codigo_bien FK
        string nombre
        int cantidad_entregada
    }

    SALIDA_ALMACEN {
        string numero PK
        string cedula_responsable FK
        date fecha_salida
        date fecha_entrega
        string numero_entrada FK
    }

    ITEM_SALIDA_ALMACEN {
        string numero_salida FK
        int item PK
        string codigo_bien FK
        string nombre
        int cantidad_entregada
    }

    UBICACION_BIEN {
        string codigo_bien FK
        string cedula_responsable FK
        date fecha_entrega PK
        string direccion
        string localizacion_fisica
    }

    RESPONSABLE_BIEN {
        string cedula_empleado FK
        string codigo_centro_costo FK
    }
