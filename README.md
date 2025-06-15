<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>เพื่อนรับฟังของคุณ</title>
  <style>
    body {
      font-family: 'Prompt', sans-serif;
      text-align: center;
      padding: 50px 20px;
      background: linear-gradient(to bottom, #e0f7fa, #ffffff);
      position: relative;
      overflow: hidden;
      margin: 0;
    }
    #page2 {
      display: none;
    }
    #note {
      width: 100%;
      max-width: 500px;
      height: 240px;
      margin: 20px auto;
      font-size: 18px;
      padding: 20px 25px;
      border: 1px solid #ccc;
      border-radius: 8px;
      resize: none;
      background-color: #fef9e7;
      background-image: repeating-linear-gradient(to bottom, #ddd 0, #ddd 1px, transparent 1px, transparent 24px);
      background-size: 100% 24px;
      line-height: 24px;
      color: #333;
      font-family: 'Courier New', Courier, monospace;
      box-shadow: 0 0 8px rgba(0,0,0,0.15);
      transition: transform 0.3s ease;
      position: relative;
      z-index: 10;
      text-align: left;
      box-sizing: border-box;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      border: none;
      border-radius: 10px;
      background-color: #ff6f61;
      color: white;
      cursor: pointer;
      max-width: 90vw;
    }
    button:hover {
      background-color: #e64a19;
    }
    .fade {
      animation: fadeIn 1.5s ease-in-out forwards;
      opacity: 0;
    }
    @keyframes fadeIn {
      to { opacity: 1; }
    }
    @keyframes burn {
      0% { opacity: 1; transform: scale(1) translateY(0); filter: brightness(1); }
      100% { opacity: 0; transform: scale(0.8) translateY(-100px); filter: brightness(0.1); }
    }
    @keyframes flame {
      0% { opacity: 1; transform: scale(2.5) translateY(0); }
      30% { opacity: 1; transform: scale(3.5) translateY(-20px); }
      60% { opacity: 0.9; transform: scale(3) translateY(-40px); }
      100% { opacity: 0; transform: scale(2.2) translateY(-60px); }
    }
    .flame {
      position: absolute;
      width: 50px;
      height: 100px;
      background: radial-gradient(circle, #ffffcc, #ff6600, #990000);
      border-radius: 50%;
      animation: flame 1.2s ease-in-out infinite;
      pointer-events: none;
      z-index: 60;
      mix-blend-mode: screen;
      opacity: 0.95;
    }
    .ash {
      position: absolute;
      width: 2px;
      height: 10px;
      background: #555;
      opacity: 0.8;
      animation: fall 3s ease-in forwards;
    }
    .smoke {
      position: absolute;
      width: 40px;
      height: 40px;
      background: radial-gradient(closest-side, rgba(200,200,200,0.5), transparent);
      border-radius: 50%;
      animation: rise 4s ease-out forwards;
      pointer-events: none;
      z-index: 40;
    }
    @keyframes rise {
      to {
        transform: translateY(-200px) scale(2);
        opacity: 0;
      }
    }
    @keyframes fall {
      to {
        transform: translateY(200px) scale(0.5);
        opacity: 0;
      }
    }
    @keyframes fadeInUp {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    @media (max-width: 600px) {
      body {
        padding: 30px 15px;
      }
      h1, h2 {
        font-size: 1.5rem;
      }
      button {
        font-size: 14px;
        padding: 8px 16px;
      }
    }
  </style>
</head>
<body>
  <audio id="burnSound" src="https://cdn.pixabay.com/audio/2021/12/15/audio_1d42944f45.mp3"></audio>
  <audio id="bgMusic" src="https://cdn.pixabay.com/audio/2023/04/10/audio_2055023ed8.mp3" autoplay loop></audio>

  <div id="page1">
    <h1>ยินดีที่ได้เจอคุณ</h1>
    <p>ผมจะเป็นเพื่อนที่รับฟังคุณ</p>
    <button onclick="goToPage2()">ระบายให้ฉันฟัง</button>
  </div>

  <div id="page2">
    <h2>ระบายความรู้สึกของคุณ</h2>
    <textarea id="note" placeholder="เขียนอะไรก็ได้ที่คุณรู้สึก..."></textarea><br>
    <button onclick="burnNote()">เผาความเศร้า</button>
    <div id="message" class="fade" style="margin-top: 30px; font-size: 20px; color: #333; display: none;"></div>
  </div>

  <script>
    function goToPage2() {
      document.getElementById('page1').style.display = 'none';
      document.getElementById('page2').style.display = 'block';
    }

    function burnNote() {
      const note = document.getElementById('note');
      const burnSound = document.getElementById('burnSound');
      burnSound.play();
      note.style.animation = 'burn 2.5s ease-in-out forwards';

      for (let i = 0; i < 60; i++) {
        const flame = document.createElement('div');
        flame.className = 'flame';
        flame.style.left = (note.offsetLeft + Math.random() * note.offsetWidth) + 'px';
        flame.style.top = (note.offsetTop + note.offsetHeight - 10 - Math.random() * 20) + 'px';
        document.body.appendChild(flame);
        setTimeout(() => flame.remove(), 2000);
      }

      for (let i = 0; i < 40; i++) {
        const ash = document.createElement('div');
        ash.className = 'ash';
        ash.style.left = (note.offsetLeft + Math.random() * note.offsetWidth) + 'px';
        ash.style.top = (note.offsetTop + Math.random() * note.offsetHeight) + 'px';
        document.body.appendChild(ash);
        setTimeout(() => ash.remove(), 3000);
      }

      for (let i = 0; i < 35; i++) {
        const smoke = document.createElement('div');
        smoke.className = 'smoke';
        smoke.style.left = (note.offsetLeft + Math.random() * note.offsetWidth) + 'px';
        smoke.style.top = (note.offsetTop + Math.random() * note.offsetHeight) + 'px';
        document.body.appendChild(smoke);
        setTimeout(() => smoke.remove(), 4000);
      }

      setTimeout(() => {
        const message = document.getElementById('message');
        message.innerHTML = `
          <div style="animation: fadeInUp 2.5s ease-in-out forwards; margin-top: 0; padding-top: 5px;">
            <p style="font-size: 18px; color: #444; margin-bottom: 10px;">ขอให้เราได้ช่วยเป็นสิ่งหนึ่งในการรับฟังและระบายของคุณ<br>เราจะอยู่ข้างคุณเสมอ</p>
            <p style="margin-top: 5px;">ระบายสิ่งที่ไม่สบายใจอีกรอบ</p>
            <br><button onclick=\"resetPage()\">กลับไประบายอีกครั้ง</button>
          </div>`;
        message.classList.add('fade');
        message.style.display = 'block';
        message.style.opacity = '1';
      }, 2600);
    }

    function resetPage() {
      const note = document.getElementById('note');
      const message = document.getElementById('message');
      note.style.display = 'block';
      note.style.marginTop = '20px';
      note.value = '';
      note.style.animation = '';
      message.style.display = 'none';
      message.innerHTML = '';
    }
  </script>
</body>
</html>
