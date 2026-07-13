```mermaid
sequenceDiagram
    participant browser
    participant server

    Note over browser: User writes text in the field and clicks the Save button

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note over server: Server extracts the data, creates a new note object,<br/>and pushes it into the notes array
    server-->>browser: HTTP status code 302 (Redirect to /exampleapp/notes)
    deactivate server

    Note right of browser: The redirect triggers the browser to reload the notes page

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: the updated JSON data (including the new note)
    deactivate server

    Note right of browser: The browser executes the callback function that renders the updated notes list
