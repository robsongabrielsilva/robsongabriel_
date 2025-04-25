
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Checklist Semanal</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
      max-width: 900px;
      margin: auto;
      color: #000;
    }
    h1, h2 {
      text-align: center;
      color: #000;
    }
    .section {
      border-radius: 12px;
      padding: 20px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      margin-bottom: 20px;
      background-color: #fff;
    }
    ul {
      list-style: none;
      padding-left: 0;
      min-height: 50px;
    }
    li {
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      background: rgba(255,255,255,0.9);
      padding: 8px;
      border-radius: 6px;
      cursor: grab;
      color: #000;
    }
    input[type="checkbox"] {
      margin-right: 10px;
      width: 20px;
      height: 20px;
      appearance: none;
      border: 2px solid #888;
      border-radius: 4px;
      outline: none;
      cursor: pointer;
      position: relative;
    }
    input[type="checkbox"]:checked {
      background-color: #4CAF50;
      border-color: #4CAF50;
    }
    input[type="checkbox"]:checked::after {
      content: "\2713";
      color: white;
      font-size: 16px;
      position: absolute;
      top: 0;
      left: 4px;
    }
    .add-btn, .delete-btn {
      margin-top: 10px;
      padding: 6px 12px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    .add-btn:hover {
      background-color: #45a049;
    }
    .delete-btn {
      background-color: #e74c3c;
      margin-left: auto;
    }
    .delete-btn:hover {
      background-color: #c0392b;
    }
    .footer {
      text-align: center;
      margin-top: 30px;
      font-size: 0.9em;
      color: #777;
    }
    .weekdays {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      margin: 20px 0;
    }
    .weekday {
      background: #eee;
      border: 1px solid #ccc;
      padding: 8px 12px;
      margin: 4px;
      border-radius: 8px;
      cursor: pointer;
      color: #000;
    }
    .weekday.active {
      background: #4CAF50;
      color: white;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>✅ Checklist Semanal</h1>

  <div class="weekdays">
    <div class="weekday" onclick="changeDay('domingo')">Dom</div>
    <div class="weekday" onclick="changeDay('segunda')">Seg</div>
    <div class="weekday" onclick="changeDay('terca')">Ter</div>
    <div class="weekday" onclick="changeDay('quarta')">Qua</div>
    <div class="weekday" onclick="changeDay('quinta')">Qui</div>
    <div class="weekday" onclick="changeDay('sexta')">Sex</div>
    <div class="weekday" onclick="changeDay('sabado')">Sáb</div>
  </div>

  <div class="section">
    <h2>☀️ Manhã</h2>
    <ul id="manha"></ul>
    <button class="add-btn" onclick="addTask('manha')">+ Adicionar tarefa</button>
  </div>

  <div class="section">
    <h2>🌤 Tarde</h2>
    <ul id="tarde"></ul>
    <button class="add-btn" onclick="addTask('tarde')">+ Adicionar tarefa</button>
  </div>

  <div class="section">
    <h2>🌙 Noite</h2>
    <ul id="noite"></ul>
    <button class="add-btn" onclick="addTask('noite')">+ Adicionar tarefa</button>
  </div>

  <div class="footer">
    Organize sua semana com autonomia e flexibilidade.
  </div>

  <script>
    let currentDay = 'segunda';
    const weekData = JSON.parse(localStorage.getItem('weekData')) || {};

    function saveData() {
      localStorage.setItem('weekData', JSON.stringify(weekData));
    }

    function changeDay(day) {
      currentDay = day;
      document.querySelectorAll('.weekday').forEach(el => el.classList.remove('active'));
      document.querySelector(`.weekday[onclick*="${day}"]`).classList.add('active');
      renderTasks();
    }

    function renderTasks() {
      ['manha', 'tarde', 'noite'].forEach(period => {
        const ul = document.getElementById(period);
        ul.innerHTML = '';
        const tasks = weekData[currentDay]?.[period] || [];
        tasks.forEach((task, index) => {
          const li = document.createElement('li');
          const checkbox = document.createElement('input');
          checkbox.type = 'checkbox';
          checkbox.checked = task.done;
          checkbox.onchange = () => {
            weekData[currentDay][period][index].done = checkbox.checked;
            saveData();
          };

          const span = document.createElement('span');
          span.textContent = task.text;

          const deleteBtn = document.createElement('button');
          deleteBtn.className = 'delete-btn';
          deleteBtn.textContent = '✖';
          deleteBtn.onclick = () => {
            weekData[currentDay][period].splice(index, 1);
            saveData();
            renderTasks();
          };

          li.appendChild(checkbox);
          li.appendChild(span);
          li.appendChild(deleteBtn);
          ul.appendChild(li);
        });
      });
    }

    function addTask(period) {
      const taskText = prompt('Digite a tarefa:');
      if (!taskText) return;
      if (!weekData[currentDay]) weekData[currentDay] = { manha: [], tarde: [], noite: [] };
      weekData[currentDay][period].push({ text: taskText, done: false });
      saveData();
      renderTasks();
    }

    changeDay('segunda');
  </script>
</body>
</html>
