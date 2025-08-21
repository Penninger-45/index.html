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
            --card-bg: rgba(0, 0, 0, 0.4);
            --card-border: rgba(255, 255, 255, 0.15);
            --glow-shadow-primary: 0 0 15px rgba(247, 37, 133, 0.6);
            --glow-shadow-secondary: 0 0 15px rgba(76, 201, 240, 0.6);
            --red-accent: #e53935;
            --green-accent: #34c759;
        }

        *, *::before, *::after { box-sizing: border-box; }

        @keyframes animateBackground {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(-45deg, #000000, #1d0c33, #f72585, #4cc9f0, #3a0ca3);
            background-size: 400% 400%;
            animation: animateBackground 20s ease infinite;
            background-attachment: fixed;
            color: var(--text-light);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }
        
        .top-header-bar {
            text-align: center;
            padding: 10px 20px;
            background: rgba(0,0,0,0.3);
            backdrop-filter: blur(5px);
            -webkit-backdrop-filter: blur(5px);
            font-weight: 600;
            color: var(--text-light);
            text-shadow: 0 0 5px var(--secondary-accent);
            width: 100%;
            position: sticky;
            top: 0;
            z-index: 1001;
        }

        .container { max-width: 1400px; margin: 0 auto; padding: 20px; position: relative; }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 20px;
            margin-bottom: 30px;
            position: relative;
            flex-wrap: wrap;
            gap: 20px;
        }
        .header-left { text-align: center; flex-grow: 1; }
        .header .subtitle { color: var(--text-light); margin: 0 0 15px 0; font-size: 1.8em; font-weight: 700; text-shadow: 0 0 8px #fff, 0 0 20px var(--primary-accent), 0 0 30px var(--primary-accent); }

        #class-selector {
            -webkit-appearance: none; -moz-appearance: none; appearance: none;
            background-color: var(--card-bg);
            color: var(--text-light);
            border: 1px solid var(--card-border);
            border-radius: 8px;
            padding: 10px 40px 10px 20px;
            font-family: inherit;
            font-size: 1.1em;
            font-weight: 600;
            cursor: pointer;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23adb5bd' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: right 1rem center;
            background-size: 1em;
        }

        .navbar { display: flex; justify-content: center; margin-bottom: 30px; flex-wrap: wrap; gap: 15px; }
        .nav-link { padding: 12px 28px; text-decoration: none; color: var(--text-light); background-color: transparent; border: 1px solid var(--card-border); border-radius: 50px; transition: all 0.3s ease; cursor: pointer; font-weight: 600; }
        .nav-link:hover { transform: translateY(-3px); box-shadow: var(--glow-shadow-primary); border-color: var(--primary-accent); color: var(--primary-accent); }
        .nav-link.active { background: linear-gradient(90deg, var(--primary-accent), var(--secondary-accent)); color: white; border-color: transparent; font-weight: 700; box-shadow: 0 0 15px rgba(247, 37, 133, 0.5); }
        
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        
        .grid-container { display: grid; gap: 25px; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); }
        
        .card { background: var(--card-bg); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); padding: 24px; border-radius: 16px; border: 1px solid var(--card-border); transition: transform 0.3s ease, box-shadow 0.3s ease; display: flex; flex-direction: column; }
        .card:not(.timer-widget-base):hover { transform: translateY(-8px) scale(1.02); box-shadow: var(--glow-shadow-secondary); }
        .card h2 { margin-top: 0; border-bottom: 2px solid; border-image: linear-gradient(to right, var(--primary-accent), var(--secondary-accent)) 1; padding-bottom: 12px; margin-bottom: 18px; color: var(--text-light); font-weight: 600; display: flex; align-items: center; justify-content: space-between; gap: 10px; }
        .card h2 .title-text { display: flex; align-items: center; flex-grow: 1; min-width: 0; }
        .card h2 .emoji-icon { font-size: 1.2em; margin-right: 12px; }
        .card h2 a { color: inherit; text-decoration: none; transition: color 0.3s ease; }
        .card h2 a:hover { color: var(--secondary-accent); }
        .card textarea { width: 100%; min-height: 150px; padding: 12px; background-color: rgba(0, 0, 0, 0.2); color: var(--text-light); border: 1px solid var(--card-border); border-radius: 8px; resize: vertical; font-family: inherit; }
        .connect-link { display: block; background: linear-gradient(90deg, var(--primary-accent), #c03089); color: white; padding: 12px 24px; border-radius: 50px; text-decoration: none; transition: all 0.3s ease; font-weight: 600; border: none; text-align: center; }
        .connect-link:hover { transform: translateY(-2px); box-shadow: var(--glow-shadow-primary); }

        .calculator { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; }
        .calc-display { grid-column: 1 / -1; background-color: rgba(0,0,0,0.3); color: var(--text-light); font-size: 2.5em; padding: 15px; text-align: right; border-radius: 8px; margin-bottom: 10px; word-wrap: break-word; word-break: break-all; }
        .calc-btn { background-color: rgba(255,255,255,0.1); border: 1px solid var(--card-border); color: var(--text-light); font-size: 1.5em; padding: 20px; border-radius: 8px; cursor: pointer; transition: all 0.2s ease; }
        .calc-btn:hover { background-color: rgba(255,255,255,0.2); transform: scale(1.05); }
        .calc-btn.operator { background-color: rgba(76, 201, 240, 0.5); }
        .calc-btn.equals { background-color: rgba(247, 37, 133, 0.5); grid-column: span 2; }

        .link-list a { display: block; background: rgba(0,0,0,0.2); padding: 15px; margin-bottom: 10px; border-radius: 8px; text-decoration: none; color: var(--text-secondary); font-weight: 600; transition: all 0.3s ease; }
        .link-list a:hover { color: var(--text-light); background: var(--primary-accent); transform: translateX(10px); }

        .image-placeholder { width: 100%; height: 200px; border: 2px dashed var(--card-border); border-radius: 8px; display: flex; flex-direction: column; justify-content: center; align-items: center; color: var(--text-secondary); cursor: pointer; transition: all 0.3s ease; }
        .image-placeholder:hover { border-color: var(--primary-accent); color: var(--primary-accent); }
        .image-placeholder.has-image { border: none; padding: 0; overflow: hidden; }
        .image-placeholder.has-image img { width: 100%; height: 100%; object-fit: contain; border-radius: 8px; }
        .remove-btn { background-color: var(--red-accent); color: white; border: none; padding: 8px 16px; border-radius: 50px; cursor: pointer; font-size: 14px; margin-top: 10px; display: none; transition: all 0.3s ease; }
        .remove-btn:hover { transform: translateY(-2px); box-shadow: 0 0 10px var(--red-accent); }

        .card-footer-action { margin-top: auto; padding-top: 15px; border-top: 1px solid var(--card-border); }
        .action-input-group { display: flex; gap: 10px; align-items: center; }
        .action-input { flex-grow: 1; background-color: rgba(0,0,0,0.2); border: 1px solid var(--card-border); color: var(--text-light); border-radius: 8px; padding: 10px; font-family: 'Poppins', sans-serif; font-size: 1em; }
        select.action-input { -webkit-appearance: none; -moz-appearance: none; appearance: none; background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23adb5bd' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e"); background-repeat: no-repeat; background-position: right 1rem center; background-size: 1em; padding-right: 2.5rem; }
        .action-btn { background: linear-gradient(90deg, var(--green-accent), #2a9d8f); color: white; border: none; padding: 10px 15px; border-radius: 8px; cursor: pointer; font-weight: 600; transition: all 0.3s ease; }
        .action-btn:hover { transform: translateY(-2px); box-shadow: 0 0 10px rgba(52, 199, 89, 0.5); }
        .gemini-result-box { background-color: rgba(0,0,0,0.2); border: 1px solid var(--card-border); border-radius: 8px; padding: 15px; margin-top: 10px; min-height: 50px; }
        .loader { text-align: center; padding: 10px; display: none; }
        #generate-prompt-btn { display: none; margin-top: 10px; width: 100%; }

        .agenda-item { background-color: rgba(0,0,0,0.2); border: 1px solid var(--card-border); border-radius: 8px; padding: 10px 15px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; }
        .agenda-item-content img { max-width: 100%; border-radius: 8px; margin-top: 5px; }
        .delete-item-btn { background-color: transparent; color: var(--text-secondary); border: none; cursor: pointer; font-size: 1.2em; padding: 5px; }
        .delete-item-btn:hover { color: var(--red-accent); }
        #custom-agenda-group { display: none; margin-top: 10px; }
        
        .clear-btn { background: transparent; border: 1px solid var(--card-border); color: var(--text-secondary); font-size: 0.7em; padding: 4px 8px; border-radius: 50px; cursor: pointer; transition: all 0.3s ease; flex-shrink: 0; }
        .clear-btn:hover { color: var(--red-accent); border-color: var(--red-accent); }
        
        /* --- Dynamic Timer Widget --- */
        .timer-widget-base { transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        .timer-widget-static { width: 160px; padding: 12px; }
        .timer-widget-static .timer-display { font-size: 1.8em; }
        .timer-widget-static .timer-controls, .timer-widget-static .timer-progress-bar { display: none; }

        .timer-widget-active { width: 280px; padding: 20px; box-shadow: var(--glow-shadow-secondary), 0 8px 32px rgba(0, 0, 0, 0.4) !important; }
        .timer-widget-active .timer-display { font-size: 2.2em; }
        .timer-widget-active .timer-controls { display: flex; }
        .timer-widget-active .timer-progress-bar { display: block; }
        
        .timer-widget-base .timer-display { font-weight: 700; margin-bottom: 12px; text-align: center; color: var(--text-light); text-shadow: 0 0 10px var(--secondary-accent); }
        .timer-presets { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 10px; justify-content: center; }
        .timer-widget-base .timer-controls { flex-wrap: wrap; gap: 6px; margin-bottom: 10px; justify-content: center; }
        .timer-widget-base .timer-progress-bar { width: 100%; height: 4px; background-color: rgba(255, 255, 255, 0.2); border-radius: 2px; overflow: hidden; margin-top: 10px; }
        .timer-widget-base .progress { height: 100%; width: 0%; background: linear-gradient(90deg, var(--primary-accent), var(--secondary-accent)); border-radius: 2px; transition: width 1s linear; }
        
        .timer-btn, .timer-control-btn { padding: 6px 12px; font-size: 0.8em; background: rgba(255, 255, 255, 0.1); color: var(--text-light); border: 1px solid var(--card-border); border-radius: 6px; cursor: pointer; transition: all 0.2s ease; font-weight: 500; }
        .timer-btn:hover, .timer-control-btn:hover { background: var(--secondary-accent); color: #111; transform: translateY(-1px); }
        .timer-btn.active { background: var(--primary-accent); color: white; border-color: var(--primary-accent); }
        
        .rss-item { margin-bottom: 15px; padding-bottom: 15px; border-bottom: 1px solid var(--card-border); }
        .rss-item:last-child { border-bottom: none; }
        .rss-item a { text-decoration: none; color: var(--secondary-accent); font-weight: 600; transition: color 0.3s ease; }
        .rss-item a:hover { color: var(--primary-accent); }
        .rss-feed p { margin: 5px 0 0; color: var(--text-secondary); font-size: 0.9em; }

        /* --- Archive Styles --- */
        #archive-display h2 { border-bottom: 2px solid var(--primary-accent); padding-bottom: 10px; margin-top: 20px; }
        .archive-class-grid { display: grid; gap: 20px; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); }
        .archive-entry { padding: 15px; font-size: 0.9em; }
        .archive-entry h4 { margin-top: 0; color: var(--primary-accent); font-size: 1.1em; }
        .archive-entry h5 { color: var(--secondary-accent); border-bottom: 1px solid var(--secondary-accent); padding-bottom: 3px; margin-top: 10px; margin-bottom: 5px; font-size: 1em; }
        .archive-entry p, .archive-entry ul { margin-top: 0; font-size: 0.95em; }
        .archive-entry ul { list-style-type: disc; padding-left: 20px; }
        #github-publish-section { margin-top: 40px; padding-top: 20px; border-top: 2px solid var(--card-border); }
        #github-publish-section textarea { width: 100%; min-height: 250px; font-family: monospace; font-size: 0.9em; }
        
        /* --- Notification Styles --- */
        .notification {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(90deg, var(--green-accent), #2a9d8f);
            color: white;
            padding: 15px 25px;
            border-radius: 50px;
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.5s, visibility 0.5s, bottom 0.5s;
            font-weight: 600;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .notification.show {
            opacity: 1;
            visibility: visible;
            bottom: 40px;
        }
    </style>
</head>
<body>
    <div class="top-header-bar" id="top-header-bar"></div>

    <div class="container">
        <div class="header">
            <div class="header-left">
                <h2 class="subtitle">Ms. P's Daily Hub</h2>
                <select id="class-selector">
                    <option value="Lit Basics">Lit Basics</option>
                    <option value="Study Skills">Study Skills</option>
                    <option value="Math Essentials 2/3">Math Essentials 2/3</option>
                    <option value="Advocacy">Advocacy</option>
                </select>
            </div>
            <div class="card timer-widget-base timer-widget-static" id="timer-widget">
                <h2 style="font-size: 0.9em; margin: 0 0 8px 0; border: none; padding: 0;"><span class="title-text"><span class="emoji-icon">⏱️</span>Timer</span></h2>
                <div class="timer-display" id="timerDisplay">00:00</div>
                <div class="timer-presets">
                    <button class="timer-btn" data-time="300">5min</button>
                    <button class="timer-btn" data-time="600">10min</button>
                    <button class="timer-btn" data-time="900">15min</button>
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

        <nav class="navbar">
            <a href="#" class="nav-link active" data-tab="home">Home</a>
            <a href="#" class="nav-link" data-tab="resources">Resources</a>
            <a href="#" class="nav-link" data-tab="game-links">Game Links</a>
            <a href="#" class="nav-link" data-tab="teacher-tools">Teacher Tools</a>
            <a href="#" class="nav-link" data-tab="archive">Daily Archive</a>
        </nav>

        <!-- Home Tab -->
        <div id="home" class="tab-content active">
            <div class="grid-container">
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">📋</span>Today's Agenda</span></h2>
                    <div id="agenda-list" style="flex-grow: 1;"></div>
                    <div class="card-footer-action">
                        <div class="action-input-group">
                            <select id="agenda-preset-select" class="action-input">
                                <option value="" disabled selected>Add an item...</option>
                                <option value="Do Now: Math Warm-ups">Do Now: Math Warm-ups</option>
                                <option value="Do Now: Weekly Word Wizard">Do Now: Weekly Word Wizard</option>
                                <option value="Direct Instruction">Direct Instruction</option>
                                <option value="Group Work">Group Work</option>
                                <option value="Independent Practice">Independent Practice</option>
                                <option value="Exit Ticket">Exit Ticket</option>
                                <option value="custom">Custom Item...</option>
                            </select>
                            <button id="add-agenda-item-btn" class="action-btn">Add</button>
                        </div>
                        <div id="custom-agenda-group">
                            <input type="text" id="custom-agenda-input" class="action-input" placeholder="Enter custom text...">
                        </div>
                        <div class="action-input-group" style="margin-top: 10px;">
                             <button id="add-agenda-image-btn" class="action-btn" style="width:100%; background: var(--secondary-accent);">Add Image</button>
                             <input type="file" id="agenda-image-input" style="display: none;" accept="image/*">
                        </div>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🧠</span>Learning Objective</span> <button id="clear-objective-btn" class="clear-btn">Clear</button></h2>
                    <textarea id="learningObjective" placeholder="Type or generate..."></textarea>
                    <div class="card-footer-action">
                        <div class="action-input-group">
                            <input type="text" id="objective-topic" class="action-input" placeholder="Enter a topic...">
                            <button id="generate-objective-btn" class="action-btn gemini-btn">✨ Generate</button>
                        </div>
                        <div class="loader" id="objective-loader">Generating...</div>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🤝</span>Check and Connect</span> <button id="clear-donow-btn" class="clear-btn">Clear</button></h2>
                    <textarea id="doNow" placeholder="Enter or generate a 'Do Now'..."></textarea>
                    <div class="card-footer-action">
                         <button id="generate-donow-btn" class="action-btn gemini-btn" style="width: 100%;">✨ Generate Daily Question</button>
                        <div class="loader" id="donow-loader">Generating...</div>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">😂</span> Daily Drop</span></h2>
                    <div class="image-placeholder" id="daily-drop-placeholder">
                        <input type="file" id="daily-drop-input" style="display: none;" accept="image/*">
                        <p>Click to upload a photo!</p>
                    </div>
                    <button id="remove-daily-drop-btn" class="remove-btn">Remove Photo</button>
                    <div class="card-footer-action">
                        <button id="generate-prompt-btn" class="action-btn gemini-btn">✨ Generate Writing Prompt</button>
                        <div class="loader" id="prompt-loader">Analyzing...</div>
                        <div class="gemini-result-box" id="prompt-result" style="display: none;"></div>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🏛️</span>On This Day</span></h2>
                    <div style="margin-bottom: auto;">
                        <a href="https://www.britannica.com/on-this-day" target="_blank" class="connect-link">On This Day</a>
                        <a href="https://www.britannica.com/one-good-fact" target="_blank" class="connect-link" style="background: linear-gradient(90deg, #4cc9f0, #2575fc); margin-top: 10px;">One Good Fact</a>
                    </div>
                    <p style="margin-top: 20px; color: var(--text-secondary);">Explore historical events and interesting facts for today's date from Britannica.</p>
                </div>
                 <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">📰</span><a href="https://thekidshouldseethis.com/" target="_blank">The Kids Should See This</a></span></h2>
                    <div class="link-list" style="margin-top:auto;">
                        <a href="https://thekidshouldseethis.com/music" target="_blank">Music</a>
                        <a href="https://thekidshouldseethis.com/art" target="_blank">Art</a>
                        <a href="https://thekidshouldseethis.com/tagged/humor" target="_blank">Funny</a>
                        <a href="https://thekidshouldseethis.com/tagged/stop-motion" target="_blank">Stop-Motion</a>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🎓</span>TED-Ed Videos</span></h2>
                    <p>Explore engaging educational videos covering science, history, literature, and more.</p>
                    <div class="link-list" style="margin-top:auto;">
                        <a href="https://ed.ted.com/?popular=1" target="_blank">Popular Lessons</a>
                        <a href="https://ed.ted.com/?category=mathematics" target="_blank">Mathematics</a>
                        <a href="https://ed.ted.com/?category=literature-language" target="_blank">Literature & Language</a>
                        <a href="https://ed.ted.com/?category=thinking-learning" target="_blank">Thinking & Learning</a>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🗞️</span>NYT Learning Network</span></h2>
                    <div class="link-list" style="margin-top:auto;">
                        <a href="https://www.nytimes.com/column/learning-student-opinion" target="_blank">Student Opinion Questions</a>
                        <a href="https://www.nytimes.com/spotlight/accessible-activities" target="_blank">Picture Prompts</a>
                        <a href="https://www.nytimes.com/column/learning-word-of-the-day" target="_blank">Word of the Day</a>
                        <a href="https://www.nytimes.com/spotlight/learning-contests" target="_blank">Contests</a>
                    </div>
                </div>
            </div>
            <!-- Action Buttons -->
            <div class="grid-container" style="margin-top: 25px; grid-template-columns: 1fr 1fr;">
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">📤</span>Export Today's Plan</span></h2>
                    <p>Copy a formatted version of today's plan to paste into Google Classroom, a doc, or a slide.</p>
                    <button id="copy-for-sharing-btn" class="action-btn" style="width: 100%; margin-top: auto;">Copy for Sharing</button>
                </div>
                 <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">✅</span>Submit for the Record</span></h2>
                    <p>Post today's plan to the Daily Archive for students to view later.</p>
                    <button id="submit-to-archive-btn" class="action-btn" style="width: 100%; background: var(--primary-accent); margin-top: auto;">Submit Today's Plan to Archive</button>
                </div>
            </div>
        </div>

        <div id="resources" class="tab-content"><div class="grid-container"><div class="card"><h2><span class="title-text"><span class="emoji-icon">📚</span>Helpful Links</span></h2><div class="link-list"><a href="https://www.khanacademy.org/" target="_blank">Khan Academy</a><a href="https://www.virtualnerd.com/" target="_blank">Virtual Nerd</a><a href="https://mathantics.com/" target="_blank">Math Antics</a><a href="https://www.ixl.com/" target="_blank">IXL</a><a href="https://www.wewillwrite.com/" target="_blank">WeWillWrite</a><a href="https://www.merriam-webster.com/" target="_blank">Merriam-Webster Dictionary</a><a href="https://newsela.com/" target="_blank">Newsela</a></div></div><div class="card"><h2><span class="title-text"><span class="emoji-icon">🧮</span>Calculator</span></h2><div class="calculator"><div id="calc-display" class="calc-display">0</div><button class="calc-btn operator">C</button><button class="calc-btn operator">+/-</button><button class="calc-btn operator">%</button><button class="calc-btn operator">/</button><button class="calc-btn">7</button><button class="calc-btn">8</button><button class="calc-btn">9</button><button class="calc-btn operator">*</button><button class="calc-btn">4</button><button class="calc-btn">5</button><button class="calc-btn">6</button><button class="calc-btn operator">-</button><button class="calc-btn">1</button><button class="calc-btn">2</button><button class="calc-btn">3</button><button class="calc-btn operator">+</button><button class="calc-btn" style="grid-column: span 2;">0</button><button class="calc-btn">.</button><button class="calc-btn equals">=</button></div></div></div></div>
        <div id="game-links" class="tab-content"><div class="card"><h2><span class="title-text"><span class="emoji-icon">🎮</span>Game Links</span></h2><div class="link-list"><a href="https://kahoot.it/" target="_blank">Kahoot!</a><a href="https://quizizz.com/join" target="_blank">Quizizz</a><a href="https://www.blooket.com/play" target="_blank">Blooket</a><a href="https://quizlet.com/live" target="_blank">Quizlet Live</a><a href="https://www.gimkit.com/join" target="_blank">Gimkit</a><a href="https://www.99math.com/join" target="_blank">99math</a></div></div></div>
        <div id="teacher-tools" class="tab-content">
            <div class="card">
                <h2><span class="title-text"><span class="emoji-icon">📝</span>Document Generator</span></h2>
                <p>Select a document type, generate a template, and download it as a text file.</p>
                <select id="doc-type-select" class="action-input" style="margin-bottom: 10px;">
                    <option value="behavior">Behavior Log</option>
                    <option value="parent">Parent Communication</option>
                    <option value="notes">Miscellaneous Notes</option>
                </select>
                <textarea id="doc-generator-textarea" style="min-height: 250px;"></textarea>
                <div class="card-footer-action">
                    <div class="action-input-group">
                        <button id="generate-doc-btn" class="action-btn gemini-btn">✨ Generate Template</button>
                        <button id="download-doc-btn" class="action-btn" style="background: var(--secondary-accent);">📥 Download .txt</button>
                    </div>
                </div>
            </div>
        </div>
        <div id="archive" class="tab-content">
            <div class="card">
                <h2><span class="title-text"><span class="emoji-icon">🗄️</span>Daily Archive</span></h2>
                <p>This is a view-only archive of past lessons. This archive is saved in your browser. New entries are added daily and will remain here unless you clear your browser's cache.</p>
                <div id="archive-display"></div>
                <div id="github-publish-section">
                     <h2><span class="title-text"><span class="emoji-icon">🚀</span>Publish Archive</span></h2>
                    <p>Generate a complete HTML file of the archive to upload to a static website for students and parents to view.</p>
                    <div class="action-input-group" style="margin-bottom: 15px;">
                        <button id="generate-archive-html-btn" class="action-btn" style="width: 50%;">Generate Archive HTML</button>
                        <button id="clear-archive-btn" class="action-btn" style="width: 50%; background: var(--red-accent);">Clear Entire Archive</button>
                    </div>
                    <textarea id="archive-for-github" readonly placeholder="Generated HTML code will appear here..."></textarea>
                </div>
            </div>
        </div>
    </div>
    
    <div id="notification-box" class="notification"></div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // --- GLOBAL STATE & ELEMENTS ---
            const classSelector = document.getElementById('class-selector');
            let currentClass = classSelector.value;
            const notificationBox = document.getElementById('notification-box');
            let archives = [];

            // --- NOTIFICATION ---
            function showNotification(message) {
                notificationBox.textContent = message;
                notificationBox.classList.add('show');
                setTimeout(() => {
                    notificationBox.classList.remove('show');
                }, 3000);
            }

            // --- DATE & TIME ---
            const topHeaderBar = document.getElementById('top-header-bar');
            function updateTime() {
                const now = new Date();
                const timeOptions = { hour: '2-digit', minute: '2-digit', second: '2-digit' };
                const dateOptions = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
                topHeaderBar.textContent = `${now.toLocaleDateString([], dateOptions)} | ${now.toLocaleTimeString([], timeOptions)}`;
            }
            setInterval(updateTime, 1000);
            updateTime();

            // --- TIMER LOGIC ---
            const timerWidget = document.getElementById('timer-widget');
            const timerDisplay = document.getElementById('timerDisplay');
            const startBtn = document.getElementById('start-btn');
            const pauseBtn = document.getElementById('pause-btn');
            const resetBtn = document.getElementById('reset-btn');
            const progressBar = document.getElementById('progressBar');
            const presetBtns = document.querySelectorAll('.timer-btn');
            
            let timerInterval = null;
            let totalSeconds = 0;
            let secondsRemaining = 0;

            function formatTime(seconds) {
                const minutes = Math.floor(seconds / 60);
                const remainingSeconds = seconds % 60;
                return `${String(minutes).padStart(2, '0')}:${String(remainingSeconds).padStart(2, '0')}`;
            }

            function updateDisplay() {
                timerDisplay.textContent = formatTime(secondsRemaining);
                document.title = `${formatTime(secondsRemaining)} - Ms. P's Hub`;
            }

            function updateProgressBar() {
                const percentage = totalSeconds > 0 ? ((totalSeconds - secondsRemaining) / totalSeconds) * 100 : 0;
                progressBar.style.width = `${percentage}%`;
            }
            
            function startTimer() {
                if (timerInterval) return;
                startBtn.textContent = 'Start';
                
                timerInterval = setInterval(() => {
                    if (secondsRemaining > 0) {
                        secondsRemaining--;
                        updateDisplay();
                        updateProgressBar();
                    } else {
                        clearInterval(timerInterval);
                        timerInterval = null;
                        showNotification("Time's up!");
                        document.title = "Ms. P's Daily Hub";
                        resetTimer();
                    }
                }, 1000);
            }

            function pauseTimer() {
                clearInterval(timerInterval);
                timerInterval = null;
                startBtn.textContent = 'Resume';
            }

            function resetTimer() {
                clearInterval(timerInterval);
                timerInterval = null;
                startBtn.textContent = 'Start';
                totalSeconds = 0;
                secondsRemaining = 0;
                updateDisplay();
                updateProgressBar();
                presetBtns.forEach(btn => btn.classList.remove('active'));
                timerWidget.classList.remove('timer-widget-active');
                timerWidget.classList.add('timer-widget-static');
                document.title = "Ms. P's Daily Hub";
            }

            presetBtns.forEach(button => {
                button.addEventListener('click', () => {
                    if (timerInterval) resetTimer();
                    totalSeconds = parseInt(button.dataset.time, 10);
                    secondsRemaining = totalSeconds;
                    updateDisplay();
                    presetBtns.forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                    timerWidget.classList.add('timer-widget-active');
                    timerWidget.classList.remove('timer-widget-static');
                });
            });

            startBtn.addEventListener('click', () => {
                if (secondsRemaining > 0) {
                    startTimer();
                }
            });

            pauseBtn.addEventListener('click', () => {
                pauseTimer();
            });

            resetBtn.addEventListener('click', () => {
                resetTimer();
            });

            // --- TAB NAVIGATION ---
            const navLinks = document.querySelectorAll('.nav-link');
            const tabContents = document.querySelectorAll('.tab-content');

            navLinks.forEach(link => {
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    const tab = link.dataset.tab;

                    navLinks.forEach(l => l.classList.remove('active'));
                    link.classList.add('active');

                    tabContents.forEach(content => {
                        content.id === tab ? content.classList.add('active') : content.classList.remove('active');
                    });
                });
            });
            
            // --- DATA PERSISTENCE (using localStorage) ---
            const learningObjective = document.getElementById('learningObjective');
            const doNow = document.getElementById('doNow');
            const agendaList = document.getElementById('agenda-list');
            const dailyDropPlaceholder = document.getElementById('daily-drop-placeholder');
            const removeDailyDropBtn = document.getElementById('remove-daily-drop-btn');

            function getInitialData() {
                return { objective: '', doNow: '', agenda: [], dailyDrop: null };
            }

            function saveData() {
                try {
                    const data = {
                        objective: learningObjective.value,
                        doNow: doNow.value,
                        agenda: Array.from(agendaList.children).map(item => ({
                            type: item.dataset.type,
                            content: item.dataset.content
                        })),
                        dailyDrop: dailyDropPlaceholder.dataset.imageData || null
                    };
                    localStorage.setItem(`classData_${currentClass}`, JSON.stringify(data));
                } catch (e) {
                    console.error("Error saving data:", e);
                    showNotification("Could not save data. Browser storage might be full.");
                }
            }

            function loadData() {
                const data = JSON.parse(localStorage.getItem(`classData_${currentClass}`)) || getInitialData();
                learningObjective.value = data.objective || '';
                doNow.value = data.doNow || '';
                renderAgenda(data.agenda || []);
                data.dailyDrop ? displayImage(dailyDropPlaceholder, data.dailyDrop, removeDailyDropBtn) : clearImage(dailyDropPlaceholder, removeDailyDropBtn);
            }
            
            classSelector.addEventListener('change', (e) => {
                saveData();
                currentClass = e.target.value;
                loadData();
            });

            [learningObjective, doNow].forEach(el => el.addEventListener('input', saveData));

            // --- AGENDA LOGIC ---
            const addAgendaBtn = document.getElementById('add-agenda-item-btn');
            const agendaPresetSelect = document.getElementById('agenda-preset-select');
            const customAgendaGroup = document.getElementById('custom-agenda-group');
            const customAgendaInput = document.getElementById('custom-agenda-input');
            const addAgendaImageBtn = document.getElementById('add-agenda-image-btn');
            const agendaImageInput = document.getElementById('agenda-image-input');

            function renderAgenda(agendaItems) {
                agendaList.innerHTML = '';
                agendaItems.forEach(item => addAgendaItem(item.type, item.content, false));
            }

            function addAgendaItem(type, content, shouldSave = true) {
                const item = document.createElement('div');
                item.className = 'agenda-item';
                item.dataset.type = type;
                item.dataset.content = content;

                const itemContent = document.createElement('div');
                itemContent.className = 'agenda-item-content';
                if (type === 'text') {
                    itemContent.textContent = content;
                } else if (type === 'image') {
                    const img = document.createElement('img');
                    img.src = content;
                    itemContent.appendChild(img);
                }
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'delete-item-btn';
                deleteBtn.innerHTML = '&times;';
                deleteBtn.onclick = () => { item.remove(); saveData(); };

                item.appendChild(itemContent);
                item.appendChild(deleteBtn);
                agendaList.appendChild(item);
                if (shouldSave) saveData();
            }

            agendaPresetSelect.addEventListener('change', () => {
                customAgendaGroup.style.display = agendaPresetSelect.value === 'custom' ? 'block' : 'none';
            });

            addAgendaBtn.addEventListener('click', () => {
                let value = agendaPresetSelect.value;
                if (value === 'custom') value = customAgendaInput.value.trim();
                if (value && value !== 'custom') {
                    addAgendaItem('text', value);
                    customAgendaInput.value = '';
                    agendaPresetSelect.value = '';
                    customAgendaGroup.style.display = 'none';
                }
            });

            addAgendaImageBtn.addEventListener('click', () => agendaImageInput.click());
            agendaImageInput.addEventListener('change', (e) => {
                if (e.target.files[0]) {
                    const reader = new FileReader();
                    reader.onload = (event) => addAgendaItem('image', event.target.result);
                    reader.readAsDataURL(e.target.files[0]);
                }
            });

            // --- CLEAR BUTTONS ---
            document.getElementById('clear-objective-btn').addEventListener('click', () => { learningObjective.value = ''; saveData(); });
            document.getElementById('clear-donow-btn').addEventListener('click', () => { doNow.value = ''; saveData(); });

            // --- IMAGE UPLOAD LOGIC ---
            function displayImage(placeholder, imageData, removeBtn) {
                placeholder.innerHTML = `<img src="${imageData}" alt="Daily Drop">`;
                placeholder.classList.add('has-image');
                placeholder.dataset.imageData = imageData;
                if(removeBtn) removeBtn.style.display = 'block';
            }

            function clearImage(placeholder, removeBtn) {
                placeholder.innerHTML = '<p>Click to upload a photo!</p>';
                placeholder.classList.remove('has-image');
                delete placeholder.dataset.imageData;
                if(removeBtn) removeBtn.style.display = 'none';
                saveData();
            }

            dailyDropPlaceholder.addEventListener('click', () => document.getElementById('daily-drop-input').click());
            document.getElementById('daily-drop-input').addEventListener('change', (e) => {
                if (e.target.files[0]) {
                    const reader = new FileReader();
                    reader.onload = (event) => { displayImage(dailyDropPlaceholder, event.target.result, removeDailyDropBtn); saveData(); };
                    reader.readAsDataURL(e.target.files[0]);
                }
            });
            removeDailyDropBtn.addEventListener('click', () => clearImage(dailyDropPlaceholder, removeDailyDropBtn));
            
            // --- CALCULATOR LOGIC ---
            const calcDisplay = document.getElementById('calc-display');
            const calcBtns = document.querySelectorAll('.calc-btn');
            let calcValue = '0', firstOperand = null, operator = null, waitingForSecondOperand = false;

            calcBtns.forEach(btn => btn.addEventListener('click', () => {
                const value = btn.textContent;
                if (!isNaN(value) || value === '.') {
                    if (waitingForSecondOperand) { calcValue = value; waitingForSecondOperand = false; } 
                    else { calcValue = calcValue === '0' ? value : calcValue + value; }
                } else if (value === 'C') { calcValue = '0'; firstOperand = null; operator = null; waitingForSecondOperand = false; } 
                else if (value === '=') {
                    if (operator && firstOperand !== null) {
                        const secondOperand = parseFloat(calcValue);
                        let result = 0;
                        if (operator === '+') result = firstOperand + secondOperand;
                        if (operator === '-') result = firstOperand - secondOperand;
                        if (operator === '*') result = firstOperand * secondOperand;
                        if (operator === '/') result = firstOperand / secondOperand;
                        calcValue = String(result);
                        firstOperand = null; operator = null;
                    }
                } else { firstOperand = parseFloat(calcValue); operator = value; waitingForSecondOperand = true; }
                calcDisplay.textContent = calcValue;
            }));

            // --- ARCHIVE & EXPORT LOGIC ---
            const archiveDisplay = document.getElementById('archive-display');
            const submitToArchiveBtn = document.getElementById('submit-to-archive-btn');
            const copyForSharingBtn = document.getElementById('copy-for-sharing-btn');
            const generateArchiveHtmlBtn = document.getElementById('generate-archive-html-btn');
            const archiveForGithubTextarea = document.getElementById('archive-for-github');
            const clearArchiveBtn = document.getElementById('clear-archive-btn');

            function loadArchives() {
                archives = JSON.parse(localStorage.getItem('dailyArchives')) || [];
                renderArchive();
            }

            function saveArchives() {
                 try {
                    localStorage.setItem('dailyArchives', JSON.stringify(archives));
                } catch (e) {
                    console.error("Error saving archives:", e);
                    showNotification("Could not save archive. Browser storage might be full.");
                }
            }

            function renderArchive() {
                archiveDisplay.innerHTML = '';
                if (archives.length === 0) {
                    archiveDisplay.innerHTML = '<p>No entries yet. Submit a plan from the Home tab!</p>';
                    return;
                }
                const groupedByDate = archives.reduce((acc, entry) => {
                    (acc[entry.date] = acc[entry.date] || []).push(entry);
                    return acc;
                }, {});
                const sortedDates = Object.keys(groupedByDate).sort().reverse();

                sortedDates.forEach(date => {
                    const dateObj = new Date(date);
                    const adjustedDate = new Date(dateObj.valueOf() + dateObj.getTimezoneOffset() * 60 * 1000);

                    const dateHeader = document.createElement('h2');
                    dateHeader.textContent = adjustedDate.toLocaleDateString([], { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
                    archiveDisplay.appendChild(dateHeader);
                    
                    const classGrid = document.createElement('div');
                    classGrid.className = 'archive-class-grid';
                    groupedByDate[date].forEach(entry => {
                        const entryCard = document.createElement('div');
                        entryCard.className = 'card archive-entry';
                        let agendaHTML = entry.data.agenda.map(item => `<li>${item.type === 'text' ? item.content : '[Image]'}</li>`).join('');
                        entryCard.innerHTML = `<h4>${entry.className}</h4><h5>Learning Objective</h5><p>${entry.data.objective || 'N/A'}</p><h5>Check and Connect</h5><p>${entry.data.doNow || 'N/A'}</p><h5>Agenda</h5><ul>${agendaHTML || '<li>No agenda items.</li>'}</ul>`;
                        classGrid.appendChild(entryCard);
                    });
                    archiveDisplay.appendChild(classGrid);
                });
            }

            submitToArchiveBtn.addEventListener('click', () => {
                const today = new Date().toISOString().split('T')[0];
                const currentData = JSON.parse(localStorage.getItem(`classData_${currentClass}`)) || getInitialData();
                const existingIndex = archives.findIndex(entry => entry.date === today && entry.className === currentClass);
                const newEntry = { date: today, className: currentClass, data: currentData };
                if (existingIndex > -1) archives[existingIndex] = newEntry; else archives.push(newEntry);
                saveArchives();
                renderArchive();
                showNotification(`Plan for ${currentClass} submitted to archive!`);
            });

            copyForSharingBtn.addEventListener('click', () => {
                const data = JSON.parse(localStorage.getItem(`classData_${currentClass}`)) || getInitialData();
                let output = `Class: ${currentClass}\nDate: ${new Date().toLocaleDateString()}\n\n🧠 Learning Objective:\n${data.objective || 'Not specified.'}\n\n🤝 Check and Connect:\n${data.doNow || 'Not specified.'}\n\n📋 Agenda:\n`;
                output += data.agenda && data.agenda.length > 0 ? data.agenda.map(item => `- ${item.type === 'text' ? item.content : '[Image]'}`).join('\n') : `No agenda items.`;
                
                const tempTextArea = document.createElement('textarea');
                tempTextArea.value = output;
                document.body.appendChild(tempTextArea);
                tempTextArea.select();
                try {
                    document.execCommand('copy');
                    showNotification('Plan copied to clipboard!');
                } catch (err) {
                    showNotification('Failed to copy.');
                    console.error('Copy failed', err);
                }
                document.body.removeChild(tempTextArea);
            });

            generateArchiveHtmlBtn.addEventListener('click', () => {
                const archiveHTML = generateStaticArchivePage(archives);
                archiveForGithubTextarea.value = archiveHTML;
                showNotification('Archive HTML generated!');
            });

            clearArchiveBtn.addEventListener('click', () => {
                if (window.confirm("Are you sure you want to permanently delete the entire archive? This action cannot be undone.")) {
                    archives = [];
                    saveArchives();
                    renderArchive();
                    archiveForGithubTextarea.value = '';
                    showNotification('Archive has been cleared.');
                }
            });
            
            function generateStaticArchivePage(archiveData) {
                const groupedByDate = archiveData.reduce((acc, entry) => {
                    (acc[entry.date] = acc[entry.date] || []).push(entry);
                    return acc;
                }, {});
                const sortedDates = Object.keys(groupedByDate).sort().reverse();

                let bodyContent = '';
                sortedDates.forEach(date => {
                    const dateObj = new Date(date);
                    const adjustedDate = new Date(dateObj.valueOf() + dateObj.getTimezoneOffset() * 60 * 1000);
                    bodyContent += `<h2>${adjustedDate.toLocaleDateString([], { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</h2>`;
                    bodyContent += `<div class="archive-class-grid">`;
                    groupedByDate[date].forEach(entry => {
                        let agendaHTML = entry.data.agenda.map(item => `<li>${item.type === 'text' ? item.content.replace(/</g, "&lt;").replace(/>/g, "&gt;") : '[Image]'}</li>`).join('');
                        bodyContent += `
                            <div class="card archive-entry">
                                <h4>${entry.className}</h4>
                                <h5>Learning Objective</h5>
                                <p>${(entry.data.objective || 'N/A').replace(/</g, "&lt;").replace(/>/g, "&gt;")}</p>
                                <h5>Check and Connect</h5>
                                <p>${(entry.data.doNow || 'N/A').replace(/</g, "&lt;").replace(/>/g, "&gt;")}</p>
                                <h5>Agenda</h5>
                                <ul>${agendaHTML || '<li>No agenda items.</li>'}</ul>
                            </div>
                        `;
                    });
                    bodyContent += `</div>`;
                });

                return `
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms. P's Daily Archive</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root { --primary-accent: #f72585; --secondary-accent: #4cc9f0; --text-light: #f0f0f0; --card-bg: rgba(0, 0, 0, 0.4); --card-border: rgba(255, 255, 255, 0.15); }
        body { font-family: 'Poppins', sans-serif; background: linear-gradient(-45deg, #000000, #1d0c33, #3a0ca3); color: var(--text-light); margin: 0; padding: 20px; }
        .container { max-width: 1200px; margin: 0 auto; }
        h1 { text-align: center; font-size: 2.5em; text-shadow: 0 0 15px var(--primary-accent); }
        h2 { border-bottom: 2px solid var(--primary-accent); padding-bottom: 10px; margin-top: 40px; }
        .archive-class-grid { display: grid; gap: 20px; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); }
        .card { background: var(--card-bg); backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px); padding: 20px; border-radius: 15px; border: 1px solid var(--card-border); }
        h4 { margin-top: 0; color: var(--primary-accent); font-size: 1.2em; }
        h5 { color: var(--secondary-accent); border-bottom: 1px solid var(--secondary-accent); padding-bottom: 5px; margin-top: 15px; }
        p, ul { margin-top: 0; }
        ul { list-style-type: disc; padding-left: 20px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Ms. P's Daily Archive</h1>
        ${bodyContent}
    </div>
</body>
</html>`;
            }

            // --- DOCUMENT GENERATOR ---
            const generateDocBtn = document.getElementById('generate-doc-btn');
            const downloadDocBtn = document.getElementById('download-doc-btn');
            const docTypeSelect = document.getElementById('doc-type-select');
            const docGeneratorTextarea = document.getElementById('doc-generator-textarea');

            generateDocBtn.addEventListener('click', async () => {
                const docType = docTypeSelect.value;
                let prompt = '';
                switch(docType) {
                    case 'behavior':
                        prompt = 'Generate a simple, structured template for a student behavior log. Include fields for Student Name, Date, Time, Location, Antecedent (what happened before), Behavior (what the student did), Consequence (what happened after), and Staff Initials.';
                        break;
                    case 'parent':
                        prompt = 'Generate a template for a parent communication log. It should be structured for multiple entries. Each entry should have fields for Date, Student Name, Parent/Guardian Contacted, Method (Phone, Email, In-person), Reason for Contact, and a summary of the conversation.';
                        break;
                    case 'notes':
                        prompt = 'Generate a simple template for taking miscellaneous meeting notes. Include fields for Meeting Title, Date, Attendees, Key Points/Discussion, and Action Items (with assigned person and deadline).';
                        break;
                }
                
                if (prompt) {
                    docGeneratorTextarea.value = "Generating...";
                    try {
                        let chatHistory = [{ role: "user", parts: [{ text: prompt }] }];
                        const payload = { contents: chatHistory };
                        const apiKey = "";
                        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
                        const response = await fetch(apiUrl, {
                            method: 'POST',
                            headers: { 'Content-Type': 'application/json' },
                            body: JSON.stringify(payload)
                        });
                        if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
                        const result = await response.json();
                        if (result.candidates && result.candidates[0].content.parts[0].text) {
                            docGeneratorTextarea.value = result.candidates[0].content.parts[0].text;
                        } else {
                            docGeneratorTextarea.value = "Sorry, could not generate a template. Please try again.";
                        }
                    } catch (error) {
                        console.error("Error generating document:", error);
                        docGeneratorTextarea.value = "An error occurred. Could not connect to the AI service.";
                        showNotification("Error: Could not connect to the AI service.");
                    }
                }
            });

            downloadDocBtn.addEventListener('click', () => {
                const text = docGeneratorTextarea.value;
                if (!text || text === "Generating...") {
                    showNotification('Nothing to download!');
                    return;
                }
                const filename = `${docTypeSelect.value}_template.txt`;
                const element = document.createElement('a');
                element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
                element.setAttribute('download', filename);
                element.style.display = 'none';
                document.body.appendChild(element);
                element.click();
                document.body.removeChild(element);
            });

            function checkLocalStorage() {
                try {
                    localStorage.setItem('__test', 'test');
                    localStorage.removeItem('__test');
                    return true;
                } catch (e) {
                    return false;
                }
            }

            // --- GEMINI API CALLS ---
            const generateObjectiveBtn = document.getElementById('generate-objective-btn');
            const objectiveTopicInput = document.getElementById('objective-topic');
            const objectiveLoader = document.getElementById('objective-loader');
            const generateDonowBtn = document.getElementById('generate-donow-btn');
            const donowLoader = document.getElementById('donow-loader');

            async function callGemini(prompt) {
                try {
                    let chatHistory = [{ role: "user", parts: [{ text: prompt }] }];
                    const payload = { contents: chatHistory };
                    const apiKey = "";
                    const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
                    const result = await response.json();
                    if (result.candidates && result.candidates[0].content.parts[0].text) {
                        return result.candidates[0].content.parts[0].text;
                    } else {
                        return "Sorry, could not generate a response. Please try again.";
                    }
                } catch (error) {
                    console.error("Error calling Gemini:", error);
                    showNotification("Error: Could not connect to the AI service.");
                    return "An error occurred while generating content.";
                }
            }

            generateObjectiveBtn.addEventListener('click', async () => {
                const topic = objectiveTopicInput.value.trim();
                if (!topic) {
                    showNotification("Please enter a topic for the objective.");
                    return;
                }
                objectiveLoader.style.display = 'block';
                const prompt = `Generate a concise student learning objective for the topic: "${topic}". Frame it as "Students will be able to..."`;
                const result = await callGemini(prompt);
                learningObjective.value = result;
                saveData();
                objectiveLoader.style.display = 'none';
            });

            generateDonowBtn.addEventListener('click', async () => {
                donowLoader.style.display = 'block';
                const prompt = `Generate a short, engaging "Check and Connect" or "Do Now" question for a middle school class. The question should be a thought-provoking conversation starter.`;
                const result = await callGemini(prompt);
                doNow.value = result;
                saveData();
                donowLoader.style.display = 'none';
            });


            // Initial Load
            if (!checkLocalStorage()) {
                showNotification("Warning: Browser storage is disabled. Your work will not be saved.");
            }
            loadData();
            loadArchives();
        });
    </script>
</body>
</html>
