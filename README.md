# translation-game
<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <title>لعبة الترجمة الإنجليزية ↔ العربية</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f8ff;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #333;
    }
    .question {
      font-size: 24px;
      margin: 20px 0;
    }
    button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 6px;
      border: 1px solid #007BFF;
      background-color: #fff;
      color: #007BFF;
      transition: 0.3s;
    }
    button:hover {
      background-color: #007BFF;
      color: #fff;
    }
    #feedback {
      margin-top: 15px;
      font-weight: bold;
      font-size: 20px;
    }
    #nextBtn {
      margin-top: 20px;
      padding: 10px 25px;
      font-size: 18px;
      display: none;
    }
  </style>
</head>
<body>
  <h1>لعبة الترجمة الإنجليزية ↔ العربية</h1>
  <div class="question" id="question">جارٍ تحميل السؤال...</div>
  <div id="options"></div>
  <div id="feedback"></div>
  <button id="nextBtn" onclick="nextQuestion()">السؤال التالي</button>

  <script>
    const questions = [
      {q: "What is the Arabic for 'apple'?", options: ["تفاحة", "موز", "كتاب"], answer: "تفاحة"},
      {q: "ما الترجمة الإنجليزية لكلمة 'شمس'؟", options: ["moon", "sun", "rain"], answer: "sun"},
      {q: "What is the Arabic for 'book'?", options: ["قلم", "كتاب", "كرسي"], answer: "كتاب"},
      {q: "ما الترجمة الإنجليزية لكلمة 'قطة'؟", options: ["dog", "cat", "fish"], answer: "cat"},
      {q: "What is the Arabic for 'tree'?", options: ["جبل", "شجرة", "سيارة"], answer: "شجرة"},
    ];

    let currentIndex = 0;

    function loadQuestion() {
      document.getElementById("feedback").innerText = "";
      document.getElementById("nextBtn").style.display = "none";

      let q = questions[currentIndex];
      document.getElementById("question").innerText = q.q;

      let optionsDiv = document.getElementById("options");
      optionsDiv.innerHTML = "";

      q.options.forEach(option => {
        let btn = document.createElement("button");
        btn.innerText = option;
        btn.onclick = () => checkAnswer(option);
        optionsDiv.appendChild(btn);
      });
    }

    function checkAnswer(selected) {
      let q = questions[currentIndex];
      let feedback = document.getElementById("feedback");

      if (selected === q.answer) {
        feedback.innerText = "✅ إجابة صحيحة!";
        feedback.style.color = "green";
      } else {
        feedback.innerText = "❌ إجابة خاطئة! الإجابة الصحيحة: " + q.answer;
        feedback.style.color = "red";
      }

      // تعطيل الأزرار بعد الإجابة
      Array.from(document.getElementById("options").children).forEach(btn => {
        btn.disabled = true;
      });

      document.getElementById("nextBtn").style.display = "inline-block";
    }

    function nextQuestion() {
      currentIndex = (currentIndex + 1) % questions.length;
      loadQuestion();
    }

    window.onload = loadQuestion;
  </script>
</body>
</html>
