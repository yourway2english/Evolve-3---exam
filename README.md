<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Evolve 3 Interactive Exam Bank</title>
    <style>
        :root {
            --primary-color: #1e293b;
            --accent-color: #ffd700;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #0f172a;
            --correct-color: #22c55e;
            --wrong-color: #ef4444;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

        header {
            background-color: var(--primary-color);
            color: white;
            text-align: center;
            padding: 2rem 1rem;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
        }

        .highlight-badge {
            background-color: var(--accent-color);
            color: var(--primary-color);
            display: inline-block;
            padding: 0.75rem 2.5rem;
            border-radius: 8px;
            font-weight: bold;
            box-shadow: 0 4px 6px rgba(0,0,0,0.15);
        }

        header h1 {
            margin: 0 0 0.1rem 0;
            font-size: 2.4rem;
            letter-spacing: 1.5px;
        }

        header h2 {
            margin: 0;
            font-size: 1.4rem;
            text-transform: lowercase;
            letter-spacing: 0.5px;
        }

        .dashboard {
            background: #e2e8f0;
            max-width: 850px;
            margin: 1.5rem auto;
            padding: 1rem;
            border-radius: 8px;
            display: flex;
            justify-content: space-around;
            font-weight: 600;
            font-size: 1.1rem;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
            position: sticky;
            top: 135px;
            z-index: 99;
        }

        .main-container {
            max-width: 850px;
            margin: 0 auto;
            padding: 0 1.5rem 4rem 1.5rem;
        }

        .section-title {
            background: #334155;
            color: white;
            padding: 0.75rem 1rem;
            border-radius: 6px;
            margin-top: 2.5rem;
            font-size: 1.4rem;
        }

        .quiz-card {
            background: var(--card-bg);
            border-radius: 8px;
            padding: 1.5rem;
            margin: 1.5rem 0;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05);
            border-left: 5px solid #64748b;
        }

        .question-text {
            font-size: 12pt;
            font-weight: bold;
            color: #000000;
            margin-bottom: 1rem;
        }

        .options-container {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .option-label {
            display: flex;
            align-items: center;
            padding: 0.75rem 1rem;
            border: 2px solid #e2e8f0;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12pt;
            transition: all 0.2s ease;
            position: relative;
        }

        .option-label input {
            margin-right: 1rem;
            accent-color: var(--correct-color);
        }

        .option-label.selected {
            background-color: rgba(34, 197, 94, 0.15) !important;
            border-color: var(--correct-color) !important;
        }

        .text-input-style {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid #e2e8f0;
            border-radius: 6px;
            font-size: 12pt;
            margin-top: 0.5rem;
            box-sizing: border-box;
        }

        .text-input-container.selected .text-input-style {
            background-color: rgba(34, 197, 94, 0.08);
            border-color: var(--correct-color);
        }

        .graded-correct {
            border-color: var(--correct-color) !important;
            background-color: rgba(34, 197, 94, 0.1) !important;
        }

        .graded-wrong {
            border-color: var(--wrong-color) !important;
            background-color: rgba(239, 68, 68, 0.1) !important;
        }

        .feedback-icon {
            margin-left: auto;
            font-weight: bold;
            font-size: 1.3rem;
        }

        .feedback-icon.correct {
            color: var(--correct-color);
        }

        .feedback-icon.wrong {
            color: var(--wrong-color);
        }

        .correction-note {
            margin-top: 0.8rem;
            font-size: 11pt;
            color: #1e293b;
            background: #f1f5f9;
            padding: 0.6rem 1rem;
            border-radius: 4px;
            border-left: 4px solid var(--wrong-color);
        }

        .submit-panel {
            text-align: center;
            margin: 3rem 0;
        }

        .btn-action {
            background-color: #2563eb;
            color: white;
            border: none;
            padding: 1rem 3.5rem;
            font-size: 1.3rem;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(37,99,235,0.3);
            transition: all 0.2s;
        }

        .btn-action:hover {
            background-color: #1d4ed8;
            transform: translateY(-2px);
        }

        #results-card {
            background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
            color: white;
            border-radius: 12px;
            padding: 2.5rem;
            text-align: center;
            margin-top: 2rem;
            display: none;
            box-shadow: 0 10px 25px -5px rgba(0,0,0,0.3);
        }

        #results-card h3 {
            font-size: 2.2rem;
            margin: 0 0 1rem 0;
            color: var(--accent-color);
        }

        .score-display {
            font-size: 4rem;
            font-weight: 800;
            margin: 1rem 0;
            color: #ffffff;
        }
    </style>
