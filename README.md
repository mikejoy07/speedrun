<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Đồng hồ bấm giờ</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      margin-top: 100px;
      background-color: #f5f5f5;
    }
    h1 {
      font-size: 48px;
    }
    #time {
      font-size: 64px;
      margin: 20px;
    }
    button {
      font-size: 20px;
      margin: 10px;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
    button:disabled {
      background-color: #aaa;
      cursor: default;
    }
  </style>
</head>
<body>
  <h1>Đồng hồ bấm giờ</h1>
  <div id="time">00:00:00</div>
  <div>
    <button id="startBtn">Bắt đầu</button>
    <button id="pauseBtn" disabled>Tạm dừng</button>
    <button id="resetBtn">Reset</button>
  </div>

  <script>
    let startTime = 0;
    let elapsed = 0;
    let timerInterval;
    let running = false;

    function formatTime(ms) {
      const totalSeconds = Math.floor(ms / 1000);
      const hours = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
      const minutes = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
      const seconds = String(totalSeconds % 60).padStart(2, '0');
      return `${hours}:${minutes}:${seconds}`;
    }

    function updateTime() {
      const now = Date.now();
      const diff = now - startTime + elapsed;
      document.getElementById('time').textContent = formatTime(diff);
    }

    document.getElementById('startBtn').addEventListener('click', () => {
      if (!running) {
        startTime = Date.now();
        timerInterval = setInterval(updateTime, 1000);
        running = true;
        document.getElementById('startBtn').textContent = 'Tiếp tục';
        document.getElementById('pauseBtn').disabled = false;
      }
    });

    document.getElementById('pauseBtn').addEventListener('click', () => {
      if (running) {
        clearInterval(timerInterval);
        elapsed += Date.now() - startTime;
        running = false;
        document.getElementById('pauseBtn').disabled = true;
      }
    });

    document.getElementById('resetBtn').addEventListener('click', () => {
      clearInterval(timerInterval);
      startTime = 0;
      elapsed = 0;
      running = false;
      document.getElementById('time').textContent = '00:00:00';
      document.getElementById('startBtn').textContent = 'Bắt đầu';
      document.getElementById('pauseBtn').disabled = true;
    });
  </script>
</body>
</html>
