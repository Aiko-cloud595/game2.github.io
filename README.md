<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Терминал Архива</title>
  <style>
    body {
      background: black;
      color: #33ff33;
      font-family: 'Courier New', monospace;
      padding: 20px;
      overflow-x: hidden;
      overflow-y: auto;
      position: relative;
    }

    .scanlines {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-image: repeating-linear-gradient(to bottom, rgba(0,0,0,0.1), rgba(0,0,0,0.1) 1px, transparent 1px, transparent 3px);
      pointer-events: none;
      z-index: 100;
      animation: flicker 0.15s infinite;
    }

    @keyframes flicker {
      0%   { opacity: 0.95; }
      50%  { opacity: 0.85; }
      100% { opacity: 0.95; }
    }

    .section {
      margin-bottom: 40px;
    }

    .hidden {
      display: none;
    }

    input[type="text"] {
      background-color: black;
      border: 1px solid #33ff33;
      color: #33ff33;
      font-family: 'Courier New', monospace;
      padding: 4px;
    }

    button {
      background-color: #000;
      color: #33ff33;
      border: 1px solid #33ff33;
      padding: 4px 8px;
      cursor: pointer;
    }

    button:hover {
      background-color: #111;
    }
  </style>
</head>
<body>
  <div class="scanlines"></div>

  <audio id="bgm" loop>
    <source src="eyes-of-fear-1.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>
  <button onclick="playBgm()">▶ Включить атмосферу</button>

  <h1>Добро пожаловать в Терминал Архива</h1>

  <!-- Вступление -->
  <div class="section">
    <p>Вы активируете старый терминал в центре заброшенного комплекса. Экран мерцает, воздух наполнен запахом пыли и озона. Что вы хотите осмотреть?</p>
    <ul>
      <li><button onclick="document.getElementById('locker').classList.remove('hidden')">📁 Шкафчик у стены</button></li>
      <li><button onclick="document.getElementById('desk').classList.remove('hidden')">🗂 Письменный стол</button></li>
      <li><button onclick="document.getElementById('monitor').classList.remove('hidden')">🖥 Монитор с зелёным свечением</button></li>
    </ul>
  </div>

  <!-- Подсказки по локациям -->
  <div class="section hidden" id="locker">
    <h3>Шкафчик</h3>
    <p>Внутри шкафчика находится пожелтевшая записка с надписью:</p>
    <p><i>MRZRG YVH GSV MLG</i></p>
    <p>Рядом, почерневшим от времени, рукой написано одно слово — «Атбаш». Похоже, это шифр. Ты чувствуешь, как холодная тень охватывает твоё тело, будто бы нечто следит за каждым твоим шагом...</p>
    <button onclick="document.getElementById('riddle1').classList.remove('hidden')">Рассшифровать</button>
  </div>

  <div class="section hidden" id="desk">
    <h3>Письменный стол</h3>
    <p>Журнал, выцветший и покрытый пылью, лежит на столе. На одной из страниц, через десятки лет, остаются ярко выделенные заглавные буквы:</p>
    <p><i><b>S</b>hifted <b>P</b>aths <b>E</b>merge <b>C</b>louded <b>T</b>rails <b>R</b>evealed <b>A</b>new</i></p>
    <p>Ты медленно выводишь эти буквы. Вдруг ощущение, что кто-то смотрит тебе в спину, становится невыносимым. Зловещий взгляд невидимой силы ощущается в воздухе.</p>
  </div>

  <div class="section hidden" id="monitor">
    <h3>Монитор</h3>
    <p>На экране мигает и трещит код в азбуке Морзе:</p>
    <code>..-. .. -. .- .-..</code>
    <p>Звуки, исходящие от устройства, кажутся странно громкими в этой тишине. Ты прислушиваешься и ощущаешь, как напряжение растёт. Этот код — не просто набор символов. Он может быть ключом. Ты не можешь отделаться от ощущения, что здесь давно никто не был...</p>
  </div>

  <!-- Первая загадка -->
  <div class="section hidden" id="riddle1">
    <p>Введите расшифровку записки из шкафчика:</p>
    <input type="text" id="input1" placeholder="Введите ответ">
    <button onclick="checkAnswer('input1', 'riddle2', 'THESE YOU THE NOT')">Проверить</button>
  </div>

  <!-- Вторая загадка -->
  <div class="section hidden" id="riddle2">
    <p>Введите перевод морзянки с монитора:</p>
    <input type="text" id="input2" placeholder="Введите ответ">
    <button onclick="checkAnswer('input2', 'riddle3', 'FINAL')">Проверить</button>
  </div>

  <!-- Третья загадка -->
  <div class="section hidden" id="riddle3">
    <p>Какое слово складывается из выделенных букв в журнале?</p>
    <input type="text" id="input3" placeholder="Введите ответ">
    <button onclick="checkAnswer('input3', 'riddle4', 'SPECTRA')">Проверить</button>
  </div>

  <!-- Четвёртая загадка -->
  <div class="section hidden" id="riddle4">
    <p>На экране терминала появляются странные символы:</p>
    <i>♓︎♋︎♐︎♓︎♐︎♌︎</i><br>
    <p>Подсказка: шрифт Winding. Ты понимаешь, что это не обычный шифр. Символы напоминают нечто из древних знаний, затмённого временем. В воздухе снова возникает зловещее чувство...</p>
    <input type="text" id="input4" placeholder="Введите ответ">
    <button onclick="checkAnswer('input4', 'riddle5', 'ВРЕМЕННАЯ ПЕТЛЯ')">Проверить</button>
  </div>

  <!-- Пятая загадка -->
  <div class="section hidden" id="riddle5">
    <p>Экран снова мигает, и ты видишь простую строку:</p>
    <p>Введите время...</p>
    <input type="text" id="input5" placeholder="Введите ответ">
    <button onclick="checkAnswer('input5', 'finalLog', '03:12')">Проверить</button>
  </div>

  <!-- Финальный лог -->
  <div class="section hidden" id="finalLog">
    <h2>ФИНАЛЬНЫЙ ЛОГ</h2>
    <p>
      Ты слышишь треск, и экран наполняется странным светом. Лог-файл появляется, отображая данные. Ты видишь сообщение, которое буквально парализует твоё сознание.<br>
      <i>"Ты приходил сюда десять раз. Ты умирал десять раз. Ты выбирал один и тот же путь. Единственной переменной... было твоё сознание. И теперь ты очнулся. Цикл заканчивается, когда сознание = 1".</i><br>
      В комнате нарастают странные вибрации, и время, кажется, замедляется...
    </p>
    <p>Вы хотите прервать цикл? Или попробовать ещё раз?</p>
    <button onclick="restartGame()">Попробовать ещё раз</button>
    <button onclick="endGame()">Прервать цикл</button>
  </div>

  <script>
    function playBgm() {
      const audioElement = document.getElementById('bgm');
      if (audioElement) {
        audioElement.play();
        this.style.display = 'none';
      } else {
        alert("Не удалось найти файл музыки.");
      }
    }

    function checkAnswer(inputId, nextId, correctAnswer) {
      const val = document.getElementById(inputId).value.trim().toUpperCase();
      if (val === correctAnswer.toUpperCase()) {
        document.getElementById(nextId).classList.remove("hidden");
      } else {
        alert("Неверно. Попробуйте снова.");
      }
    }

    function restartGame() {
      location.reload();
    }

    function endGame() {
      document.body.innerHTML = "<h1>До встречи в следующем измерении...</h1>";
    }
  </script>
</body>
</html>
