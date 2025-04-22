sequenceDiagram
    participant User
    participant Browser
    participant Server

    User->>Browser: Navega a https://studies.cs.helsinki.fi/exampleapp/spa
    
    Browser->>Server: GET /exampleapp/spa
    activate Server
    Server-->>Browser: HTML document (sin notas)
    deactivate Server
    
    Browser->>Server: GET /exampleapp/main.css
    activate Server
    Server-->>Browser: CSS file
    deactivate Server
    
    Browser->>Server: GET /exampleapp/spa.js
    activate Server
    Server-->>Browser: JavaScript específico de SPA
    deactivate Server
    
    Note right of Browser: spa.js se ejecuta y hace:<br>1. Configura event handlers<br>2. Carga inicial de notas via fetch
    
    Browser->>Server: GET /exampleapp/data.json
    activate Server
    Server-->>Browser: [{content: "note1", date: "..."}, ...]
    deactivate Server
    
    Note right of Browser: spa.js procesa los datos y renderiza<br>las notas dinámicamente en el DOM
    
    User->>Browser: Escribe nueva nota y hace click en Save
    
    Note right of Browser: spa.js intercepta el submit,<br>previene recarga de página
    
    Browser->>Server: POST /exampleapp/new_note_spa 
    activate Server
    Server-->>Browser: 201 Created (nueva nota en JSON)
    deactivate Server
    
    Note right of Browser: spa.js agrega la nueva nota<br>al DOM sin recargar