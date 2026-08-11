<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sify iWay | 2000s Cyber Cafe Nostalgia</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=VT323&family=Outfit:wght@300;400;700&family=Playfair+Display:ital@1&display=swap" rel="stylesheet">
    <style>
        :root {
            --xp-blue: #245edb;
            --xp-green: #3c813f;
            --glass: rgba(255, 255, 255, 0.1);
            --border: rgba(255, 255, 255, 0.2);
            --text-glow: 0 0 10px rgba(0, 255, 255, 0.5);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            cursor: url('https://cur.cursors-4u.net/windows/win-6/win518.cur'), auto;
        }

        body {
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            height: 100vh;
            overflow: hidden;
            font-family: 'Outfit', sans-serif;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: relative;
        }

        /* Scanline Overlay */
        body::before {
            content: " ";
            display: block;
            position: absolute;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.1) 50%), 
                        linear-gradient(90deg, rgba(255, 0, 0, 0.03), rgba(0, 255, 0, 0.01), rgba(0, 0, 255, 0.03));
            background-size: 100% 4px, 3px 100%;
            z-index: 10;
            pointer-events: none;
        }

        /* Retro Background Elements */
        .vibe-bg {
            position: absolute;
            width: 100%;
            height: 100%;
            background: url('https://images.unsplash.com/photo-1550751827-4bd374c3f58b?auto=format&fit=crop&q=80&w=2070') center/cover no-repeat;
            opacity: 0.15;
            filter: grayscale(100%) contrast(150%) blur(5px);
            z-index: -1;
        }

        .header {
            text-align: center;
            z-index: 5;
            margin-bottom: 2rem;
            animation: fadeInDown 1.5s ease;
        }

        .title {
            font-family: 'Playfair Display', serif;
            font-size: 5rem;
            font-weight: 700;
            letter-spacing: -2px;
            background: linear-gradient(to bottom, #ffffff 40%, #888 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 10px 20px rgba(0,0,0,0.5));
            margin-bottom: 0.5rem;
        }

        .subtitle {
            font-family: 'VT323', monospace;
            font-size: 1.5rem;
            color: #00ffcc;
            text-transform: uppercase;
            letter-spacing: 5px;
            opacity: 0.8;
        }

        /* Central Visual */
        .monitor-container {
            position: relative;
            width: 500px;
            height: 400px;
            background: #d1d1d1;
            border-radius: 40px 40px 10px 10px;
            border: 12px solid #b1b1b1;
            box-shadow: 0 50px 100px rgba(0,0,0,0.8), inset 0 -10px 0 #999;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            transition: transform 0.3s ease;
            animation: monitorFloat 6s ease-in-out infinite;
        }

        .monitor-container:hover {
            transform: scale(1.02) rotate(-1deg);
        }

        .screen {
            width: 92%;
            height: 85%;
            background: #1a1a1a;
            border-radius: 20px;
            position: relative;
            overflow: hidden;
            border: 4px solid #333;
            box-shadow: inset 0 0 50px #000;
        }

        .xp-desktop {
            width: 100%;
            height: 100%;
            background: url('https://i.imgur.com/86m2YwU.png') center/cover; /* Classic Bliss */
            opacity: 0.9;
            display: flex;
            flex-direction: column;
            padding: 20px;
        }

        .icon-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
        }

        .icon {
            display: flex;
            flex-direction: column;
            align-items: center;
            font-size: 0.7rem;
            text-align: center;
            transition: filter 0.2s;
        }

        .icon:hover { filter: brightness(1.2); }

        .icon img { width: 32px; margin-bottom: 5px; }

        /* Floating Quotes */
        .quote-container {
            margin-top: 30px;
            font-style: italic;
            height: 30px;
            color: #ccc;
            font-size: 1.1rem;
            text-align: center;
            text-shadow: 0 2px 4px rgba(0,0,0,0.5);
        }

        /* Music Player Overlay */
        .player-wrapper {
            position: fixed;
            bottom: 40px;
            width: 450px;
            background: var(--glass);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border: 1px solid var(--border);
            border-radius: 24px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 15px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
            z-index: 100;
            transition: all 0.3s ease;
        }

        .player-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .album-art {
            width: 50px;
            height: 50px;
            background: linear-gradient(45deg, #ff3366, #ffcc00);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            animation: pulse 2s infinite;
        }

        .track-details { flex-grow: 1; }
        .track-name { font-weight: 700; font-size: 1rem; color: #fff; }
        .artist-name { font-size: 0.8rem; color: #aaa; }

        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .btn {
            background: none;
            border: none;
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            padding: 10px;
            transition: transform 0.2s, opacity 0.2s;
        }

        .btn:hover { transform: scale(1.1); opacity: 0.8; }

        .progress-container {
            width: 100%;
            height: 4px;
            background: rgba(255,255,255,0.1);
            border-radius: 2px;
            overflow: hidden;
        }

        .progress-bar {
            width: 45%;
            height: 100%;
            background: #00ffcc;
            box-shadow: 0 0 10px #00ffcc;
        }

        /* Authentic Details */
        .status-labels {
            position: fixed;
            top: 40px;
            right: 40px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            font-family: 'VT323', monospace;
            text-align: right;
        }

        .label {
            background: rgba(0,0,0,0.6);
            padding: 5px 15px;
            border-left: 4px solid #f1c40f;
            font-size: 1.2rem;
            color: #f1c40f;
        }

        .label.red { border-left-color: #e74c3c; color: #e74c3c; }

        /* Animations */
        @keyframes monitorFloat {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }

        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes pulse {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.05); opacity: 0.8; }
            100% { transform: scale(1); opacity: 1; }
        }

        /* Hidden YT Iframe */
        #yt-player { display: none; }

        /* Click Interaction */
        .buzz-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255, 0, 255, 0.2);
            pointer-events: none;
            opacity: 0;
            z-index: 1000;
        }

        .buzz-anim { animation: buzzEffect 0.2s linear 3; }

        @keyframes buzzEffect {
            0% { opacity: 0; transform: translate(2px, 2px); }
            50% { opacity: 0.5; transform: translate(-2px, -2px); }
            100% { opacity: 0; transform: translate(0); }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .title { font-size: 3rem; }
            .monitor-container { width: 350px; height: 280px; }
            .player-wrapper { width: 90%; bottom: 20px; }
        }
    </style>