</head>
<body>

<header>
    <div class="highlight-badge">
        <h1>EVOLVE 3</h1>
        <h2>yourway2english</h2>
    </div>
</header>

<div class="dashboard">
    <div>Total Exam Items: <span id="total-count">200</span></div>
    <div>Not Answered: <span id="unanswered-count">200</span></div>
</div>

<div class="main-container">
    <form id="quiz-form">
        <div id="quiz-questions-target"></div>

        <div class="submit-panel">
            <button type="button" id="submit-btn" class="btn-action" onclick="gradeQuiz()">Submit Exam</button>
        </div>
    </form>

    <div id="results-card">
        <h3>Examination Results</h3>
        <div class="score-display" id="final-score">0 / 200</div>
        <p id="final-percentage" style="font-size: 1.3rem; opacity: 0.95;"></p>
        <button type="button" class="btn-action" style="background:#475569; margin-top:1.5rem; padding:0.6rem 2rem; font-size:1.1rem;" onclick="window.scrollTo({top:0, behavior:'smooth'});">Review Graded Sheet</button>
    </div>
</div>

<!-- CONNECTING CORE EXTERNAL QUESTION STRUCT DATA -->
<script src="questions.js"></script>

<script>
function buildQuiz() {
    const container = document.getElementById("quiz-questions-target");
    let currentSection = 0;

    questionBank.forEach((item) => {
        if (item.section !== currentSection) {
            currentSection = item.section;
            const heading = document.createElement("h2");
            heading.className = "section-title";
            heading.innerText = currentSection === 1 ? "SECTION 1: VOCABULARY & MATCHING BLOCKS" : "SECTION 2: GRAMMAR & SYNTAX STRUCTURES";
            container.appendChild(heading);
        }

        const card = document.createElement("div");
        card.className = "quiz-card";
        card.id = `card-q-${item.id}`;

        const qText = document.createElement("div");
        qText.className = "question-text";
        qText.innerText = item.q;
        card.appendChild(qText);

        if (item.type === "mcq") {
            const optionsBox = document.createElement("div");
            optionsBox.className = "options-container";

            item.options.forEach(opt => {
                const label = document.createElement("label");
                label.className = "option-label";
                label.id = `label-${item.id}-${opt.replace(/[^a-zA-Z0-9]/g, "")}`;

                const radio = document.createElement("input");
                radio.type = "radio";
                radio.name = `question-${item.id}`;
                radio.value = opt;
                radio.onclick = function() { selectOption(item.id, this); };

                label.appendChild(radio);
                label.appendChild(document.createTextNode(opt));
                optionsBox.appendChild(label);
            });
            card.appendChild(optionsBox);
        } else {
            const inputContainer = document.createElement("div");
            inputContainer.className = "text-input-container";
            inputContainer.id = `input-container-${item.id}`;

            const inputField = document.createElement("input");
            inputField.type = "text";
            inputField.className = "text-input-style";
            inputField.placeholder = "Type your assessment answer here...";
            inputField.oninput = function() { textInputChanged(item.id, this); };

            inputContainer.appendChild(inputField);
            card.appendChild(inputContainer);
        }

        container.appendChild(card);
    });
    updateDashboardCounters();
}

function selectOption(qId, inputElement) {
    const siblings = document.querySelectorAll(`[id^="label-${qId}-"]`);
    siblings.forEach(el => el.classList.remove("selected"));

    if (inputElement.checked) {
        inputElement.parentElement.classList.add("selected");
    }
    updateDashboardCounters();
}

