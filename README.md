# CHATBOT-WITH-RULE-BASED-RESPONSES
A simple rule-based chatbot built using Python and Flask for understanding basic NLP conversation flows
.

🌐 Rule-Based Chatbot using Flask
📁 Project Structure:
rule_based_chatbot/
│
├── app.py                # Flask app
├── chatbot.py            # Chatbot logic
└── templates/
    └── index.html        # HTML for chat interface

🧠 chatbot.py – Chat Logic
import re

def chatbot_response(user_input):
    user_input = user_input.lower()

    if re.search(r'\b(hi|hello|hey)\b', user_input):
        return "Hello! How can I assist you today?"

    elif re.search(r'\bhow are you\b', user_input):
        return "I'm just a bot, but I'm functioning well!"

    elif re.search(r'\bwhat is your name\b', user_input):
        return "I'm your friendly chatbot, powered by Flask."

    elif re.search(r'\btell me a joke\b', user_input):
        return "Why did the computer go to the doctor? Because it had a virus!"

    elif re.search(r'\b(bye|goodbye|exit)\b', user_input):
        return "Goodbye! Hope to chat again soon."

    else:
        return "Sorry, I didn't quite get that. Can you rephrase?"

🚀 app.py – Flask App
from flask import Flask, render_template, request, jsonify
from chatbot import chatbot_response

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/get", methods=["GET"])
def get_bot_response():
    user_input = request.args.get("msg")
    return chatbot_response(user_input)

if __name__ == "__main__":
    app.run(debug=True)

🖼️ templates/index.html – Basic Chat UI
<!DOCTYPE html>
<html>
<head>
    <title>Rule-Based Chatbot</title>
    <style>
        body { font-family: Arial; background: #f2f2f2; margin: 0; padding: 0; }
        .chat-container { width: 500px; margin: 100px auto; background: white; padding: 20px; border-radius: 8px; box-shadow: 0 0 10px #ccc; }
        .chat-box { height: 300px; overflow-y: auto; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; }
        .chat-message { margin: 10px 0; }
        .user { text-align: right; }
        .bot { text-align: left; color: #444; }
        input[type="text"] { width: 80%; padding: 10px; }
        button { padding: 10px; }
    </style>
</head>
<body>
    <div class="chat-container">
        <h2>Chat with Bot</h2>
        <div class="chat-box" id="chat-box"></div>
        <input type="text" id="user-input" placeholder="Type your message..." />
        <button onclick="sendMessage()">Send</button>
    </div>

    <script>
        function sendMessage() {
            var userInput = document.getElementById("user-input").value;
            if (userInput.trim() === "") return;

            var chatBox = document.getElementById("chat-box");

            chatBox.innerHTML += "<div class='chat-message user'><b>You:</b> " + userInput + "</div>";
            document.getElementById("user-input").value = "";

            fetch("/get?msg=" + encodeURIComponent(userInput))
                .then(response => response.text())
                .then(botResponse => {
                    chatBox.innerHTML += "<div class='chat-message bot'><b>Bot:</b> " + botResponse + "</div>";
                    chatBox.scrollTop = chatBox.scrollHeight;
                });
        }

        document.getElementById("user-input").addEventListener("keydown", function (e) {
            if (e.key === "Enter") sendMessage();
        });
    </script>
</body>
</html>

▶️ How to Run the Web App

Install Flask:

pip install flask


Run the Flask App:
Navigate to your rule_based_chatbot directory and run:

python app.py


Open your browser:
Visit http://127.0.0.1:5000/

✅ Result:

You'll get a clean, functional web-based chatbot that responds based on rules you define.
