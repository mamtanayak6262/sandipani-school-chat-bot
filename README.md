
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sandipni School chhatwai Chatbot AI</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    --primary: #6258e8;
    --secondary: #8878ff;
    --bg: #f2f4fb;
    --white: #ffffff;
    --text: #22243a;
    --muted: #777c94;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 18px;
}

.chat-app {
    width: 100%;
    max-width: 900px;
    height: min(850px, 94vh);
    min-height: 500px;
    background: var(--white);
    border-radius: 22px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    box-shadow: 0 15px 55px rgba(48, 49, 100, 0.14);
}

/* Header */
.header {
    background: linear-gradient(120deg, #5146d8, #8878ff);
    color: white;
    padding: 20px 24px;
    display: flex;
    align-items: center;
    gap: 14px;
}

.bot-avatar {
    width: 52px;
    height: 52px;
    flex-shrink: 0;
    border-radius: 17px;
    background: rgba(255,255,255,0.19);
    display: grid;
    place-items: center;
    font-size: 27px;
}

.header-info {
    flex: 1;
}

.header h1 {
    font-size: 21px;
    margin-bottom: 6px;
}

.status {
    font-size: 13px;
    opacity: 0.9;
}

.status::before {
    content: "";
    display: inline-block;
    width: 8px;
    height: 8px;
    background: #66ffad;
    border-radius: 50%;
    margin-right: 7px;
}

.clear-btn {
    border: 1px solid rgba(255,255,255,.5);
    background: transparent;
    color: white;
    padding: 10px 13px;
    border-radius: 10px;
    cursor: pointer;
}

.clear-btn:hover {
    background: rgba(255,255,255,.15);
}

/* Chat area */
.chat-area {
    flex: 1;
    overflow-y: auto;
    padding: 25px;
    background:
        radial-gradient(circle at top right,
        rgba(136,120,255,.07), transparent 35%),
        #fafaff;
    scroll-behavior: smooth;
}

.welcome {
    text-align: center;
    padding: 28px 10px 22px;
}

.welcome-icon {
    font-size: 48px;
    margin-bottom: 12px;
}

.welcome h2 {
    font-size: 24px;
    margin-bottom: 10px;
}

.welcome p {
    color: var(--muted);
    line-height: 1.6;
    font-size: 14px;
}

.suggestions {
    display: flex;
    flex-wrap: wrap;
    gap: 9px;
    justify-content: center;
    margin-top: 19px;
}

.suggestion {
    border: 1px solid #dedcff;
    color: #554bd3;
    background: white;
    border-radius: 22px;
    padding: 10px 14px;
    font-size: 13px;
    cursor: pointer;
    transition: .2s;
}

.suggestion:hover {
    background: #efedff;
    transform: translateY(-2px);
}

.message {
    display: flex;
    gap: 10px;
    margin: 18px 0;
    align-items: flex-end;
    animation: appear .25s ease;
}

.message.user {
    justify-content: flex-end;
}

.message-avatar {
    width: 34px;
    height: 34px;
    border-radius: 12px;
    background: #e9e7ff;
    display: grid;
    place-items: center;
    flex-shrink: 0;
}

.message.user .message-avatar {
    background: #e1eaff;
}

.message-content {
    max-width: 78%;
}

.bubble {
    padding: 13px 16px;
    border-radius: 17px 17px 17px 5px;
    background: white;
    border: 1px solid #eeedf7;
    line-height: 1.65;
    font-size: 14px;
    overflow-wrap: anywhere;
    white-space: pre-wrap;
}

.message.user .bubble {
    background: var(--primary);
    color: white;
    border: none;
    border-radius: 17px 17px 5px 17px;
}

.time {
    font-size: 10px;
    color: #999db0;
    margin-top: 5px;
    padding: 0 5px;
}

.message.user .time {
    text-align: right;
}

.typing {
    display: flex;
    gap: 5px;
    padding: 17px;
}

.typing span {
    width: 7px;
    height: 7px;
    background: #8b83dc;
    border-radius: 50%;
    animation: bounce .7s infinite alternate;
}

.typing span:nth-child(2) {
    animation-delay: .2s;
}

.typing span:nth-child(3) {
    animation-delay: .4s;
}

@keyframes bounce {
    to { transform: translateY(-6px); opacity: .5; }
}

@keyframes appear {
    from { opacity: 0; transform: translateY(7px); }
    to { opacity: 1; transform: translateY(0); }
}

/* Input area */
.input-area {
    border-top: 1px solid #eeeef5;
    padding: 17px 20px;
    background: white;
}

.input-box {
    display: flex;
    align-items: center;
    gap: 10px;
    border: 1px solid #e3e2f0;
    background: #f9f9fe;
    border-radius: 16px;
    padding: 7px 8px 7px 16px;
    transition: .2s;
}

.input-box:focus-within {
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(98,88,232,.09);
}

#userInput {
    flex: 1;
    min-width: 0;
    padding: 10px 0;
    border: none;
    outline: none;
    background: transparent;
    color: var(--text);
    font-size: 15px;
}

