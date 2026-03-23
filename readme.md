```mermaid
graph TD
    classDef water fill:#3498db,stroke:#2980b9,stroke-width:2px,color:white;
    classDef air fill:#ecf0f1,stroke:#bdc3c7,stroke-width:2px;
    classDef tank fill:#95a5a6,stroke:#7f8c8d,stroke-width:3px;
    classDef pipe stroke:#7f8c8d,stroke-width:4px;
    classDef important fill:#e74c3c,stroke:#c0392b,color:white,font-weight:bold;

    subgraph Tanque_y_Bomba [Tanque y Bomba]
        Tanque["Tanque de Agua\n(Nivel Alto)"]:::tank
        Bomba["Bomba\nCentrífuga"]:::tank
        Succion["Tubería de\nSucción"]:::pipe
        
        Tanque -->|Gravedad| Succion
        Succion --> Bomba
    end

    subgraph Sistema_Apagado [ESTADO: BOMBA APAGADA (Sin Solución)]
        Descarga_A["Tubería de Descarga"]:::pipe
        Salida_A["Salida de Riego\n(Nivel Bajo)"]
        
        Bomba -.->|Paso Libre| Descarga_A
        Descarga_A -->|Flujo Continuo\npor Gravedad| Salida_A:::important
    end

    subgraph Sistema_Con_Solucion [ESTADO: BOMBA APAGADA (Con Rompe-Sifón)]
        Tuberia_Elevada["Tubería Elevada\n(Sobre Nivel Máx. Tanque)"]:::pipe
        Valvula_Vacio["Válvula Rompe-Sifón\n(Punto más alto)"]:::important
        Descarga_B["Tubería de Descarga"]:::pipe
        Salida_B["Salida de Riego"]
        Aire["Entrada de Aire"]:::air
        
        Bomba --> Tuberia_Elevada
        Tuberia_Elevada --- Valvula_Vacio
        Valvula_Vacio -->|Corta Sifón| Descarga_B
        Descarga_B --> Salida_B
        
        Aire -.->|Entra Aire| Valvula_Vacio
    end

    Bomba -.-> Descarga_A
    Tuberia_Elevada -.-> Valvula_Vacio
    Valvula_Vacio -.-> Aire
```