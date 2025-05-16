<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Physics Measurement Quiz</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background-color: #f4f4f4;
    }
    h1 {
      text-align: center;
    }
    .timer {
      text-align: center;
      font-size: 20px;
      margin-bottom: 20px;
    }
    form {
      background: white;
      padding: 20px;
      border-radius: 8px;
      max-width: 800px;
      margin: auto;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .question {
      margin-bottom: 15px;
    }
    .submit-btn {
      display: block;
      width: 100%;
      padding: 10px;
      background-color: #28a745;
      color: white;
      font-size: 18px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .result {
      text-align: center;
      font-size: 22px;
      margin-top: 20px;
    }
  </style>
</head>
<body><h1>Physics Quiz: Measurements</h1>
<div class="timer" id="timer">Time Left: 30:00</div><form id="quizForm">
  <!-- Questions will be inserted here by JavaScript -->
  <button type="submit" class="submit-btn">Submit</button>
</form>
<div class="result" id="result"></div><script>
const questions = [
  { q: "Which of the following is a base quantity?", options: ["Speed", "Length", "Area", "Volume"], answer: 1 },
  { q: "The SI unit of time is:", options: ["Minute", "Second", "Hour", "Day"], answer: 1 },
  { q: "Which instrument is used to measure mass?", options: ["Thermometer", "Stopwatch", "Spring balance", "Voltmeter"], answer: 2 },
  { q: "Which unit is used to measure electric current?", options: ["Ohm", "Volt", "Ampere", "Coulomb"], answer: 2 },
  { q: "Which prefix represents one billionth (10^-9)?", options: ["Micro", "Nano", "Milli", "Pico"], answer: 1 },
  { q: "The basic SI unit of length is:", options: ["Inch", "Metre", "Centimetre", "Foot"], answer: 1 },
  { q: "Which of the following is not a base quantity?", options: ["Length", "Mass", "Speed", "Time"], answer: 2 },
  { q: "Instrument used to measure temperature is:", options: ["Thermometer", "Barometer", "Ammeter", "Hygrometer"], answer: 0 },
  { q: "Derived quantity among these is:", options: ["Mass", "Area", "Time", "Length"], answer: 1 },
  { q: "Which physical quantity is measured in kilograms?", options: ["Mass", "Time", "Length", "Speed"], answer: 0 },
  { q: "Which of these quantities is scalar?", options: ["Velocity", "Force", "Acceleration", "Speed"], answer: 3 },
  { q: "Volume is measured in:", options: ["m", "m^2", "m^3", "kg"], answer: 2 },
  { q: "What does a stopwatch measure?", options: ["Mass", "Temperature", "Time interval", "Area"], answer: 2 },
  { q: "Micrometer screw gauge measures:", options: ["Length", "Mass", "Current", "Volume"], answer: 0 },
  { q: "Which of the following is not a unit of length?", options: ["Meter", "Kilogram", "Centimeter", "Millimeter"], answer: 1 },
  { q: "1 kilometer is equal to how many meters?", options: ["10", "100", "1000", "10000"], answer: 2 },
  { q: "Which of these is used to measure small thickness?", options: ["Ruler", "Thermometer", "Vernier caliper", "Barometer"], answer: 2 },
  { q: "Which unit is used for measuring frequency?", options: ["Hz", "s", "m", "kg"], answer: 0 },
  { q: "Which of the following is not an SI base unit?", options: ["Candela", "Kelvin", "Newton", "Mole"], answer: 2 },
  { q: "The prefix 'kilo' stands for:", options: ["10", "100", "1000", "10000"], answer: 2 },
  { q: "Force is measured in:", options: ["Joule", "Newton", "Watt", "Ampere"], answer: 1 },
  { q: "Which instrument measures atmospheric pressure?", options: ["Barometer", "Thermometer", "Hygrometer", "Anemometer"], answer: 0 },
  { q: "A standard kilogram is defined by:", options: ["A platinum-iridium cylinder", "Mass of water", "A stone", "Mass of gold"], answer: 0 },
  { q: "The unit 'joule' is used to measure:", options: ["Force", "Work", "Power", "Speed"], answer: 1 },
  { q: "Which instrument is used to measure electric current?", options: ["Voltmeter", "Ammeter", "Wattmeter", "Galvanometer"], answer: 1 },
  { q: "What is the SI unit of energy?", options: ["Joule", "Watt", "Volt", "Ohm"], answer: 0 },
  { q: "Power is measured in:", options: ["Joule", "Watt", "Volt", "Ampere"], answer: 1 },
  { q: "Which of these instruments measures voltage?", options: ["Voltmeter", "Ammeter", "Galvanometer", "Thermometer"], answer: 0 },
  { q: "Which of the following is a vector quantity?", options: ["Speed", "Temperature", "Force", "Distance"], answer: 2 },
  { q: "Which of the following is a scalar quantity?", options: ["Displacement", "Acceleration", "Velocity", "Time"], answer: 3 },
  { q: "Which unit is equivalent to kg·m/s²?", options: ["Joule", "Watt", "Newton", "Pascal"], answer: 2 },
  { q: "Work is equal to:", options: ["Force × Time", "Mass × Distance", "Force × Distance", "Distance / Time"], answer: 2 },
  { q: "The SI unit of pressure is:", options: ["Bar", "Pascal", "Newton", "Joule"], answer: 1 },
  { q: "1 liter is equal to:", options: ["1000 cm³", "100 cm³", "10 cm³", "1 cm³"], answer: 0 },
  { q: "Which of the following measures humidity?", options: ["Barometer", "Thermometer", "Hygrometer", "Altimeter"], answer: 2 },
  { q: "Speed is calculated by:", options: ["Distance × Time", "Distance / Time", "Time / Distance", "Force / Mass"], answer: 1 },
  { q: "Which unit is used to measure density?", options: ["kg/m²", "kg/m³", "kg", "m³"], answer: 1 },
  { q: "Which of the following measures light intensity?", options: ["Luxmeter", "Thermometer", "Hygrometer", "Barometer"], answer: 0 },
  { q: "Which instrument is used to measure altitude?", options: ["Barometer", "Altimeter", "Thermometer", "Speedometer"], answer: 1 },
];

const form = document.getElementById("quizForm");
const resultDiv = document.getElementById("result");

questions.forEach((q, i) => {
  const div = document.createElement("div");
  div.className = "question";
  div.innerHTML = `<p><strong>Q${i + 1}.</strong> ${q.q}</p>` +
    q.options.map((opt, j) => `
      <label><input type="radio" name="q${i}" value="${j}"> ${opt}</label><br>`
    ).join("");
  form.insertBefore(div, form.lastElementChild);
});

form.addEventListener("submit", function(e) {
  e.preventDefault();
  let score = 0;
  questions.forEach((q, i) => {
    const userAnswer = form[`q${i}`].value;
    if (parseInt(userAnswer) === q.answer) score++;
  });
  resultDiv.textContent = `You scored ${score} out of ${questions.length}`;
});

let timeLeft = 30 * 60;
const timerDisplay = document.getElementById("timer");
const countdown = setInterval(() => {
  let minutes = Math.floor(timeLeft / 60);
  let seconds = timeLeft % 60;
  timerDisplay.textContent = `Time Left: ${minutes}:${seconds.toString().padStart(2, '0')}`;
  timeLeft--;
  if (timeLeft < 0) {
    clearInterval(countdown);
    form.dispatchEvent(new Event('submit'));
    form.querySelector(".submit-btn").disabled = true;
    timerDisplay.textContent = "Time is up!";
  }
}, 1000);
</script></body>
</html>