#userInput::placeholder {
    color: #a1a3b6;
}

.send-btn {
    width: 44px;
    height: 44px;
    flex-shrink: 0;
    border: none;
    border-radius: 12px;
    background: var(--primary);
    color: white;
    font-size: 20px;
    cursor: pointer;
    transition: .2s;
}

.send-btn:hover {
    background: #4940c4;
    transform: scale(1.04);
}

.send-btn:disabled {
    opacity: .5;
    cursor: not-allowed;
}

.footer-text {
    text-align: center;
    color: #a0a1b2;
    font-size: 11px;
    margin-top: 12px;
}

/* Mobile */
@media (max-width: 600px) {
    body {
        padding: 0;
    }

    .chat-app {
        height: 100dvh;
        min-height: 0;
        border-radius: 0;
    }

    .header {
        padding: 16px;
    }

    .header h1 {
        font-size: 18px;
    }

    .bot-avatar {
        width: 45px;
        height: 45px;
    }

    .clear-btn {
        padding: 9px;
        font-size: 12px;
    }

    .chat-area {
        padding: 15px;
    }

    .welcome h2 {
        font-size: 21px;
    }

    .message-content {
        max-width: 85%;
    }

    .input-area {
        padding: 12px;
    }
}
</style>
</head>

<body>

<div class="chat-app">

    <header class="header">
        <div class="bot-avatar">🤖</div>

        <div class="header-info">
            <h1>Sandipni School chhatwai Chatbot AI</h1>
            <div class="status">Chat assistant ready</div>
        </div>

        <button class="clear-btn" id="clearBtn"
                type="button" title="Clear conversation">
            🗑 Clear
        </button>
    </header>

    <main class="chat-area" id="chatArea">

        <section class="welcome" id="welcome">
            <div class="welcome-icon">✨</div>
            <h2>HELLO PTHON</h2>
            <p>
                I am your Smart Chatbot Assistant.<br>
                Ask me a question in English or Hindi!
            </p>

            <div class="suggestions">
                <button class="suggestion" data-message="HELLO">
                    👋 Say HELLO
                </button>
                <button class="suggestion" data-message="What can you do?">
                    💡 What can you do?
                </button>
                <button class="suggestion" data-message="Help me with study">
                    📚 Study Help
                </button>
                <button class="suggestion" data-message="Tell me a joke">
                    😂 Tell me a joke
                </button>
            </div>
        </section>

        <div id="messages"></div>

    </main>

    <form class="input-area" id="chatForm">
        <div class="input-box">
            <input
                type="text"
                id="userInput"
                placeholder="Type your message here..."
                autocomplete="off"
                maxlength="2000"
                aria-label="Your message"
                required
            >
            <button class="send-btn" id="sendBtn"
                    type="submit" aria-label="Send message">
                ➤
            </button>
        </div>

        <p class="footer-text">
            Smart Chatbot Demo • Built with HTML, CSS & JavaScript
        </p>
    </form>

</div>

