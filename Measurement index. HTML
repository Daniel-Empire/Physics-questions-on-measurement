<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>JAMB Past Questions: Measurement Question Bank</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background-color: #f7f7f7;
    }
    h1 {
      text-align: center;
      color: #2c3e50;
    }
    .quiz-container {
      max-width: 800px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .question {
      margin: 20px 0;
    }
    .timer {
      font-weight: bold;
      color: red;
      text-align: right;
    }
    .start-btn, .submit-btn {
      padding: 10px 20px;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .correct {
      color: green;
    }
    .wrong {
      color: red;
    }
  </style>
</head>
<body>
  <h1>JAMB Past Questions on Measurement – Question Bank (500 Questions)</h1>
  <div class="quiz-container">
    <div id="timer" class="timer">Time Left: 30:00</div>
    <button class="start-btn" onclick="startQuiz()">Start Quiz</button>
    <form id="quiz-form" style="display:none;"></form>
    <div id="result"></div>
  </div>  <script>
    const questions = [
      {
        q: "Which of the following is a base quantity?",
        options: ["Speed", "Volume", "Length", "Area"],
        answer: 2
      },
      {
        q: "The S.I unit of temperature is:",
        options: ["Degree Celsius", "Kelvin", "Fahrenheit", "Rankine"],
        answer: 1
      },
      // Add more questions up to 500 here...
    ];

    let timerInterval;
    let timeLeft = 30 * 60; // 30 minutes in seconds

    function startQuiz() {
      document.querySelector('.start-btn').style.display = 'none';
      document.getElementById('quiz-form').style.display = 'block';
      showQuestions();
      startTimer();
    }

    function startTimer() {
      timerInterval = setInterval(() => {
        if (timeLeft <= 0) {
          clearInterval(timerInterval);
          document.getElementById('quiz-form').requestSubmit();
        } else {
          timeLeft--;
          const mins = String(Math.floor(timeLeft / 60)).padStart(2, '0');
          const secs = String(timeLeft % 60).padStart(2, '0');
          document.getElementById('timer').textContent = `Time Left: ${mins}:${secs}`;
        }
      }, 1000);
    }

    function showQuestions() {
      const form = document.getElementById('quiz-form');
      form.innerHTML = '';

      questions.forEach((q, index) => {
        const div = document.createElement('div');
        div.className = 'question';
        div.innerHTML = `<p>${index + 1}. ${q.q}</p>`;

        q.options.forEach((opt, i) => {
          div.innerHTML += `
            <label>
              <input type="radio" name="q${index}" value="${i}" required>
              ${opt}
            </label><br>`;
        });

        form.appendChild(div);
      });

      const submitBtn = document.createElement('button');
      submitBtn.textContent = 'Submit';
      submitBtn.className = 'submit-btn';
      submitBtn.type = 'submit';
      form.appendChild(submitBtn);

      form.addEventListener('submit', function(e) {
        e.preventDefault();
        clearInterval(timerInterval);
        const formData = new FormData(form);
        let score = 0;
        let resultHTML = '';

        questions.forEach((q, i) => {
          const userAnswer = parseInt(formData.get(`q${i}`));
          if (userAnswer === q.answer) {
            score++;
            resultHTML += `<p>${i+1}. ${q.q} <span class="correct">Correct</span></p>`;
          } else {
            resultHTML += `<p>${i+1}. ${q.q} <span class="wrong">Wrong</span> (Correct: ${q.options[q.answer]})</p>`;
          }
        });

        resultHTML = `<h2>You scored ${score} out of ${questions.length}</h2>` + resultHTML;
        document.getElementById('quiz-form').style.display = 'none';
        document.getElementById('result').innerHTML = resultHTML;
      });
    }
  </script></body>
</html>
