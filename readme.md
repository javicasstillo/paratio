## Diagrama Sistema de Agua

```mermaid
graph TD
    classDef water fill:#3498db,stroke:#2980b9,stroke-width:2px,color:white;
    classDef air fill:#ecf0f1,stroke:#bdc3c7,stroke-width:2px;
    classDef tank fill:#95a5a6,stroke:#7f8c8d,stroke-width:3px;
    classDef pipe stroke:#7f8c8d,stroke-width:4px;
    classDef important fill:#e74c3c,stroke:#c0392b,color:white,font-weight:bold;

    subgraph Tanque_y_Bomba [Tanque y Bomba]
        Tanque[<b>Tanque de Agua</b><br/>(Nivel Alto)]:::tank
        Bomba[<b>Bomba<br/>Centrífuga</b>]:::tank
        Succion[Tubería de<br/>Succión]:::pipe
        
        Tanque ==>|Gravedad| Succion
        Succion ==> Bomba
    end

    subgraph Sistema_Apagado [ESTADO: BOMBA APAGADA (Sin Solución)]
        Descarga_A[Tubería de Descarga]:::pipe
        Salida_A[Salida de Riego<br/>(Nivel Bajo)]
        
        Bomba -.->|Paso Libre| Descarga_A
        Descarga_A ==>|<b>Flujo Continuo</b><br/>por Gravedad| Salida_A:::important
    end

    subgraph Sistema_Con_Solucion [ESTADO: BOMBA APAGADA (Con Rompe-Sifón)]
        Tubería_Elevada[<b>Tubería Elevada</b><br/>(Sobre Nivel Máx. Tanque)]:::pipe
        Valvula_Vacio[<b>Válvula<br/>Rompe-Sifón</b><br/>(Punto más alto)]:::important
        Descarga_B[Tubería de Descarga]:::pipe
        Salida_B[Salida de Riego]
        Aire[Entrada de Aire]:::air
        
        Bomba --> Tubería_Elevada
        Tubería_Elevada --- Valvula_Vacio
        Valvula_Vacio ==>|<b>Corta Sifón</b>| Descarga_B
        Descarga_B --> Salida_B
        
        Aire -.->|Entra Aire| Valvula_Vacio
    end

    Bomba -.-> Descarga_A
    Tubería_Elevada -.-> Valvula_Vacio
    Valvula_Vacio -.-> Aire
```