<script>
const chatArea = document.getElementById("chatArea");
const messages = document.getElementById("messages");
const welcome = document.getElementById("welcome");
const userInput = document.getElementById("userInput");
const chatForm = document.getElementById("chatForm");
const sendBtn = document.getElementById("sendBtn");
const clearBtn = document.getElementById("clearBtn");

let isTyping = false;

// Get current time
function getTime() {
    return new Date().toLocaleTimeString([], {
        hour: "2-digit",
        minute: "2-digit"
    });
}

// Add a chat message safely
function addMessage(text, sender) {
    welcome.style.display = "none";

    const row = document.createElement("div");
    row.className = "message " + sender;

    const avatar = document.createElement("div");
    avatar.className = "message-avatar";
    avatar.textContent = sender === "bot" ? "🤖" : "👤";

    const content = document.createElement("div");
    content.className = "message-content";

    const bubble = document.createElement("div");
    bubble.className = "bubble";
    bubble.textContent = text;

    const time = document.createElement("div");
    time.className = "time";
    time.textContent = getTime();

    content.appendChild(bubble);
    content.appendChild(time);

    if (sender === "bot") {
        row.appendChild(avatar);
        row.appendChild(content);
    } else {
        row.appendChild(content);
        row.appendChild(avatar);
    }

    messages.appendChild(row);
    chatArea.scrollTop = chatArea.scrollHeight;
}

// Show typing animation
function showTyping() {
    const row = document.createElement("div");
    row.className = "message bot";
    row.id = "typingIndicator";

    const avatar = document.createElement("div");
    avatar.className = "message-avatar";
    avatar.textContent = "🤖";

    const bubble = document.createElement("div");
    bubble.className = "bubble typing";

    for (let i = 0; i < 3; i++) {
        const dot = document.createElement("span");
        bubble.appendChild(dot);
    }

    row.appendChild(avatar);
    row.appendChild(bubble);
    messages.appendChild(row);

    chatArea.scrollTop = chatArea.scrollHeight;
}

function hideTyping() {
    const indicator = document.getElementById("typingIndicator");
    if (indicator) indicator.remove();
}