function textInputChanged(qId, inputField) {
    const parent = document.getElementById(`input-container-${qId}`);
    if (inputField.value.trim() !== "") {
        parent.classList.add("selected");
    } else {
        parent.classList.remove("selected");
    }
    updateDashboardCounters();
}

function updateDashboardCounters() {
    let unanswered = 0;
    questionBank.forEach(item => {
        if (item.type === "mcq") {
            const checked = document.querySelector(`input[name="question-${item.id}"]:checked`);
            if (!checked) unanswered++;
        } else {
            const textVal = document.querySelector(`#input-container-${item.id} input`).value.trim();
            if (textVal === "") unanswered++;
        }
    });
    document.getElementById("unanswered-count").innerText = unanswered;
}

function gradeQuiz() {
    let score = 0;

    questionBank.forEach(item => {
        const card = document.getElementById(`card-q-${item.id}`);
        
        card.querySelectorAll('.feedback-icon').forEach(el => el.remove());
        card.querySelectorAll('.correction-note').forEach(el => el.remove());

        if (item.type === "mcq") {
            const selectedRadio = document.querySelector(`input[name="question-${item.id}"]:checked`);
            const chosenValue = selectedRadio ? selectedRadio.value : null;

            item.options.forEach(opt => {
                const cleanOptId = opt.replace(/[^a-zA-Z0-9]/g, "");
                const label = document.getElementById(`label-${item.id}-${cleanOptId}`);
                label.classList.remove("graded-correct", "graded-wrong");
            });

            if (chosenValue === item.answer) {
                score++;
                const selectedLabel = document.getElementById(`label-${item.id}-${chosenValue.replace(/[^a-zA-Z0-9]/g, "")}`);
                selectedLabel.classList.add("graded-correct");
                
                const icon = document.createElement("span");
                icon.className = "feedback-icon correct";
                icon.innerHTML = "&#10004;"; 
                selectedLabel.appendChild(icon);
            } else {
                if (chosenValue) {
                    const wrongLabel = document.getElementById(`label-${item.id}-${chosenValue.replace(/[^a-zA-Z0-9]/g, "")}`);
                    wrongLabel.classList.add("graded-wrong");
                    
                    const icon = document.createElement("span");
                    icon.className = "feedback-icon wrong";
                    icon.innerHTML = "&#10008;"; 
                    wrongLabel.appendChild(icon);
                } else {
                    const inlineIcon = document.createElement("div");
                    inlineIcon.className = "correction-note";
                    inlineIcon.style.borderColor = "var(--wrong-color)";
                    inlineIcon.innerHTML = "<strong>&#10008; Skipped:</strong> Left blank.";
                    card.appendChild(inlineIcon);
                }
                
                const correctLabel = document.getElementById(`label-${item.id}-${item.answer.replace(/[^a-zA-Z0-9]/g, "")}`);
                if(correctLabel) correctLabel.classList.add("graded-correct");
            }
        } else {
            const textInput = document.querySelector(`#input-container-${item.id} input`);
            const userAns = textInput.value.trim().toLowerCase().replace(/[^a-zA-Z0-9]/g, "");
            const targetAns = item.answer.toLowerCase().replace(/[^a-zA-Z0-9]/g, "");

            textInput.classList.remove("graded-correct", "graded-wrong");

            if (userAns === targetAns) {
                score++;
                textInput.classList.add("graded-correct");
            } else {
                textInput.classList.add("graded-wrong");
                
                const note = document.createElement("div");
                note.className = "correction-note";
                note.innerHTML = `<strong>&#10008; Correct Answer:</strong> ${item.answer}`;
                card.appendChild(note);
            }
        }
    });

    const resultsCard = document.getElementById("results-card");
    resultsCard.style.display = "block";
    document.getElementById("final-score").innerText = `${score} / 200`;
    
    const percentage = Math.round((score / 200) * 100);
    document.getElementById("final-percentage").innerText = `Total Grade Score: ${percentage}%`;
    
    resultsCard.scrollIntoView({ behavior: 'smooth' });
}

window.onload = buildQuiz;
</script>

</body>
</html>
