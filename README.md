<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ball Knowers 2025 NFL Pick 'Em</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FFFFFF;
            color: #121C2C; /* Dark Blue for text */
        }
        .container {
            max-width: 1200px;
        }
        .card {
            background-color: #F8F9FA; /* Light Gray for cards */
        }
        .btn {
            background-color: #D50A0A; /* NFL Red */
            transition: all 0.3s ease;
        }
        .btn:hover {
            background-color: #C00909; /* Darker Red on hover */
            transform: translateY(-2px);
        }
        .input-field {
            background-color: #F8F9FA;
            border-color: #D50A0A;
            color: #121C2C;
        }
        .leaderboard-table th, .leaderboard-table td {
            padding: 12px;
            text-align: left;
        }
        .leaderboard-table th {
            background-color: #E2E8F0; /* Light Gray for table headers */
            color: #121C2C; /* Dark Blue text for headers */
        }
        .modal-bg {
            background-color: rgba(0, 0, 0, 0.7);
        }
        .leaderboard-table tbody tr:hover {
            background-color: #EBF1F7;
        }
        .tab-btn {
            background-color: #E2E8F0;
            color: #121C2C;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        .tab-btn.active {
            background-color: #D50A0A;
            color: white;
        }
        .tie-break-list li {
            cursor: pointer;
            padding: 8px;
            border-radius: 4px;
            transition: background-color 0.2s;
        }
        .tie-break-list li:hover {
            background-color: #E2E8F0;
        }
        .tie-break-list li.selected {
            background-color: #D50A0A;
            color: white;
        }
    </style>
