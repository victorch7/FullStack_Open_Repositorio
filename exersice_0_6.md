sequenceDiagram
    participant User
    participant Browser
    participant Server

    Note left of User: Página SPA ya cargada<br>(spa.js en ejecución)
    
    User->>Browser: 1. Escribe texto en el campo<br>2. Click en "Save"
    
    Note right of Browser: spa.js tiene un event handler<br>que intercepta el submit
    
    Browser->>Browser: Ejecuta preventDefault()<br> evitar recarga
    
    Browser->>Browser: Crea objeto JSON con la nota:<br>{content: "nueva nota", date: timestamp}
    
    Browser->>Server: POST /exampleapp/new_note_spa<br>Headers: {"Content-Type":"application/json"}<br>Body: JSON de la nota
    activate Server
    
    Note left of Server: 1. Valida datos<br>2. Agrega nota a data.json<br>3. Da respuesta
    
    Server-->>Browser: HTTP 201 Created<br>(con copia de la nota en JSON)
    deactivate Server
    
    Note right of Browser: Callback del fetch:<br>1. Verifica status 201<br>2. Agrega nota al array local<br>3. Invoca función de renderizado
    
    Browser->>Browser: DOM update:<br>- Crea nuevos elementos<br>- Añade al listado<br>- Limpia formulario
    
    Note right of User: La nueva nota aparece<br>instantáneamente<br>