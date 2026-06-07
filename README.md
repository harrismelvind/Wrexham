<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wrexham AFC Fan Dashboard</title>
    <style>
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            background: #111; 
            color: #fff; 
            margin: 0; 
            padding: 20px; 
        }
        h1 {
            text-align: center;
            color: #cf142b;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 30px;
        }
        .dashboard { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); 
            gap: 25px; 
            max-width: 1200px;
            margin: 0 auto;
        }
        .card { 
            background: #1a1a1a; 
            padding: 25px; 
            border-radius: 12px; 
            border-top: 4px solid #cf142b; 
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }
        h2 { 
            color: #fff; 
            font-size: 1.4rem;
            border-bottom: 2px solid #2d2d2d; 
            padding-bottom: 12px; 
            margin-top: 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .yt-link { 
            color: #e1e1e1; 
            text-decoration: none; 
            display: flex;
            align-items: center;
            padding: 12px;
            margin: 10px 0; 
            background: #242424;
            border-radius: 6px;
            transition: all 0.2s ease;
            font-weight: 500;
        }
        .yt-link:hover {
            background: #cf142b;
            color: #fff;
            transform: translateX(5px);
        }
        .yt-link::before {
            content: "▶";
            margin-right: 10px;
            color: #cf142b;
            transition: color 0.2s ease;
        }
        .yt-link:hover::before {
            color: #fff;
        }
        a.news-item { 
            color: #58a6ff; 
            text-decoration: none; 
            display: block; 
            margin-bottom: 15px;
        }
        a.news-item:hover {
            text-decoration: underline;
        }
        ul { list-style: none; padding: 0; margin: 0; }
        li { 
            margin-bottom: 15px; 
            padding-bottom: 10px; 
            border-bottom: 1px solid #2d2d2d; 
            font-size: 0.95rem;
        }
        li:last-child { border-bottom: none; }
        .date-badge {
            background: #cf142b;
            color: white;
            padding: 2px 6px;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: bold;
            margin-right: 5px;
        }
    </style>
</head>
<body>

    <h1>🔴 Wrexham AFC Command Center</h1>
    
    <div class="dashboard">
        <!-- 1. NEWS HEADLINES -->
        <div class="card" id="news-section">
            <h2>📰 Flagged Rumors & News</h2>
            <div id="headlines-container">Loading transfer updates...</div>
        </div>

        <!-- 2. YOUTUBE HUB -->
        <div class="card">
            <h2>📺 Creator Hub</h2>
            <a href="https://www.youtube.com/@WxmAFCofficial" class="yt-link" target="_blank">Official Wrexham AFC YouTube Channel</a>
            <a href="https://www.youtube.com/@fearlessindevotion" class="yt-link" target="_blank">Fearless In Devotion Podcast</a>
            <a href="https://www.youtube.com/channel/UCRWvluNDYv3dRtgESD0vxRw" class="yt-link" target="_blank">RobRyanRed Wrexham AFC Podcast</a>
            <a href="https://www.youtube.com/@WrexhamAFCfanzone" class="yt-link" target="_blank">Wrexham AFC Fanzone</a>
        </div>

        <!-- 3. FIXTURES -->
        <div class="card">
            <h2>📅 Preseason & Beyond</h2>
            <ul>
                <li><span class="date-badge">JUL 11</span> <strong>vs Wisła Kraków</strong><br><small>Synerise Arena, Kraków (POL)</small></li>
                <li><span class="date-badge">JUL 18</span> <strong>vs Manchester United</strong><br><small>Olympic Stadium, Helsinki (FIN)</small></li>
                <li><span class="date-badge">JUL 25</span> <strong>vs Leeds United</strong><br><small>Raymond James Stadium, Tampa (USA)</small></li>
                <li><span class="date-badge">JUL 29</span> <strong>vs Liverpool</strong><br><small>Yankee Stadium, New York (USA)</small></li>
                <li><span class="date-badge">AUG 02</span> <strong>vs Sunderland</strong><br><small>Subaru Park, Philadelphia (USA)</small></li>
            </ul>
        </div>
    </div>

    <script>
        async function fetchTransferNews() {
            const container = document.getElementById('headlines-container');
            try {
                // Your active functional NewsAPI key is successfully mapped below
                const response = await fetch('https://newsapi.org/v2/everything?q=Wrexham+transfer&sortBy=publishedAt&apiKey=465ac406127e480fb5a393972c1f9d87');
                const data = await response.json();
                
                if(data.articles && data.articles.length > 0) {
                    container.innerHTML = data.articles.slice(0, 5).map(article => 
                        `<div style="margin-bottom: 15px;">
                            <a class="news-item" href="${article.url}" target="_blank"><strong>${article.title}</strong></a>
                            <small style="color: #888;">${new Date(article.publishedAt).toLocaleDateString()}</small>
                        </div>`
                    ).join('');
                } else {
                    container.innerHTML = "<p style='color: #888;'>No new headlines flagged in the last 24 hours.</p>";
                }
            } catch (error) {
                container.innerHTML = "<p style='color: #888;'>Failed to reach NewsAPI. Check network connection.</p>";
            }
        }
        
        fetchTransferNews();
    </script>
</body>
</html>
