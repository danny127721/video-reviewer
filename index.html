<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video Review Tool Pro</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2"></script>
    <style>
        :root { --primary: #3498db; --success: #2ed573; --warning: #ffa502; --danger: #ff4757; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background: #121212; color: #e0e0e0; margin: 0; padding: 10px; }
        .container { max-width: 1000px; margin: auto; background: #1e1e1e; padding: 20px; border-radius: 16px; box-shadow: 0 8px 32px rgba(0,0,0,0.5); }
        .upload-area { border: 2px dashed #444; padding: 20px; border-radius: 12px; margin-bottom: 20px; cursor: pointer; text-align: center; }
        .upload-area:hover { border-color: var(--primary); background: #252525; }
        video { width: 100%; border-radius: 12px; background: #000; }
        .btn-group { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; margin: 20px 0; }
        button { padding: 15px; font-size: 18px; border: none; border-radius: 10px; cursor: pointer; font-weight: bold; color: white; transition: 0.2s; }
        .btn-bad { background: var(--danger); }
        .btn-mark { background: var(--warning); }
        .btn-good { background: var(--success); }
        .charts-section { background: white; padding: 20px; border-radius: 12px; display: flex; flex-wrap: wrap; gap: 20px; margin-top: 20px; color: #333; }
        .chart-wrapper { flex: 1; min-width: 300px; position: relative; }
        #logBox { background: #000; color: #00ff00; padding: 10px; border-radius: 8px; font-family: monospace; height: 60px; overflow-y: auto; font-size: 12px; margin: 10px 0; text-align: left; }
        .export-btn { background: var(--primary); width: 100%; margin-top: 20px; padding: 15px; font-size: 18px; border-radius: 50px; }
        input[type="file"] { display: none; }
    </style>
</head>
<body>

<div class="container">
    <div class="upload-area" onclick="document.getElementById('videoInput').click()">
        <span id="uploadHint">📂 點擊選擇影片檔案</span>
        <input type="file" id="videoInput" accept="video/*">
    </div>

    <video id="myVideo" controls></video>

    <div id="logBox">>> 系統就緒...</div>

    <div class="btn-group">
        <button class="btn-bad" onclick="recordAction(-1, '倒讚')">👎 1: 倒讚</button>
        <button class="btn-mark" onclick="recordAction(0, '標記')">📌 2: 標記</button>
        <button class="btn-good" onclick="recordAction(1, '讚')">👍 3: 讚</button>
    </div>

    <div class="charts-section">
        <div class="chart-wrapper">
            <h4 style="margin:0 0 10px 0; text-align:center;">情緒起伏波動圖</h4>
            <canvas id="lineChart"></canvas>
        </div>
        <div class="chart-wrapper" style="max-width: 250px; margin: auto;">
            <h4 style="margin:0 0 10px 0; text-align:center;">評價佔比</h4>
            <canvas id="pieChart"></canvas>
        </div>
    </div>

    <button class="export-btn" onclick="exportData()">💾 下載數據分析報告 (CSV)</button>
</div>

<script>
    Chart.register(ChartDataLabels);
    const video = document.getElementById('myVideo');
    const videoInput = document.getElementById('videoInput');
    let reviewData = [];
    let counts = { '讚': 0, '標記': 0, '倒讚': 0 };

    videoInput.onchange = function() {
        const file = this.files[0];
        if (file) {
            document.getElementById('uploadHint').innerText = "當前影片：" + file.name;
            video.src = URL.createObjectURL(file);
            video.play();
            resetApp();
        }
    };

    function resetApp() {
        reviewData = [];
        counts = { '讚': 0, '標記': 0, '倒讚': 0 };
        lineChart.data.labels = [];
        lineChart.data.datasets[0].data = [];
        lineChart.update();
        pieChart.data.datasets[0].data = [0,0,0];
        pieChart.update();
    }

    function formatTime(s) {
        return `${Math.floor(s/60).toString().padStart(2,'0')}:${Math.floor(s%60).toString().padStart(2,'0')}`;
    }

    // --- 改良版情緒波動圖 ---
    const ctxLine = document.getElementById('lineChart').getContext('2d');
    const lineChart = new Chart(ctxLine, {
        type: 'line',
        data: {
            labels: [],
            datasets: [{
                label: '情緒值',
                data: [],
                borderColor: '#3498db',
                borderWidth: 2,
                tension: 0.3,
                fill: false,
                // 設定點的顏色：根據數值變色
                pointBackgroundColor: function(context) {
                    const v = context.raw;
                    if (v === 1) return '#2ed573';  // 讚：綠色
                    if (v === 0) return '#ffa502';  // 標記：橘色
                    if (v === -1) return '#ff4757'; // 倒讚：紅色
                    return '#333';
                },
                pointBorderColor: '#fff',
                pointRadius: 7,
                pointHoverRadius: 9
            }]
        },
        options: {
            scales: {
                y: {
                    min: -1.2,
                    max: 1.2,
                    ticks: {
                        stepSize: 1,
                        // 強制顯示文字註明
                        callback: function(value) {
                            if (value === 1) return '讚 👍';
                            if (value === 0) return '標記 📌';
                            if (value === -1) return '倒讚 👎';
                            return '';
                        },
                        font: { weight: 'bold', size: 14 }
                    }
                }
            },
            plugins: {
                legend: { display: false },
                datalabels: { display: false }
            }
        }
    });

    // --- 圓餅圖 ---
    const ctxPie = document.getElementById('pieChart').getContext('2d');
    const pieChart = new Chart(ctxPie, {
        type: 'pie',
        data: {
            labels: ['讚', '標記', '倒讚'],
            datasets: [{
                data: [0, 0, 0],
                backgroundColor: ['#2ed573', '#ffa502', '#ff4757']
            }]
        },
        options: {
            plugins: {
                datalabels: {
                    color: '#fff',
                    font: { weight: 'bold' },
                    formatter: (v, ctx) => {
                        let sum = 0;
                        ctx.chart.data.datasets[0].data.map(d => sum += d);
                        return sum > 0 ? `${((v*100)/sum).toFixed(0)}%` : "";
                    }
                }
            }
        }
    });

    function recordAction(score, label) {
        if (!video.src) return alert("請先選擇影片");
        const time = formatTime(video.currentTime);
        reviewData.push({ time, score, label });
        counts[label]++;
        
        lineChart.data.labels.push(time);
        lineChart.data.datasets[0].data.push(score);
        lineChart.update();
        
        pieChart.data.datasets[0].data = [counts['讚'], counts['標記'], counts['倒讚']];
        pieChart.update();

        document.getElementById('logBox').innerHTML = `[${time}] 記錄：${label}<br>` + document.getElementById('logBox').innerHTML;
    }

    window.onkeydown = (e) => {
        if(e.key === '1') recordAction(-1, '倒讚');
        if(e.key === '2') recordAction(0, '標記');
        if(e.key === '3') recordAction(1, '讚');
    };

    function exportData() {
        let csv = "\uFEFF時間,評價,分數\n";
        reviewData.forEach(d => csv += `${d.time},${d.label},${d.score}\n`);
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement("a");
        a.href = URL.createObjectURL(blob);
        a.download = "video_report.csv";
        a.click();
    }
</script>
</body>
</html>
