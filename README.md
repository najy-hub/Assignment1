<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>اختبار Assignment 1</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      background: #e3f2fd;
      padding: 20px;
      color: #333;
    }

    h2 {
      text-align: center;
      color: #1565c0;
      margin-bottom: 30px;
    }

    .question {
      background: #ffffff;
      padding: 20px;
      margin-bottom: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }

    .question:hover {
      transform: scale(1.01);
    }

    .question p {
      font-weight: bold;
      color: #0d47a1;
    }

    input[type="radio"], textarea {
      margin-top: 10px;
      margin-right: 10px;
    }

    button {
      display: block;
      margin: 30px auto;
      padding: 14px 28px;
      background: #1976d2;
      color: #fff;
      border: none;
      border-radius: 10px;
      font-size: 18px;
      cursor: pointer;
      transition: background 0.3s, transform 0.2s;
    }

    button:hover {
      background: #0d47a1;
      transform: scale(1.03);
    }

    #resultBox {
      text-align: center;
      font-weight: bold;
      margin-top: 20px;
      color: #1b5e20;
      background: #c8e6c9;
      padding: 20px;
      border-radius: 12px;
      border: 2px solid #66bb6a;
      display: none;
    }
  </style>
</head>
<body>

<h2>📘 اختبار Assignment 1 - الطاقة الشمسية</h2>

<form id="quizForm">
  <div class="question">
    <p>1. السيليكون Si يحتوى فى المدار الاخير على .... ذرات تساهميه؟</p>
    <input type="radio" name="q1" value="2"> 2
    <input type="radio" name="q1" value="3"> 3
    <input type="radio" name="q1" value="4"> 4
  </div>

  <div class="question">
    <p>2. أي نوع من أنواع الألواح أكبر تدهور من السنة الأولى؟</p>
    <input type="radio" name="q2" value="P.type"> P-type
    <input type="radio" name="q2" value="N.type"> N-type
  </div>

  <div class="question">
    <p>3. أي من نتائج الاختبارات تستخدم للمقارنة بين الألواح؟</p>
    <input type="radio" name="q3" value="STC"> STC
    <input type="radio" name="q3" value="NOCT"> NOCT
  </div>

  <div class="question">
    <p>4. هل Air Mass المكتوبة على الألواح تعني كتلة الهواء المار خلال الألواح؟</p>
    <input type="radio" name="q4" value="نعم"> نعم
    <input type="radio" name="q4" value="لا"> لا
  </div>

  <div class="question">
    <p>5. أي أنواع الألواح أكثر تأثراً بدرجة الحرارة؟</p>
    <input type="radio" name="q5" value="Monocrystalline"> Monocrystalline
    <input type="radio" name="q5" value="Polycrystalline"> Polycrystalline
  </div>

  <div class="question">
    <p>6. إذا كانت درجة حرارة البيئة Ambient Temperature 35°C، ما هي درجة حرارة الخلية المتوقعة؟</p>
    <input type="radio" name="q6" value="25"> 25
    <input type="radio" name="q6" value="40"> 40
    <input type="radio" name="q6" value="50"> 50
  </div>

  <div class="question">
    <p>7. ✍️ اكتب باختصار الاستراتيجية العامة لاختيار الألواح لمشروع 10 كيلوواط سكني:</p>
    <textarea name="q7" rows="4" style="width:100%" placeholder="اكتب إجابتك هنا..."></textarea>
  </div>

  <button type="submit">إرسال الإجابات</button>
</form>

<div id="resultBox"></div>

<script>
document.getElementById("quizForm").addEventListener("submit", function(e) {
  e.preventDefault();

  const answers = {};
  for (let i = 1; i <= 6; i++) {
    answers["q" + i] = document.querySelector(`input[name="q${i}"]:checked`)?.value || "";
  }
  answers["q7"] = document.querySelector('textarea[name="q7"]').value || "";

  const correct = {
    q1: "4", q2: "P.type", q3: "NOCT", q4: "لا", q5: "Polycrystalline", q6: "50"
  };

  let score = 0;
  for (let i = 1; i <= 6; i++) {
    if (answers["q" + i] === correct["q" + i]) score++;
  }

  const resultBox = document.getElementById("resultBox");
  resultBox.style.display = "block";
  resultBox.innerHTML = `✅ نتيجتك: ${score} من 6 (${Math.round(score / 6 * 100)}%)<br><br>
  📌 إجابتك الأخيرة:<br>${answers.q7}`;

  // إرسال إلى Google Sheets
  fetch("https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec", {
    method: "POST",
    body: JSON.stringify(answers),
    headers: {
      "Content-Type": "application/json",
    },
  });
});
</script>

</body>
</html>
