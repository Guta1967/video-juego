<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Práctica de Matemáticas</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gradient-to-r from-purple-500 to-blue-500 text-white flex flex-col items-center justify-center min-h-screen">
    <div class="bg-white text-black rounded-xl shadow-xl p-6 text-center w-96">
        <h1 class="text-2xl font-bold">¡Practica Matemáticas!</h1>
        <p id="question" class="text-xl my-4 font-semibold"></p>
        <input type="number" id="answer" class="border rounded p-2 w-full text-center" placeholder="Tu respuesta aquí">
        <button onclick="checkAnswer()" class="bg-blue-600 text-white py-2 px-4 rounded mt-4 w-full">Verificar</button>
        <p id="feedback" class="mt-3 font-bold"></p>
        <p class="mt-2">Puntuación: <span id="score">0</span></p>
        <button onclick="restartGame()" class="bg-red-600 text-white py-2 px-4 rounded mt-4 w-full">Reiniciar</button>
    </div>
    <audio id="correctSound" src="https://www.myinstants.com/media/sounds/correct.mp3"></audio>
    <audio id="wrongSound" src="https://www.myinstants.com/media/sounds/error.mp3"></audio>

    <script>
        let score = 0;
        let currentAnswer = 0;
        function generateQuestion() {
            const num1 = Math.floor(Math.random() * 9000) + 1000;
            const num2 = Math.floor(Math.random() * 9000) + 1000;
            const operators = ['+', '-', '*', '/'];
            const operator = operators[Math.floor(Math.random() * operators.length)];
            let question;
            if (operator === '/') {
                let dividend = num1 * num2;
                question = `${dividend} ÷ ${num1}`;
                currentAnswer = num2;
            } else {
                question = `${num1} ${operator} ${num2}`;
                currentAnswer = eval(question);
            }
            document.getElementById('question').innerText = question;
        }
        function checkAnswer() {
            const userAnswer = parseFloat(document.getElementById('answer').value);
            if (userAnswer === currentAnswer) {
                document.getElementById('feedback').innerText = '¡Correcto! 🎉';
                document.getElementById('feedback').classList.add('text-green-600');
                document.getElementById('correctSound').play();
                score++;
            } else {
                document.getElementById('feedback').innerText = 'Incorrecto. ❌';
                document.getElementById('feedback').classList.add('text-red-600');
                document.getElementById('wrongSound').play();
            }
            document.getElementById('score').innerText = score;
            document.getElementById('answer').value = '';
            generateQuestion();
        }
        function restartGame() {
            score = 0;
            document.getElementById('score').innerText = score;
            document.getElementById('feedback').innerText = '';
            generateQuestion();
        }
        generateQuestion();
    </script>
</body>
</html>
