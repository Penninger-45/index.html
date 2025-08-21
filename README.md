title>Ms. Penninger's Class Hub</title> <style> /* Basic styling for the page */ body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; line-height: 1.6; margin: 0; padding: 20px; background-color: #f4f4f9; color: #333; } .container { max-width: 800px; margin: auto; background: #fff; padding: 20px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); } h1, h2, h3 { color: #444; } hr { border: 0; height: 1px; background: #ddd; margin: 30px 0; } /* Styling for the daily agenda entries */ .agenda-day { border-left: 4px solid #007bff; padding-left: 15px; margin-bottom: 25px; } /* Styling for the generator tools */ button { background-color: #007bff; color: white; border: none; padding: 10px 15px; border-radius: 5px; cursor: pointer; font-size: 16px; margin-right: 10px; } button:hover { background-color: #0056b3; } textarea { width: 100%; margin-top: 10px; padding: 10px; font-size: 16px; border-radius: 5px; border: 1px solid #ccc; box-sizing: border-box; /* Ensures padding doesn't affect width */ } </style>
<div class="container">
    <h1>Ms. Penninger's Class Hub</h1>

    <h2>Daily Agenda & Archive</h2>
    <div id="agenda-container">
        </div>

    <hr>

    <h2>Classroom Tools</h2>

    <h3>Check & Connect Prompt Generator</h3>
    <p>Click the button to generate a new warm-up prompt for students.</p>
    <button id="generate-connect-btn">Generate New Prompt</button>
    <button id="clear-connect-btn">Clear</button>
    <textarea id="connect-output" rows="4"></textarea>

    <h3>Learning Objective Generator</h3>
    <p>Click the button to generate a new learning objective template.</p>
    <button id="generate-objective-btn">Generate New Objective</button>
    <button id="clear-objective-btn">Clear</button>
    <textarea id="objective-output" rows="4"></textarea>

    <h3>Behavior Template Generator</h3>
    <p>Click the button to generate a template for student reflections or parent communication.</p>
    <button id="generate-behavior-btn">Generate New Template</button>
    <button id="clear-behavior-btn">Clear</button>
    <textarea id="behavior-output" rows="6"></textarea>
</div>

<script id="archive-data-source" type="application/json">
[
  {
    "id": 1755659074369,
    "date": "August 19, 2025",
    "className": "Lit Basics",
    "agenda": [
      {
        "type": "text",
        "content": "Independent Practice"
      }
    ],
    "objective": "Ms. Penninger will learn if this github website will work for her agenda and task management.",
    "doNow": "Tune Tuesday! What's one song that's stuck in your head right now? Is it from a movie, a game, or TikTok?"
  },
  {
    "id": 1755724906108,
    "date": "August 20, 2025",
    "className": "Lit Basics",
    "agenda": [
      {
        "type": "text",
        "content": "Work on Class Website"
      }
    ],
    "objective": "Ms. P will be able to analyze the key components of testing website continues and explain its significance using evidence from the text.",
    "doNow": "If you could design a new level for your favorite video game, what would it be like?"
  }
]
</script>

<script>
    // --- PART 1: AGENDA RENDERING LOGIC ---
    
    // Find the data source and the container element on the page
    const dataSource = document.getElementById('archive-data-source');
    const agendaContainer = document.getElementById('agenda-container');

    // Parse the JSON data from the script tag
    const agendaData = JSON.parse(dataSource.textContent);

    // Loop through the data in reverse to show the newest day first
    agendaData.reverse().forEach(day => {
        // Create a new div for each day's entry
        const dayElement = document.createElement('div');
        dayElement.className = 'agenda-day';

        // Build the HTML structure for the entry
        dayElement.innerHTML = `
            <h3>🗓️ ${day.date}</h3>
            <p><strong>Today's Goal:</strong> ${day.objective}</p>
            <p><strong>🧠 Warm-Up:</strong> ${day.doNow}</p>
            <p><strong>✅ Today's Plan:</strong> ${day.agenda[0].content}</p>
        `;

        // Add the new day's HTML to the container
        agendaContainer.appendChild(dayElement);
    });

    // --- PART 2: GENERATOR BUTTON LOGIC ---

    // --- DATA BANKS ---
    const connectPrompts = [
        "What's one thing you're looking forward to this week?",
        "If you could have any superpower, what would it be and why?",
        "What's a song or artist you can't stop listening to right now?",
        "Share one small victory you've had recently.",
        "If you could travel anywhere in the world, where would you go first?",
        "What's the best thing you've watched or played recently?",
        "What's one goal you have for yourself today?",
        "Describe your perfect weekend."
    ];

    const objectivePrompts = [
        "Students will be able to analyze...",
        "Students will be able to explain the significance of...",
        "Students will be able to compare and contrast...",
        "Students will be able to use evidence from the text to support...",
        "Students will be able to identify the key components of...",
        "Students will be able to summarize the main idea of...",
        "Students will be able to evaluate the effectiveness of..."
    ];

    const behaviorPrompts = [
        "Behavior Reflection:\n1. What action did I take?\n2. Why did I choose to do it?\n3. Who was affected by my action?\n4. What can I do differently next time to make a better choice?",
        "Glow Note:\nHi [Student Name]! I wanted to let you know that you did an amazing job with [Specific Action] today. You showed real [Positive Trait, e.g., leadership/perseverance] and it stood out. Keep up the great work!",
        "Parent Communication (Concern):\nHi [Parent Name],\nI'm writing to you today regarding [Student Name]. In class today, I observed that [Describe specific, observable behavior]. I would love to partner with you to support them.\nThank you,\nMs. Penninger",
        "Simple Behavior Log:\nDate: [Date]\nStudent: [Student Name]\nObservation: [Describe behavior]\nAction Taken: [Describe action taken]"
    ];

    // --- GET HTML ELEMENTS ---
    const generateConnectBtn = document.getElementById('generate-connect-btn');
    const clearConnectBtn = document.getElementById('clear-connect-btn');
    const connectOutput = document.getElementById('connect-output');
    
    const generateObjectiveBtn = document.getElementById('generate-objective-btn');
    const clearObjectiveBtn = document.getElementById('clear-objective-btn');
    const objectiveOutput = document.getElementById('objective-output');
    
    const generateBehaviorBtn = document.getElementById('generate-behavior-btn');
    const clearBehaviorBtn = document.getElementById('clear-behavior-btn');
    const behaviorOutput = document.getElementById('behavior-output');

    // --- FUNCTIONS & EVENT LISTENERS ---
    function getRandomItem(arr) {
        const randomIndex = Math.floor(Math.random() * arr.length);
        return arr[randomIndex];
    }

    generateConnectBtn.addEventListener('click', () => {
        connectOutput.value = getRandomItem(connectPrompts);
    });
    clearConnectBtn.addEventListener('click', () => {
        connectOutput.value = '';
    });

    generateObjectiveBtn.addEventListener('click', () => {
        objectiveOutput.value = getRandomItem(objectivePrompts);
    });
    clearObjectiveBtn.addEventListener('click', () => {
        objectiveOutput.value = '';
    });

    generateBehaviorBtn.addEventListener('click', () => {
        behaviorOutput.value = getRandomItem(behaviorPrompts);
    });
    clearBehaviorBtn.addEventListener('click', () => {
        behaviorOutput.value = '';
    });
</script>
