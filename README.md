<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>karaoke room v7</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet" />
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!DOCTYPE html>
<html lang="id" class="theme-dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Karaoke App</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />
  <!-- Tone.js library for generating sound effects -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.8.49/Tone.min.js"></script>
  <!-- Firebase SDK (removed as playlist management is handled locally) -->
  <script type="module">
    // Firebase SDK imports and initialization are removed as playlist management is removed.
    // If other Firebase features are needed in the future, they would need to be re-added.
  </script>
  <style>
    body {
      background: url('https://cdn.pixabay.com/photo/2017/08/06/22/01/karaoke-2590549_1280.jpg') no-repeat center center fixed;
      background-size: cover;
      /* Default colors, overridden by theme classes */
      --primary-bg: rgba(0, 0, 0, 0.7);
      --secondary-bg: rgba(0, 0, 0, 0.6); /* for .glass */
      --text-color: #fff;
      --header-color: #fcd34d; /* yellow-300 */
      --info-heading-color: #f472b6; /* pink-400 */
      --lyrics-heading-color: #86efac; /* green-300 */
      --button-primary-bg: #f59e0b; /* yellow-500 */
      --button-primary-hover-bg: #d97706; /* yellow-600 */
      --button-secondary-bg: #a855f7; /* purple-500 */
      --button-secondary-hover-bg: #9333ea; /* purple-600 */
      --search-button-bg: #ef4444; /* red-500 */
      --search-button-hover-bg: #dc2626; /* red-600 */
      --search-input-border: #fcd34d; /* yellow-400 for ring */
      --modal-bg: #1a1a1a;
      --modal-text: #fff;
      --modal-close-color: #aaa;
    }

    /* Apply variables */
    body {
      background-color: var(--primary-bg); /* Fallback, background image is primary */
      color: var(--text-color);
    }
    .glass {
      background: var(--secondary-bg);
      backdrop-filter: blur(5px); /* Added subtle blur for glass effect */
      -webkit-backdrop-filter: blur(5px); /* Safari support */
    }
    h1 { color: var(--header-color); }
    h2.text-pink-400 { color: var(--info-heading-color); }
    h2.text-green-300 { color: var(--lyrics-heading-color); }
    button.bg-yellow-500 {
      background-color: var(--button-primary-bg);
    }
    button.bg-yellow-500:hover {
      background-color: var(--button-primary-hover-bg);
    }
    button.bg-purple-500 {
      background-color: var(--button-secondary-bg);
    }
    button.bg-purple-500:hover {
      background-color: var(--button-secondary-hover-bg);
    }
    button.bg-red-500 { /* Search button */
      background-color: var(--search-button-bg);
    }
    button.bg-red-500:hover {
      background-color: var(--search-button-hover-bg);
    }
    input#searchArtistInput.focus\:ring-teal-400 {
      --tw-ring-color: var(--search-input-border);
    }
    .modal-content {
      background: var(--modal-bg);
      color: var(--modal-text);
    }
    .modal-content .close-button {
      color: var(--modal-close-color);
    }

    /* Theme classes - apply to <body> */
    .theme-default-dark { /* This is the initial default */
      --primary-bg: rgba(0, 0, 0, 0.7);
      --secondary-bg: rgba(0, 0, 0, 0.6);
      --text-color: #fff;
      --header-color: #fcd34d;
      --info-heading-color: #f472b6;
      --lyrics-heading-color: #86efac;
      --button-primary-bg: #f59e0b;
      --button-primary-hover-bg: #d97706;
      --button-secondary-bg: #a855f7;
      --button-secondary-hover-bg: #9333ea;
      --search-button-bg: #ef4444;
      --search-button-hover-bg: #dc2626;
      --search-input-border: #fcd34d;
      --modal-bg: #1a1a1a;
      --modal-text: #fff;
      --modal-close-color: #aaa;
    }

    .theme-default-light {
      --primary-bg: rgba(255, 255, 255, 0.8);
      --secondary-bg: rgba(255, 255, 255, 0.7);
      --text-color: #333;
      --header-color: #eab308; /* yellow-500 */
      --info-heading-color: #d946ef; /* fuchsia-500 */
      --lyrics-heading-color: #22c55e; /* green-500 */
      --button-primary-bg: #fde047; /* yellow-300 */
      --button-primary-hover-bg: #facc15; /* yellow-400 */
      --button-secondary-bg: #8b5cf6; /* violet-500 */
      --button-secondary-hover-bg: #7c3aed; /* violet-600 */
      --search-button-bg: #ef4444;
      --search-button-hover: #dc2626;
      --search-input-border: #facc15;
      --modal-bg: #f0f0f0;
      --modal-text: #333;
      --modal-close-color: #555;
    }

    .theme-neon-nights {
      --primary-bg: rgba(10, 5, 20, 0.9);
      --secondary-bg: rgba(20, 10, 40, 0.8);
      --text-color: #e0f2f7; /* light cyan */
      --header-color: #00ffff; /* cyan */
      --info-heading-color: #ff00ff; /* magenta */
      --lyrics-heading-color: #00ff00; /* lime */
      --button-primary-bg: #ff00ff;
      --button-primary-hover-bg: #cc00cc;
      --button-secondary-bg: #00ffff;
      --button-secondary-hover-bg: #00cccc;
      --search-button-bg: #ff00ff;
      --search-button-hover: #cc00cc;
      --search-input-border: #00ffff;
      --modal-bg: #0d0a20;
      --modal-text: #e0f2f7;
      --modal-close-color: #00ffff;
    }

    .theme-ocean-breeze {
      --primary-bg: rgba(20, 50, 80, 0.8);
      --secondary-bg: rgba(30, 70, 110, 0.7);
      --text-color: #e0f7fa;
      --header-color: #81d4fa; /* light blue */
      --info-heading-color: #4fc3f7; /* deep sky blue */
      --lyrics-heading-color: #a7ffeb; /* aqua light */
      --button-primary-bg: #4fc3f7;
      --button-primary-hover-bg: #03a9f4;
      --button-secondary-bg: #81d4fa;
      --button-secondary-hover-bg: #29b6f6;
      --search-button-bg: #ef4444; /* Keeping search button red for consistency */
      --search-button-hover: #dc2626;
      --search-input-border: #4fc3f7;
      --modal-bg: #1c3b57;
      --modal-text: #e0f7fa;
      --modal-close-color: #81d4fa;
    }

    .theme-sunset-glow {
      --primary-bg: rgba(50, 10, 0, 0.8);
      --secondary-bg: rgba(80, 20, 0, 0.7);
      --text-color: #fff3e0;
      --header-color: #ffb74d; /* orange */
      --info-heading-color: #ff8a65; /* deep orange */
      --lyrics-heading-color: #ffcc80; /* amber */
      --button-primary-bg: #ffb74d;
      --button-primary-hover-bg: #ffa726;
      --button-secondary-bg: #ff8a65;
      --button-secondary-hover-bg: #ff7043;
      --search-button-bg: #ef4444;
      --search-button-hover: #dc2626;
      --search-input-border: #ffb74d;
      --modal-bg: #320a00;
      --modal-text: #fff3e0;
      --modal-close-color: #ffb74d;
    }

    .theme-forest-retreat {
      --primary-bg: rgba(20, 40, 20, 0.8);
      --secondary-bg: rgba(30, 60, 30, 0.7);
      --text-color: #e8f5e9;
      --header-color: #a5d6a7; /* light green */
      --info-heading-color: #66bb6a; /* green */
      --lyrics-heading-color: #b9f6ca; /* teal */
      --button-primary-bg: #a5d6a7;
      --button-primary-hover-bg: #81c784;
      --button-secondary-bg: #66bb6a;
      --button-secondary-hover-bg: #4caf50;
      --search-button-bg: #ef4444;
      --search-button-hover: #dc2626;
      --search-input-border: #a5d6a7;
      --modal-bg: #142814;
      --modal-text: #e8f5e9;
      --modal-close-color: #a5d6a7;
    }

    .theme-cyberpunk-city {
      --primary-bg: rgba(0, 0, 10, 0.9);
      --secondary-bg: rgba(0, 0, 20, 0.8);
      --text-color: #ff00ff; /* neon magenta */
      --header-color: #00ffff; /* neon cyan */
      --info-heading-color: #ffff00; /* neon yellow */
      --lyrics-heading-color: #ff00ff;
      --button-primary-bg: #ff00ff;
      --button-primary-hover-bg: #cc00cc;
      --button-secondary-bg: #00ffff;
      --button-secondary-hover-bg: #00cccc;
      --search-button-bg: #ff00ff;
      --search-button-hover: #cc00cc;
      --search-input-border: #00ffff;
      --modal-bg: #000000;
      --modal-text: #ff00ff;
      --modal-close-color: #00ffff;
    }

    .theme-vintage-vinyl {
      --primary-bg: rgba(80, 70, 60, 0.8);
      --secondary-bg: rgba(100, 90, 80, 0.7);
      --text-color: #f5f5dc; /* beige */
      --header-color: #d2b48c; /* tan */
      --info-heading-color: #a0522d; /* sienna */
      --lyrics-heading-color: #deb887; /* burlywood */
      --button-primary-bg: #d2b48c;
      --button-primary-hover-bg: #c1a47c;
      --button-secondary-bg: #a0522d;
      --button-secondary-hover-bg: #8b4513;
      --search-button-bg: #ef4444;
      --search-button-hover: #dc2626;
      --search-input-border: #d2b48c;
      --modal-bg: #50463c;
      --modal-text: #f5f5dc;
      --modal-close-color: #d2b48c;
    }

    .theme-galaxy-dreams {
      --primary-bg: rgba(10, 0, 30, 0.9);
      --secondary-bg: rgba(20, 0, 50, 0.8);
      --text-color: #e0b0ff; /* light purple */
      --header-color: #9370db; /* medium purple */
      --info-heading-color: #ba55d3; /* medium orchid */
      --lyrics-heading-color: #dda0dd; /* plum */
      --button-primary-bg: #9370db;
      --button-primary-hover-bg: #7b68ee;
      --button-secondary-bg: #ba55d3;
      --button-secondary-hover-bg: #9932cc;
      --search-input-border: #9370db;
      --modal-bg: #0a001e;
      --modal-text: #e0b0ff;
      --modal-close-color: #9370db;
    }

    .theme-vibrant-pop {
      --primary-bg: rgba(255, 255, 255, 0.95);
      --secondary-bg: rgba(240, 240, 240, 0.9);
      --text-color: #333;
      --header-color: #ff4d4d; /* red */
      --info-heading-color: #4d4dff; /* blue */
      --lyrics-heading-color: #4dff4d; /* green */
      --button-primary-bg: #ff4d4d;
      --button-primary-hover-bg: #cc0000;
      --button-secondary-bg: #4d4dff;
      --button-secondary-hover-bg: #0000cc;
      --search-input-border: #ff4d4d;
      --modal-bg: #ffffff;
      --modal-text: #333;
      --modal-close-color: #555;
    }


    .scrollbar-hide::-webkit-scrollbar { display: none; }
    /* Settings button now takes the place of fullscreen button on the right */
    .settings-btn {
      position: fixed; /* Changed from absolute to fixed */
      top: 10px;
      right: 10px; /* Aligned to the far right */
      z-index: 70; /* Higher z-index to ensure visibility */
      background: rgba(255, 255, 255, 0.1);
      border-radius: 9999px;
      padding: 0.5rem;
      color: white;
      transition: background-color 0.3s ease;
    }
    .settings-btn:hover {
      background: rgba(255, 255, 255, 0.3);
    }
    .settings-menu {
      position: fixed; /* Changed from absolute to fixed */
      top: 60px; /* Below the settings button */
      right: 10px;
      z-index: 80; /* Even higher z-index for the menu */
      background: rgba(0, 0, 0, 0.8);
      backdrop-filter: blur(10px);
      border-radius: 10px;
      padding: 1rem;
      width: 200px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
      display: none;
    }
    .settings-menu button {
      width: 100%;
      padding: 0.75rem;
      margin-bottom: 0.5rem;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 8px;
      color: white;
      text-align: left;
      transition: background-color 0.2s ease;
    }
    .settings-menu button:hover {
      background-color: rgba(255, 255, 255, 0.2);
    }
    .settings-menu button:last-child {
      margin-bottom: 0;
    }
    .theme-selection-menu {
        display: none; /* Hidden by default */
        padding-top: 10px;
        border-top: 1px solid rgba(255,255,255,0.1);
        margin-top: 10px;
        max-height: 300px; /* Set a max height for scrolling */
        overflow-y: auto; /* Enable vertical scrolling */
    }
    .theme-selection-menu .theme-option-button {
        background-color: #333; /* Darker background for theme options */
        border: 1px solid transparent;
    }
    .theme-selection-menu .theme-option-button.active-theme {
        border-color: var(--header-color); /* Highlight active theme */
        box-shadow: 0 0 5px var(--header-color);
    }
    /* Modal styles for About Info */
    .modal {
      position: fixed;
      z-index: 100;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.7);
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .modal-content {
      background: var(--modal-bg);
      padding: 30px;
      border-radius: 15px;
      max-width: 500px;
      color: white;
      text-align: center;
      position: relative;
      box-shadow: 0 5px 15px rgba(0,0,0,0.5);
    }
    .close-button {
      position: absolute;
      top: 10px;
      right: 15px;
      font-size: 24px;
      cursor: pointer;
      color: #aaa;
    }
    .close-button:hover {
      color: #fff;
    }
    /* Style for the main content wrapper for consistent padding */
    .main-content-wrapper {
        padding: 1rem; /* Base padding */
        width: 100%;
        max-width: 100vw; /* Ensure it doesn't overflow horizontally */
    }
    @media (min-width: 768px) { /* md breakpoint */
        .main-content-wrapper {
            padding: 2rem; /* More padding on larger screens */
        }
    }
    /* New style for the playlist input area */
    .playlist-input-area {
        background-color: rgba(255, 255, 255, 0.05); /* Slightly visible background */
        border: 2px solid var(--search-input-border); /* Highlighted border */
        box-shadow: 0 0 15px rgba(255, 255, 255, 0.2); /* Soft glow */
        padding: 1rem;
        border-radius: 1rem;
        transition: all 0.3s ease;
    }
    .playlist-input-area:focus-within {
        box-shadow: 0 0 20px var(--header-color); /* Stronger glow on focus */
        border-color: var(--header-color); /* Change border color on focus */
    }
    /* Styling for search results items */
    .suggested-song-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: rgba(255, 255, 255, 0.1);
        padding: 0.75rem;
        border-radius: 0.5rem;
        margin-bottom: 0.5rem;
        transition: background-color 0.2s ease;
    }
    .suggested-song-item:hover {
        background-color: rgba(255, 255, 255, 0.15);
    }
    .suggested-song-item:last-child {
        margin-bottom: 0;
    }
    /* New CSS for video expansion */
    .video-player-expanded {
        max-width: 95vw !important; /* Hampir selebar viewport */
        width: 95vw !important; /* Memastikan lebar yang tersedia */
        height: 90vh !important; /* Membuatnya lebih tinggi (dari 80vh) */
        aspect-ratio: auto !important; /* Mengizinkan tinggi menentukan aspek, atau mengisi ruang */
        margin-top: 0 !important; /* Menghilangkan margin atas */
        margin-bottom: 0 !important; /* Menghilangkan margin bawah */
        border-radius: 0 !important; /* Membuat sudut menjadi tajam untuk tampilan yang lebih "penuh" */
        transition: all 0.5s ease-in-out; /* Transisi yang mulus */
    }
    /* New class to hide elements */
    .hidden-flex {
        display: none !important;
    }

    /* Styles for individual playlist items */
    .playlist-item {
        display: flex;
        align-items: center;
        background-color: rgba(255, 255, 255, 0.15);
        padding: 0.5rem;
        border-radius: 0.5rem;
        margin-bottom: 0.5rem;
        transition: background-color 0.2s ease, transform 0.2s ease;
    }
    .playlist-item:last-child {
        margin-bottom: 0;
    }
    .playlist-item input {
        background-color: rgba(0, 0, 0, 0.3);
        border: 1px solid rgba(255, 255, 255, 0.2);
        color: white;
        padding: 0.5rem 0.75rem;
        border-radius: 0.375rem;
        flex-grow: 1;
        margin-left: 0.5rem; /* Space after number */
    }
    .playlist-item input:focus {
        outline: none;
        box-shadow: 0 0 0 2px var(--search-input-border);
    }
    .playlist-item .move-btn {
        background: none;
        border: none;
        color: #81d4fa; /* light blue */
        cursor: pointer;
        padding: 0.25rem;
        font-size: 1.25rem;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .playlist-item .move-btn:hover {
        color: #4fc3f7; /* deep sky blue */
    }
    .playlist-item .remove-btn {
        background: none;
        border: none;
        color: #ef4444; /* red-500 */
        cursor: pointer;
        padding: 0.5rem;
        margin-left: 0.5rem;
    }
    .playlist-item .remove-btn:hover {
        color: #dc2626; /* red-600 */
    }
  </style>
</head>
<body class="flex flex-col items-center justify-start min-h-screen relative theme-default-dark">

  <header class="w-full max-w-4xl text-center py-6 px-4 md:px-0"> <!-- Added responsive padding -->
    <h1 class="text-5xl font-extrabold tracking-wider text-yellow-300 drop-shadow-md animate-pulse">
      <i class="fa-solid fa-microphone-lines"></i> KARAOKE ROOM
    </h1>
    <p class="text-gray-200 text-lg italic">Nyanyikan lagu favoritmu dengan penuh gaya!</p>
  </header>

  <div id="videoPlayerContainer" class="relative w-full max-w-6xl aspect-video rounded-2xl overflow-hidden shadow-2xl border-4 border-yellow-400 mt-4 px-4 md:px-0"> <!-- Added responsive padding and margin-top -->
    <div id="player" class="w-full h-full"></div>
    <div class="flex justify-center items-center gap-4 mt-4 text-white text-xl">
      <button onclick="prevTrack()" title="Sebelumnya" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-backward-step"></i></button>
      <button onclick="rewind()" title="Mundur" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-backward"></i></button>
      <button onclick="togglePlayPause()" title="Putar/Jeda" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-play"></i></button>
      <button onclick="stopPlayback()" title="Stop" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-stop"></i></button>
      <button onclick="forward()" title="Majukan" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-forward"></i></button>
      <button onclick="nextTrack()" title="Berikutnya" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-forward-step"></i></button>
      <!-- Volume buttons moved to the right -->
      <button onclick="volumeUp()" title="Volume Naik" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-volume-high"></i></button>
      <button onclick="volumeDown()" title="Volume Turun" class="p-2 hover:text-yellow-300"><i class="fa-solid fa-volume-low"></i></button>
    </div>
  </div>

  <!-- Settings Button -->
  <button onclick="toggleSettingsMenu()" class="settings-btn">
    <i class="fa-solid fa-cog"></i>
  </button>

  <!-- Settings Menu -->
  <div id="settingsMenu" class="settings-menu">
    <div id="mainSettingsOptions"> <!-- New wrapper for main settings buttons -->
        <button onclick="showThemeSelection()">
          <i class="fa-solid fa-adjust mr-2"></i> <span id="themeToggleText">Ubah Tema</span>
        </button>
        <button onclick="toggleSoundEffects()">
          <i class="fa-solid fa-volume-up mr-2"></i> <span id="soundEffectsToggleText">Efek Suara: ON</span>
        </button>
        <button onclick="showAboutInfo()">
          <i class="fa-solid fa-info-circle mr-2"></i> Tentang Aplikasi
        </button>
    </div>

    <!-- Theme Selection Sub-Menu -->
    <div id="themeSelectionMenu" class="theme-selection-menu">
        <h4 class="text-sm text-gray-400 mb-2">Pilih Tema:</h4>
        <button class="theme-option-button" data-theme="default-dark" onclick="applyTheme('default-dark')">Tema Gelap Default</button>
        <button class="theme-option-button" data-theme="default-light" onclick="applyTheme('default-light')">Tema Terang Default</button>
        <button class="theme-option-button" data-theme="neon-nights" onclick="applyTheme('neon-nights')">Neon Nights</button>
        <button class="theme-option-button" data-theme="ocean-breeze" onclick="applyTheme('ocean-breeze')">Ocean Breeze</button>
        <button class="theme-option-button" data-theme="sunset-glow" onclick="applyTheme('sunset-glow')">Sunset Glow</button>
        <button class="theme-option-button" data-theme="forest-retreat" onclick="applyTheme('forest-retreat')">Forest Retreat</button>
        <button class="theme-option-button" data-theme="cyberpunk-city" onclick="applyTheme('cyberpunk-city')">Cyberpunk City</button>
        <button class="theme-option-button" data-theme="vintage-vinyl" onclick="applyTheme('vintage-vinyl')">Vintage Vinyl</button>
        <button class="theme-option-button" data-theme="galaxy-dreams" onclick="applyTheme('galaxy-dreams')">Galaxy Dreams</button>
        <button class="theme-option-button" data-theme="vibrant-pop" onclick="applyTheme('vibrant-pop')">Vibrant Pop</button>
        <button class="mt-4 bg-gray-600 hover:bg-gray-700" onclick="hideThemeSelection()">
            <i class="fa-solid fa-arrow-left mr-2"></i> Kembali ke Pengaturan
        </button>
    </div>
  </div>

  <div class="main-content-wrapper space-y-6 md:space-y-8 mt-6"> <!-- Wrapper for main content sections -->
    <section class="w-full max-w-5xl glass rounded-2xl p-6 shadow-lg mx-auto"> <!-- Added mx-auto for centering -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6"> <!-- New grid container for side-by-side layout -->
          <div>
              <!-- Playlist input area with draggable items -->
              <div class="playlist-input-area mb-4">
                  <label for="playlistContainer" class="block text-lg font-semibold text-white mb-2">Daftar Lagu Anda (Atur dengan Panah):</label>
                  <div id="playlistContainer" class="bg-gray-800 p-4 rounded-lg h-48 overflow-y-auto scrollbar-hide space-y-2">
                      <!-- Song inputs will be dynamically added here by JavaScript -->
                      <p class="text-gray-400 italic text-center py-4">Daftar lagu kosong. Tambahkan lagu di bawah atau cari.</p>
                  </div>
                  <button onclick="addSongInput()" class="w-full bg-blue-500 hover:bg-blue-600 px-4 py-2 mt-4 rounded-xl text-white font-bold text-base flex gap-2 justify-center items-center shadow-md">
                      <i class="fa-solid fa-plus-circle"></i> Tambah Lagu
                  </button>
              </div>
              <div class="flex flex-col md:flex-row gap-4">
                <button onclick="startPlaylist()" class="w-full bg-yellow-500 hover:bg-yellow-600 px-6 py-3 rounded-xl text-white font-bold text-lg flex gap-3 justify-center items-center shadow-md">
                  <i class="fa-solid fa-play text-sm"></i> Mulai Karaoke
                </button>
              </div>
          </div>

          <!-- New search features and Genre/Trending section -->
          <div class="mt-8 pt-4 border-t border-gray-700 md:mt-0 md:pt-0 md:border-t-0"> <!-- Adjusted margin/padding/border for grid layout -->
            <h2 class="text-3xl font-bold text-teal-400 mb-4 flex items-center gap-2">
              <i class="fa-solid fa-magnifying-glass"></i> Cari Lagu & Artis
            </h2>

            <div class="space-y-4">
              <!-- Search Songs by Artist -->
              <div class="glass p-4 rounded-xl space-y-2">
                <label for="searchArtistInput" class="block text-lg font-semibold text-white">Cari Lagu Berdasarkan Artis/lagu:</label>
                <input type="text" id="searchArtistInput" class="w-full p-3 rounded text-black focus:outline-none focus:ring-2 focus:ring-teal-400" placeholder="Masukkan nama artis/lagu...">
                <button onclick="searchSongsByArtist()" class="w-full bg-red-500 hover:bg-red-600 px-6 py-3 rounded-xl text-white font-bold text-lg flex gap-3 justify-center items-center shadow-md">
                  <i class="fa-solid fa-music"></i> Temukan Lagu
                </button>
                <div id="suggestedSongs" class="text-gray-100 mt-2 space-y-1">
                  <p class="italic">Lagu-lagu akan muncul di sini...</p>
                </div>
              </div>
            </div>

            <!-- NEW SECTION: Genre & Trending -->
            <div class="mt-8 pt-4 border-t border-gray-700"> <!-- New border for separation -->
                <h2 class="text-3xl font-bold text-purple-400 mb-4 flex items-center gap-2">
                    <i class="fa-solid fa-chart-line"></i> Kategori & Trending
                </h2>
                <div class="space-y-4">
                    <label for="trendCategorySelect" class="block text-lg font-semibold text-white">Pilih Kategori Tren:</label>
                    <select id="trendCategorySelect" class="w-full p-3 rounded text-black focus:outline-none focus:ring-2 focus:ring-purple-400">
                        <option value="Pop">Pop</option>
                        <option value="Koplo">Koplo</option>
                        <option value="Dangdut">Dangdut</option>
                        <option value="Barat">Barat (Western)</option>
                        <option value="Rock">Rock</option>
                        <option value="Hip Hop">Hip Hop</option>
                        <option value="EDM">EDM</option>
                        <option value="K-Pop">K-Pop</option>
                      
                        <option value="Google Trends">Trending di Google (Hari Ini)</option>
                        <option value="TikTok Trends">Trending di TikTok (Hari Ini)</option>
                        <option value="YouTube Trends">Trending di YouTube (Hari Ini)</option>
                        <option value="Spotify Trends">Trending di Spotify (Hari Ini)</option>
                    </select>
                    <button onclick="fetchTrendingSongs()" class="w-full bg-purple-500 hover:bg-purple-600 px-6 py-3 rounded-xl text-white font-bold text-lg flex gap-3 justify-center items-center shadow-md">
                        <i class="fa-solid fa-fire"></i> Dapatkan Top 10 Trending
                    </button>
                    <div id="trendingSongsDisplay" class="text-gray-100 mt-2 space-y-1">
                        <p class="italic text-gray-400">Pilih kategori dan klik tombol untuk melihat lagu trending...</p>
                    </div>
                </div>
            </div>
          </div>
      </div>
    </section>

    <section class="w-full max-w-6xl grid grid-cols-1 md:grid-cols-2 gap-6 mx-auto"> <!-- Added mx-auto for centering -->
      <div class="glass p-6 rounded-2xl space-y-3">
        <h2 class="text-2xl font-semibold text-pink-400 flex items-center gap-3">
          <i class="fa-solid fa-info-circle"></i> Info Lagu
        </h2>
        <p><i class="fa-solid fa-user"></i> Artis: <span id="artist">-</span></p>
        <p><i class="fa-solid fa-music"></i> Judul: <span id="title">-</span></p>
      </div>
      <div class="glass p-6 rounded-2xl h-60 overflow-y-auto scrollbar-hide">
        <h2 class="text-2xl font-semibold text-green-300 mb-2 flex items-center gap-3">
          <i class="fa-solid fa-file-audio"></i> Lirik Lagu
        </h2>
        <pre id="lyricsText" class="whitespace-pre-wrap text-gray-100 italic">Lirik akan muncul di sini...</pre>
      </div>
    </section>
  </div> <!-- End of main-content-wrapper -->

  <footer class="text-sm text-gray-300 mt-10 text-center pb-4"> <!-- Added pb-4 for bottom padding -->
    © 2025 Karaoke Room • Dibuat oleh kamar flasher
  </footer>

  <!-- About Info Modal -->
  <div id="aboutModal" class="modal" style="display: none;">
    <div class="modal-content">
      <span class="close-button" onclick="closeAboutModal()">&times;</span>
      <h2 class="text-3xl font-bold text-yellow-300 mb-4">Tentang Karaoke Room</h2>
      <p class="mb-2">Karaoke Room adalah aplikasi web sederhana yang memungkinkan Anda menikmati sesi karaoke dengan video YouTube dan lirik.</p>
      <p class="mb-4">Fitur tambahan termasuk pencarian lagu, perkenalan lagu bertenaga AI (Gemini), dan kontrol pemutaran yang mudah. Selamat menikmati hari-hari Anda. Salam dari kami KAMAR FLASHER</p>
    </div>
  </div>

  <script src="https://www.youtube.com/iframe_api"></script>
  <script>
    let player, playlist = [], currentIndex = 0;
    const synth = new Tone.Synth().toDestination();
    let soundEffectsOn = true;
    let currentTheme = 'default-dark'; // Track the current active theme
    let isVideoExpanded = false; // New state to track video expansion

    // Define available themes and their display names
    const themes = {
        'default-dark': 'Tema Gelap Default',
        'default-light': 'Tema Terang Default',
        'neon-nights': 'Neon Nights',
        'ocean-breeze': 'Ocean Breeze',
        'sunset-glow': 'Sunset Glow',
        'forest-retreat': 'Forest Retreat',
        'cyberpunk-city': 'Cyberpunk City',
        'vintage-vinyl': 'Vintage Vinyl',
        'galaxy-dreams': 'Galaxy Dreams',
        'vibrant-pop': 'Vibrant Pop'
    };

    function onYouTubeIframeAPIReady() {
      player = new YT.Player('player', {
        height: '100%', width: '100%', videoId: '',
        playerVars: { autoplay: 1, controls: 1 },
        events: { onStateChange: onPlayerStateChange }
      });
    }

    // Function to render the playlist array into the HTML UI
    function renderPlaylist() {
      const playlistContainer = document.getElementById('playlistContainer');
      playlistContainer.innerHTML = ''; // Clear existing items

      if (playlist.length === 0) {
        playlistContainer.innerHTML = '<p class="text-gray-400 italic text-center py-4">Daftar lagu kosong. Tambahkan lagu di bawah atau cari.</p>';
        return;
      }

      playlist.forEach((song, index) => {
        const itemDiv = document.createElement('div');
        itemDiv.className = 'playlist-item flex items-center bg-gray-700 p-2 rounded-lg text-white text-sm';
        itemDiv.dataset.index = index; // Store index

        // Song number
        const songNumber = document.createElement('span');
        songNumber.className = 'w-6 text-center font-bold';
        songNumber.textContent = `${index + 1}.`;
        itemDiv.appendChild(songNumber);

        // Input field for song title
        const input = document.createElement('input');
        input.type = 'text';
        input.className = 'bg-gray-800 text-white p-2 rounded-md flex-grow mx-2 focus:ring-yellow-400 focus:outline-none';
        input.value = song;
        input.placeholder = 'Judul lagu - Artis';
        input.addEventListener('change', (e) => {
          playlist[index] = e.target.value.trim(); // Update playlist array on change
          // No need to re-render the whole playlist on single input change, just update the array
        });
        itemDiv.appendChild(input);

        // Up arrow button
        const upButton = document.createElement('button');
        upButton.className = 'move-btn';
        upButton.innerHTML = '<i class="fa-solid fa-arrow-up"></i>';
        upButton.title = 'Geser ke Atas';
        upButton.onclick = () => moveSongUp(index);
        itemDiv.appendChild(upButton);

        // Down arrow button
        const downButton = document.createElement('button');
        downButton.className = 'move-btn';
        downButton.innerHTML = '<i class="fa-solid fa-arrow-down"></i>';
        downButton.title = 'Geser ke Bawah';
        downButton.onclick = () => moveSongDown(index);
        itemDiv.appendChild(downButton);

        // Remove button
        const removeButton = document.createElement('button');
        removeButton.className = 'remove-btn text-red-400 hover:text-red-600 ml-2';
        removeButton.innerHTML = '<i class="fa-solid fa-trash-alt"></i>';
        removeButton.title = 'Hapus Lagu';
        removeButton.onclick = () => removeSongInput(index);
        itemDiv.appendChild(removeButton);

        playlistContainer.appendChild(itemDiv);
      });
    }

    // Function to move a song up in the playlist
    function moveSongUp(index) {
      if (index > 0) {
        [playlist[index], playlist[index - 1]] = [playlist[index - 1], playlist[index]]; // Swap elements
        renderPlaylist(); // Re-render to reflect new order
      }
    }

    // Function to move a song down in the playlist
    function moveSongDown(index) {
      if (index < playlist.length - 1) {
        [playlist[index], playlist[index + 1]] = [playlist[index + 1], playlist[index]]; // Swap elements
        renderPlaylist(); // Re-render to reflect new order
      }
    }

    // Function to add a new empty song input field
    function addSongInput(songTitle = '') {
      playlist.push(songTitle); // Add to the data array
      renderPlaylist(); // Re-render the UI
      // Scroll to the bottom to see the new input
      const playlistContainer = document.getElementById('playlistContainer');
      playlistContainer.scrollTop = playlistContainer.scrollHeight;
    }

    // Function to remove a song input field by its index
    function removeSongInput(index) {
      playlist.splice(index, 1); // Remove from the data array
      renderPlaylist(); // Re-render the UI
    }

    function onPlayerStateChange(event) {
      if (event.data === YT.PlayerState.ENDED) {
        // Remove the currently played song from the playlist
        if (playlist.length > 0) {
          playlist.shift(); // Removes the first element
          renderPlaylist(); // Update the UI immediately
        }
        
        // Play the next song if available
        if (playlist.length > 0) {
          playSong(playlist[0]); // Always play the first song in the *remaining* playlist
        } else {
          // If no more songs, clear artist and title info
          document.getElementById('artist').textContent = "-";
          document.getElementById('title').textContent = "-";
          document.getElementById('lyricsText').textContent = "Daftar putar selesai.";
        }
      }
    }

    async function startPlaylist() {
      // Update the playlist array from the current UI inputs
      const currentInputs = Array.from(document.querySelectorAll('#playlistContainer input')).map(input => input.value.trim());
      playlist = currentInputs.filter(song => song !== ""); // Only keep non-empty songs

      if (playlist.length === 0) {
        document.getElementById('lyricsText').textContent = "Mohon masukkan minimal 1 lagu di daftar putar.";
        return;
      }
      
      currentIndex = 0; // Start from the beginning of the new playlist
      await Tone.start();
      playSong(playlist[0]);
      renderPlaylist(); // Re-render to ensure UI matches the active playlist
    }

    async function playSong(query) {
      if (soundEffectsOn) {
        synth.triggerAttackRelease("C4", "8n");
      }
      // Appends " karaoke" to the search query to specifically look for karaoke versions
      const apiKey = 'AIzaSyAMj5Bgs8tEf7lrNwspQq1rSSc5cXxScRc';
      const ytUrl = `https://www.googleapis.com/youtube/v3/search?part=snippet&type=video&maxResults=1&q=${encodeURIComponent(query + " karaoke")}&key=${apiKey}`;

      try {
        const res = await fetch(ytUrl);
        if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
        const data = await res.json();

        if (data.items && data.items.length > 0) {
          const video = data.items[0];
          player.loadVideoById(video.id.videoId);
          const titleText = video.snippet.title;
          const [artist, title] = parseArtistTitle(titleText);
          document.getElementById('artist').textContent = artist;
          document.getElementById('title').textContent = title;
          fetchLyrics(artist, title);
        } else {
          document.getElementById('lyricsText').textContent = "Video karaoke tidak ditemukan untuk lagu ini.";
          document.getElementById('artist').textContent = "Tidak ditemukan";
          document.getElementById('title').textContent = query;
        }
      } catch (error) {
        console.error("Error fetching YouTube video:", error);
        document.getElementById('lyricsText').textContent = "Gagal memuat video atau informasi lagu.";
      }
    }

    function parseArtistTitle(text) {
      const parts = text.split("-").map(x => x.trim());
      return parts.length >= 2 ? [parts[0], parts[1]] : ["Tidak diketahui", text];
    }

    async function fetchLyrics(artist, title) {
      try {
        const res = await fetch(`https://api.lyrics.ovh/v1/${encodeURIComponent(artist)}/${encodeURIComponent(title)}`);
        if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
        const data = await res.json();
        document.getElementById('lyricsText').textContent = data.lyrics || "Lirik tidak ditemukan.";
      } catch {
        document.getElementById('lyricsText').textContent = "Gagal mengambil lirik.";
      }
    }

    async function searchSongsByArtist() {
      const searchArtistInput = document.getElementById('searchArtistInput').value.trim();
      const suggestedSongsElement = document.getElementById('suggestedSongs');
      // Clear previous results and show loading message
      suggestedSongsElement.innerHTML = "<p class='italic text-gray-400'>Mencari lagu...</p>";

      if (!searchArtistInput) {
        suggestedSongsElement.innerHTML = "<p class='italic text-gray-400'>Mohon masukkan nama artis/lagu.</p>";
        return;
      }

      // Appends " karaoke" to the search query to specifically look for karaoke versions
      const apiKey = 'AIzaSyAMj5Bgs8tEf7lrNwspQq1rSSc5cXxScRc';
      const ytUrl = `https://www.googleapis.com/youtube/v3/search?part=snippet&type=video&maxResults=10&q=${encodeURIComponent(searchArtistInput + " karaoke")}&key=${apiKey}`;

      try {
        const res = await fetch(ytUrl);
        if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
        const data = await res.json();

        suggestedSongsElement.innerHTML = ''; // Clear loading message before populating

        if (data.items && data.items.length > 0) {
          const resultHeader = document.createElement('p');
          resultHeader.className = 'font-semibold text-white mb-2';
          resultHeader.textContent = 'Lagu-lagu yang ditemukan:';
          suggestedSongsElement.appendChild(resultHeader);

          const ul = document.createElement('ul');
          ul.className = 'space-y-2'; // Add spacing between list items
          data.items.forEach(item => {
            const li = document.createElement('li');
            li.className = 'suggested-song-item'; // Custom class for styling
            
            const songTitleSpan = document.createElement('span');
            songTitleSpan.textContent = item.snippet.title;
            songTitleSpan.className = 'text-gray-100 flex-grow mr-2'; // Allow text to grow, add right margin

            const addButton = document.createElement('button');
            addButton.textContent = "Tambahkan";
            addButton.className = "text-sm bg-blue-500 hover:bg-blue-600 px-3 py-1 rounded-md shadow-md transition duration-200 ease-in-out"; // Improved button styling
            addButton.onclick = () => {
              addSongInput(item.snippet.title); // Add song directly to playlist and re-render
            };
            
            li.appendChild(songTitleSpan);
            li.appendChild(addButton);
            ul.appendChild(li);
          });
          suggestedSongsElement.appendChild(ul);
        } else {
          suggestedSongsElement.innerHTML = "<p class='italic text-gray-400'>Tidak ada lagu yang ditemukan untuk artis/lagu ini.</p>";
        }
      } catch (error) {
        console.error("Error searching songs by artist/song:", error);
        suggestedSongsElement.innerHTML = "<p class='italic text-red-400'>Gagal mencari lagu. Silakan coba lagi nanti.</p>"; // More descriptive error
      }
    }

    async function fetchTrendingSongs() {
        const trendCategorySelect = document.getElementById('trendCategorySelect');
        const selectedCategory = trendCategorySelect.value;
        const trendingSongsDisplay = document.getElementById('trendingSongsDisplay');

        trendingSongsDisplay.innerHTML = `<p class='italic text-gray-400'>Mendapatkan ${selectedCategory} lagu trending...</p>`;

        let prompt = "";
        if (selectedCategory.includes("Trends")) {
            // Extract the platform name, e.g., "Google" from "Google Trends"
            const platform = selectedCategory.replace(" Trends", "");
            prompt = `Berikan daftar 10 lagu teratas yang sedang tren di ${platform} hari ini. Formatnya hanya berupa judul lagu dan artisnya, satu per baris. Jangan sertakan nomor atau bullet point. Contoh:&#10;Lagu A - Artis X&#10;Lagu B - Artis Y`;
        } else {
            // Existing genre prompt
            prompt = `Berikan daftar 10 lagu teratas yang sedang tren untuk genre ${selectedCategory} saat ini. Formatnya hanya berupa judul lagu dan artisnya, satu per baris. Jangan sertakan nomor atau bullet point. Contoh:&#10;Lagu A - Artis X&#10;Lagu B - Artis Y`;
        }
        
        let chatHistory = [];
        chatHistory.push({ role: "user", parts: [{ text: prompt }] });

        const payload = { contents: chatHistory };
        const apiKey = ""; // Canvas will provide this automatically
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

        try {
            const response = await fetch(apiUrl, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });

            if (!response.ok) {
                const errorData = await response.json();
                throw new Error(`API error: ${response.status} - ${errorData.error.message}`);
            }

            const result = await response.json();
            if (result.candidates && result.candidates.length > 0 &&
                result.candidates[0].content && result.candidates[0].content.parts &&
                result.candidates[0].content.parts.length > 0) {
                const text = result.candidates[0].content.parts[0].text;
                const trendingSongs = text.split('\n').filter(line => line.trim() !== '');

                trendingSongsDisplay.innerHTML = ''; // Clear loading message

                if (trendingSongs.length > 0) {
                    const resultHeader = document.createElement('p');
                    resultHeader.className = 'font-semibold text-white mb-2';
                    resultHeader.textContent = `Top 10 Trending ${selectedCategory} Lagu:`;
                    trendingSongsDisplay.appendChild(resultHeader);

                    const ul = document.createElement('ul');
                    ul.className = 'space-y-2';
                    trendingSongs.forEach(song => {
                        const li = document.createElement('li');
                        li.className = 'suggested-song-item';
                        
                        const songTitleSpan = document.createElement('span');
                        songTitleSpan.textContent = song.trim();
                        songTitleSpan.className = 'text-gray-100 flex-grow mr-2';

                        const addButton = document.createElement('button');
                        addButton.textContent = "Tambahkan";
                        addButton.className = "text-sm bg-blue-500 hover:bg-blue-600 px-3 py-1 rounded-md shadow-md transition duration-200 ease-in-out";
                        addButton.onclick = () => {
                            addSongInput(song.trim()); // Add song directly to playlist and re-render
                        };
                        
                        li.appendChild(songTitleSpan);
                        li.appendChild(addButton);
                        ul.appendChild(li);
                    });
                    trendingSongsDisplay.appendChild(ul);
                } else {
                    trendingSongsDisplay.innerHTML = `<p class='italic text-gray-400'>Tidak dapat menemukan lagu trending untuk kategori ${selectedCategory}.</p>`;
                }

            } else {
                trendingSongsDisplay.innerHTML = `<p class='italic text-gray-400'>Gagal mendapatkan lagu trending. Coba lagi.</p>`;
            }
        } catch (error) {
            console.error("Error calling Gemini API for trending songs:", error);
            trendingSongsDisplay.innerHTML = `<p class='italic text-red-400'>Error: ${error.message}. Gagal mendapatkan lagu trending.</p>`;
        }
    }

    // Function to toggle video expansion
    function toggleVideoExpansion() {
        const videoPlayerContainer = document.getElementById('videoPlayerContainer');
        const mainContentWrapper = document.querySelector('.main-content-wrapper'); // Get the main content wrapper

        isVideoExpanded = !isVideoExpanded; // Toggle the state

        if (isVideoExpanded) {
            videoPlayerContainer.classList.add('video-player-expanded');
            // Remove original size constraints and margins to allow expansion
            videoPlayerContainer.classList.remove('max-w-6xl', 'aspect-video', 'mt-4'); 
            mainContentWrapper.style.display = 'none'; // Hide main content when video is expanded
        } else {
            videoPlayerContainer.classList.remove('video-player-expanded');
            // Restore original size constraints and margins
            videoPlayerContainer.classList.add('max-w-6xl', 'aspect-video', 'mt-4'); 
            mainContentWrapper.style.display = 'block'; // Show main content when video is normal size
        }
        // Force YouTube player to resize within its new container
        player.setSize('100%', '100%'); 
    }

    // Fungsi untuk menampilkan/menyembunyikan menu pengaturan
    function toggleSettingsMenu() {
      const settingsMenu = document.getElementById('settingsMenu');
      // Toggle visibility of the main settings menu
      settingsMenu.style.display = settingsMenu.style.display === 'block' ? 'none' : 'block';
      
      // Ensure that when the main settings menu is opened, the main options are visible
      // and the theme selection sub-menu is hidden.
      if (settingsMenu.style.display === 'block') {
          document.getElementById('mainSettingsOptions').style.display = 'block';
          document.getElementById('themeSelectionMenu').style.display = 'none';
      }
    }

    // Fungsi untuk menampilkan menu pemilihan tema
    function showThemeSelection() {
      document.getElementById('mainSettingsOptions').style.display = 'none'; // Hide main settings options
      document.getElementById('themeSelectionMenu').style.display = 'block'; // Show theme selection menu
    }

    // Fungsi untuk menyembunyikan menu pemilihan tema dan kembali ke pengaturan utama
    function hideThemeSelection() {
      document.getElementById('themeSelectionMenu').style.display = 'none'; // Hide theme selection menu
      document.getElementById('mainSettingsOptions').style.display = 'block'; // Show main settings options
    }

    // Fungsi untuk menerapkan tema yang dipilih
    function applyTheme(themeName) {
      // Remove all existing theme classes from body
      for (const theme in themes) {
        document.body.classList.remove(`theme-${theme}`);
      }
      // Add the selected theme class
      document.body.classList.add(`theme-${themeName}`);
      currentTheme = themeName; // Update current theme state

      // Update active theme button visual
      document.querySelectorAll('.theme-option-button').forEach(button => {
        button.classList.remove('active-theme');
      });
      document.querySelector(`.theme-option-button[data-theme="${themeName}"]`).classList.add('active-theme');

      // Update the "Ubah Tema" text in the main settings menu
      const themeToggleText = document.getElementById('themeToggleText');
      themeToggleText.textContent = `Ubah Tema: ${themes[themeName]}`;

      // Automatically hide theme selection menu after selection
      // hideThemeSelection(); // Removed this to keep settings menu open after theme change for better UX
      // toggleSettingsMenu(); // Removed this to keep settings menu open after theme change for better UX
    }
  
    function toggleSoundEffects() {
      soundEffectsOn = !soundEffectsOn;
      const soundEffectsToggleText = document.getElementById('soundEffectsToggleText');
      soundEffectsToggleText.textContent = `Efek Suara: ${soundEffectsOn ? 'ON' : 'OFF'}`;
    }

    function showAboutInfo() {
      const aboutModal = document.getElementById('aboutModal');
      aboutModal.style.display = 'flex';
      toggleSettingsMenu(); // Close settings menu when opening modal
    }

    function closeAboutModal() {
      const aboutModal = document.getElementById('aboutModal');
      aboutModal.style.display = 'none';
    }

    function togglePlayPause() {
      const state = player.getPlayerState();
      if (state === YT.PlayerState.PLAYING) {
        player.pauseVideo();
      } else {
        player.playVideo();
      }
    }

    function stopPlayback() {
      player.stopVideo();
    }

    function rewind() {
      const currentTime = player.getCurrentTime();
      player.seekTo(currentTime - 5, true);
    }

    function forward() {
      const currentTime = player.getCurrentTime();
      player.seekTo(currentTime + 5, true);
    }

    function volumeUp() {
      let vol = player.getVolume();
      if (vol < 100) player.setVolume(vol + 10);
    }

    function volumeDown() {
      let vol = player.getVolume();
      if (vol > 0) player.setVolume(vol - 10);
    }

    function nextTrack() {
      // This function now just calls playSong for the next track in the current playlist.
      // The playlist array itself is modified by onPlayerStateChange.
      if (playlist.length > 0) {
        playSong(playlist[0]); // Always play the first song in the *remaining* playlist
      }
    }

    function prevTrack() {
      // If there's a previous track concept, it would require storing history,
      // but with auto-removal, "previous" would mean re-adding.
      // For simplicity, if a user wants to go back, they'd re-add to the top of the playlist.
      // Or, this button could be disabled if there's no "previous" concept with auto-removal.
      // Keeping it as is for now, which means it will try to play the *current* song again if shifted.
      // A more robust solution might store a "history" of played songs.
      if (playlist.length > 0) {
        player.seekTo(0, true); // Restart current song if any
      }
    }

    // Initial state setup for theme and sound effects text and render initial playlist
    document.addEventListener('DOMContentLoaded', () => {
      applyTheme(currentTheme); 
      document.getElementById('soundEffectsToggleText').textContent = `Efek Suara: ${soundEffectsOn ? 'ON' : 'OFF'}`;
      // Removed the text for video expansion from here as it's now a direct icon button
      // document.getElementById('videoExpansionToggleText').textContent = `Perbesar Video`; // Initial text for expansion button

      // Ensure theme selection menu is hidden and main options are visible on initial load
      document.getElementById('themeSelectionMenu').style.display = 'none';
      document.getElementById('mainSettingsOptions').style.display = 'block';

      // Initial playlist items (example)
      playlist.push("Queen - Bohemian Rhapsody");
      playlist.push("Adele - Rolling in the Deep");
      playlist.push("Dewa 19 - Kangen");
      renderPlaylist(); // Render initial playlist
    });
</script>
</body>
</html>

    <script src="script.js"></script>
</body>
</html>