</head>
<body class="p-4 md:p-8">
    <div id="app" class="container mx-auto">
        <header class="flex items-center justify-between mb-6">
            <div class="flex flex-col items-center flex-grow">
                <h1 class="text-4xl md:text-5xl font-bold text-blue-900 mb-2 text-center">Ball Knowers 2025 NFL Pick 'Em</h1>
                <p class="text-lg text-gray-700 text-center">Track weekly and season standings for your league.</p>
            </div>
        </header>
        <main>
            <!-- Tab Navigation -->
            <div class="flex justify-center mb-6" role="tablist">
                <button id="home-tab-btn" class="tab-btn flex-1 rounded-l-lg px-6 py-3 whitespace-nowrap focus:outline-none" role="tab" aria-controls="home-content" aria-selected="false">Home</button>
                <button id="admin-tab-btn" class="tab-btn flex-1 px-6 py-3 whitespace-nowrap focus:outline-none" role="tab" aria-controls="admin-content" aria-selected="false">Admin</button>
                <button id="weekly-tab-btn" class="tab-btn flex-1 px-6 py-3 whitespace-nowrap focus:outline-none" role="tab" aria-controls="weekly-content" aria-selected="false">Weekly Leaderboard</button>
                <button id="season-tab-btn" class="tab-btn flex-1 rounded-r-lg px-6 py-3 whitespace-nowrap focus:outline-none" role="tab" aria-controls="season-content" aria-selected="false">Season Leaderboard</button>
            </div>
            <!-- Tab Content -->
            <div id="home-content" class="tab-content" role="tabpanel">
                <!-- NFL Logo -->
                <div class="flex justify-center mb-12 mt-8">
                    <img src="https://ssl.gstatic.com/ui/v1/icons/mail/images/nfl_logo_64.png" 
                         alt="NFL Logo" 
                         class="w-32 md:w-48 max-w-full"
                         onerror="this.style.display='none';">
                </div>
                 <div class="card rounded-lg shadow-lg p-6 flex flex-col items-center justify-center mt-6">
                     <p>App ID: <span id="app-id-display" class="font-mono bg-gray-200 text-gray-800 rounded px-2 py-1"></span></p>
                     <p>Share this ID with other league members to join!</p>
                 </div>   
                <!-- Final Rules and Payouts -->
                <div class="card rounded-lg shadow-lg p-6 mt-6">
                    <h3 class="text-2xl font-bold text-blue-900 mb-4">Final Rules</h3>
                    <h4 class="font-bold text-lg mb-2">General Layout:</h4>
                    <ul class="list-disc list-inside space-y-2 mb-4">
                        <li>$10 weekly entry (whether you make your picks or forget, weekly entry will not be voided if you forget).</li>
                        <li>$8 of every weekly entry will go to that week's winner. $2 of every entry will be added to season total pool.</li>
                        <li>The season standings will be calculated on the players entire season W/L record. (Format rewards the most consistent players).</li>
                        <li>Picks will be made on ESPN & player +/- & standings will be tracked on separate website. (Website will be up by start of week 2)</li>
                        <li>Results will be tracked and everyone will be settled out at the end of the regular season.</li>
                        <li>There will be a separate playoff pick em for those who wish to continue but will not play into season record as that will conclude after last regular season game.</li>
                    </ul>
                    <h4 class="font-bold text-lg mb-2">Weekly Payout Structure W/ 27 Players ($216):</h4>
                    <ul class="list-disc list-inside space-y-2 mb-4">
                        <li>1st: $150</li>
                        <li>2nd: $56</li>
                        <li>3rd: $10</li>
                    </ul>
                    <h4 class="font-bold text-lg mb-2">Season Payout Structure W/ 27 Players ($972):</h4>
                    <ul class="list-disc list-inside space-y-2">
                        <li>1st: $700</li>
                        <li>2nd: $222</li>
                        <li>3rd: $50</li>
                    </ul>
                </div>
            </div>
            <div id="admin-content" class="tab-content hidden" role="tabpanel">
                <!-- Admin password form -->
                <div id="password-form" class="card rounded-lg shadow-lg p-6 flex flex-col items-center justify-center mb-6">
                    <h2 class="text-2xl font-bold text-blue-900 mb-4 text-center">Admin Access</h2>
                    <form id="admin-login-form" class="w-full">
                        <input type="password" id="admin-password-input" placeholder="Enter Admin Password" class="w-full input-field rounded-md p-3 focus:outline-none focus:ring-2 focus:ring-red-500 mb-4" required>
                        <button type="submit" class="btn w-full text-white rounded-md p-3 font-bold focus:outline-none">Unlock</button>
                    </form>
                </div>
                <!-- Admin features, hidden by default -->
                <div id="admin-features" class="hidden">
                    <div id="add-player-card" class="card rounded-lg shadow-lg p-6 flex flex-col items-center justify-center mb-6">
                        <h2 class="text-2xl font-bold text-blue-900 mb-4 text-center">Add New Player</h2>
                        <form id="add-player-form" class="w-full">
                            <input type="text" id="player-name-input" placeholder="Player Name" class="w-full input-field rounded-md p-3 focus:outline-none focus:ring-2 focus:ring-red-500 mb-4" required>
                            <button type="submit" class="btn w-full text-white rounded-md p-3 font-bold focus:outline-none">Add Player</button>
                        </form>
                    </div>
                    <div id="enter-scores-card" class="card rounded-lg shadow-lg p-6 mb-6">
                        <h2 class="text-2xl font-bold text-blue-900 mb-4">Enter Weekly Results</h2>
                        <form id="enter-scores-form" class="w-full">
                            <div class="mb-4">
                                <label for="week-number-input" class="block text-gray-700 font-bold mb-2">Week Number</label>
                                <input type="number" id="week-number-input" placeholder="e.g., 1" class="w-full input-field rounded-md p-3 focus:outline-none focus:ring-2 focus:ring-red-500" required min="1">
                            </div>
                            <div id="player-score-inputs" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mb-4">
                                <!-- Player score and winnings inputs will be generated here by JavaScript -->
                            </div>
                            <div class="mb-4">
                                <label class="block text-gray-700 font-bold mb-2">Tie Break Winners (Click to select)</label>
                                <ul id="tie-break-winners-list" class="tie-break-list grid grid-cols-2 sm:grid-cols-3 gap-2">
                                    <!-- Tie break winner options will be generated here -->
                                </ul>
                            </div>
                            <button type="submit" class="btn w-full text-white rounded-md p-3 font-bold focus:outline-none">Save Weekly Scores</button>
                        </form>
                    </div>
                    <div id="weekly-results-card" class="card rounded-lg shadow-lg p-6 hidden mb-6">
                        <h2 class="text-2xl font-bold text-blue-900 mb-4">Weekly Results</h2>
                        <div id="weekly-admin-leaderboard-list">
                            <!-- Weekly leaderboard for admin will be rendered here -->
                        </div>
                    </div>
                    <div id="enter-season-card" class="card rounded-lg shadow-lg p-6 mb-6">
                        <h2 class="text-2xl font-bold text-blue-900 mb-4">Enter Season Results</h2>
                        <form id="enter-season-form" class="w-full">
                            <div id="player-season-inputs" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mb-4">
                                <!-- Player season inputs will be generated here by JavaScript -->
                            </div>
                            <div class="mb-4">
                                <label class="block text-gray-700 font-bold mb-2">Tie Break Winners (Click to select)</label>
                                <ul id="tie-break-winners-season-list" class="tie-break-list grid grid-cols-2 sm:grid-cols-3 gap-2">
                                    <!-- Tie break winner options will be generated here -->
                                </ul>
                            </div>
                            <button type="submit" class="btn w-full text-white rounded-md p-3 font-bold focus:outline-none">Save Season Results</button>
                        </form>
                    </div>
                    <div id="season-results-card" class="card rounded-lg shadow-lg p-6 hidden">
                        <h2 class="text-2xl font-bold text-blue-900 mb-4">Season Results</h2>
                        <div id="season-admin-leaderboard-list">
                            <!-- Season leaderboard for admin will be rendered here -->
                        </div>
                    </div>
                </div>
            </div>
            <div id="weekly-content" class="tab-content hidden grid grid-cols-1 gap-6" role="tabpanel">
                <!-- Weekly Leaderboard -->
                <div id="weekly-leaderboard-card" class="card rounded-lg shadow-lg p-6">
                    <div class="flex flex-col items-center mb-4">
                        <h2 class="text-2xl font-bold text-blue-900">Weekly Leaderboard</h2>
                        <div class="flex flex-col md:flex-row items-center space-y-2 md:space-y-0 md:space-x-4 w-full">
                            <select id="week-selector" class="rounded-md p-2 bg-gray-200 text-sm focus:outline-none mt-2 md:mt-0 flex-1"></select>
                        </div>
                    </div>        
                    <div id="weekly-leaderboard-list">
                        <p class="text-center text-gray-700">Loading weekly standings...</p>
                    </div>
                </div>
            </div>
            <div id="season-content" class="tab-content hidden" role="tabpanel">
                <!-- Season Leaderboard -->
                <div id="season-leaderboard-card" class="card rounded-lg shadow-lg p-6">
                    <h2 class="text-2xl font-bold text-blue-900 mb-4 text-center">Season Leaderboard</h2>
                    <div id="season-leaderboard-list">
                        <p class="text-center text-gray-700">No players added yet.</p>
                    </div>
                </div>
            </div>
        </main>
        <!-- Custom Message Modal -->
        <div id="message-modal" class="fixed inset-0 modal-bg hidden justify-center items-center z-50">
            <div class="bg-gray-100 p-8 rounded-lg shadow-2xl max-w-sm w-full mx-4">
                <h3 id="modal-title" class="text-2xl font-bold mb-4 text-blue-900"></h3>
                <p id="modal-message" class="text-gray-700 mb-6"></p>
                <button id="modal-close-btn" class="btn w-full text-white rounded-md p-3 font-bold">OK</button>
            </div>
        </div>
        <!-- Loading Spinner -->
        <div id="loading-spinner" class="fixed inset-0 modal-bg flex justify-center items-center z-50">
            <div class="w-16 h-16 border-4 border-red-500 border-t-transparent rounded-full animate-spin"></div>
        </div>
    </div>
    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, addDoc, setDoc, onSnapshot, collection, query, getDocs, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        // Global variables provided by the Canvas environment
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
        let db, auth;
        let playersData = {};
        let weeklyResultsData = {};
        let seasonResultsData = {};
        let isPasswordCorrect = false;
        let isAuthReady = false;
        // UI elements
        const loadingSpinner = document.getElementById('loading-spinner');
        const weeklyLeaderboardList = document.getElementById('weekly-leaderboard-list');
        const seasonLeaderboardList = document.getElementById('season-leaderboard-list');
        const messageModal = document.getElementById('message-modal');
        const modalTitle = document.getElementById('modal-title');
        const modalMessage = document.getElementById('modal-message');
        const modalCloseBtn = document.getElementById('modal-close-btn');
        const addPlayerForm = document.getElementById('add-player-form');
        const playerNameInput = document.getElementById('player-name-input');
        const enterScoresForm = document.getElementById('enter-scores-form');
        const playerScoresInputs = document.getElementById('player-score-inputs');
        const appIdDisplay = document.getElementById('app-id-display');
        const adminTabBtn = document.getElementById('admin-tab-btn');
        const weekSelector = document.getElementById('week-selector');
        const tieBreakWinnersList = document.getElementById('tie-break-winners-list');
        const weeklyResultsCard = document.getElementById('weekly-results-card');
        const weeklyAdminLeaderboardList = document.getElementById('weekly-admin-leaderboard-list');
        const enterSeasonForm = document.getElementById('enter-season-form');
        const playerSeasonInputs = document.getElementById('player-season-inputs');
        const seasonResultsCard = document.getElementById('season-results-card');
        const seasonAdminLeaderboardList = document.getElementById('season-admin-leaderboard-list');
        const tieBreakWinnersSeasonList = document.getElementById('tie-break-winners-season-list');
        const adminFeatures = document.getElementById('admin-features');
        const passwordForm = document.getElementById('password-form');
        const adminLoginForm = document.getElementById('admin-login-form');
        const adminPasswordInput = document.getElementById('admin-password-input');
        // Tab elements
        const homeTabBtn = document.getElementById('home-tab-btn');
        const weeklyTabBtn = document.getElementById('weekly-tab-btn');
        const seasonTabBtn = document.getElementById('season-tab-btn');
        const homeContent = document.getElementById('home-content');
        const adminContent = document.getElementById('admin-content');
        const weeklyContent = document.getElementById('weekly-content');
        const seasonContent = document.getElementById('season-content');
        // Firestore paths
        const playersCollectionPath = `/artifacts/${appId}/public/data/players`;
        const weeklyResultsCollectionPath = `/artifacts/${appId}/public/data/weekly_results`;
        const seasonResultsCollectionPath = `/artifacts/${appId}/public/data/season_results`;
        let selectedWeek = null;
        let selectedWeeklyTieBreakWinners = [];
        let selectedSeasonTieBreakWinners = [];
        // Initialize Firebase
        function initFirebase() {
            try {
                if (Object.keys(firebaseConfig).length > 0) {
                    const app = initializeApp(firebaseConfig);
                    db = getFirestore(app);
                    auth = getAuth(app);
                    setLogLevel('debug'); // Enable Firestore debug logging
                    handleAuthentication();
                } else {
                    showMessage("Error", "Firebase configuration is missing. Please check the environment setup.");
                    loadingSpinner.style.display = 'none';
                }
            } catch (error) {
                console.error("Firebase initialization failed:", error);
                showMessage("Error", "Failed to initialize Firebase. Please try again.");
                loadingSpinner.style.display = 'none';
            }
        }
        // Handle Firebase authentication
        async function handleAuthentication() {
            onAuthStateChanged(auth, async (user) => {
                if (initialAuthToken) {
                    try {
                        await signInWithCustomToken(auth, initialAuthToken);
                    } catch (error) {
                        console.error("Custom token sign-in failed:", error);
                        await signInAnonymously(auth);
                    }
                } else {
                    await signInAnonymously(auth);
                }         
                loadingSpinner.style.display = 'none';
                isAuthReady = true;
                // Start real-time listeners after authentication is ready
                if (isAuthReady) {
                    setupListeners();
                }
            });
        }      
        // Setup Firestore real-time listeners
        function setupListeners() {
            // Listen for changes to the players collection
            onSnapshot(collection(db, playersCollectionPath), (snapshot) => {
                const players = [];
                snapshot.forEach(doc => {
                    players.push({ id: doc.id, ...doc.data() });
                });
                playersData = players.reduce((acc, player) => {
                    acc[player.id] = player;
                    return acc;
                }, {});
                // Render player inputs if the admin features are currently visible
                if (!adminFeatures.classList.contains('hidden')) {
                    renderPlayerInputs(players);
                }
            }, (error) => {
                console.error("Error fetching players:", error);
                showMessage("Error", "Failed to get real-time player data. Please check your network connection.");
            });
            // Listen for changes to the weekly results collection
            onSnapshot(collection(db, weeklyResultsCollectionPath), (snapshot) => {
                weeklyResultsData = {};
                snapshot.forEach(doc => {
                    const data = doc.data();
                    weeklyResultsData[data.week] = data; // Store the whole doc data
                });
                displayWeeklyLeaderboard();
            }, (error) => {
                console.error("Error fetching weekly results:", error);
                showMessage("Error", "Failed to get real-time weekly results. Please check your network connection.");
            });
            // Listen for changes to the season results collection
            onSnapshot(doc(db, seasonResultsCollectionPath, "season_doc"), (docSnapshot) => {
                if (docSnapshot.exists()) {
                    seasonResultsData = docSnapshot.data().results || {};
                    selectedSeasonTieBreakWinners = docSnapshot.data().tieBreakWinners || [];
                } else {
                    seasonResultsData = {};
                    selectedSeasonTieBreakWinners = [];
                }
                renderSeasonLeaderboard();
            }, (error) => {
                console.error("Error fetching season results:", error);
                showMessage("Error", "Failed to get real-time season results. Please check your network connection.");
            });
        }        
        // Add a new player to Firestore
        async function addPlayer(name) {
            if (!isPasswordCorrect) {
                 showMessage("Access Denied", "Please enter the admin password to add players.");
                 return;
            }
            try {
                if (!isAuthReady) {
                    showMessage("Error", "Authentication is not ready. Please wait a moment and try again.");
                    return;
                }
                                await addDoc(collection(db, playersCollectionPath), {
                    name: name
                });
            } catch (error) {
                console.error("Error adding player:", error);
                showMessage("Error", "Failed to add player. Please try again.");
            }
        }
        // Save weekly scores and winnings to Firestore
        async function saveWeeklyScores(week, results, tieBreakWinners) {
            if (!isPasswordCorrect) {
                 showMessage("Access Denied", "Please enter the admin password to save weekly scores.");
                 return;
            }
            try {
                if (!isAuthReady) {
                    showMessage("Error", "Authentication is not ready. Please wait a moment and try again.");
                }                
                const weeklyResultDocRef = doc(db, weeklyResultsCollectionPath, `week_${week}`);                
                await setDoc(weeklyResultDocRef, { 
                    week: week, 
                    results: results,
                    tieBreakWinners: tieBreakWinners
                }, { merge: true });
                showMessage("Success", `Scores for Week ${week} saved successfully!`);                
                // Render the results in the new admin card
                weeklyResultsCard.classList.remove('hidden');
                renderWeeklyTable(week, weeklyAdminLeaderboardList);
            } catch (error) {
                console.error("Error saving weekly scores:", error);
                showMessage("Error", "Failed to save scores. Please try again.");
            }
        }
        // Save season scores and winnings to Firestore
        async function saveSeasonScores(results, tieBreakWinners) {
            if (!isPasswordCorrect) {
                 showMessage("Access Denied", "Please enter the admin password to save season scores.");
                 return;
            }
            try {
                if (!isAuthReady) {
                    showMessage("Error", "Authentication is not ready. Please wait a moment and try again.");
                }              
                const seasonResultDocRef = doc(db, seasonResultsCollectionPath, `season_doc`);              
                await setDoc(seasonResultDocRef, { 
                    results: results,
                    tieBreakWinners: tieBreakWinners
                });
                showMessage("Success", `Season results saved successfully!`);
                seasonResultsCard.classList.remove('hidden');
                renderSeasonTable(Object.values(results).map((item, index) => ({ id: Object.keys(results)[index], ...item })), seasonAdminLeaderboardList);
            } catch (error) {
                console.error("Error saving season scores:", error);
                showMessage("Error", "Failed to save season scores. Please try again.");
            }
        }
        // Render the player score and tie break inputs dynamically
        function renderPlayerInputs(players) {
            playerScoresInputs.innerHTML = '';
            playerSeasonInputs.innerHTML = '';
            tieBreakWinnersList.innerHTML = '';
            tieBreakWinnersSeasonList.innerHTML = '';
            selectedWeeklyTieBreakWinners = [];
            selectedSeasonTieBreakWinners = [];
            if (players.length === 0) {
                playerScoresInputs.innerHTML = '<p class="text-gray-700 text-center col-span-full">No players added yet.</p>';
                playerSeasonInputs.innerHTML = '<p class="text-gray-700 text-center col-span-full">No players added yet.</p>';
                tieBreakWinnersList.innerHTML = '<p class="text-gray-700 text-center col-span-full">No players added yet.</p>';
                tieBreakWinnersSeasonList.innerHTML = '<p class="text-gray-700 text-center col-span-full">No players added yet.</p>';
                return;
            }
            // Create weekly input section
            const weeklyHeader = document.createElement('div');
            weeklyHeader.className = 'grid grid-cols-3 gap-2 col-span-3 text-sm font-bold text-gray-700 mb-2';
            weeklyHeader.innerHTML = `<div>Player</div><div class="text-right">Score</div><div class="text-right">Winnings</div>`;
            playerScoresInputs.appendChild(weeklyHeader);
            // Create season input section
            const seasonHeader = document.createElement('div');
            seasonHeader.className = 'grid grid-cols-3 gap-2 col-span-3 text-sm font-bold text-gray-700 mb-2';
            seasonHeader.innerHTML = `<div>Player</div><div class="text-right">Score</div><div class="text-right">Winnings</div>`;
            playerSeasonInputs.appendChild(seasonHeader);
            players.forEach(player => {
                // Weekly input fields
                const weeklyDiv = document.createElement('div');
                weeklyDiv.className = 'grid grid-cols-3 gap-2 items-center';
                weeklyDiv.innerHTML = `
                    <label class="text-sm text-gray-700">${player.name}</label>
                    <input type="number" data-player-id="${player.id}" data-type="score" class="w-full input-field rounded-md p-2 text-right focus:outline-none focus:ring-2 focus:ring-red-500" min="0" required>
                    <input type="number" data-player-id="${player.id}" data-type="winnings" class="w-full input-field rounded-md p-2 text-right focus:outline-none focus:ring-2 focus:ring-red-500" step="0.01" required>
                `;
                playerScoresInputs.appendChild(weeklyDiv);
                // Season input fields
                const seasonDiv = document.createElement('div');
                seasonDiv.className = 'grid grid-cols-3 gap-2 items-center';
                seasonDiv.innerHTML = `
                    <label class="text-sm text-gray-700">${player.name}</label>
                    <input type="number" data-player-id="${player.id}" data-type="score" class="w-full input-field rounded-md p-2 text-right focus:outline-none focus:ring-2 focus:ring-red-500" min="0" required>
                    <input type="number" data-player-id="${player.id}" data-type="winnings" class="w-full input-field rounded-md p-2 text-right focus:outline-none focus:ring-2 focus:ring-red-500" step="0.01" required>
                `;
                playerSeasonInputs.appendChild(seasonDiv);
                // Add player to weekly tie break winner list
                const weeklyLi = document.createElement('li');
                weeklyLi.dataset.playerId = player.id;
                weeklyLi.textContent = player.name;
                weeklyLi.className = 'rounded-md p-2';
                weeklyLi.addEventListener('click', () => {
                    const playerId = weeklyLi.dataset.playerId;
                    const index = selectedWeeklyTieBreakWinners.indexOf(playerId);
                    if (index > -1) {
                        selectedWeeklyTieBreakWinners.splice(index, 1);
                        weeklyLi.textContent = player.name;
                        weeklyLi.classList.remove('selected');
                    } else {
                        selectedWeeklyTieBreakWinners.push(playerId);
                        weeklyLi.textContent = `${player.name} ⭐`;
                        weeklyLi.classList.add('selected');
                    }
                });
                tieBreakWinnersList.appendChild(weeklyLi);
                // Add player to season tie break winner list
                const seasonLi = document.createElement('li');
                seasonLi.dataset.playerId = player.id;
                seasonLi.textContent = player.name;
                seasonLi.className = 'rounded-md p-2';
                seasonLi.addEventListener('click', () => {
                    const playerId = seasonLi.dataset.playerId;
                    const index = selectedSeasonTieBreakWinners.indexOf(playerId);
                    if (index > -1) {
                        selectedSeasonTieBreakWinners.splice(index, 1);
                        seasonLi.textContent = player.name;
                        seasonLi.classList.remove('selected');
                    } else {
                        selectedSeasonTieBreakWinners.push(playerId);
                        seasonLi.textContent = `${player.name} ⭐`;
                        seasonLi.classList.add('selected');
                    }
                });
                tieBreakWinnersSeasonList.appendChild(seasonLi);
            });
        }
        // Function to display the weekly leaderboard with week selector
        function displayWeeklyLeaderboard() {
            const weekKeys = Object.keys(weeklyResultsData);
            const sortedWeeks = weekKeys.map(Number).sort((a, b) => b - a);       
            // Clear existing options and create new ones
            weekSelector.innerHTML = '';
            sortedWeeks.forEach(week => {
                const option = document.createElement('option');
                option.value = week;
                option.textContent = `Week ${week}`;
                weekSelector.appendChild(option);
            });            
            // Get the currently selected week, or default to the latest
            if (!selectedWeek && sortedWeeks.length > 0) {
                selectedWeek = sortedWeeks[0];
            } else if (!selectedWeek) {
                // If there's no data at all, set a default placeholder
                weeklyLeaderboardList.innerHTML = `<p class="text-center text-gray-700">No scores entered yet.</p>`;
                return;
            }
           weekSelector.value = selectedWeek;
            renderWeeklyTable(selectedWeek, weeklyLeaderboardList);
        }
        // Renders the leaderboard table for a specific week and target container
        function renderWeeklyTable(weekNumber, container) {
            const currentWeekData = weeklyResultsData[weekNumber];
            if (!currentWeekData || !currentWeekData.results || Object.keys(currentWeekData.results).length === 0) {
                container.innerHTML = `<p class="text-center text-gray-700">No scores entered for Week ${weekNumber} yet.</p>`;
                return;
            }
            const playersArray = Object.values(playersData);
            const tieBreakWinners = currentWeekData.tieBreakWinners || [];          
            const sortedPlayers = playersArray.slice().sort((a, b) => {
                const resultA = currentWeekData.results[a.id];
                const resultB = currentWeekData.results[b.id];
                const scoreA = resultA?.score || 0;
                const scoreB = resultB?.score || 0;
                const isWinnerA = tieBreakWinners.includes(a.id);
                const isWinnerB = tieBreakWinners.includes(b.id);             
              // Primary sort by score (desc)
                if (scoreA !== scoreB) {
                    return scoreB - scoreA;
                }             
                // Secondary sort for tie-breaks
                if (isWinnerA && !isWinnerB) {
                    return -1;
                }
                if (!isWinnerA && isWinnerB) {
                    return 1;
                }                
                // No change in order if scores and tie-breaks are the same
                return 0;
            });
            let html = `
                <table id="weekly-leaderboard-table" class="w-full leaderboard-table rounded-lg overflow-hidden">
                    <thead>
                        <tr>
                            <th class="bg-gray-200 text-center">Rank</th>
                            <th class="bg-gray-200">Player</th>
                            <th class="bg-gray-200 text-center">Score</th>
                            <th class="bg-gray-200 text-center">Winnings</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            sortedPlayers.forEach((player, index) => {
                const item = currentWeekData.results[player.id];
                if (item) {
                    const rankClass = index < 3 ? 'text-green-600' : 'text-red-600';
                    const winningsClass = parseFloat(item.winnings) >= 0 ? 'text-green-600' : 'text-red-600';
                    const tieBreakStar = tieBreakWinners.includes(player.id) ? '⭐' : '';
                    html += `
                        <tr class="border-b border-gray-300 last:border-b-0" data-player-id="${player.id}">
                            <td class="${rankClass} font-bold text-center">${index + 1}</td>
                            <td class="text-gray-800">${player.name} ${tieBreakStar}</td>
                            <td class="text-gray-800 text-center">${item.score}</td>
                            <td class="${winningsClass} font-bold text-center">$${parseFloat(item.winnings).toFixed(2)}</td>
                        </tr>
                    `;
                }
            });
            html += `</tbody></table>`;
            container.innerHTML = html;
        }
        // Render the public season leaderboard
        function renderSeasonLeaderboard() {
            const playersArray = Object.values(playersData);
            if (playersArray.length === 0 || Object.keys(seasonResultsData).length === 0) {
                seasonLeaderboardList.innerHTML = `<p class="text-center text-gray-700">No season results entered yet.</p>`;
                return;
            }            
            // Combine player data with season results
            const combinedData = playersArray.map(player => ({
                ...player,
                ...seasonResultsData[player.id]
            }));
            // Sort by total score descending, with a tie-breaker
            const sortedPlayers = combinedData.sort((a, b) => {
                const scoreA = a.totalScore || 0;
                const scoreB = b.totalScore || 0;
                const isWinnerA = selectedSeasonTieBreakWinners.includes(a.id);
                const isWinnerB = selectedSeasonTieBreakWinners.includes(b.id);             
              if (scoreA !== scoreB) {
                    return scoreB - scoreA;
              }
              if (isWinnerA && !isWinnerB) {
                    return -1;
                }
                if (!isWinnerA && isWinnerB) {
                    return 1;
                }
                return 0;
            });
            renderSeasonTable(sortedPlayers, seasonLeaderboardList);
        }
        // Renders the leaderboard table for a specific week and target container
        function renderSeasonTable(sortedPlayers, container) {
            if (!sortedPlayers || sortedPlayers.length === 0) {
                container.innerHTML = `<p class="text-center text-gray-700">No players added yet.</p>`;
                return;
            }
            let html = `
                <table class="w-full leaderboard-table rounded-lg overflow-hidden">
                    <thead>
                        <tr>
                            <th class="bg-gray-200 text-center">Rank</th>
                            <th class="bg-gray-200">Player</th>
                            <th class="bg-gray-200 text-center">Total Score</th>
                            <th class="bg-gray-200 text-center">Season Payout</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            sortedPlayers.forEach((player, index) => {
                const rankClass = index < 3 ? 'text-green-600' : 'text-red-600';
                const winningsClass = parseFloat(player.totalWinnings) >= 0 ? 'text-green-600' : 'text-red-600';
                const tieBreakStar = selectedSeasonTieBreakWinners.includes(player.id) ? '⭐' : '';
                html += `
                    <tr class="border-b border-gray-300 last:border-b-0">
                        <td class="${rankClass} font-bold text-center">${index + 1}</td>
                        <td class="text-gray-800">${player.name} ${tieBreakStar}</td>
                        <td class="text-gray-800 text-center">${player.totalScore || 0}</td>
                        <td class="${winningsClass} font-bold text-center">$${(player.totalWinnings || 0).toFixed(2)}</td>
                    </tr>
                `;
            });
            html += `</tbody></table>`;
            container.innerHTML = html;
        }
        // Show a custom message modal
        function showMessage(title, message) {
            modalTitle.textContent = title;
            modalMessage.textContent = message;
            messageModal.style.display = 'flex';
        }
        // Event Listeners
        window.onload = function() {
            initFirebase();
            showTab('home-content');
            appIdDisplay.textContent = appId;
        }      
        function showTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.add('hidden');
            });
            document.getElementById(tabId).classList.remove('hidden');
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
                btn.setAttribute('aria-selected', 'false');
            });
            if (tabId === 'home-content') {
                homeTabBtn.classList.add('active');
                homeTabBtn.setAttribute('aria-selected', 'true');
            } else if (tabId === 'admin-content') {
                adminTabBtn.classList.add('active');
                adminTabBtn.setAttribute('aria-selected', 'true');
            } else if (tabId === 'weekly-content') {
                weeklyTabBtn.classList.add('active');
                weeklyTabBtn.setAttribute('aria-selected', 'true');
                displayWeeklyLeaderboard();
            } else {
                seasonTabBtn.classList.add('active');
                seasonTabBtn.setAttribute('aria-selected', 'true');
            }
        }
        homeTabBtn.addEventListener('click', () => showTab('home-content'));
        adminTabBtn.addEventListener('click', () => {
            if (isPasswordCorrect) {
                passwordForm.classList.add('hidden');
                adminFeatures.classList.remove('hidden');
            } else {
                passwordForm.classList.remove('hidden');
                adminFeatures.classList.add('hidden');
            }
            showTab('admin-content');
        });
        weeklyTabBtn.addEventListener('click', () => showTab('weekly-content'));
        seasonTabBtn.addEventListener('click', () => showTab('season-content'));
        weekSelector.addEventListener('change', (e) => {
            selectedWeek = e.target.value;
            renderWeeklyTable(selectedWeek, weeklyLeaderboardList);
        });
        adminLoginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const enteredPassword = adminPasswordInput.value;
            if (enteredPassword === "NFL2025") {
                isPasswordCorrect = true;
                passwordForm.classList.add('hidden');
                adminFeatures.classList.remove('hidden');
                renderPlayerInputs(Object.values(playersData)); // Render inputs after successful login
            } else {
                showMessage("Access Denied", "Incorrect password. Please try again.");
                adminPasswordInput.value = '';
            }
        });
      addPlayerForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const playerName = playerNameInput.value.trim();
            if (playerName) {
                addPlayer(playerName);
                playerNameInput.value = '';
            }
        });
        enterScoresForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const weekNumber = parseInt(document.getElementById('week-number-input').value, 10);
            const results = {};
            let allScoresEntered = true;
            document.querySelectorAll('#player-score-inputs input[data-type="score"]').forEach(input => {
                const playerId = input.dataset.playerId;
                const score = input.value.trim();
                const winnings = document.querySelector(`#player-score-inputs input[data-player-id="${playerId}"][data-type="winnings"]`).value.trim();
                if (score === '' || winnings === '') {
                    allScoresEntered = false;
                    return;
                }                
                results[playerId] = {
                    score: parseInt(score, 10),
                    winnings: parseFloat(winnings)
                };
            });
            if (!allScoresEntered) {
                showMessage("Error", "Please enter scores and winnings for all players.");
                return;
            }
            if (weekNumber > 0) {
                saveWeeklyScores(weekNumber, results, selectedWeeklyTieBreakWinners);
                enterScoresForm.reset();
                selectedWeeklyTieBreakWinners = []; // Reset after saving
                document.querySelectorAll('.tie-break-list li').forEach(li => {
                    li.classList.remove('selected');
                    const playerId = li.dataset.playerId;
                    const playerName = playersData[playerId]?.name || 'Player';
                    li.textContent = playerName;
                });
            } else {
                showMessage("Error", "Please enter a valid week number.");
            }
        });
        enterSeasonForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const results = {};
            let allScoresEntered = true;
            document.querySelectorAll('#player-season-inputs input[data-type="score"]').forEach(input => {
                const playerId = input.dataset.playerId;
                const score = input.value.trim();
                const winnings = document.querySelector(`#player-season-inputs input[data-player-id="${playerId}"][data-type="winnings"]`).value.trim();
                if (score === '' || winnings === '') {
                    allScoresEntered = false;
                    return;
                }               
                results[playerId] = {
                    totalScore: parseInt(score, 10),
                    totalWinnings: parseFloat(winnings)
                };
            });
            if (!allScoresEntered) {
                showMessage("Error", "Please enter scores and winnings for all players.");
                return;
            }
            saveSeasonScores(results, selectedSeasonTieBreakWinners);
        });
        modalCloseBtn.addEventListener('click', () => {
            messageModal.style.display = 'none';
        });
    </script>
</body>
</html>