// Chatbot response logic
function getBotReply(message) {
    const msg = message.toLowerCase().trim();

    // Greetings
    if (/\b(hi|HELLO|hey|hii|good morning|good evening)\b/.test(msg)
        || /नमस्ते|नमस्कार|हेलो|हाय/.test(msg)) {
        return "HELLO! 👋 Welcome to Sandipni School chhatwai Chatbot AI. How can I help you today?";
    }

    // Identity
    if (msg.includes("your name") || msg.includes("who are you")
        || msg.includes("tumhara naam") || msg.includes("आपका नाम")) {
        return "I am Sandipni School chhatwai Chatbot AI 🤖, a demo chatbot built using HTML, CSS and JavaScript.";
    }

    // Capabilities
    if (msg.includes("what can you do") || msg.includes("help")
        || msg.includes("kya kar") || msg.includes("क्या कर")) {
        return "I can help with basic questions, study tips, greetings, simple coding guidance and more.\n\nTry asking:\n• Tell me a joke\n• Help me with study\n• How to learn HTML?\n• What is JavaScript?";
    }

    // Thanks
    if (/\b(thanks|thank you|thx)\b/.test(msg)
        || /धन्यवाद|शुक्रिया/.test(msg)) {
        return "You're welcome! 😊 Feel free to ask me another question.";
    }

    // Goodbye
    if (/\b(bye|goodbye|see you)\b/.test(msg)
        || /अलविदा|बाय/.test(msg)) {
        return "Goodbye! 👋 Have a wonderful day. You can come back whenever you need help.";
    }

    // Study
    if (msg.includes("study") || msg.includes("exam")
        || msg.includes("पढ़ाई") || msg.includes("परीक्षा")) {
        return "📚 Here are some useful study tips:\n\n1. Set a small daily goal.\n2. Study in focused 25-minute sessions.\n3. Take short breaks.\n4. Revise important topics.\n5. Practise questions regularly.\n\nWhich subject are you studying?";
    }

    // HTML
    if (msg.includes("html")) {
        return "🌐 HTML is the standard markup language used to structure web pages.\n\nBasic HTML example:\n\n<!DOCTYPE html>\n<html>\n<body>\n  <h1>HELLO World!</h1>\n  <p>My first webpage.</p>\n</body>\n</html>\n\nSave this as index.html and open it in your browser.";
    }

    // CSS
    if (msg.includes("css")) {
        return "🎨 CSS is used to style web pages, including colors, layouts, fonts and animations.\n\nExample:\n\nh1 {\n  color: blue;\n  text-align: center;\n}\n\nAdd CSS inside a <style> tag in your HTML file.";
    }

    // JavaScript
    if (msg.includes("javascript") || msg.includes(" js ")) {
        return "⚡ JavaScript adds interaction to websites. It can handle buttons, forms, chat messages and more.\n\nExample:\n\nalert('HELLO World!');\n\nThis chatbot also uses JavaScript to process your messages.";
    }

    // Project ideas
    if (msg.includes("project idea") || msg.includes("college project")
        || msg.includes("school project")) {
        return "💡 Some beginner-friendly project ideas:\n\n1. Smart Chatbot\n2. Student Management System\n3. Online Shopping Website\n4. Weather Dashboard\n5. Quiz Application\n6. Sign Language Learning Website\n\nYou can build a basic frontend using HTML, CSS and JavaScript.";
    }

    // Jokes
    if (msg.includes("joke") || msg.includes("funny")
        || msg.includes("चुटकुला")) {
        return "😂 Why do programmers prefer dark mode?\n\nBecause light attracts bugs! 🐛";
    }

    // Time
    if (msg.includes("time") || msg.includes("समय")) {
        return "🕒 Your device's current time is " + getTime() + ".";
    }

    // Date
    if (msg.includes("date") || msg.includes("today")
        || msg.includes("तारीख")) {
        return "📅 Today's date is " +
            new Date().toLocaleDateString(undefined, {
                day: "numeric",
                month: "long",
                year: "numeric"
            }) + ".";
    }

    // How are you?
    if (msg.includes("how are you") || msg.includes("kaise ho")
        || msg.includes("कैसे हो")) {
        return "I'm ready to help! 😊 What would you like to talk about?";
    }

    // Hindi response
    if (/[\u0900-\u097F]/.test(msg)) {
        return "आपका सवाल समझने की कोशिश कर रहा हूँ। 😊\n\nआप मुझसे पढ़ाई, HTML, CSS, JavaScript या प्रोजेक्ट आइडिया के बारे में पूछ सकते हैं।\n\nध्यान दें: मैं अभी एक demo chatbot हूँ, इसलिए हर सवाल का जवाब नहीं दे सकता।";
    }

    // Default response
    return "That's an interesting question! 😊\n\nI am currently a rule-based demo chatbot, so I may not know the answer to every question.\n\nTry asking about HTML, CSS, JavaScript, study tips, project ideas or tell me a joke.";
}

// Send message
function sendMessage(text) {
    const message = text.trim();

    if (!message || isTyping) return;

    addMessage(message, "user");
    userInput.value = "";
    isTyping = true;
    sendBtn.disabled = true;
    userInput.disabled = true;

    showTyping();

    // Simulate a short response delay
    window.setTimeout(function() {
        hideTyping();

        const reply = getBotReply(message);
        addMessage(reply, "bot");

        isTyping = false;
        sendBtn.disabled = false;
        userInput.disabled = false;
        userInput.focus();
    }, 650);
}

// Form submission
chatForm.addEventListener("submit", function(event) {
    event.preventDefault();
    sendMessage(userInput.value);
});

// Suggestion buttons
document.querySelectorAll(".suggestion").forEach(function(button) {
    button.addEventListener("click", function() {
        sendMessage(button.dataset.message);
    });
});

// Clear conversation
clearBtn.addEventListener("click", function() {
    if (isTyping) return;

    messages.replaceChildren();
    welcome.style.display = "block";
    userInput.value = "";
    userInput.focus();
});
</script>

</body>
</html># sandipani-school-chat-bot
