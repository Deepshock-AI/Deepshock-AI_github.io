# Deepshock-AI_github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Deepshock AI</title>
    <style>
        :root {
            --primary: #6e3bdc;
            --secondary: #f0f2f5;
            --dark: #1a1a2e;
        }
        
        body {
            font-family: 'Segoe UI', system-ui, sans-serif;
            margin: 0;
            padding: 0;
            background: #f7f7f8;
            color: #333;
            height: 100vh;
            display: flex;
            flex-direction: column;
        }
        
        header {
            background: var(--primary);
            color: white;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .auth-container {
            max-width: 400px;
            margin: 50px auto;
            padding: 30px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .chat-container {
            flex: 1;
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
            width: 100%;
            overflow-y: auto;
        }
        
        .message {
            max-width: 70%;
            padding: 12px 16px;
            border-radius: 18px;
            margin-bottom: 15px;
            line-height: 1.5;
        }
        
        .user-message {
            background: var(--primary);
            color: white;
            margin-left: auto;
            border-bottom-right-radius: 5px;
        }
        
        .bot-message {
            background: var(--secondary);
            margin-right: auto;
            border-bottom-left-radius: 5px;
        }
        
        .input-container {
            display: flex;
            padding: 15px;
            background: white;
            border-top: 1px solid #e5e7eb;
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            max-width: 800px;
            margin: 0 auto;
        }
        
        #user-input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 25px;
            font-size: 16px;
        }
        
        #send-btn {
            margin-left: 10px;
            padding: 0 25px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 600;
        }
        
        .welcome-message {
            text-align: center;
            margin: 40px 0;
        }
        
        .feature-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin: 20px 0;
        }
        
        .action-btn {
            padding: 12px 24px;
            border-radius: 8px;
            font-weight: 500;
            cursor: pointer;
        }
        
        .primary-btn {
            background: var(--primary);
            color: white;
            border: none;
        }
        
        .secondary-btn {
            background: white;
            color: var(--primary);
            border: 1px solid #ddd;
        }
        
        .recording {
            background: #ff4d4d !important;
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.7; }
            100% { opacity: 1; }
        }
        
        #video-container {
            display: none;
            margin: 20px 0;
            text-align: center;
        }
        
        #video-preview {
            width: 100%;
            max-width: 400px;
            border-radius: 8px;
        }
        
        body.dark-mode {
            background: var(--dark);
            color: #f0f0f0;
        }
        
        .dark-mode .chat-container,
        .dark-mode .auth-container {
            background: #16213e;
            color: #f0f0f0;
        }
        
        .dark-mode .bot-message {
            background: #2d3748;
            color: #f0f0f0;
        }
        
        .dark-mode .secondary-btn {
            background: #2d3748;
            color: #f0f0f0;
            border-color: #4a5568;
        }
    </style>
