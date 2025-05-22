
```mermaid
sequenceDiagram
participant browser
participant server

browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note: Do a URL Redirect to new_note address in the server
activate server
server-->>browser: Returns 302 Status call, and tells browser to make a GET call at location /exampleapp/notes (called note) a.k.a. reload site
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
activate server
server-->>browser: The resulting GET call following the POST Header Request, returning the HTML
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
activate server
server-->>browser: The CSS file linked in the styles tab from the server
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
activate server
server-->>browser: The JavaScript file from the server
deactivate server

Note right of browser: Browser begins running JavaScript, which tells it to fetch the JSON from the server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
activate server
server-->>browser: The note data; i.e: [{ "content": " ", "date": "2025-05-22T14:06:58.746Z"}, ...]
deactivate server

Note right of browser: Browser now executes callback function to display the notes
```