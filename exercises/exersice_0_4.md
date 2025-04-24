sequenceDiagram
    participant User
    participant Browser
    participant Server

    User->>Browser: Escribe nota en el input de texto y haz clic en "Save"
    
    Note right of Browser: El evento click ejecuta el handler en main.js
    
    Browser->>Server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate Server
    Note left of Server: El servidor guarda la nueva nota en data.json
    Server-->>Browser: HTTP 302 Redirect (a /exampleapp/notes)
    deactivate Server
    
    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate Server
    Server-->>Browser: HTML document
    deactivate Server
    
    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate Server
    Server-->>Browser: the css file
    deactivate Server
    
    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate Server
    Server-->>Browser: the JavaScript file
    deactivate Server
    
    Note right of Browser: El navegador ejecuta main.js que hace fetch de data.json
    
    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate Server
    Server-->>Browser: [{...}, {...}, (nueva nota)]
    deactivate Server
    