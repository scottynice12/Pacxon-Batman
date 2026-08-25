🦇 BATXON: GOTHAM REALMS
A Complete HTML5 Game for Learning & Play
📖 Quick Overview
BatXon: Gotham Realms is a complete HTML5 game combining Pac-Man territory capture with Snake-style movement. Built as a single HTML file with vanilla JavaScript, it's perfect for learning game development concepts.

Play it here: Live Demo

🎮 Game Features
Feature	Description
60 Levels	Progressive difficulty with more/faster goons
Snake Movement	Continuous movement with direction queue
Territory Capture	Draw walls to close loops and capture land
3 Lives	Lose a life when a goon touches you
Power-ups ⭐	Collect to fill large areas instantly
Corner Bonus	Fill opposite corners to auto-fill the middle
Level Select	Only shows levels you've unlocked
Pause Menu	Continue, Main Menu, Mute Music options
Background Music	Batman theme with toggle
Mobile Support	Touch controls for phones/tablets

🚀 Quick Start
bash
# 1. Download or copy the HTML file
# 2. Open in any browser
# 3. Click "START GAME"
# 4. Use arrow keys to move
Keyboard Controls:

⬆⬇⬅➡ = Move Batman

P or ESC = Pause/Resume

R = Restart Game

🏗️ Technical Specs
Aspect	Details
Language	Vanilla JavaScript (ES6)
Rendering	HTML5 Canvas 2D
Audio	Web Audio API
File	Single HTML (~30KB)
Grid	20x20 (400 cells)
Levels	60
Browser	Chrome, Firefox, Safari, Edge
🧠 Core Concepts
1. Grid & Cell States
javascript
const GRID = 20;          // 20x20 grid
const EMPTY = 0;          // Empty cell
const WALL = 1;           // Drawn wall
const CAPTURED = 2;       // Claimed territory
const GOON = 3;           // Enemy
const POWERUP = 4;        // Collectible
2. Territory Capture (Loop Detection)
When walls form a closed loop, the area inside gets captured:

javascript
function captureEnclosedArea() {
    // Find cells reachable from player
    const reachable = getReachable(player.x, player.y);
    // Capture all cells NOT reachable (they're trapped!)
    for (let y = 0; y < GRID; y++) {
        for (let x = 0; x < GRID; x++) {
            if (grid[y][x] === EMPTY && !reachableSet.has(x + ',' + y)) {
                grid[y][x] = CAPTURED;
            }
        }
    }
}
3. Snake-Style Movement
Directions are queued for smooth control:

javascript
let moveQueue = [];  // Buffer for inputs
let dir = { dx: 0, dy: 0 };

function movePlayer() {
    // Take next direction from queue
    if (moveQueue.length > 0) {
        const next = moveQueue.shift();
        // Can't reverse direction (Snake rule)
        if (!(next.dx === -dir.dx && next.dy === -dir.dy)) {
            dir = next;
        }
    }
    // Apply movement
}
4. Goon AI (Random Walk)
Goons randomly choose valid directions:

javascript
function moveGoons() {
    const dirs = [[0,1],[0,-1],[1,0],[-1,0]];
    // Shuffle directions (Fisher-Yates)
    for (const goon of goons) {
        const shuffled = [...dirs];
        // Try each direction until one works
        for (const [dx, dy] of shuffled) {
            const nx = goon.x + dx, ny = goon.y + dy;
            if (grid[ny][nx] !== WALL && grid[ny][nx] !== CAPTURED) {
                // Move goon
                break;
            }
        }
    }
}
🗂️ Project Structure
text
BatXon/
├── index.html          # Complete game (all in one file)
│   ├── <style>         # All CSS (responsive design)
│   ├── <body>          # HTML structure
│   │   ├── Main Menu   # Start screen
│   │   ├── Level Select # Unlocked levels
│   │   ├── Pause Menu  # Continue/Menu/Mute
│   │   ├── Game Canvas # 600x600 game board
│   │   ├── Info Panel  # Level/Lives/Percent
│   │   └── Controls    # Buttons + touch controls
│   └── <script>        # All JavaScript
│       ├── Audio System # Web Audio API
│       ├── Game State  # Variables & state management
│       ├── Grid System # 20x20 grid operations
│       ├── Player Logic # Movement & collision
│       ├── Enemy AI    # Goon movement
│       ├── Power-ups   # Spawning & collection
│       ├── Level System # 60 levels with scaling
│       ├── Rendering   # Canvas drawing
│       └── Input       # Keyboard + touch
└── README.md           # This file
📊 Level Progression
Levels	Goons	Speed (ms)	Difficulty
1-10	3-5	200-180	😊 Easy
11-20	4-6	180-160	🙂 Medium
21-30	5-7	160-140	😐 Challenging
31-40	6-8	140-120	😤 Hard
41-50	7-8	120-100	😰 Very Hard
51-60	8	100-80	💀 Insane
🎨 Customization Guide
Change the Grid Size
javascript
const GRID = 20;  // Change to 15, 25, etc.
const CELL = 600 / GRID;  // Auto-calculates
Change Player Speed
javascript
// In startLoops() function
moveInterval = setInterval(movePlayer, 50);  // Lower = faster
Change Goon Speed
javascript
// In getConfig() function
const s = Math.max(80, 200 - (lvl - 1) * 2);
// Start speed: 200ms, minimum: 80ms
Add New Power-ups
javascript
function collectPowerup(x, y) {
    const powerup = powerups.find(p => p.x === x && p.y === y);
    switch(powerup.type) {
        case 'star':
            // Fill area
            break;
        case 'speed':
            // Speed boost
            break;
        case 'shield':
            // Invincibility
            break;
    }
}
Change Number of Levels
javascript
const MAX_LEVELS = 60;  // Change to 50, 100, etc.
📱 Mobile Support
The game automatically detects touch devices and shows on-screen controls:

