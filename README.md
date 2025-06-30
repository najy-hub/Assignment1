<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>اختبار Assignment 1 - الطاقة الشمسية</title>
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      background: #f2f2f2;
      padding: 20px;
      color: #333;
      max-width: 800px;
      margin: auto;
    }
    h2 { color: #00695c; }
    .question { margin-bottom: 25px; background: #fff; padding: 15px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
    button { background: #00695c; color: #fff; padding: 10px 20px; border: none; border-radius: 6px; cursor: pointer; }
    .result { font-weight: bold; margin-top: 20px; }
  </style>
</head>
<body>

<h2>📘 Assignment 1 - اختبار الطاقة الشمسية</h2>
<form id="quizForm">

  <div class="question">
    <p>1. السيليكون Si يحتوى فى المدار الاخير على .... ذرات تساهميه؟</p>
    <input type="radio" name="q1" value="2"> 2<br>
    <input type="radio" name="q1" value="3"> 3<br>
    <input type="radio" name="q1" value="4"> 4
  </div>

  <div class="question">
    <p>2. أي نوع من أنواع الألواح أكبر تدهور من السنة الأولى؟</p>
    <input type="radio" name="q2" value="P.type"> P.type<br>
    <input type="radio" name="q2" value="N.type"> N.type
  </div>

  <div class="question">
    <p>3. أي من نتائج الاختبارات تستخدم للمقارنة بين الألواح؟</p>
    <input type="radio" name="q3" value="STC"> STC<br>
    <input type="radio" name="q3" value="NOCT"> NOCT
  </div>

  <div class="question">
    <p>4. هل Air Mass المكتوبة على الألواح تعني كتلة الهواء المار خلال الألواح؟</p>
    <input type="radio" name="q4" value="نعم"> نعم<br>
    <input type="radio" name="q4" value="لا"> لا
  </div>

  <div class="question">
    <p>5. أي أنواع الألواح أكثر تأثراً بدرجة الحرارة؟</p>
    <input type="radio" name="q5" value="Monocrystalline"> Monocrystalline<br>
    <input type="radio" name="q5" value="Polycrystalline"> Polycrystalline
  </div>

  <div class="question">
    <p>6. إذا كانت درجة حرارة البيئة Ambient Temperature 35°C، ما هي درجة حرارة الخلية المتوقعة؟</p>
    <input type="radio" name="q6" value="25"> 25<br>
    <input type="radio" name="q6" value="40"> 40<br>
    <input type="radio" name="q6" value="50"> 50
  </div>

  <div class="question">
    <p>7. اكتب باختصار الاستراتيجية العامة المقترحة لاختيار الألواح لمشروع معين؟ (مثال: نظام 10 كيلوواط سكني)</p>
    <textarea name="q7" rows="4" style="width:100%" placeholder="اكتب هنا..."></textarea>
  </div>

  <button type="submit">إرسال الإجابات</button>
</form>

<div class="result" id="resultBox"></div>

<script>
document.getElementById('quizForm').addEventListener('submit', function(e) {
  e.preventDefault();

  const correctAnswers = {
    q1: '4',
    q2: 'P.type',
    q3: 'NOCT',
    q4: 'لا',
    q5: 'Polycrystalline',
    q6: '50'
  };

  let score = 0;
  for (let i = 1; i <= 6; i++) {
    const selected = document.querySelector(`input[name="q${i}"]:checked`);
    if (selected && selected.value === correctAnswers[`q${i}`]) score++;
  }

  const q7Text = document.querySelector('textarea[name="q7"]').value;
  const percentage = Math.round((score / 6) * 100);
  document.getElementById('resultBox').innerHTML =
    `✅ نتيجتك: ${score} من 6 (${percentage}%)<br><br>📌 إجابتك النصية:<br>${q7Text}`;

  // لإرسال النتائج إلى Google Sheets (اختياري)
  /*
  fetch('https://script.google.com/macros/s/XXX/exec', {
    method: 'POST',
    body: JSON.stringify({
      q1: document.querySelector('input[name="q1"]:checked')?.value || "",
      q2: document.querySelector('input[name="q2"]:checked')?.value || "",
      q3: document.querySelector('input[name="q3"]:checked')?.value || "",
      q4: document.querySelector('input[name="q4"]:checked')?.value || "",
      q5: document.querySelector('input[name="q5"]:checked')?.value || "",
      q6: document.querySelector('input[name="q6"]:checked')?.value || "",
      q7: q7Text
    }),
    headers: { 'Content-Type': 'application/json' }
  });
  */
});
</script>
</body>
</html>
