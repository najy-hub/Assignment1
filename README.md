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

    input[type="text"],
    input[type="radio"],
    textarea {
      margin-top: 10px;
      margin-right: 10px;
    }

    input[type="text"] {
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    textarea {
      width: 100%;
      padding: 8px;
      border-radius: 8px;
      border: 1px solid #ccc;
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
    <p>🧑‍🎓 الاسم الكامل:</p>
    <input type="text" name="student_name" required placeholder="أدخل اسمك الثلاثي">
  </div>

  <div class="question">
    <p>1. السيليكون Si يحتوي في المدار الأخير على .... ذرات تساهمية؟</p>
    <input type="radio" name="q1" value="4"> 4
    <input type="radio" name="q1" value="3"> 3
    <input type="radio" name="q1" value="2"> 2
  </div>

  <div class="question">
    <p>2. أي نوع من أنواع الألواح أكبر تدهور من السنة الأولى؟</p>
    <input type="radio" name="q2" value="P-type"> P-type
    <input type="radio" name="q2" value="N-type"> N-type
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
    <textarea name="q7" rows="4" placeholder="اكتب إجابتك هنا..."></textarea>
  </div>

  <button type="submit">إرسال الإجابات</button>
</form>

<div id="resultBox"></div>

<script>
document.getElementById("quizForm").addEventListener("submit", function(e) {
  e.preventDefault();

  const answers = {
    name: document.querySelector('input[name="student_name"]').value.trim(),
    q1: document.querySelector('input[name="q1"]:checked')?.value.trim() || "",
    q2: document.querySelector('input[name="q2"]:checked')?.value.trim() || "",
    q3: document.querySelector('input[name="q3"]:checked')?.value.trim() || "",
    q4: document.querySelector('input[name="q4"]:checked')?.value.trim() || "",
    q5: document.querySelector('input[name="q5"]:checked')?.value.trim() || "",
    q6: document.querySelector('input[name="q6"]:checked')?.value.trim() || "",
    q7: document.querySelector('textarea[name="q7"]').value.trim() || ""
  };

  const correct = {
    q1: "4",
    q2: "N-type",
    q3: "STC",
    q4: "لا",
    q5: "Monocrystalline",
    q6: "50"
  };

  let score = 0;
  for (let i = 1; i <= 6; i++) {
    const userAnswer = (answers["q" + i] || "").trim().toLowerCase();
    const correctAnswer = (correct["q" + i] || "").trim().toLowerCase();
    if (userAnswer === correctAnswer) {
      score++;
    } else {
      console.warn(`❌ سؤال ${i} غير مطابق. المرسل: "${userAnswer}"، المتوقع: "${correctAnswer}"`);
    }
  }

  const resultBox = document.getElementById("resultBox");
  resultBox.style.display = "block";
  resultBox.innerHTML = `✅ مرحباً ${answers.name}<br>
  نتيجتك: ${score} من 6 (${Math.round(score / 6 * 100)}%)<br><br>
  ✍️ إجابتك النصية:<br>${answers.q7}`;

const resultData = {
  name: answers.name,
  score: `${score} من 6 (${Math.round(score / 6 * 100)}%)`
};

fetch("https://script.google.com/macros/s/AKfycbzcd6uA7SrtqbTB7cs3_EqnhNpPIuxRHadWJqGbz60BuCttcCf3NNCDPd1J5LntWrV19g/exec", {
  method: "POST",
  body: JSON.stringify(resultData),
  headers: {
    "Content-Type": "application/json",
  },
})
;

});
</script>

</body>
</html>
