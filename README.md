<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Championship & Wrexham Hub</title>
    <style>
        body { 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; 
            background: #111; 
            color: #ccc; 
            margin: 0; 
            padding: 12px; 
            font-size: 13px;
            line-height: 1.4;
        }
        .app-header {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin: 10px 0 20px 0;
        }
        .app-header img {
            height: 35px;
            width: auto;
        }
        h1 { 
            color: #cf142b; 
            font-size: 1.3rem; 
            margin: 0;
            letter-spacing: 0.5px;
            text-transform: uppercase;
        }
        .dashboard { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(290px, 1fr)); 
            gap: 12px; 
            max-width: 1000px; 
            margin: 0 auto; 
        }
        .card { 
            background: #161616; 
            padding: 14px; 
            border-radius: 6px; 
            border-top: 3px solid #cf142b; 
        }
        h2 { 
            color: #fff; 
            font-size: 1rem; 
            border-bottom: 1px solid #282828; 
            padding-bottom: 6px; 
            margin-top: 0; 
            margin-bottom: 12px;
            text-transform: uppercase; 
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .header-icon {
            height: 18px;
            width: auto;
            object-fit: contain;
        }
        
        .yt-link, .wiki-btn { 
            color: #fff; 
            text-decoration: none; 
            display: block; 
            padding: 8px 10px; 
            margin: 5px 0; 
            background: #222; 
            border-radius: 4px; 
            font-weight: bold; 
            font-size: 0.85rem;
            transition: background 0.2s;
        }
        .wiki-btn { background: #005a8d; text-align: center; margin-top: 12px; }
        .yt-link:hover { background: #cf142b; }
        .wiki-btn:hover { opacity: 0.9; }

        .news-wrapper { display: flex; flex-direction: column; gap: 10px; }
        a.news-item { 
            color: #58a6ff; 
            text-decoration: none; 
            display: block; 
            font-weight: 700; 
            font-size: 0.9rem;
            margin-bottom: 2px;
        }
        a.news-item:hover { text-decoration: underline; }
        small { color: #777; font-size: 0.75rem; display: block; }
        
        ul { list-style: none; padding: 0; margin: 0; }
        li { 
            margin-bottom: 8px; 
            border-bottom: 1px solid #222; 
            padding-bottom: 6px; 
            font-size: 0.85rem;
        }
        li:last-child { border-bottom: none; margin-bottom: 0; padding-bottom: 0; }
        .date-badge { color: #cf142b; font-weight: bold; margin-right: 6px; }
    </style>
</head>
<body>

    <div class="app-header">
        <img src="https://cdn.freebiesupply.com/logos/large/2x/wrexham-afc-logo-png-transparent.png" alt="Wrexham AFC Badge">
        <h1>Wrexham & Championship Hub</h1>
    </div>
    
    <div class="dashboard">
        <!-- 1. NEWS COLUMN -->
        <div class="card">
            <h2>
                <img src="https://png.pngtree.com/png-vector/20240531/ourlarge/pngtree-red-dragon-silhouette-mascot-logo-design-full-body-vector-icon-png-image_12587332.png" class="header-icon" alt="Dragon Icon">
                Championship Transfers
            </h2>
            <div id="headlines-container" class="news-wrapper">Fetching live market updates...</div>
        </div>

        <!-- 2. CREATOR HUB & WIKI -->
        <div class="card">
            <h2>
                <img src="https://img.freeflagicons.com/thumb/round_icon/wales/wales_640.png" class="header-icon" alt="Wales Flag">
                Media & Info
            </h2>
            <a href="https://www.youtube.com/@WxmAFCofficial" class="yt-link" target="_blank">Official Wrexham AFC</a>
            <a href="https://www.youtube.com/@fearlessindevotion" class="yt-link" target="_blank">Fearless In Devotion</a>
            <a href="https://www.youtube.com/channel/UCRWvluNDYv3dRtgESD0vxRw" class="yt-link" target="_blank">RobRyanRed</a>
            <a href="https://www.youtube.com/@WrexhamAFCfanzone" class="yt-link" target="_blank">Wrexham AFC Fanzone</a>
            <a href="https://en.wikipedia.org/wiki/Wrexham" class="wiki-btn" target="_blank">City of Wrexham (Wikipedia)</a>
        </div>

        <!-- 3. PRESEASON FIXTURES -->
        <div class="card">
            <h2>📅 Preseason Schedule</h2>
            <ul>
                <li><span class="date-badge">JUL 18</span> Manchester United (Helsinki)</li>
                <li><span class="date-badge">JUL 25</span> Leeds United (Tampa)</li>
                <li><span class="date-badge">JUL 29</span> Liverpool (New York)</li>
                <li><span class="date-badge">AUG 02</span> Sunderland (Philadelphia)</li>
            </ul>
        </div>
    </div>

    <script>
        async function fetchTransferNews() {
            const container = document.getElementById('headlines-container');
            const apiKey = '465ac406127e480fb5a393972c1f9d87';
            try {
                const response = await fetch(`https://newsapi.org/v2/everything?q=("EFL Championship" AND transfer AND (rumor OR signing OR contract OR Wrexham))&sortBy=publishedAt&language=en&apiKey=${apiKey}`);
                const data = await response.json();
                
                if(data.articles && data.articles.length > 0) {
                    container.innerHTML = data.articles.slice(0, 6).map(a => 
                        `<div>
                            <a class="news-item" href="${a.url}" target="_blank">${a.title}</a>
                            <small>${new Date(a.publishedAt).toLocaleDateString()} via ${a.source.name || 'EFL News'}</small>
                        </div>`
                    ).join('');
                } else {
                    container.innerHTML = "<p style='color: #777; margin: 0;'>No broad Championship rumors indexed in the last 24 hours. Pre-window quiet period.</p>";
                }
            } catch (e) {
                container.innerHTML = "<p style='color: #777; margin: 0;'>Update feed temporarily unavailable.</p>";
            }
        }
        fetchTransferNews();
    </script>
</body>
</html>
