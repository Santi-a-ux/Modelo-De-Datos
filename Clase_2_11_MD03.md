```mermaid
erDiagram
	direction TB
	ITEM_SOLICITUD {
		string numero_solicitud FK ""  
		int item PK ""  
		string codigo_bien FK ""  
		string nombre  ""  
		int cantidad  ""  
		string unidad_medida  ""  
		decimal valor_unitario  ""  
		decimal valor_total  ""  
	}

	EMPLEADO {
		string Cedula PK ""  
		string Nombre  ""  
		string Apellido  ""  
		string Area  ""  
	}

	SOLICITUD {
		string numero PK ""  
		date fecha  ""  
		string cedula_responsable FK ""  
		decimal valor_total  ""  
		string estado  ""  
	}

	CENTRO_COSTOS {
		string id  ""  
	}

	RUBRO_PRESUPUESTAL {

	}

	BIEN {

	}

	EMPLEADO||--o{SOLICITUD:"Responsable"
	SOLICITUD||--o{ITEM_SOLICITUD:"contiene"
	EMPLEADO||--o{SOLICITUD:"Autoriza"
	EMPLEADO}|--|{SOLICITUD:"Aprueba"
