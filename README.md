<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <title>نموذج اختبار</title>
</head>
<body>
  <h2>اختبار تجربة الإرسال</h2>
  <form id="testForm">
    <label>الاسم:</label>
    <input type="text" id="name" required />
    <button type="submit">إرسال</button>
  </form>

  <p id="result"></p>

  <script>
    document.getElementById("testForm").addEventListener("submit", function(e) {
      e.preventDefault();

      const name = document.getElementById("name").value;

      fetch("https://script.google.com/macros/s/AKfycbzz6kNU5DPE4MVLIUr2mI4wZ6xLWARJ-vXeldHMp7D7dekauOEKEI-ihs2xB2M3GCaQjw/exec", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ name })
      })
      .then(res => res.text())
      .then(text => {
        document.getElementById("result").innerText = "✅ " + text;
      })
      .catch(err => {
        document.getElementById("result").innerText = "❌ حدث خطأ: " + err;
      });
    });
  </script>
</body>
</html>
