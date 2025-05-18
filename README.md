<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JAMB Measurement Test</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background-color: #f9f9f9; }
    h1 { color: #333; }
    button { padding: 10px 20px; margin: 10px 0; cursor: pointer; }
    .question { margin-bottom: 20px; }
    .question p { margin: 5px 0; }
    .options input { margin-right: 8px; }
    .hidden { display: none; }
  </style>
</head>
<body>
  <h1>JAMB Past Questions on Measurement – Question Bank (500 Questions) by Adara Foundation</h1>
  <button onclick="startTest()">Start Test</button>
  <div id="timer"></div>
  <form id="quiz" class="hidden" onsubmit="submitTest(event)">
    <div class="question">
      <p>1. The internationally accepted system of units (SI) for physical measurement are:</p>
      <div class="options">
        <label><input type="radio" name="q1" value="A"> A. ft, lbf, sec, °F, gallon</label><br>
        <label><input type="radio" name="q1" value="B"> B. kg, sec, °C, cm, kgm/sec</label><br>
        <label><input type="radio" name="q1" value="C"> C. m, kg, sec K, A, mole, candela</label><br>
        <label><input type="radio" name="q1" value="D"> D. dm, gm, sec</label><br>
        <label><input type="radio" name="q1" value="E"> E. K, kg, m, sec</label>
      </div>
    </div>
    <!-- Add more questions here -->
    <button type="submit">Submit</button>
  </form>
  <div id="result"></div>  <script>
    let timerInterval;
    let totalTime = 1800; // 30 minutes

    function startTest() {
      document.getElementById('quiz').classList.remove('hidden');
      document.querySelector('button[onclick="startTest()"]')?.remove();
      startTimer();
    }

    function startTimer() {
      const timer = document.getElementById('timer');
      timerInterval = setInterval(() => {
        const minutes = Math.floor(totalTime / 60);
        const seconds = totalTime % 60;
        timer.textContent = `Time Left: ${minutes}m ${seconds}s`;
        totalTime--;
        if (totalTime < 0) {
          clearInterval(timerInterval);
          submitTest();
        }
      }, 1000);
    }

    function submitTest(event) {
      if (event) event.preventDefault();
      clearInterval(timerInterval);
      const answers = { q1: 'C' }; // Add more as you go
      let score = 0;
      let total = 1;
      let result = '<h3>Result:</h3>';
      for (let q in answers) {
        const userAnswer = document.querySelector(`input[name="${q}"]:checked`);
        if (userAnswer) {
          if (userAnswer.value === answers[q]) {
            score++;
            result += `<p>${q}: Correct</p>`;
          } else {
            result += `<p>${q}: Wrong (Correct: ${answers[q]})</p>`;
          }
        } else {
          result += `<p>${q}: Not Answered (Correct: ${answers[q]})</p>`;
        }
      }
      result += `<p><strong>Score: ${score}/${total}</strong></p>`;
      document.getElementById('quiz').classList.add('hidden');
      document.getElementById('result').innerHTML = result;
    }
  </script></body>
</html>
