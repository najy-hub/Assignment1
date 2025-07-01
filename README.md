<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <title>نموذج الاختبار</title>
</head>
<body>
  <h1>اختبار سريع</h1>

  <form id="quizForm">
    <label>اسمك:</label><br>
    <input type="text" name="name" required><br><br>

    <label>السؤال 1:</label><br>
    <input type="text" name="q1"><br><br>

    <label>السؤال 2:</label><br>
    <input type="text" name="q2"><br><br>

    <label>السؤال 3:</label><br>
    <input type="text" name="q3"><br><br>

    <button type="submit">إرسال</button>
  </form>

  <script>
    const form = document.getElementById("quizForm");
    form.addEventListener("submit", function(e) {
      e.preventDefault();

      const formData = new FormData(form);
      const answers = {};
      formData.forEach((value, key) => {
        answers[key] = value;
      });

      fetch("https://script.google.com/macros/s/AKfycbzJp2DumutANZDcS9Y5gA81Jafz5RP9JOQZOmrwBTqUOMTq4fnCxlyrFWDNpsFgOqHX/exec", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(answers)
      })
      .then(response => response.text())
      .then(text => alert(text))
      .catch(error => console.error("خطأ:", error));
    });
  </script>
</body>
</html>
