// Updated JAMB Measurement Quiz App - By Adara Foundation

import React, { useState } from 'react'; import { Button } from "@/components/ui/button";

const questions = [ { q: "The internationally accepted system of units (SI) for physical measurement are", options: [ "ft, lbf, sec, °F, gallon", "kg, sec, °C, cm, kgm/sec", "m, kg, sec K, A, mole, candela", "dm, gm, sec", "K, kg, m, sec" ], answer: 2 }, { q: "To determine the weight of an object placed on a field A, use a spring balance but to calculate the body mass, use the mass of the body to attain a given acceleration. In one word, we use the concept of:", options: ["force", "weight", "mass", "reaction", "kilogram"], answer: 0 }, { q: "Why is the use of a galvanometer not ideal for electricity measurements?", options: ["It lacks sensitivity.", "Electric field intensity cannot be measured.", "A galvanometer does not obey voltmeter law.", "Galvanometer readings are wrong.", "Galvanometer readings are in degrees."], answer: 0 }, { q: "The SI unit of power is", options: ["Joule", "Ampere", "Ohm", "Volt", "Watt"], answer: 4 }, { q: "Which of the following is NOT a vector quantity?", options: ["Force", "Acceleration", "Tension", "Weight", "Distance"], answer: 4 }, { q: "The length of a wooden block is measured to be 16.50cm using a metre rule. What is the percentage error in the measurement if the end of the ruler is damaged?", options: ["0.06%", "0.15%", "0.30%", "0.60%", "0.90%"], answer: 3 }, { q: "The pair of physical quantities which are scalar is", options: ["Volume and mass", "Force and power", "Force and mass", "Force and acceleration", "Volume and velocity"], answer: 0 }, { q: "Which of the following is the unit of weight?", options: ["Kgms⁻¹", "Kgm", "Nm⁻¹", "N", "Ns⁻¹"], answer: 3 }, { q: "Which of the following physical quantities is not correctly matched with its unit?", options: ["Pressure/Nm²", "Electric field intensity/Nm⁻¹", "Capacitance/Asv⁻¹", "Potential difference/JC⁻¹", "Power/Js⁻¹"], answer: 2 }, { q: "Which of the following statements are true about the spring balance and the chemical balance?", options: [ "I and II only", "I, II and III only", "I, II, III and IV only", "I, II, III and V only", "I, II, III, IV and V" ], answer: 3 }, // Add more converted questions as needed up to 33 so far... ];

export default function QuizApp() { const [started, setStarted] = useState(false); const [submitted, setSubmitted] = useState(false); const [currentAnswers, setCurrentAnswers] = useState(Array(questions.length).fill(null)); const [score, setScore] = useState(null);

const startQuiz = () => { setStarted(true); setSubmitted(false); setCurrentAnswers(Array(questions.length).fill(null)); setScore(null); };

const submitQuiz = () => { let s = 0; currentAnswers.forEach((ans, i) => { if (ans === questions[i].answer) s++; }); setScore(s); setSubmitted(true); };

return ( <div className="p-4 max-w-3xl mx-auto"> <h1 className="text-2xl font-bold text-center mb-4"> JAMB Past Questions on Measurement – Question Bank (500 Questions)<br /> <span className="text-lg">by Adara Foundation</span> </h1>

{!started && (
    <Button onClick={startQuiz}>Start Quiz</Button>
  )}

  {started && (
    <>
      {questions.map((q, index) => (
        <div key={index} className="mb-4">
          <p className="font-medium">{index + 1}. {q.q}</p>
          {q.options.map((opt, i) => (
            <div key={i}>
              <label>
                <input
                  type="radio"
                  name={`q${index}`}
                  disabled={submitted}
                  checked={currentAnswers[index] === i}
                  onChange={() => {
                    const newAnswers = [...currentAnswers];
                    newAnswers[index] = i;
                    setCurrentAnswers(newAnswers);
                  }}
                />{' '}{opt}
                {submitted && i === q.answer && (
                  <span className="text-green-600 font-semibold ml-2">✔</span>
                )}
                {submitted && currentAnswers[index] === i && i !== q.answer && (
                  <span className="text-red-500 ml-2">✘</span>
                )}
              </label>
            </div>
          ))}
        </div>
      ))}
      {!submitted && <Button onClick={submitQuiz}>Submit</Button>}
      {submitted && <p className="mt-4 font-semibold">You scored {score} out of {questions.length}</p>}
    </>
  )}
</div>

); }

