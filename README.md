# Project Responsive Web Design using Bootstrap
## Date:

## AIM:
To create a simplified clone of Dribbble (https://dribbble.com/) landing page.


## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Insert the necessary CSS and JavaScript files as external in order to use Bootstrap.

### Step 5:
Create a HTML file and include the needed Bootstrap components.

### Step 6:
Publish the website in the LocalHost.

## PROGRAM :
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>StreamSphere - Ad-Free Music</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" />
  <style>
    body {
      background: #121212;
      color: #fff;
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    }
    .sidebar {
      background: #181818;
      min-height: 100vh;
      padding: 1rem 0;
    }
    .sidebar a {
      color: #b3b3b3;
      display: block;
      padding: 1rem 2rem;
      text-decoration: none;
      font-weight: 600;
      cursor: pointer;
      transition: background 0.3s;
    }
    .sidebar a.active,
    .sidebar a:hover {
      background: #1db954;
      color: #fff;
      border-radius: 0 25px 25px 0;
    }
    .main-content {
      padding: 2rem;
      min-height: 100vh;
      background: #121212;
    }
    .song-card {
      background: #181818;
      border-radius: 8px;
      overflow: hidden;
      margin-bottom: 1rem;
      transition: background 0.3s;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 0.5rem;
    }
    .song-card:hover {
      background: #282828;
    }
    .song-img {
      width: 150px;
      height: 150px;
      object-fit: cover;
      border-radius: 8px;
      margin-bottom: 0.5rem;
    }
    .song-title {
      font-weight: 700;
      font-size: 1.1rem;
      margin: 0.3rem 0;
      text-align: center;
    }
    .song-artist {
      color: #b3b3b3;
      font-size: 0.9rem;
      margin-bottom: 0.3rem;
      text-align: center;
    }
    audio {
      width: 100%;
      outline: none;
      border-radius: 5px;
    }
    .like-btn {
      background: none;
      border: none;
      color: #b3b3b3;
      font-size: 1.5rem;
      cursor: pointer;
      transition: color 0.3s;
    }
    .like-btn.liked {
      color: #1db954;
    }
    .search-bar {
      margin-bottom: 1rem;
    }
    .settings-section {
      background: #181818;
      border-radius: 10px;
      padding: 1.5rem;
      max-width: 500px;
      margin: auto;
      color: #ccc;
    }
    .settings-section label {
      font-weight: 600;
      margin-top: 1rem;
      display: block;
    }
    /* Dark mode toggle */
    .form-switch .form-check-input:checked {
      background-color: #1db954;
      border-color: #1db954;
    }
    /* Responsive grid for songs */
    .songs-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 1rem;
    }
    @media (max-width: 576px) {
      .song-img {
        width: 100%;
        height: auto;
      }
    }
  </style>
</head>
<body>
  <div class="d-flex">
    <nav class="sidebar flex-shrink-0">
      <a href="#" id="menuHome" class="active">Home</a>
      <a href="#" id="menuPlaylists">Your Playlists</a>
      <a href="#" id="menuLiked">Liked Songs</a>
      <a href="#" id="menuSettings">Settings</a>
    </nav>

    <main class="main-content flex-grow-1">
      <!-- Search Bar -->
      <div id="searchContainer" class="search-bar">
        <input
          type="search"
          id="searchInput"
          class="form-control"
          placeholder="Search songs or artists..."
          autocomplete="off"
        />
      </div>

      <!-- Home Section -->
      <section id="homeSection">
        <h2 class="mb-4">Featured Kollywood Hits</h2>
        <div id="homeSongList" class="songs-grid"></div>
      </section>

      <!-- Playlists Section -->
      <section id="playlistsSection" style="display:none;">
        <h2>Your Playlists</h2>
        <div id="playlistButtons" class="mb-3"></div>
        <div id="playlistSongList" class="songs-grid"></div>
        <p id="noPlaylistSelected" style="color:#666;">Select a playlist above to see songs.</p>
      </section>

      <!-- Liked Songs Section -->
      <section id="likedSection" style="display:none;">
        <h2>Liked Songs</h2>
        <div id="likedSongList" class="songs-grid"></div>
        <p id="noLikedMsg" style="color:#666;">You have no liked songs yet.</p>
      </section>

      <!-- Settings Section -->
       
      <section id="settingsSection" style="display:none;">
        <div class="settings-section">
          <h3>Settings</h3>
          <!-- Inside your Settings tab content container -->

