# Chatbot in JavaScript 🤖

A fully functional AI-powered chatbot widget built with HTML, CSS, and vanilla JavaScript, integrated with the **Google Gemini API** (`gemini-1.5-flash` model).

---

## Features

- Floating toggle button to open/close the chatbot
- Real-time AI responses powered by Google Gemini 1.5 Flash
- "Thinking..." indicator while waiting for a response
- Auto-expanding textarea input
- Send messages via button click or `Enter` key
- Error handling with styled error messages
- Fully responsive — full-screen on mobile devices
- Smooth open/close animations

---

## Project Structure

```
├── index.html      # Chatbot UI structure and layout
├── script.js       # Chat logic and Gemini API integration
└── style.css       # All styles including responsive design
```

---

## How It Works

### HTML (`index.html`)
The UI consists of two main elements:
- A **floating toggle button** (bottom-right corner) to show/hide the chatbot.
- A **chatbot panel** containing a header, a scrollable message list (`<ul class="chatbox">`), and a textarea input with a send button.

Material Symbols icons are used for the bot avatar, send button, and toggle icons.

### JavaScript (`script.js`)

**Opening & closing:**
```js
chatbotToggler.addEventListener("click", () =>
  document.body.classList.toggle("show-chatbot")
);
```
Toggling the `show-chatbot` class on `<body>` shows or hides the chatbot via CSS.

**Sending a message:**
```js
const handleChat = () => {
  userMessage = chatInput.value.trim();
  if (!userMessage) return;
  chatbox.appendChild(createChatLi(userMessage, "outgoing"));
  // Show "Thinking..." then call the API
};
```

**Calling the Gemini API:**
```js
const API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`;

const response = await fetch(API_URL, requestOptions);
const data = await response.json();
messageElement.textContent = data.candidates[0].content.parts[0].text;
```
The user's message is sent as a POST request. The response text is extracted and displayed in the chat.

### CSS (`style.css`)
- The chatbot panel uses `position: fixed` and animates in with `transform: scale(0.5 → 1)` and `opacity: 0 → 1`.
- Outgoing messages are purple (`#724ae8`), incoming messages are light gray.
- On screens narrower than 490px, the chatbot expands to full screen.

---

## Setup & Usage

### 1. Get a Gemini API Key
- Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
- Create a new API key

### 2. Add Your API Key
Open `script.js` and replace the placeholder:
```js
const API_KEY = "YOUR_API_KEY_HERE";
```

### 3. Run the Project
No build tools required. Just open `index.html` in a browser:
```bash
open index.html
```

---

## API Reference

| Property | Value |
|----------|-------|
| Provider | Google Generative Language API |
| Model | `gemini-1.5-flash` |
| Method | `POST` |
| Endpoint | `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent` |

**Request body format:**
```json
{
  "contents": [
    {
      "role": "user",
      "parts": [{ "text": "Your message here" }]
    }
  ]
}
```

---

## Known Issues & TODOs

| Issue | Details |
|-------|---------|
| API key exposed in client code | The API key is hardcoded in `script.js` — it should be moved to a backend proxy for production use |
| No conversation history | Each request is sent independently; the bot has no memory of earlier messages in the session |
| No message timestamps | Chat messages do not show when they were sent |
| Markdown not fully rendered | Bold markers (`**text**`) are stripped but other Markdown (lists, code blocks) is not formatted |

---

## Planned Improvements

- Move API key to a secure backend/proxy server
- Pass full conversation history with each request for context-aware replies
- Render Markdown responses (code blocks, bullet points)
- Add message timestamps
- Add typing animation instead of static "Thinking..." text

---

## Tech Stack

| Technology | Purpose |
|------------|---------|
| HTML5 | Chatbot structure and layout |
| CSS3 | Styling, animations, responsive design |
| JavaScript (ES6+) | Chat logic, DOM manipulation, API calls |
| Fetch API | Async communication with Gemini API |
| Google Gemini 1.5 Flash | AI response generation |
| Google Fonts (Poppins) | Typography |
| Material Symbols | Icons (send, bot avatar, close, toggle) |

---

## Responsive Design

| Screen Size | Behaviour |
|-------------|-----------|
| > 490px | Floating panel (420px wide, bottom-right corner) |
| ≤ 490px | Full-screen chatbot with close button in header |

## Author 

Aman Kumar
