<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms. P's Daily Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-accent: #f72585; /* Vibrant Pink */
            --secondary-accent: #4cc9f0; /* Vibrant Blue/Cyan */
            --text-light: #f0f0f0;
            --text-secondary: #adb5bd;
            --card-bg: rgba(0, 0, 0, 0.4); /* Darker, more black card background */
            --card-border: rgba(255, 255, 255, 0.15);
            --glow-shadow-primary: 0 0 15px rgba(247, 37, 133, 0.6);
            --glow-shadow-secondary: 0 0 15px rgba(76, 201, 240, 0.6);
            --red-accent: #e53935;
            --green-accent: #34c759;
        }

        *, *::before, *::after {
            box-sizing: border-box;
        }

        /* --- Animated Background --- */
        @keyframes animateBackground {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        body {
            font-family: 'Poppins', sans-serif;
            /* Animated gradient combining original and TikTok colors */
            background: linear-gradient(-45deg, #000000, #1d0c33, #f72585, #4cc9f0, #3a0ca3);
            background-size: 400% 400%;
            animation: animateBackground 20s ease infinite;
            background-attachment: fixed;
            color: var(--text-light);
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 20px auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            padding-bottom: 20px;
            margin-bottom: 30px;
        }
        
        .header .date-display {
            font-size: 3em;
            font-weight: 700;
            margin: 0;
            color: #fff;
            text-shadow: 0 0 10px var(--glow-shadow-secondary);
        }

        .header .time-display {
            font-size: 1.8em;
            font-weight: 600;
            margin: 5px 0 0;
            color: #fff;
            text-shadow: 0 0 8px var(--glow-shadow-secondary);
        }
        
        .header .subtitle {
            color: var(--text-secondary);
            margin: 10px 0 0;
            font-size: 1.2em;
            font-weight: 400;
        }
        
        .grid-container {
            display: grid;
            gap: 25px;
            grid-template-columns: repeat(2, 1fr);
        }

        .card {
            background: var(--card-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            padding: 24px;
            border-radius: 16px;
            border: 1px solid var(--card-border);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            display: flex;
            flex-direction: column;
        }

        .card:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: var(--glow-shadow-secondary);
        }

        .card h2 {
            margin-top: 0;
            border-bottom: 2px solid;
            border-image: linear-gradient(to right, var(--primary-accent), var(--secondary-accent)) 1;
            padding-bottom: 12px;
            margin-bottom: 18px;
            color: var(--text-light);
            font-weight: 600;
            display: flex;
            align-items: center;
        }
        
        .card h2 .emoji-icon {
            font-size: 1.2em;
            margin-right: 12px;
        }

        .card textarea {
            width: 100%;
            min-height: 150px;
            padding: 12px;
            background-color: rgba(0, 0, 0, 0.2);
            color: var(--text-light);
            border: 1px solid var(--card-border);
            border-radius: 8px;
            resize: vertical;
            font-family: inherit;
        }

        .rss-item {
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px solid var(--card-border);
        }
        .rss-item:last-child { border-bottom: none; }
        .rss-item a {
            text-decoration: none;
            color: var(--secondary-accent);
            font-weight: 600;
            transition: color 0.3s ease;
        }
        .rss-item a:hover { color: var(--primary-accent); }
        .rss-feed p {
            margin: 5px 0 0;
            color: var(--text-secondary);
            font-size: 0.9em;
        }
        
        .connect-link {
            display: inline-block;
            background: linear-gradient(90deg, var(--primary-accent), #c03089);
            color: white;
            padding: 12px 24px;
            border-radius: 50px;
            text-decoration: none;
            transition: all 0.3s ease;
            font-weight: 600;
            border: none;
            text-align: center;
        }
        
        .connect-link:hover {
            transform: translateY(-2px);
            box-shadow: var(--glow-shadow-primary);
        }
        
        .nyt-link {
            background: transparent;
            border: 1px solid var(--secondary-accent);
            color: var(--secondary-accent);
            padding: 10px 20px;
            border-radius: 50px;
            text-decoration: none;
            transition: all 0.3s ease;
            font-weight: 600;
            display: block;
            margin-top: 10px;
            text-align: center;
        }
        
        .nyt-link:hover {
            background-color: var(--secondary-accent);
            color: #111;
            box-shadow: var(--glow-shadow-secondary);
            transform: translateY(-2px);
        }

        /* Timer Section */
        .timer-card { 
            grid-column: 1 / -1; 
        }
        .timer-display {
            font-size: 4em;
            font-weight: 700;
            color: #fff;
            text-align: center;
            margin-bottom: 15px;
            text-shadow: 0 0 10px var(--glow-shadow-secondary);
        }
        
        .timer-controls {
            display: flex;
            justify-content: center;
            gap: 10px;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }
        
        .timer-btn, .timer-control-btn {
            background-color: transparent;
            color: var(--text-light);
            border: 1px solid var(--card-border);
            padding: 10px 20px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        .timer-btn:hover, .timer-control-btn:hover {
            border-color: var(--secondary-accent);
            color: var(--secondary-accent);
            box-shadow: var(--glow-shadow-secondary);
        }
        .timer-btn.active {
            background-color: var(--secondary-accent);
            color: #111;
            border-color: var(--secondary-accent);
        }

        .timer-progress-bar {
            width: 100%;
            height: 10px;
            background-color: rgba(0, 0, 0, 0.3);
            border-radius: 5px;
            overflow: hidden;
            margin-top: 15px;
        }
        .progress {
            height: 100%;
            background: linear-gradient(90deg, var(--secondary-accent), var(--primary-accent));
            width: 0;
            transition: width 1s linear;
            border-radius: 5px;
        }

        /* Uploader Styles */
        .image-placeholder {
            width: 100%;
            height: 200px;
            border: 2px dashed var(--card-border);
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .image-placeholder:hover {
            border-color: var(--primary-accent);
            color: var(--primary-accent);
            background-color: rgba(247, 37, 133, 0.1);
        }
        .image-placeholder.has-image {
            border: none; padding: 0; overflow: hidden;
        }
        .image-placeholder.has-image img {
            width: 100%; height: 100%; object-fit: contain; border-radius: 8px;
        }
        .remove-btn {
            background-color: var(--red-accent); color: white; border: none; padding: 8px 16px; border-radius: 5px; cursor: pointer; font-size: 14px; margin-top: 10px; display: none; transition: background-color 0.3s ease;
        }
        .remove-btn:hover { background-color: #c62828; }

        /* Gemini Features */
        .gemini-feature {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid var(--card-border);
        }
        .gemini-input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
        }
        .gemini-input {
            flex-grow: 1;
            background-color: rgba(0,0,0,0.2);
            border: 1px solid var(--card-border);
            color: var(--text-light);
            border-radius: 8px;
            padding: 10px;
        }
        .gemini-btn {
            background: linear-gradient(90deg, var(--green-accent), #2a9d8f);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
        }
        .gemini-btn:hover {
             transform: translateY(-2px);
             box-shadow: 0 0 10px rgba(52, 199, 89, 0.5);
        }
        .gemini-result-box {
            background-color: rgba(0,0,0,0.2);
            border: 1px solid var(--card-border);
            border-radius: 8px;
            padding: 15px;
            margin-top: 10px;
            min-height: 50px;
        }
        .loader {
            text-align: center;
            padding: 10px;
            display: none;
        }
         #generate-prompt-btn {
            display: none; /* Hidden until an image is uploaded */
            margin-top: 10px;
            width: 100%;
        }

        /* Agenda Styles */
        .agenda-item {
            background-color: rgba(0,0,0,0.2);
            border: 1px solid var(--card-border);
            border-radius: 8px;
            padding: 10px 15px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .delete-item-btn {
            background-color: transparent;
            color: var(--text-secondary);
            border: none;
            cursor: pointer;
            font-size: 1.2em;
            padding: 5px;
        }
        .delete-item-btn:hover { color: var(--red-accent); }
        .add-item-btn {
            width: 100%;
            background: transparent;
            border: 1px solid var(--card-border);
            color: var(--text-secondary);
            font-weight: 600;
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .add-item-btn:hover {
            background-color: var(--secondary-accent);
            color: #111;
            border-color: var(--secondary-accent);
        }

        @media (max-width: 768px) {
            .container { padding: 15px; }
            .header .date-display { font-size: 2.2em; }
            .header .time-display { font-size: 1.5em; }
            .grid-container { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1 class="date-display"><span id="currentDate"></span></h1>
            <p class="time-display"><span id="currentTime"></span></p>
            <p class="subtitle">Ms. P's Daily Hub</p>
        </div>

        <div class="grid-container">
            <!-- Row 1 -->
            <div class="card">
                <h2><span class="emoji-icon">📋</span>Today's Agenda</h2>
                <div id="agenda-list"></div>
                <button class="add-item-btn" id="add-agenda-btn">+ Add Item</button>
            </div>
            <div class="card">
                <h2><span class="emoji-icon">🧠</span>Learning Objective</h2>
                <textarea id="learningObjective" placeholder="Type today's learning objective..."></textarea>
            </div>

            <!-- Row 2 -->
            <div class="card">
                <h2><span class="emoji-icon">🤝</span>Check and Connect</h2>
                <textarea id="doNow" placeholder="Enter the 'Do Now' activity..."></textarea>
                <div style="margin-top: auto;">
                    <a href="https://edtomorrow.com" target="_blank" class="connect-link">Go to edtomorrow.com</a>
                </div>
            </div>
            <div class="card">
                <h2><span class="emoji-icon">😂</span> Daily Drop</h2>
                <div class="image-placeholder" id="meme-placeholder">
                    <input type="file" id="memeInput" style="display: none;" accept="image/*">
                    <p>Click to upload a meme or photo!</p>
                </div>
                <button id="removeMemeBtn" class="remove-btn">Remove Photo</button>
                <div class="gemini-feature">
                    <button id="generate-prompt-btn" class="gemini-btn">✨ Generate Writing Prompt</button>
                    <div class="loader">Analyzing image...</div>
                    <div class="gemini-result-box" id="prompt-result" style="display: none;"></div>
                </div>
            </div>

            <!-- Row 3 -->
            <div class="card">
                <h2><span class="emoji-icon">🏛️</span>On This Day</h2>
                <p>Discover historical events and educational facts from today's date.</p>
                <a href="https://www.britannica.com/on-this-day" target="_blank" class="nyt-link">On This Day</a>
                <a href="https://www.britannica.com/one-good-fact" target="_blank" class="nyt-link">One Good Fact</a>
            </div>
            <div class="card">
                <h2><a href="https://thekidshouldseethis.com/" target="_blank" style="color: inherit; text-decoration: none; display: flex; align-items: center;"><span class="emoji-icon">📺</span>The Kids Should See This</a></h2>
                <div id="rss-feed" class="rss-feed">
                    <p>Loading the latest educational videos...</p>
                </div>
                <a href="https://ed.ted.com/" target="_blank" class="nyt-link">TED-Ed Videos</a>
            </div>
            
            <!-- Row 4 -->
            <div class="card">
                <h2><a href="https://www.nytimes.com/section/learning" target="_blank" style="color: inherit; text-decoration: none; display: flex; align-items: center;"><span class="emoji-icon">🗞️</span>NYT Learning Network</a></h2>
                <a href="https://www.nytimes.com/column/learning-student-opinion" target="_blank" class="nyt-link">Student Opinion Questions</a>
                <a href="https://www.nytimes.com/spotlight/accessible-activities" target="_blank" class="nyt-link">Picture Prompts</a>
                <a href="https://www.nytimes.com/column/learning-word-of-the-day" target="_blank" class="nyt-link">Word of the Day</a>
                <a href="https://www.nytimes.com/spotlight/learning-contests" target="_blank" class="nyt-link">Contests</a>
            </div>

            <!-- Row 5 (Full Width) -->
            <div class="card timer-card">
                <h2><span class="emoji-icon">⏱️</span>Class Timer</h2>
                <div class="timer-display" id="timerDisplay">00:00</div>
                <div class="timer-controls">
                    <button class="timer-btn" data-time="300">5 min</button>
                    <button class="timer-btn" data-time="600">10 min</button>
                    <button class="timer-btn" data-time="900">15 min</button>
                </div>
                <div class="timer-controls">
                    <button class="timer-control-btn" id="start-btn">Start</button>
                    <button class="timer-control-btn" id="pause-btn">Pause</button>
                    <button class="timer-control-btn" id="reset-btn">Reset</button>
                </div>
                <div class="timer-progress-bar">
                    <div class="progress" id="progressBar"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
    document.addEventListener('DOMContentLoaded', function () {
        const AGENDA_KEY = 'dailyHubAgenda';

        // --- 1. INITIALIZATION ---
        updateDateTime();
        setInterval(updateDateTime, 1000);
        initializeTimer();
        initializeMemeUploader();
        fetchRssFeed();
        loadSavedContent();
        initializeAgenda();
        initializeGeminiFeatures();

        // --- 2. UI & BASIC FUNCTIONALITY ---
        function updateDateTime() {
            const now = new Date();
            const dateOptions = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const timeOptions = { hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: true };
            document.getElementById('currentDate').textContent = now.toLocaleDateString('en-US', dateOptions);
            document.getElementById('currentTime').textContent = now.toLocaleTimeString('en-US', timeOptions);
        }

        function initializeTimer() {
            let timer;
            let totalTime;
            let timeLeft;
            let isPaused = false;
            let isRunning = false;
            const timerDisplay = document.getElementById('timerDisplay');
            const progressBar = document.getElementById('progressBar');
            const startBtn = document.getElementById('start-btn');
            const pauseBtn = document.getElementById('pause-btn');
            const resetBtn = document.getElementById('reset-btn');
            const timerButtons = document.querySelectorAll('.timer-btn');

            function formatTime(seconds) {
                if (typeof seconds !== 'number' || seconds < 0) return '00:00';
                const minutes = Math.floor(seconds / 60);
                const remainingSeconds = seconds % 60;
                return `${String(minutes).padStart(2, '0')}:${String(remainingSeconds).padStart(2, '0')}`;
            }

            function runTimer() {
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    isRunning = false;
                    timerDisplay.textContent = '00:00';
                    progressBar.style.width = '100%';
                    new Audio("data:audio/wav;base64,UklGRl9vT19XQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YU"+Array(300).join("12345678")).play();
                    return;
                }
                timeLeft--;
                timerDisplay.textContent = formatTime(timeLeft);
                const progress = ((totalTime - timeLeft) / totalTime) * 100;
                progressBar.style.width = `${progress}%`;
            }

            startBtn.addEventListener('click', () => {
                if ((!isRunning || isPaused) && timeLeft > 0) {
                    isRunning = true;
                    isPaused = false;
                    timer = setInterval(runTimer, 1000);
                }
            });

            pauseBtn.addEventListener('click', () => {
                if (isRunning && !isPaused) {
                    clearInterval(timer);
                    isPaused = true;
                }
            });

            resetBtn.addEventListener('click', () => {
                clearInterval(timer);
                isRunning = false;
                isPaused = false;
                timeLeft = totalTime || 0;
                timerDisplay.textContent = formatTime(timeLeft);
                progressBar.style.width = '0%';
            });

            timerButtons.forEach(button => {
                button.addEventListener('click', () => {
                    clearInterval(timer);
                    const timeInSeconds = parseInt(button.getAttribute('data-time'));
                    timeLeft = timeInSeconds;
                    totalTime = timeInSeconds;
                    timerDisplay.textContent = formatTime(timeLeft);
                    progressBar.style.width = '0%';
                    timerButtons.forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                    isRunning = false;
                    isPaused = false;
                });
            });
        }
        
        function initializeMemeUploader() {
            const memePlaceholder = document.getElementById('meme-placeholder');
            const memeInput = document.getElementById('memeInput');
            const removeMemeBtn = document.getElementById('removeMemeBtn');
            const genPromptBtn = document.getElementById('generate-prompt-btn');
            const promptResultBox = document.getElementById('prompt-result');

            memePlaceholder.addEventListener('click', () => memeInput.click());

            memeInput.addEventListener('change', function() {
                if (this.files && this.files[0]) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        displayImage(e.target.result);
                    };
                    reader.readAsDataURL(this.files[0]);
                }
            });

            removeMemeBtn.addEventListener('click', () => {
                memePlaceholder.innerHTML = `<p>Click to upload a meme or photo!</p>`;
                memePlaceholder.classList.remove('has-image');
                memeInput.value = '';
                removeMemeBtn.style.display = 'none';
                genPromptBtn.style.display = 'none';
                promptResultBox.style.display = 'none';
            });
        }
        
        function displayImage(imageUrl) {
            const memePlaceholder = document.getElementById('meme-placeholder');
            const removeMemeBtn = document.getElementById('removeMemeBtn');
            const genPromptBtn = document.getElementById('generate-prompt-btn');
            memePlaceholder.innerHTML = `<img src="${imageUrl}" alt="Uploaded Meme">`;
            memePlaceholder.classList.add('has-image');
            removeMemeBtn.style.display = 'block';
            genPromptBtn.style.display = 'block';
        }

        async function fetchRssFeed() {
            const feedContainer = document.getElementById('rss-feed');
            const rssUrl = 'https://thekidshouldseethis.com/feed';
            const proxyUrl = `https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(rssUrl)}`;
            try {
                const response = await fetch(proxyUrl);
                const data = await response.json();
                if (data.status === 'ok') {
                    feedContainer.innerHTML = '';
                    data.items.slice(0, 4).forEach(item => {
                        const itemEl = document.createElement('div');
                        itemEl.className = 'rss-item';
                        itemEl.innerHTML = `<a href="${item.link}" target="_blank">${item.title}</a><p>Published: ${new Date(item.pubDate).toLocaleDateString()}</p>`;
                        feedContainer.appendChild(itemEl);
                    });
                }
            } catch (error) {
                feedContainer.innerHTML = '<p>Could not load feed.</p>';
            }
        }
        
        function loadSavedContent() {
            // Auto-save content as user types
            document.getElementById('learningObjective').addEventListener('input', (e) => {
                // Content persists during session
            });
            document.getElementById('doNow').addEventListener('input', (e) => {
                // Content persists during session  
            });
        }

        // --- 3. AGENDA FUNCTIONALITY ---
        function initializeAgenda() {
            // Initialize agenda items array
            let agendaItems = [];
            const addBtn = document.getElementById('add-agenda-btn');
            addBtn.addEventListener('click', () => {
                const text = prompt("Enter new agenda item:");
                if (text && text.trim() !== "") {
                    agendaItems.push({ id: Date.now(), text: text.trim() });
                    renderAgenda();
                }
            });
            
            function renderAgenda() {
                const list = document.getElementById('agenda-list');
                list.innerHTML = '';
                if (agendaItems.length === 0) {
                    list.innerHTML = `<p style="color: var(--text-secondary);">No agenda items yet.</p>`;
                } else {
                    agendaItems.forEach(item => {
                        const itemEl = document.createElement('div');
                        itemEl.className = 'agenda-item';
                        itemEl.innerHTML = `<span>${item.text}</span><button class="delete-item-btn" data-id="${item.id}">&times;</button>`;
                        list.appendChild(itemEl);
                    });
                }
                // Add event listeners to new delete buttons
                document.querySelectorAll('.delete-item-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        const idToDelete = parseInt(e.target.dataset.id);
                        agendaItems = agendaItems.filter(item => item.id !== idToDelete);
                        renderAgenda();
                    });
                });
            }
            
            renderAgenda();
        }

        // --- 4. GEMINI API FEATURES ---
        async function callGeminiApi(payload, loaderElement, maxRetries = 3) {
            if (loaderElement) loaderElement.style.display = 'block';
            
            // Note: Add your Gemini API key here for the AI features to work
            const apiKey = "YOUR_GEMINI_API_KEY_HERE";
            if (!apiKey || apiKey === "YOUR_GEMINI_API_KEY_HERE") {
                if (loaderElement) loaderElement.style.display = 'none';
                return "Please add your Gemini API key to enable AI features.";
            }
            
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;

            let attempt = 0;
            while (attempt < maxRetries) {
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
                    
                    const result = await response.json();
                    if (loaderElement) loaderElement.style.display = 'none';
                    
                    if (result.candidates && result.candidates[0]?.content?.parts?.[0]?.text) {
                        return result.candidates[0].content.parts[0].text.trim();
                    } else {
                        return `Content blocked or unavailable. Reason: ${result.promptFeedback?.blockReason || 'Unknown'}`;
                    }
                } catch (error) {
                    console.error(`Attempt ${attempt + 1} failed:`, error);
                    attempt++;
                    if (attempt >= maxRetries) {
                        if (loaderElement) loaderElement.style.display = 'none';
                        return "Error: AI assistant is unavailable after multiple retries.";
                    }
                    await new Promise(resolve => setTimeout(resolve, Math.pow(2, attempt) * 1000));
                }
            }
        }

        function initializeGeminiFeatures() {
            document.getElementById('generate-prompt-btn').addEventListener('click', async () => {
                const imageEl = document.querySelector('#meme-placeholder img');
                if (!imageEl || !imageEl.src) return;
                const base64ImageData = imageEl.src.split(',')[1];
                const mimeType = imageEl.src.match(/data:(.*);/)[1];
                const prompt = "Generate a short, creative writing prompt based on this image for a middle school student.";
                const payload = { contents: [{ parts: [{ text: prompt }, { inlineData: { mimeType, data: base64ImageData } }] }] };
                const loader = document.querySelector('#generate-prompt-btn').nextElementSibling;
                const resultBox = document.getElementById('prompt-result');
                resultBox.innerHTML = '';
                const result = await callGeminiApi(payload, loader);
                resultBox.innerHTML = result.replace(/\n/g, '<br>');
                resultBox.style.display = 'block';
            });
        }
    });
    </script>
</body>
</html>
