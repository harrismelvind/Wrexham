<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wrexham AFC Dashboard</title>
    <style>
        body { 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; 
            background: #111; 
            color: #ddd; 
            margin: 0; 
            padding: 15px; 
            font-size: 14px;
        }
        h1 { text-align: center; color: #cf142b; font-size: 1.5rem; margin-bottom: 20px; }
        .dashboard { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px; max-width: 1000px; margin: 0 auto; }
        .card { background: #181818; padding: 15px; border-radius: 8px; border-top: 3px solid #cf142b; }
        h2 { color: #fff; font-size: 1.1rem; border-bottom: 1px solid #333; padding-bottom: 8px; margin-top: 0; text-transform: uppercase; }
        
        .yt-link, .wiki-btn { 
            color: #fff; text-decoration: none; display: block; padding: 8px; 
            margin: 6px 0; background: #222; border-radius: 4px; font-weight: bold; font-size: 0.9rem;
        }
        .wiki-btn { background: #005a8d; text-align: center; margin-top: 15px; }
        .yt-link:hover, .wiki-btn:hover { opacity: 0.8; }

        a.news-item { color: #58a6ff; text-decoration: none; display: block; margin-bottom: 10px; font-weight: bold; }
        small { color: #888; font-size: 0.8rem; }
        
        li { margin-bottom: 8px; border-bottom: 1px solid #222; padding-bottom: 5px; }
        .date-badge { color: #cf142b; font-weight: bold; margin-right: 5px; }
    </style>
</head>
<body>

    <h1>WREXHAM AFC</h1>
    
    <div class="dashboard">
        <div class="card">
            <h2>📰 Latest Updates</h2>
            <div id="headlines-container">Fetching...</div>
        </div>

        <div class="card">
            <h2>📺 Creator Hub</h2>
            <a href="https://www.youtube.com/@WxmAFCofficial" class="yt-link" target="_blank">Official Wrexham AFC</a>
            <a href="https://www.youtube.com/@fearlessindevotion" class="yt-link" target="_blank">Fearless In Devotion</a>
            <a href="https://www.youtube.com/channel/UCRWvluNDYv3dRtgESD0vxRw" class="yt-link" target="_blank">RobRyanRed</a>
            <a href="https://www.youtube.com/@WrexhamAFCfanzone" class="yt-link" target="_blank">Wrexham AFC Fanzone</a>
            <a href="https://en.wikipedia.org/wiki/Wrexham" class="wiki-btn" target="_blank">City of Wrexham (Wikipedia)</a>
        </div>

        <div class="card">
            <h2>📅 2026 Preseason</h2>
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
                // Widened search: Wrexham AFC, Transfers, or Parkinson
                const response = await fetch(`https://newsapi.org/v2/everything?q=(Wrexham%20AFC%20OR%20transfer%20OR%20Parkinson)&sortBy=publishedAt&apiKey=${apiKey}`);
                const data = await response.json();
                
                if(data.articles && data.articles.length > 0) {
                    container.innerHTML = data.articles.slice(0, 6).map(a => 
                        `<div><a class="news-item" href="${a.url}" target="_blank">${a.title}</a><small>${new Date(a.publishedAt).toLocaleDateString()}</small></div>`
                    ).join('');
                } else {
                    container.innerHTML = "No new updates found.";
                }
            } catch (e) {
                container.innerHTML = "Update feed unavailable.";
            }
        }
        fetchTransferNews();
    </script>
</body>
</html>
