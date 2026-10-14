<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Capital Letters Exercise</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0f8ff;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        h1, h2 {
            color: #008080;
        }
        .nav-buttons {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        button {
            background: linear-gradient(135deg, #4CAF90, #008080);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        .score {
            font-size: 18px;
            font-weight: bold;
            color: #008080;
            margin-left: auto;
        }
        .section {
            display: none;
        }
        .section.active {
            display: block;
        }
        .instructions {
            background: linear-gradient(135deg, #e6f7ff, #b3f0ff);
            border-left: 5px solid #008080;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 8px;
            font-size: 16px;
        }
        .sentence {
            background: #f9f9f9;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            border-left: 4px solid #4CAF90;
        }
        .sentence p {
            margin: 0 0 10px 0;
            font-size: 16px;
        }
        input[type="text"] {
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            width: 100%;
            box-sizing: border-box;
            font-size: 15px;
        }
        .feedback {
            margin-top: 5px;
            font-size: 14px;
            font-style: italic;
        }
        .correct {
            background-color: #d4edda !important;
            border-color: #155724 !important;
        }
        .incorrect {
            background-color: #f8d7da !important;
            border-color: #721c24 !important;
        }
        /* Exercise 2 styles */
        .correct-text {
            background: #f9f9f9;
            padding: 20px;
            border-radius: 8px;
            border-left: 4px solid #4CAF90;
            font-size: 17px;
            line-height: 2.2;
            margin-bottom: 15px;
        }
        .word {
            padding: 3px 6px;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.2s;
            display: inline-block;
        }
        .word:hover {
            background: #d1ecf1;
        }
        .word.marked {
            background: #d4edda;
            color: #155724;
            font-weight: bold;
        }
        .word.wrong-mark {
            background: #f8d7da;
            color: #721c24;
        }
        .hint {
            font-size: 14px;
            color: #666;
            font-style: italic;
        }
        .result-message {
            font-size: 18px;
            font-weight: bold;
            margin-top: 15px;
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Capital Letters ✏️</h1>
        <div class="score">Score: 0 / 32</div>
        <div class="nav-buttons">
            <button onclick="showSection('exercise1')">Exercise 1: Rewrite</button>
            <button onclick="showSection('exercise2')">Exercise 2: Correct the Text</button>
        </div>

        <!-- Exercise 1 Section -->
        <div id="exercise1" class="section active">
            <h2>Exercise 1</h2>
            <div class="instructions">
                <strong>Instructions:</strong> Rewrite the following sentences and use a capital letter for each proper noun. Type your answer in the box.
            </div>
            <div class="sentence">
                <p>1) lea pets her cat max.</p>
                <input type="text" id="ex1q1" placeholder="Write your answer here...">
                <div class="feedback" id="feedbackEx1q1"></div>
            </div>
            <div class="sentence">
                <p>2) mr. leonard visits the museum in ottawa.</p>
                <input type="text" id="ex1q2" placeholder="Write your answer here...">
                <div class="feedback" id="feedbackEx1q2"></div>
            </div>
            <div class="sentence">
                <p>3) tommy eats a cortland apple. 🍎</p>
                <input type="text" id="ex1q3" placeholder="Write your answer here...">
                <div class="feedback" id="feedbackEx1q3"></div>
            </div>
            <div class="sentence">
                <p>4) mel looks at the statue of liberty.</p>
                <input type="text" id="ex1q4" placeholder="Write your answer here...">
                <div class="feedback" id="feedbackEx1q4"></div>
            </div>
            <div class="sentence">
                <p>5) john goes to madison public school.</p>
                <input type="text" id="ex1q5" placeholder="Write your answer here...">
                <div class="feedback" id="feedbackEx1q5"></div>
            </div>
            <button onclick="checkExercise1()">Check Answers</button>
            <button onclick="resetExercise1()">Reset</button>
        </div>

        <!-- Exercise 2 Section -->
        <div id="exercise2" class="section">
            <h2>Exercise 2</h2>
            <div class="instructions">
                <strong>Instructions:</strong> Correct the text below and mark every letter which has to be a capital letter. <span class="hint">Click on a word to mark it — click again to unmark it.</span>
            </div>
            <div class="correct-text" id="correctText"></div>
            <button onclick="checkExercise2()">Check Answers</button>
            <button onclick="resetExercise2()">Reset</button>
            <div class="result-message" id="ex2Result"></div>
        </div>
    </div>

    <script>
        let score = 0;
        const totalScore = 32;

        // Exercise 1 answers
        const ex1Answers = [
            "Lea pets her cat Max.",
            "Mr. Leonard visits the museum in Ottawa.",
            "Tommy eats a Cortland apple.",
            "Mel looks at the Statue of Liberty.",
            "John goes to Madison Public School."
        ];

        // Exercise 2 text
        const ex2Text = "hello, my name is carl. i live in the united states. i enjoy chatting with people from all over the world. today, i talked to john from canada and maria from brazil. they were both very nice. i told them about myself and asked them about their lives. john likes to hike in the mountains, while maria loves to dance samba and her favourite restaurant is called stars. i think it's fascinating how different people can be and i hope to talk to more interesting folks soon.";

        // Words that need a capital letter in Exercise 2
        const needsCapital = [
            "hello,", "carl.", "i", "united", "states.", "today,", "john", "canada",
            "maria", "brazil.", "i", "told", "john", "maria", "stars.", "i", "think", "i", "hope"
        ];

        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active');
            });
            document.getElementById(sectionId).classList.add('active');
        }

        function updateScore() {
            document.querySelector('.score').textContent = `Score: ${score} / ${totalScore}`;
        }

        // ===== EXERCISE 1 =====
        function checkExercise1() {
            for (let i = 0; i < ex1Answers.length; i++) {
                const input = document.getElementById('ex1q' + (i + 1));
                const feedback = document.getElementById('feedbackEx1q' + (i + 1));
                const userAnswer = input.value.trim().replace(/\s+/g, ' ');

                if (userAnswer.toLowerCase() === ex1Answers[i].toLowerCase()) {
                    input.className = 'correct';
                    feedback.textContent = 'Correct!';
                    feedback.style.color = 'green';
                    if (input.dataset.scored !== 'true') {
                        score++;
                        input.dataset.scored = 'true';
                    }
                } else {
                    input.className = 'incorrect';
                    feedback.textContent = 'Incorrect. Check your capital letters and try again!';
                    feedback.style.color = 'red';
                    if (input.dataset.scored === 'true') {
                        score--;
                        input.dataset.scored = 'false';
                    }
                }
            }
            updateScore();
        }

        function resetExercise1() {
            for (let i = 1; i <= 5; i++) {
                const input = document.getElementById('ex1q' + i);
                input.value = '';
                input.className = '';
                input.dataset.scored = '';
                document.getElementById('feedbackEx1q' + i).textContent = '';
            }
            score = 0;
            updateScore();
        }

        // ===== EXERCISE 2 =====
        function buildExercise2() {
            const container = document.getElementById('correctText');
            container.innerHTML = '';
            const words = ex2Text.split(' ');
            words.forEach((word, index) => {
                const span = document.createElement('span');
                span.className = 'word';
                span.textContent = word;
                span.onclick = function() {
                    span.classList.toggle('marked');
                };
                container.appendChild(span);
                container.appendChild(document.createTextNode(' '));
            });
        }

        function checkExercise2() {
            const words = document.querySelectorAll('#correctText .word');
            let correctCount = 0;
            let wrongCount = 0;

            words.forEach(span => {
                const cleanWord = span.textContent.replace(/[^a-z']/gi, '').toLowerCase();
                const isCapitalWord = needsCapital.includes(cleanWord) && span.textContent === span.textContent.toLowerCase();
                const isMarked = span.classList.contains('marked');

                span.classList.remove('wrong-mark');

                if (isMarked && isCapitalWord) {
                    correctCount++;
                } else if (isMarked && !isCapitalWord) {
                    wrongCount++;
                    span.classList.add('wrong-mark');
                }
            });

            const totalNeeded = document.querySelectorAll('#correctText .word').length ?
                [...document.querySelectorAll('#correctText .word')].filter(s => {
                    const cw = s.textContent.replace(/[^a-z']/gi, '').toLowerCase();
                    return needsCapital.includes(cw) && s.textContent === s.textContent.toLowerCase();
                }).length : 0;

            const ex2Score = correctCount;
            const resultDiv = document.getElementById('ex2Result');
            resultDiv.style.display = 'block';

            if (correctCount === totalNeeded && wrongCount === 0) {
                resultDiv.textContent = `🎉 Perfect! You found all ${totalNeeded} words that need a capital letter!`;
                resultDiv.style.color = 'green';
            } else {
                resultDiv.textContent = `You found ${correctCount} of ${totalNeeded} words that need a capital letter.` +
                    (wrongCount > 0 ? ` You also marked ${wrongCount} word(s) that don't need a capital (shown in red).` : '') +
                    ` Keep trying!`;
                resultDiv.style.color = '#e67e22';
            }

            updateExercise2Score(correctCount);
        }

        let ex2PreviousScore = 0;
        function updateExercise2Score(correctCount) {
            score = score - ex2PreviousScore + correctCount;
            ex2PreviousScore = correctCount;
            updateScore();
        }

        function resetExercise2() {
            document.querySelectorAll('#correctText .word').forEach(span => {
                span.classList.remove('marked', 'wrong-mark');
            });
            score = score - ex2PreviousScore;
            ex2PreviousScore = 0;
            document.getElementById('ex2Result').style.display = 'none';
            updateScore();
        }

        // Initialize
        buildExercise2();
        updateScore();
    </script>
</body>
</html>
