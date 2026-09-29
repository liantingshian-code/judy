<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <title>全台展覽快速查詢</title>
    <style>
        body { font-family: sans-serif; padding: 20px; }
        .card { border: 1px solid #ccc; padding: 10px; margin: 10px 0; border-radius: 8px; }
        .tag { background: #eee; padding: 2px 8px; border-radius: 4px; font-size: 0.8em; }
    </style>
</head>
<body>
    <h1>全台展覽活動查詢</h1>
    <input type="text" id="searchInput" placeholder="搜尋類別 (例如: 親子)..." onkeyup="filterData()">
    <div id="eventList"></div>

    <script>
        fetch('data.json')
            .then(response => response.json())
            .then(data => {
                window.events = data;
                render(data);
            });

        function render(data) {
            const list = document.getElementById('eventList');
            list.innerHTML = data.map(e => `
                <div class="card">
                    <h3>${e.name}</h3>
                    <p>日期：${e.date} | 價格：${e.price}</p>
                    <span class="tag">${e.category}</span>
                </div>
            `).join('');
        }

        function filterData() {
            const val = document.getElementById('searchInput').value;
            const filtered = window.events.filter(e => e.category.includes(val) || e.name.includes(val));
            render(filtered);
        }
    </script>
</body>
</html>
