# robsongabriel_<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Checklist Semanal</title>
  <link rel="manifest" href="manifest.json">
  <link rel="apple-touch-icon" href="icon-192.png">
  <meta name="theme-color" content="#4CAF50">
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
      max-width: 900px;
      margin: auto;
    }
    h1, h2 {
      text-align: center;
    }
    .section {
      background: white;
      border-radius: 12px;
      padding: 20px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      margin-bottom: 20px;
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
      background: #fff;
      padding: 8px;
      border-radius: 6px;
      cursor: grab;
    }
    li.dragging {
      opacity: 0.5;
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
    .add-btn {
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
      color: white;
      border: none;
      border-radius: 4px;
      margin-left: auto;
      padding: 2px 8px;
      cursor: pointer;
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

  <script src="script.js"></script>
  <script>
    if ('serviceWorker' in navigator) {
      navigator.serviceWorker.register('service-worker.js').then(function(registration) {
        console.log('Service Worker registrado com sucesso:', registration);
      }).catch(function(error) {
        console.log('Falha ao registrar o Service Worker:', error);
      });
    }
  </script>
</body>
</html>