</head>
<body>

    <div class="vibe-bg"></div>
    <div class="buzz-overlay" id="buzz"></div>

    <div class="status-labels">
        <div class="label">RATE: RS. 20/HOUR</div>
        <div class="label">SCANNING/PRINTING AVAILABLE</div>
        <div class="label red">ID CARD COMPULSORY</div>
    </div>

    <div class="header">
        <h1 class="title">Sify iWay</h1>
        <p class="subtitle">Gateway to the World Wide Web</p>
    </div>

    <div class="monitor-container" onclick="playBuzz()">
        <div class="screen">
            <div class="xp-desktop">
                <div class="icon-grid">
                    <div class="icon"><img src="https://win98icons.alexmeub.com/icons/png/msie2-2.png"><span>Internet Explorer</span></div>
                    <div class="icon"><img src="https://win98icons.alexmeub.com/icons/png/directory_net_drive-4.png"><span>Network Neighborhood</span></div>
                    <div class="icon"><img src="https://win98icons.alexmeub.com/icons/png/msg_world-0.png"><span>Yahoo Messenger</span></div>
                    <div class="icon"><img src="https://win98icons.alexmeub.com/icons/png/joystick-0.png"><span>Counter-Strike</span></div>
                    <div class="icon"><img src="https://win98icons.alexmeub.com/icons/png/address_book_card_users-4.png"><span>Orkut</span></div>
                    <div class="icon"><img src="https://win98icons.alexmeub.com/icons/png/media_player_v2-0.png"><span>Winamp</span></div>
                </div>
            </div>
        </div>
    </div>

    <div class="quote-container" id="quote-box">
        "Bhaiya, time kitna hua?"
    </div>

    <div class="player-wrapper">
        <div class="player-info">
            <div class="album-art">📻</div>
            <div class="track-details">
                <div class="track-name" id="track-name">Loading Nostalgia...</div>
                <div class="artist-name">9XM / Channel V Era Hits</div>
            </div>
        </div>
        
        <div class="progress-container">
            <div class="progress-bar" id="progress"></div>
        </div>

        <div class="controls">
            <button class="btn" onclick="prevTrack()">⏮</button>
            <button class="btn" style="font-size: 2rem;" id="play-btn" onclick="togglePlay()">▶</button>
            <button class="btn" onclick="nextTrack()">⏭</button>
            <div style="font-family: 'VT323'; font-size: 1.2rem; color: #00ffcc;">ONLINE</div>
        </div>
    </div>

    <!-- YouTube Iframe API Placeholder -->
    <div id="yt-player"></div>

    <script>
        const quotes = [
            '"Bhaiya, time kitna hua?"',
            '"Abe, server join kar jaldi!"',
            '"Yahoo Messenger pe Buzz mat maar."',
            '"Net ki speed aaj bahut slow hai."',
            '"Log off kar ke jana, varna paise badhte rahenge."',
            '"Counter-Strike: de_dust2 only!"',
            '"Print out nikalna hai, black and white ya color?"',
            '"Bhaiya, 10 min extra de do please."'
        ];

        let quoteIndex = 0;
        const quoteBox = document.getElementById('quote-box');

        setInterval(() => {
            quoteBox.style.opacity = 0;
            setTimeout(() => {
                quoteIndex = (quoteIndex + 1) % quotes.length;
                quoteBox.textContent = quotes[quoteIndex];
                quoteBox.style.opacity = 1;
            }, 500);
        }, 4000);

        // Interaction Effect
        function playBuzz() {
            const buzz = document.getElementById('buzz');
            buzz.classList.add('buzz-anim');
            
            // Simulating Yahoo Buzz Sound (Synth)
            const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            
            osc.type = 'square';
            osc.frequency.setValueAtTime(150, audioCtx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(40, audioCtx.currentTime + 0.2);
            
            gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.2);
            
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            
            osc.start();
            osc.stop(audioCtx.currentTime + 0.2);

            setTimeout(() => buzz.classList.remove('buzz-anim'), 600);
        }

        // Music Player Logic (YouTube API)
        let player;
        const playlistId = 'PL64G6j8eW9uI-gXInZ6Xv8_Z9mS3O7J6n'; // 2000s Bollywood Mashup

        function onYouTubeIframeAPIReady() {
            player = new YT.Player('yt-player', {
                height: '0',
                width: '0',
                playerVars: {
                    'listType': 'playlist',
                    'list': playlistId,
                    'autoplay': 0,
                    'controls': 0
                },
                events: {
                    'onReady': onPlayerReady,
                    'onStateChange': onPlayerStateChange
                }
            });
        }

        function onPlayerReady(event) {
            updateTrackName();
        }

        function onPlayerStateChange(event) {
            if (event.data == YT.PlayerState.PLAYING) {
                document.getElementById('play-btn').textContent = '⏸';
                updateTrackName();
                startProgress();
            } else {
                document.getElementById('play-btn').textContent = '▶';
            }
        }

        function togglePlay() {
            const state = player.getPlayerState();
            if (state == YT.PlayerState.PLAYING) player.pauseVideo();
            else player.playVideo();
        }

        function nextTrack() { player.nextVideo(); }
        function prevTrack() { player.previousVideo(); }

        function updateTrackName() {
            const data = player.getVideoData();
            if (data && data.title) {
                document.getElementById('track-name').textContent = data.title.substring(0, 35) + '...';
            }
        }

        function startProgress() {
            setInterval(() => {
                if (player && player.getCurrentTime) {
                    const curr = player.getCurrentTime();
                    const dur = player.getDuration();
                    const perc = (curr / dur) * 100;
                    document.getElementById('progress').style.width = perc + '%';
                }
            }, 1000);
        }

        // Load YT API
        const tag = document.createElement('script');
        tag.src = "https://www.youtube.com/iframe_api";
        const firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
    </script>
</body>
</html>
