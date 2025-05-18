<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>JAMB Measurement Question Bank - Adara Foundation</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 20px; background: #f5f5f5; }
    h1 { color: #2c3e50; text-align: center; }
    .container { max-width: 800px; margin: auto; background: white; padding: 20px; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    .question { margin-bottom: 20px; }
    .options label { display: block; margin-bottom: 10px; cursor: pointer; }
    .submit-btn, .start-btn { background: #3498db; color: white; padding: 10px 20px; border: none; border-radius: 4px; cursor: pointer; }
    .timer { float: right; font-weight: bold; }
    .hidden { display: none; }
  </style>
</head>
<body>
  <h1>JAMB Measurement Question Bank - 100 Questions<br><small>by Adara Foundation</small></h1>
  <div class="container">
    <div id="startScreen">
      <p>This quiz contains 100 questions on Measurement (Physics). You have 30 minutes. Click Start when ready.</p>
      <button class="start-btn" onclick="startQuiz()">Start Quiz</button>
    </div><div id="quizScreen" class="hidden">
  <div class="timer">Time: <span id="time">30:00</span></div>
  <div id="questionContainer"></div>
  <button class="submit-btn" onclick="submitQuiz()">Submit</button>
</div>

<div id="resultScreen" class="hidden">
  <h2>Quiz Completed</h2>
  <p id="score"></p>
  <div id="corrections"></div>
</div>

  </div>  <script>
    const questions = [
      // Insert the 100 questions here as JS objects:
      // e.g. { q: "Question?", options: ["A", "B", "C", "D", "E"], answer: 1 },
      // Paste your generated question code below this line.

      { q: "The reading of a micrometer screw gauge is 5.50mm. If the actual diameter is 5.46mm, the percentage error is", options: ["0.73%", "0.36%", "0.80%", "0.66%", "0.44%"], answer: 0 },
      { q: "The correct unit of moment of a force is", options: ["Nm⁻¹", "Nm", "Nm²", "Nm⁻²", "Nm³"], answer: 1 },
      { q: "Which of the following are scalar quantities?", options: ["I, II and III", "I, III and IV", "I, II, IV and V", "I, II and IV", "I, II and V"], answer: 4 },
      { q: "Which of the following is NOT a scalar?", options: ["Electrical charge", "Electric potential", "Time", "Kinetic energy", "Impulse"], answer: 4 },
      // Continue pasting up to 100...
    ];

    let currentQuestion = 0;
    let userAnswers = [];
    let timer;
    let timeRemaining = 30 * 60; // 30 minutes in seconds

    function startQuiz() {
      document.getElementById("startScreen").classList.add("hidden");
      document.getElementById("quizScreen").classList.remove("hidden");
      showQuestion();
      startTimer();
    }

    function startTimer() {
      timer = setInterval(() => {
        timeRemaining--;
        const mins = Math.floor(timeRemaining / 60);
        const secs = timeRemaining % 60;
        document.getElementById("time").textContent = `${mins}:${secs < 10 ? '0' : ''}${secs}`;
        if (timeRemaining <= 0) {
          clearInterval(timer);
          submitQuiz();
        }
      }, 1000);
    }

    function showQuestion() {
      const container = document.getElementById("questionContainer");
      container.innerHTML = "";
      questions.forEach((question, index) => {
        const qDiv = document.createElement("div");
        qDiv.classList.add("question");
        qDiv.innerHTML = `<p><strong>Q${index + 1}:</strong> ${question.q}</p>`;

        const optionsDiv = document.createElement("div");
        optionsDiv.classList.add("options");

        question.options.forEach((option, i) => {
          const optionId = `q${index}_opt${i}`;
          const label = document.createElement("label");
          label.innerHTML = `<input type="radio" name="q${index}" value="${i}" id="${optionId}"> ${option}`;
          optionsDiv.appendChild(label);
        });

        qDiv.appendChild(optionsDiv);
        container.appendChild(qDiv);
      });
    }

    function submitQuiz() {
      clearInterval(timer);
      userAnswers = [];
      let score = 0;
      const corrections = [];

      questions.forEach((q, i) => {
        const options = document.getElementsByName(`q${i}`);
        let selected = -1;
        for (let opt of options) {
          if (opt.checked) selected = parseInt(opt.value);
        }
        userAnswers.push(selected);
        if (selected === q.answer) {
          score++;
        } else {
          corrections.push(`<p><strong>Q${i + 1}:</strong> ${q.q}<br>Correct Answer: ${q.options[q.answer]}</p>`);
        }
      });

      document.getElementById("quizScreen").classList.add("hidden");
      document.getElementById("resultScreen").classList.remove("hidden");
      document.getElementById("score").innerHTML = `You scored <strong>${score}</strong> out of ${questions.length}`;
      document.getElementById("corrections").innerHTML = corrections.join("<hr>");
    }
  </script></body>
</html>
