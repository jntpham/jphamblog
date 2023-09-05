---
toc: true
comments: false
layout: post
title: HTML Python Quiz
description: Test your knowledge on stuff
type: tangibles
courses: {csp: {week: 2, categories: [5.A]}}


---
<!DOCTYPE html>
<html>
<head>
    <title>Simple Quiz</title>
</head>
<body>
    <h1>Simple Quiz</h1>
    <form id="quiz-form">
        <fieldset>
            <legend>What command is used to include other functions that were previously developed?</legend>
            <label><input type="radio" name="q1" value="a">Import</label><br>
            <label><input type="radio" name="q1" value="b">Deliver</label><br>
            <label><input type="radio" name="q1" value="c">Return</label><br>
        </fieldset>
        <fieldset>
            <legend>What does the string, “question_with_response” do in this program?</legend>
            <label><input type="radio" name="q2" value="a">Reboots the quiz</label><br>
            <label><input type="radio" name="q2" value="b">Returns a value inputted by the user</label><br>
            <label><input type="radio" name="q2" value="c">Activates the if command</label><br>
        </fieldset>
        <fieldset>
            <legend>Question 3: What is a string concatenation?</legend>
            <label><input type="radio" name="q3" value="a">A string</label><br>
            <label><input type="radio" name="q3" value="b">Prefixes the prompt with the literal message “Question: “</label><br>
            <label><input type="radio" name="q3" value="c">A group of strings laced together</label><br>
        </fieldset>
        <fieldset>
            <legend>Question 4: What does HTML stand for?</legend>
            <label><input type="radio" name="q4" value="a">Hyper Text Markup Language</label><br>
            <label><input type="radio" name="q4" value="b">High Tech Modern Language</label><br>
            <label><input type="radio" name="q4" value="c">Hot Tamale Microwave Lingo</label><br>
        </fieldset>
        <fieldset>
            <legend>Question 5: How confident is your knowledge after this quiz?</legend>
            <label><input type="radio" name="q5" value="a">Great</label><br>
            <label><input type="radio" name="q5" value="b">Good</label><br>
            <label><input type="radio" name="q5" value="c">Horrible</label><br>
        </fieldset>
        <button type="button" id="submit-button">Submit Answers</button>
    </form>
    <div id="result"></div>
    <script>
        document.getElementById("submit-button").addEventListener("click", function() {
            const answers = {
                q1: document.querySelector('input[name="q1"]:checked'),
                q2: document.querySelector('input[name="q2"]:checked'),
                q3: document.querySelector('input[name="q3"]:checked'),
                q4: document.querySelector('input[name="q4"]:checked'),
                q5: document.querySelector('input[name="q5"]:checked')
            };
            let correctCount = 0;
            for (const question in answers) {
                if (answers[question] && answers[question].value === "a") {
                    correctCount++;
                }
            }
            const resultDiv = document.getElementById("result");
            resultDiv.innerHTML = `You got ${correctCount} out of 5 questions correct.`;
        });
    </script>
</body>
</html>