css
@media (pointer: coarse) {
    .touch-controls { display: grid; }
}
Touch controls are fully responsive and work on all screen sizes.

🎵 Audio System
How Music Works
javascript
// 1. Click any button to initialize audio
function toggleMusic() {
    initAudio();  // Creates AudioContext
    musicPlaying = !musicPlaying;
    if (musicPlaying) playBatmanTheme();
}

// 2. Batman theme plays as looping notes
function playBatmanTheme() {
    const notes = [
        [440, 0.10], [554, 0.10], [659, 0.10], [880, 0.15],
        // ... more notes
    ];
    // Schedule notes with setTimeout
    // Auto-loop when finished
}
Sound Effects
Move/Collect: Short beep

Power-up: Happy ascending notes

Death: Sad descending notes

Victory: Celebration fanfare

🔧 Common Issues & Fixes
Issue	Solution
Game not starting	Check browser console for errors
Goons not moving	Make sure startLoops() was called
Territory not capturing	Ensure walls form a complete loop
Music not playing	Click "Music On" button (requires user interaction)
Mobile controls not showing	Use a touch device or enable touch emulation
Canvas not rendering	Check canvas size and CSS display
💡 Learning Resources
JavaScript Concepts Used
Arrow Functions

setInterval

Event Listeners

Canvas API

Web Audio API

Destructuring

Set Data Structure

Template Literals

Algorithms Used
Breadth-First Search (BFS)

Fisher-Yates Shuffle

Flood Fill

Collision Detection

🚀 Deployment
GitHub Pages (Free Hosting)
bash
# 1. Create a repository
git init
git add index.html
git commit -m "Add BatXon game"
git remote add origin https://github.com/username/repo-name.git
git push -u origin main

# 2. Enable GitHub Pages
# Settings → Pages → Source: main branch → Save

# 3. Play at:
# https://username.github.io/repo-name
Local Testing
bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# VS Code
# Install "Live Server" extension → Right-click → Open with Live Server
📄 License
This project is open source for educational purposes. Use it to learn, teach, and build upon!

🤝 Contributing
Want to improve the game? Here are some ideas:

Multiplayer mode - Two players on same device

Leaderboard - Save high scores with localStorage

Level editor - Create and share custom levels

Boss battles - Special levels with unique enemies

Achievements - Track player accomplishments

More power-ups - Speed boost, shield, bomb, etc.

Particle effects - Visual feedback for actions

Custom themes - Different visual styles

Sound effects library - More varied sounds

AI improvements - Smarter enemy behavior

📞 Need Help?
Report Issues: GitHub Issues

Questions: Open a discussion or issue

Suggestions: We welcome new ideas!

⭐ Credits
Game Design: Inspired by Pac-Man and Snake

Audio: Web Audio API synthesizer

Icons: Emoji (🦇🎭⭐)

Development: Single HTML file with vanilla JS

🏆 Final Notes
BatXon: Gotham Realms demonstrates:

✅ Complete game loop implementation

✅ AI behavior (random walk)

✅ Collision detection

✅ State management (menu, play, pause)

✅ Responsive design

✅ Audio system

✅ Level progression

✅ Power-up system

✅ Mobile support

✅ Single-file deployment

Made with ❤️ for learning and fun!

"It's not about the code, it's about the experience."

📝 Quick Reference Card
javascript
// Most Important Functions
initGame()          // Start/restart game
movePlayer()        // Main movement logic
captureEnclosedArea() // Territory capture
moveGoons()         // Enemy AI
draw()              // Render everything
togglePause()       // Pause/resume
toggleMusic()       // Toggle background music
Happy Coding! 🦇

