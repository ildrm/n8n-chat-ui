# n8n Chat Interface

## Overview

This is an HTML-based chat interface designed to interact with an n8n webhook. It allows users to send messages to an n8n workflow and display responses in a simple, user-friendly chat UI. The interface supports both English and Persian languages (with separate files), includes basic styling, and uses the `marked` library to render Markdown-formatted responses from n8n.

### Key Features
- **Message Sending**: Send messages to an n8n webhook via POST requests.
- **Real-time Display**: Displays user messages and bot responses in a scrollable chat window.
- **Loading Indicator**: Shows a "Sending..." message during request processing.
- **Markdown Support**: Renders bot responses with Markdown formatting.
- **Responsive Design**: Simple, clean UI adaptable to different screen sizes.
- **Language Variants**: Available in English (`chat_en.html`) and Persian (`chat_fa.html`).

## Requirements
- A web browser (e.g., Chrome, Firefox) to run the HTML file.
- An active n8n instance with a webhook endpoint (e.g., `http://localhost:5678/webhook/2bb532df-5408-4700-849a-e54d6de1c522`).
- Internet access to load the `marked` library from CDN (or a local copy if offline).

## Installation
1. **Download or Clone the Files**:
   - Obtain the `chat_en.html` (English) and/or `chat_fa.html` (Persian) files.
   - Example:
    ```bash
    git clone https://github.com/ildrm/n8n-chat-ui.git
    cd n8n-chat-ui
    ```

2. **Set Up n8n**:
- Ensure your n8n instance is running and the webhook is configured.
- Update the webhook URL in the JavaScript `fetch` call if different from the default (`http://localhost:5678/webhook/...`).

3. **Place Files**:
- Place the HTML file(s) in a directory accessible by your web server or open directly in a browser for testing.

## Usage
### Running the Chat Interface
- Open the desired file (`chat_en.html` or `chat_fa.html`) in a web browser:
    - For local testing: Drag the file into your browser or use a local server (e.g., `php -S localhost:8000`).
    - For a web server: Upload to your server and access via URL (e.g., `http://localhost/chat_en.html`).

### Sending Messages

1. Type a message in the input field.
2. Press `Enter` or click the "Send" button to submit the message.
3. The message appears in the chat window, followed by a "Sending..." indicator.
4. The bot’s response from n8n will appear once received.

### Example Interaction

- Input: "Hello, how are you?"
- Chat Display:
```
[You]: Hello, how are you?
[Sending...]
[Bot]: Hi! I'm doing great, thanks for asking!
```

## Configuration
### Webhook Endpoint

The chat connects to an n8n webhook. The default URL and token are hardcoded in the JavaScript:
```javascript
fetch("http://localhost:5678/webhook/2bb532df-5408-4700-849a-e54d6de1c522", {
    method: "POST",
    headers: {
        "Content-Type": "application/json",
        "token": "<long-token-here>"
    },
    body: JSON.stringify([{ sessionId: "bf8a49534b464167ab469ef9b692e19a", action: "sendMessage", chatInput: messageText }])
})
```
- Modify URL: Update the URL if your n8n instance runs on a different host or port.
- Token: Replace the token with your n8n webhook’s authentication token if different

### Language Selection

## Dependencies
- Marked Library: Loaded via CDN (`https://cdn.jsdelivr.net/npm/marked/marked.min.js`) to parse Markdown responses. For offline use, download the library and reference it locally:
```html
<script src="path/to/marked.min.js"></script>
```

## Styling
The CSS is embedded in the `<style>` tag:

- Chat Container: Fixed width (400px), centered, with a border.
- Messages: Scrollable area (max-height 300px) with user (blue) and bot (green) styles.
- Loading Indicator: Hidden by default, shown during requests.

## Notes
- n8n Dependency: The chat requires an active n8n webhook to function. Ensure the workflow responds with a JSON object containing a `text` field (e.g., `{"text": "response"}`).
- Error Handling: Displays "Error receiving response" if the fetch fails. Customize this message in the `.catch` block if needed.
- Security: The hardcoded token in the script should be secured in a production environment (e.g., via environment variables or server-side logic).

## Contributing
Feel free to submit pull requests or issues to enhance the UI, add features (e.g., message history), or improve error handling.
