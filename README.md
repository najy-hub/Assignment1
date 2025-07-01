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

    .question label {
      display: block;
      margin: 8px 0;
      cursor: pointer;
    }

    input[type="text"],
    textarea {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    input[type="radio"] {
      margin-left: 8px;
    }

    textarea {
      resize: vertical;
      min-height: 100px;
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

    @media (max-width: 600px) {
      button {
        width: 100%;
      }
    }
  </style>
</head>
<body>

<h2>📘 اختبار Assignment 1 - الطاقة الشمسية</h2>

<form action="https://script.google.com/macros/s/AKfycbwC5mD_MT7LK83IQJJ1fiwRkinhMDjQZQkaTCQcL6sX8KlMuU4tXDgwyn_Xzlxw_mPiyA/exec" method="POST" target="hidden_iframe" onsubmit="return handleSubmit();">
  <div class="question">
    <p>🧑‍🎓 الاسم الكامل:</p>
    <input type="text" name="name" required placeholder="أدخل اسمك الثلاثي">
  </div>

  <div class="question">
    <p>1. السيليكون Si يحتوي في المدار الأخير على .... ذرات تساهمية؟</p>
    <label><input type="radio" name="q1" value="4"> 4</label>
    <label><input type="radio" name="q1" value="3"> 3</label>
    <label><input type="radio" name="q1" value="2"> 2</label>
  </div>

  <div class="question">
    <p>2. أي نوع من أنواع الألواح أكبر تدهور من السنة الأولى؟</p>
    <label><input type="radio" name="q2" value="P-type"> P-type</label>
    <label><input type="radio" name="q2" value="N-type"> N-type</label>
  </div>

  <div class="question">
    <p>3. أي من نتائج الاختبارات تستخدم للمقارنة بين الألواح؟</p>
    <label><input type="radio" name="q3" value="STC"> STC</label>
    <label><input type="radio" name="q3" value="NOCT"> NOCT</label>
  </div>

  <div class="question">
    <p>4. هل Air Mass المكتوبة على الألواح تعني كتلة الهواء المار خلال الألواح؟</p>
    <label><input type="radio" name="q4" value="نعم"> نعم</label>
    <label><input type="radio" name="q4" value="لا"> لا</label>
  </div>

  <div class="question">
    <p>5. أي أنواع الألواح أكثر تأثراً بدرجة الحرارة؟</p>
    <label><input type="radio" name="q5" value="Monocrystalline"> Monocrystalline</label>
    <label><input type="radio" name="q5" value="Polycrystalline"> Polycrystalline</label>
  </div>

  <div class="question">
    <p>6. إذا كانت درجة حرارة البيئة Ambient Temperature 35°C، ما هي درجة حرارة الخلية المتوقعة؟</p>
    <label><input type="radio" name="q6" value="25"> 25</label>
    <label><input type="radio" name="q6" value="40"> 40</label>
    <label><input type="radio" name="q6" value="50"> 50</label>
  </div>

  <div class="question">
    <p>7. ✍️ اكتب باختصار الاستراتيجية العامة لاختيار الألواح لمشروع 10 كيلوواط سكني:</p>
    <textarea name="q7" rows="4" placeholder="اكتب إجابتك هنا..."></textarea>
  </div>

  <input type="hidden" name="score" id="scoreField">
  <button type="submit">إرسال الإجابات</button>
</form>

<div id="resultBox"></div>
<iframe name="hidden_iframe" style="display:none;"></iframe>

<script>
function handleSubmit() {
  const correct = {
    q1: "4",
    q2: "P-type",
    q3: "NOCT",
    q4: "لا",
    q5: "Polycrystalline",
    q6: "50"
  };

  let score = 0;
  for (let i = 1; i <= 6; i++) {
    const selected = document.querySelector(`input[name="q${i}"]:checked`);
    if (selected && selected.value === correct[`q${i}`]) {
      score++;
    }
  }

  const percentage = Math.round((score / 6) * 100);
  const resultText = `${score} من 6 (${percentage}%)`;
  document.getElementById("scoreField").value = resultText;

  const name = document.querySelector('input[name="name"]').value;
  const q7 = document.querySelector('textarea[name="q7"]').value;

  const box = document.getElementById("resultBox");
  box.style.display = "block";
  box.innerHTML = `✅ مرحبًا ${name}<br> نتيجتك: ${resultText}<br><br>✍️ إجابتك:<br>${q7}`;

  return true;
}
</script>

</body>
</html>
