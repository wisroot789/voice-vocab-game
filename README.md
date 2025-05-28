<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Voice Vocab Game</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 40px;
      background-color: #f0f4f8;
    }
    h1 {
      color: #333;
    }
    input, button {
      padding: 10px;
      margin: 10px;
      font-size: 18px;
    }
    .qr {
      margin-top: 30px;
    }
    #result {
      font-weight: bold;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <h1>🎤 เกมทายคำศัพท์ภาษาอังกฤษด้วยเสียง</h1>
  <p>กด “เริ่มพูด” เพื่อฟังคำศัพท์ แล้วพิมพ์คำแปลภาษาไทย</p>

  <button onclick="speakWord()">เริ่มพูด</button><br>
  <input type="text" id="answer" placeholder="คำแปลเป็นภาษาไทย">
  <button onclick="checkAnswer()">ตรวจคำตอบ</button>

  <p id="result"></p>

  <div class="qr">
    <h3>เปิดเกมผ่านเว็บไซต์:</h3>
    <a href="https://wisroot789.github.io/voice-vocab-game/" target="_blank">
      <img src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=https://wisroot789.github.io/voice-vocab-game/" alt="QR Code to Game">
    </a>
  </div>

  <script>
    const vocab = [
      { word: "apple", meaning: "แอปเปิ้ล" },
      { word: "dog", meaning: "สุนัข" },
      { word: "school", meaning: "โรงเรียน" },
      { word: "book", meaning: "หนังสือ" },
      { word: "computer", meaning: "คอมพิวเตอร์" },
      { word: "cat", meaning: "แมว" },
      { word: "water", meaning: "น้ำ" },
      { word: "chair", meaning: "เก้าอี้" }
    ];

    let currentWord = "";

    function speakWord() {
      const random = vocab[Math.floor(Math.random() * vocab.length)];
      currentWord = random.word;
      const utterance = new SpeechSynthesisUtterance(currentWord);
      speechSynthesis.speak(utterance);
      document.getElementById("result").textContent = ""; // ล้างผลลัพธ์เดิม
    }

    function checkAnswer() {
      const userAnswer = document.getElementById("answer").value.trim();
      const correct = vocab.find(v => v.word === currentWord)?.meaning;

      if (userAnswer === correct) {
        document.getElementById("result").textContent = "✅ ถูกต้อง!";
        document.getElementById("result").style.color = "green";
      } else {
        document.getElementById("result").textContent = `❌ คำตอบคือ: ${correct}`;
        document.getElementById("result").style.color = "red";
      }
    }
  </script>

</body>
</html>