</head>
<body>
    <!-- Authentication Screen -->
    <div id="auth-screen" class="auth-container">
        <h2 style="text-align:center;color:var(--primary)">Deepshock AI</h2>
        <div id="login-form">
            <h3>Login</h3>
            <input type="email" id="login-email" placeholder="Email" style="width:100%;padding:12px;margin:10px 0;border:1px solid #ddd;border-radius:5px">
            <input type="password" id="login-password" placeholder="Password" style="width:100%;padding:12px;margin:10px 0;border:1px solid #ddd;border-radius:5px">
            <button onclick="login()" style="width:100%;padding:12px;background:var(--primary);color:white;border:none;border-radius:5px;margin:10px 0">Login</button>
            <p style="text-align:center">New user? <a href="#" onclick="showRegister()">Register</a></p>
        </div>
        
        <div id="register-form" style="display:none">
            <h3>Register</h3>
            <input type="text" id="reg-name" placeholder="Full Name" style="width:100%;padding:12px;margin:10px 0;border:1px solid #ddd;border-radius:5px">
            <input type="email" id="reg-email" placeholder="Email" style="width:100%;padding:12px;margin:10px 0;border:1px solid #ddd;border-radius:5px">
            <input type="password" id="reg-password" placeholder="Password" style="width:100%;padding:12px;margin:10px 0;border:1px solid #ddd;border-radius:5px">
            <button onclick="register()" style="width:100%;padding:12px;background:var(--primary);color:white;border:none;border-radius:5px;margin:10px 0">Register</button>
            <p style="text-align:center">Already have account? <a href="#" onclick="showLogin()">Login</a></p>
        </div>
    </div>
    
    <!-- Main Chat Interface -->
    <div id="chat-screen" style="display:none">
        <header>
            <h1>Deepshock AI</h1>
            <div>
                <button id="dark-mode-btn" style="background:transparent;color:white;border:1px solid white;padding:5px 10px;margin-right:10px">Dark Mode</button>
                <button id="logout-btn" style="background:white;color:var(--primary);border:none;padding:8px 15px;border-radius:5px">Logout</button>
            </div>
        </header>
        
        <div class="chat-container" id="chat-messages">
            <div class="welcome-message">
                <h2>Hi, I'm Deepshock</h2>
                <p>How can I help you today?</p>
            </div>
            
            <div class="feature-buttons">
                <button class="action-btn primary-btn">DeepThink (R1)</button>
                <button class="action-btn secondary-btn">Search Web</button>
                <button id="voice-btn" class="action-btn secondary-btn">🎤 Voice Input</button>
                <button id="read-btn" class="action-btn secondary-btn">🔊 Read Aloud</button>
                <button id="video-btn" class="action-btn secondary-btn">🎥 Video to Text</button>
                <button id="text-video-btn" class="action-btn secondary-btn">📝 Text to Video</button>
            </div>
            
            <div id="video-container">
                <video id="video-preview" controls></video>
                <button id="analyze-video" class="action-btn primary-btn" style="margin-top:10px">Analyze Video</button>
            </div>
        </div>
        
        <div class="input-container">
            <input type="text" id="user-input" placeholder="Type your message...">
            <button id="send-btn">Send</button>
        </div>
    </div>

    <script>
        // ======================
        // Authentication System
        // ======================
        let currentUser = null;
        const users = JSON.parse(localStorage.getItem('deepshock_users')) || [];
        
        function showRegister() {
            document.getElementById('login-form').style.display = 'none';
            document.getElementById('register-form').style.display = 'block';
        }
        
        function showLogin() {
            document.getElementById('register-form').style.display = 'none';
            document.getElementById('login-form').style.display = 'block';
        }
        
        function login() {
            const email = document.getElementById('login-email').value;
            const password = document.getElementById('login-password').value;
            
            const user = users.find(u => u.email === email && u.password === password);
            
            if (user) {
                currentUser = user;
                document.getElementById('auth-screen').style.display = 'none';
                document.getElementById('chat-screen').style.display = 'block';
                addMessage(`Welcome back, ${user.name}!`, 'bot');
            } else {
                alert('Invalid credentials');
            }
        }
        
        function register() {
            const name = document.getElementById('reg-name').value;
            const email = document.getElementById('reg-email').value;
            const password = document.getElementById('reg-password').value;
            
            if (users.some(u => u.email === email)) {
                alert('Email already registered');
                return;
            }
            
            const newUser = { name, email, password };
            users.push(newUser);
            localStorage.setItem('deepshock_users', JSON.stringify(users));
            
            alert('Registration successful! Please login');
            showLogin();
        }
        
        // ======================
        // Chat Functionality
        // ======================
        function addMessage(text, sender) {
            const chatMessages = document.getElementById('chat-messages');
            const msgDiv = document.createElement('div');
            msgDiv.className = `message ${sender}-message`;
            msgDiv.textContent = text;
            chatMessages.appendChild(msgDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }
        
        async function sendMessage() {
            const message = document.getElementById('user-input').value.trim();
            if (!message) return;
            
            addMessage(message, 'user');
            document.getElementById('user-input').value = '';
            
            // Show typing indicator
            const typingIndicator = document.createElement('div');
            typingIndicator.className = 'message bot-message';
            typingIndicator.textContent = 'Deepshock is typing...';
            typingIndicator.id = 'typing-indicator';
            document.getElementById('chat-messages').appendChild(typingIndicator);
            
            try {
                // Simulated AI response
                const response = await simulateAIResponse(message);
                
                // Remove typing indicator
                document.getElementById('typing-indicator').remove();
                
                addMessage(response, 'bot');
            } catch (error) {
                document.getElementById('typing-indicator').remove();
                addMessage("Sorry, I encountered an error. Please try again.", 'bot');
            }
        }
        
        async function simulateAIResponse(message) {
            return new Promise(resolve => {
                setTimeout(() => {
                    const responses = [
                        `I'm Deepshock AI. You asked: "${message}". Can you elaborate?`,
                        "Interesting question! According to my knowledge...",
                        "I've analyzed your query. Here's what I found...",
                        "Let me think about that... Here's my response."
                    ];
                    resolve(responses[Math.floor(Math.random()*responses.length)]);
                }, 1500);
            });
        }
        
        // ======================
        // Multimedia Features
        // ======================
        
        // Voice to Text
        const voiceBtn = document.getElementById('voice-btn');
        let recognition;
        
        if ('webkitSpeechRecognition' in window) {
            recognition = new webkitSpeechRecognition();
            recognition.continuous = false;
            recognition.interimResults = false;
            
            recognition.onresult = (event) => {
                const transcript = event.results[0][0].transcript;
                document.getElementById('user-input').value = transcript;
                voiceBtn.classList.remove('recording');
            };
            
            recognition.onerror = () => {
                voiceBtn.classList.remove('recording');
                addMessage("Voice input failed", 'bot');
            };
        }
        
        voiceBtn.addEventListener('click', () => {
            if (!recognition) {
                addMessage("Voice recognition not supported in your browser", 'bot');
                return;
            }
            
            if (voiceBtn.classList.contains('recording')) {
                recognition.stop();
                voiceBtn.classList.remove('recording');
            } else {
                recognition.start();
                voiceBtn.classList.add('recording');
                addMessage("Listening... Speak now", 'bot');
            }
        });
        
        // Text to Speech
        const readBtn = document.getElementById('read-btn');
        readBtn.addEventListener('click', () => {
            const messages = document.querySelectorAll('.bot-message');
            const lastBotMessage = messages[messages.length - 1]?.textContent;
            
            if (lastBotMessage && 'speechSynthesis' in window) {
                const utterance = new SpeechSynthesisUtterance(lastBotMessage);
                window.speechSynthesis.speak(utterance);
            } else {
                addMessage("Text-to-speech not supported", 'bot');
            }
        });
        
        // Video to Text
        const videoBtn = document.getElementById('video-btn');
        const videoPreview = document.getElementById('video-preview');
        const videoContainer = document.getElementById('video-container');
        const analyzeVideoBtn = document.getElementById('analyze-video');
        let videoStream;
        
        videoBtn.addEventListener('click', async () => {
            try {
                videoStream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
                videoPreview.srcObject = videoStream;
                videoPreview.muted = true;
                videoContainer.style.display = 'block';
                addMessage("Video recording started. Click 'Analyze' when ready", 'bot');
            } catch (error) {
                addMessage("Couldn't access camera/microphone: " + error.message, 'bot');
            }
        });
        
        analyzeVideoBtn.addEventListener('click', () => {
            // In real implementation, send video to API
            addMessage("Analyzing video... (simulated)", 'bot');
            setTimeout(() => {
                addMessage("Detected: Person speaking about AI technology", 'bot');
                stopVideo();
            }, 2000);
        });
        
        function stopVideo() {
            if (videoStream) {
                videoStream.getTracks().forEach(track => track.stop());
                videoPreview.srcObject = null;
                videoContainer.style.display = 'none';
            }
        }
        
        // Text to Video (Simulated)
        const textVideoBtn = document.getElementById('text-video-btn');
        textVideoBtn.addEventListener('click', () => {
            const input = prompt("Enter text to generate video:");
            if (input) {
                addMessage(`Generating video for: "${input}"`, 'bot');
                setTimeout(() => {
                    addMessage("Video generated! (simulated)", 'bot');
                    addMessage("In production, this would return a video URL", 'bot');
                }, 2000);
            }
        });
        
        // ======================
        // UI Features
        // ======================
        document.getElementById('dark-mode-btn').addEventListener('click', function() {
            document.body.classList.toggle('dark-mode');
            this.textContent = document.body.classList.contains('dark-mode') ? 'Light Mode' : 'Dark Mode';
        });
        
        document.getElementById('logout-btn').addEventListener('click', function() {
            if (confirm('Are you sure you want to logout?')) {
                currentUser = null;
                document.getElementById('chat-screen').style.display = 'none';
                document.getElementById('auth-screen').style.display = 'block';
                stopVideo();
            }
        });
        
        document.getElementById('send-btn').addEventListener('click', sendMessage);
        document.getElementById('user-input').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') sendMessage();
        });
        
        // Action buttons
        document.querySelectorAll('.action-btn').forEach(btn => {
            if (!btn.id) { // Skip buttons with existing functionality
                btn.addEventListener('click', function() {
                    addMessage(`${this.textContent} feature activated`, 'bot');
                });
            }
        });
    </script>
</body>
</html>