<h5>Login</h5>
<form id="loginForm" class="mb-4">
  <div class="mb-3">
    <input type="email" class="form-control" id="loginEmail" placeholder="Email" required />
  </div>
  <div class="mb-3">
    <input type="password" class="form-control" id="loginPassword" placeholder="Password" required />
  </div>
  <button type="submit" class="btn btn-primary w-100">Login</button>
</form>

<h5>Sign Up</h5>
<form id="signupForm">
  <div class="mb-3">
    <input type="email" class="form-control" id="signupEmail" placeholder="Email" required />
  </div>
  <div class="mb-3">
    <input type="password" class="form-control" id="signupPassword" placeholder="Password" required />
  </div>
  <button type="submit" class="btn btn-success w-100">Sign Up</button>
</form>

<!-- User info display after login -->
<div id="userInfo" class="mt-3" style="display:none;"></div>

          <div class="form-check form-switch mt-3">
            <input class="form-check-input" type="checkbox" id="darkModeToggle" />
            <label class="form-check-label" for="darkModeToggle">Dark Mode</label>
          </div>

          <label for="volumeRange" class="mt-4">Volume: <span id="volumeValue">100%</span></label>
          <input
            type="range"
            class="form-range"
            min="0"
            max="1"
            step="0.01"
            id="volumeRange"
            value="1"
          />

          <label for="speedSelect" class="mt-4">Playback Speed:</label>
          <select id="speedSelect" class="form-select w-auto">
            <option value="0.5">0.5x</option>
            <option value="0.75">0.75x</option>
            <option value="1" selected>1x (Normal)</option>
            <option value="1.25">1.25x</option>
            <option value="1.5">1.5x</option>
            <option value="2">2x</option>
          </select>
        </div>
      </section>
    </main>
  </div>

  <script>
    // Data
    const playlists = [
      { name: "SPB Hits" },
      { name: "Top Trending" },
      { name: "Old Melodies" },
      { name: "Romantic Hits" },
      { name: "Party Anthems" },
      { name: "MY CREATION" },
    ];

    const allSongs = [
      // SPB Hits
      {
        id: 1,
        title: "Kannukkul Nilavu",
        artist: "SPB",
        playlist: "SPB Hits",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 2,
        title: "Sundari Neeyum",
        artist: "SPB",
        playlist: "SPB Hits",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 3,
        title: "Oru Naal Oru Kanavu",
        artist: "SPB",
        playlist: "SPB Hits",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      // Top Trending
      {
        id: 4,
        title: "Vaathi Coming",
        artist: "Anirudh",
        playlist: "Top Trending",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 5,
        title: "Arabic Kuthu",
        artist: "Anirudh",
        playlist: "Top Trending",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-5.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 6,
        title: "Rowdy Baby",
        artist: "Dhanush",
        playlist: "Top Trending",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-6.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      // Old Melodies
      {
        id: 7,
        title: "Unnai Kaanadhu",
        artist: "S. Janaki",
        playlist: "Old Melodies",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-7.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 8,
        title: "Nilaave Vaa",
        artist: "P. Susheela",
        playlist: "Old Melodies",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 9,
        title: "Anjali Anjali",
        artist: "SPB & S. Janaki",
        playlist: "Old Melodies",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-9.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      // Romantic Hits
      {
        id: 10,
        title: "Ennai Thalatta",
        artist: "Hariharan",
        playlist: "Romantic Hits",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-10.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 11,
        title: "Munbe Vaa",
        artist: "Shreya Ghoshal",
        playlist: "Romantic Hits",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-11.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 12,
        title: "Vinnaithaandi",
        artist: "Karthik",
        playlist: "Romantic Hits",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-12.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      // Party Anthems
      {
        id: 13,
        title: "Danga Maari",
        artist: "Anirudh",
        playlist: "Party Anthems",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-13.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 14,
        title: "Simtaangaran",
        artist: "A. R. Rahman",
        playlist: "Party Anthems",
        audioSrc: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-14.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      {
        id: 15,
        title: "Party All Night",
        artist: "Yo Yo Honey Singh",
        playlist: "Party Anthems",
        audioSrc: "https://www.soundhelix.com/examples/mp3/MYSONG.mp3",
        imageSrc: "https://cdn.pixabay.com/photo/2014/04/03/00/30/record-player-308469_1280.png",
      },
      
    ];

    // DOM Elements
    const menuHome = document.getElementById("menuHome");
    const menuPlaylists = document.getElementById("menuPlaylists");
    const menuLiked = document.getElementById("menuLiked");
    const menuSettings = document.getElementById("menuSettings");

    const searchContainer = document.getElementById("searchContainer");
    const searchInput = document.getElementById("searchInput");

    const homeSection = document.getElementById("homeSection");
    const playlistsSection = document.getElementById("playlistsSection");
    const likedSection = document.getElementById("likedSection");
    const settingsSection = document.getElementById("settingsSection");

    const homeSongList = document.getElementById("homeSongList");
    const playlistButtons = document.getElementById("playlistButtons");
    const playlistSongList = document.getElementById("playlistSongList");
    const likedSongList = document.getElementById("likedSongList");
    const noLikedMsg = document.getElementById("noLikedMsg");
    const noPlaylistSelected = document.getElementById("noPlaylistSelected");

    const darkModeToggle = document.getElementById("darkModeToggle");
    const volumeRange = document.getElementById("volumeRange");
    const volumeValue = document.getElementById("volumeValue");
    const speedSelect = document.getElementById("speedSelect");

    let likedSongs = JSON.parse(localStorage.getItem("likedSongs")) || [];
    let currentPlaylist = null;

    // Utility Functions
    // Simple localStorage-based auth demo

function getUsers() {
  return JSON.parse(localStorage.getItem('users') || '[]');
}

function saveUsers(users) {
  localStorage.setItem('users', JSON.stringify(users));
}

function signup(email, password) {
  let users = getUsers();
  if (users.some(u => u.email === email)) {
    return { success: false, message: 'Email already registered' };
  }
  users.push({ email, password }); // No hashing for demo only!
  saveUsers(users);
  return { success: true, message: 'Signup successful!' };
}

function login(email, password) {
  let users = getUsers();
  const user = users.find(u => u.email === email && u.password === password);
  if (user) {
    localStorage.setItem('loggedInUser', email);
    return { success: true, message: 'Login successful!' };
  }
  return { success: false, message: 'Invalid email or password' };
}

function logout() {
  localStorage.removeItem('loggedInUser');
}

function isLoggedIn() {
  return !!localStorage.getItem('loggedInUser');
}

function getLoggedInUser() {
  return localStorage.getItem('loggedInUser');
}

function updateAuthUI() {
  const loggedIn = isLoggedIn();
  const loginForm = document.getElementById('loginForm');
  const signupForm = document.getElementById('signupForm');
  const userInfo = document.getElementById('userInfo');

  if (loggedIn) {
    if (loginForm) loginForm.style.display = 'none';
    if (signupForm) signupForm.style.display = 'none';

    if (userInfo) {
      userInfo.style.display = 'block';
      userInfo.textContent = `Logged in as ${getLoggedInUser()} `;
      let logoutBtn = document.createElement('button');
      logoutBtn.textContent = 'Logout';
      logoutBtn.className = 'btn btn-danger btn-sm ms-2';
      logoutBtn.onclick = () => {
        logout();
        updateAuthUI();
        alert('Logged out');
      };
      userInfo.innerHTML = '';
      userInfo.appendChild(document.createTextNode(`Logged in as ${getLoggedInUser()}`));
      userInfo.appendChild(logoutBtn);
    }
  } else {
    if (loginForm) loginForm.style.display = 'block';
    if (signupForm) signupForm.style.display = 'block';
    if (userInfo) {
      userInfo.style.display = 'none';
      userInfo.textContent = '';
    }
  }
}

// Attach event listeners on DOM content loaded or after your page renders settings tab
document.addEventListener('DOMContentLoaded', () => {
  updateAuthUI();

  const loginForm = document.getElementById('loginForm');
  if (loginForm) {
    loginForm.addEventListener('submit', e => {
      e.preventDefault();
      const email = document.getElementById('loginEmail').value.trim();
      const password = document.getElementById('loginPassword').value.trim();
      const res = login(email, password);
      alert(res.message);
      if (res.success) {
        loginForm.reset();
        updateAuthUI();
      }
    });
  }

  const signupForm = document.getElementById('signupForm');
  if (signupForm) {
    signupForm.addEventListener('submit', e => {
      e.preventDefault();
      const email = document.getElementById('signupEmail').value.trim();
      const password = document.getElementById('signupPassword').value.trim();
      const res = signup(email, password);
      alert(res.message);
      if (res.success) {
        signupForm.reset();
        updateAuthUI();
      }
    });
  }
});


    // Render songs as cards
    function renderSongs(songs, container, withLike = true) {
      container.innerHTML = "";
      if (songs.length === 0) {
        container.innerHTML = "<p style='color:#666;'>No songs found.</p>";
        return;
      }

      songs.forEach((song) => {
        const card = document.createElement("div");
        card.className = "song-card";

        card.innerHTML = `
          <img src="${song.imageSrc}" alt="${song.title}" class="song-img" />
          <div class="song-title">${song.title}</div>
          <div class="song-artist">${song.artist}</div>
          <audio controls preload="none" src="${song.audioSrc}"></audio>
          ${
            withLike
              ? `<button class="like-btn ${
                  likedSongs.includes(song.id) ? "liked" : ""
                }" data-id="${song.id}" title="Like/Unlike">&#10084;</button>`
              : ""
          }
        `;

        container.appendChild(card);
      });

      // Add event listeners for like buttons
      if (withLike) {
        const likeButtons = container.querySelectorAll(".like-btn");
        likeButtons.forEach((btn) => {
          btn.addEventListener("click", () => {
            const songId = parseInt(btn.dataset.id);
            toggleLikeSong(songId, btn);
          });
        });
      }
    }

    // Toggle like/unlike song
    function toggleLikeSong(id, btn) {
      if (likedSongs.includes(id)) {
        likedSongs = likedSongs.filter((sid) => sid !== id);
        btn.classList.remove("liked");
      } else {
        likedSongs.push(id);
        btn.classList.add("liked");
      }
      localStorage.setItem("likedSongs", JSON.stringify(likedSongs));
      renderLikedSongs();
    }

    // Render home songs (all songs)
    function renderHomeSongs() {
      renderSongs(allSongs, homeSongList);
    }

    // Render playlists buttons
    function renderPlaylistButtons() {
      playlistButtons.innerHTML = "";
      playlists.forEach((pl) => {
        const btn = document.createElement("button");
        btn.className = "btn btn-outline-success me-2 mb-2";
        btn.textContent = pl.name;
        btn.addEventListener("click", () => {
          selectPlaylist(pl.name);
        });
        playlistButtons.appendChild(btn);
      });
    }

    // Select playlist and render its songs
    function selectPlaylist(name) {
      currentPlaylist = name;
      noPlaylistSelected.style.display = "none";
      const songs = allSongs.filter((s) => s.playlist === name);
      renderSongs(songs, playlistSongList);
    }

    // Render liked songs
    function renderLikedSongs() {
      const songs = allSongs.filter((s) => likedSongs.includes(s.id));
      renderSongs(songs, likedSongList);
      noLikedMsg.style.display = songs.length === 0 ? "block" : "none";
    }

    // Search function (filters home songs and playlist songs)
    function searchSongs(query) {
      query = query.trim().toLowerCase();
      if (query === "") {
        // Reset views
        if (homeSection.style.display !== "none") {
          renderHomeSongs();
        } else if (playlistsSection.style.display !== "none" && currentPlaylist) {
          selectPlaylist(currentPlaylist);
        }
        return;
      }

      const filtered = allSongs.filter(
        (song) =>
          song.title.toLowerCase().includes(query) ||
          song.artist.toLowerCase().includes(query)
      );

      if (homeSection.style.display !== "none") {
        renderSongs(filtered, homeSongList);
      } else if (playlistsSection.style.display !== "none") {
        renderSongs(filtered, playlistSongList);
        noPlaylistSelected.style.display = filtered.length === 0 ? "block" : "none";
      }
    }

    // Dark mode toggle function
    function toggleDarkMode(enabled) {
      if (enabled) {
        document.body.style.background = "#121212";
        document.body.style.color = "#fff";
      } else {
        document.body.style.background = "#fff";
        document.body.style.color = "#000";
      }
    }

    // Update volume for all audio players
    function updateVolume(value) {
      const players = document.querySelectorAll("audio");
      players.forEach((player) => {
        player.volume = value;
      });
      volumeValue.textContent = Math.round(value * 100) + "%";
    }

    // Update playback speed for all audio players
    function updatePlaybackSpeed(value) {
      const players = document.querySelectorAll("audio");
      players.forEach((player) => {
        player.playbackRate = value;
      });
    }

    // Navigation function
    function setActiveMenu(menuItem) {
      [menuHome, menuPlaylists, menuLiked, menuSettings].forEach((el) =>
        el.classList.remove("active")
      );
      menuItem.classList.add("active");

      // Hide all sections
      homeSection.style.display = "none";
      playlistsSection.style.display = "none";
      likedSection.style.display = "none";
      settingsSection.style.display = "none";

      searchContainer.style.display = "block";

      if (menuItem === menuHome) {
        homeSection.style.display = "block";
        renderHomeSongs();
      } else if (menuItem === menuPlaylists) {
        playlistsSection.style.display = "block";
        if (!currentPlaylist) {
          noPlaylistSelected.style.display = "block";
          playlistSongList.innerHTML = "";
        } else {
          selectPlaylist(currentPlaylist);
        }
      } else if (menuItem === menuLiked) {
        likedSection.style.display = "block";
        renderLikedSongs();
      } else if (menuItem === menuSettings) {
        settingsSection.style.display = "block";
        searchContainer.style.display = "none";
      }
      searchInput.value = "";
    }

    // Initialize app
    function init() {
      renderPlaylistButtons();
      setActiveMenu(menuHome);
      renderHomeSongs();

      // Event listeners
      menuHome.addEventListener("click", (e) => {
        e.preventDefault();
        setActiveMenu(menuHome);
      });
      menuPlaylists.addEventListener("click", (e) => {
        e.preventDefault();
        setActiveMenu(menuPlaylists);
      });
      menuLiked.addEventListener("click", (e) => {
        e.preventDefault();
        setActiveMenu(menuLiked);
      });
      menuSettings.addEventListener("click", (e) => {
        e.preventDefault();
        setActiveMenu(menuSettings);
      });

      searchInput.addEventListener("input", () => {
        searchSongs(searchInput.value);
      });

      darkModeToggle.addEventListener("change", () => {
        toggleDarkMode(darkModeToggle.checked);
        localStorage.setItem("darkMode", darkModeToggle.checked);
      });

      volumeRange.addEventListener("input", () => {
        updateVolume(volumeRange.value);
        localStorage.setItem("volume", volumeRange.value);
      });

      speedSelect.addEventListener("change", () => {
        updatePlaybackSpeed(speedSelect.value);
        localStorage.setItem("speed", speedSelect.value);
      });

      // Load saved settings
      const savedDarkMode = localStorage.getItem("darkMode") === "true";
      darkModeToggle.checked = savedDarkMode;
      toggleDarkMode(savedDarkMode);

      const savedVolume = localStorage.getItem("volume");
      if (savedVolume) {
        volumeRange.value = savedVolume;
        updateVolume(savedVolume);
      } else {
        updateVolume(1);
      }

      const savedSpeed = localStorage.getItem("speed");
      if (savedSpeed) {
        speedSelect.value = savedSpeed;
        updatePlaybackSpeed(savedSpeed);
      } else {
        updatePlaybackSpeed(1);
      }
    }

    init();
  </script>
</body>
</html>

```

## OUTPUT:
![alt text](<Screenshot 2025-05-27 204258.png>) 
![alt text](<Screenshot 2025-05-27 204233.png>)
![alt text](<Screenshot 2025-05-27 204324.png>) 
![alt text](<Screenshot 2025-05-27 204346.png>)
## RESULT:
The Project for responsive web design using Bootstrap is completed successfully.
