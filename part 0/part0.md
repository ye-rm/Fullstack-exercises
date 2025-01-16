#### 0.4

```mermaid
sequenceDiagram
    participant browser
    participant server

	browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
	activate server
	Note left of server: The server push a new note in array notes
	server-->>browser: HTML document
	deactivate server

	Note right of browser: Server response 302 with location /exampleapp/notes, browser reload the notes page

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
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
```

![image-20250116162226319](https://typora-markdown-2003.obs.cn-north-4.myhuaweicloud.com/image-20250116162226319.png)response from POST contains HTML document(same as the 2nd)?

#### 0.5

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback functons(parse JSON to initialize notes array and redraw notes)
```

#### 0.6

```mermaid
sequenceDiagram
    participant browser
    participant server
    
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server
    server-->>browser: JSON {"message":"note created"}
    deactivate server 
    
    Note right of browser: Browser push new note in notes array and redraw notes, then call sendToServer.
    
   	%%According to JavaScript code, Browser add the new note in notes array and call redrawNotes to update html document, then call sendToServer to send the new note in json format, bacause POST set the position '/exampleapp/new_note_spa', so server can correctly proceed this request.%%
```

According to JavaScript code, Browser add the new note in notes array and call redrawNotes to update html document, then call sendToServer to send the new note in json format, bacause POST set the position '/exampleapp/new_note_spa', so server can correctly proceed this request.