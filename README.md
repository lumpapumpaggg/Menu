# Menu
Menu for us
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Меню для двоих</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f7f7f7;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
    }
    .menu {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      max-width: 800px;
      margin: 0 auto;
    }
    .person {
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    .person h2 {
      margin-top: 0;
      text-align: center;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    input[type="checkbox"] {
      transform: scale(1.2);
    }
    .add-item {
      display: flex;
      margin-top: 15px;
      gap: 5px;
    }
    .add-item input {
      flex: 1;
      padding: 5px;
    }
    .add-item button {
      padding: 6px 10px;
      border: none;
      background: #4caf50;
      color: white;
      border-radius: 6px;
      cursor: pointer;
    }
    .add-item button:hover {
      background: #45a049;
    }
  </style>
</head>
<body>
  <h1>Шо мы сегодня будем хавать</h1>
  <div class="menu">
    <div class="person" id="person1">
      <h2>Выбирай</h2>
      <ul id="list1"></ul>
      <div class="add-item">
        <input type="text" id="input1" placeholder="Добавить блюдо...">
        <button onclick="addItem(1)">Добавить</button>
      </div>
    </div>
    <div class="person" id="person2">
 ВыбирайВыбирай

  <script>
    // Загрузка сохранённых данных
    document.addEventListener("DOMContentLoaded", () => {
      loadList(1);
      loadList(2);
    });

    function addItem(person) {
      const input = document.getElementById("input" + person);
      const text = input.value.trim();
      if (!text) return;

      const li = createListItem(text, person, false);
      document.getElementById("list" + person).appendChild(li);

      input.value = "";
      saveList(person);
    }

    function createListItem(text, person, checked) {
      const li = document.createElement("li");
      const checkbox = document.createElement("input");
      checkbox.type = "checkbox";
      checkbox.checked = checked;
      checkbox.onchange = () => saveList(person);

      const span = document.createElement("span");
      span.textContent = text;

      li.appendChild(checkbox);
      li.appendChild(span);
      return li;
    }

    function saveList(person) {
      const items = [];
      document.querySelectorAll("#list" + person + " li").forEach(li => {
        const checkbox = li.querySelector("input");
        const text = li.querySelector("span").textContent;
        items.push({ text, checked: checkbox.checked });
      });
      localStorage.setItem("menu_person" + person, JSON.stringify(items));
    }

    function loadList(person) {
      const data = localStorage.getItem("menu_person" + person);
      if (!data) return;

      const items = JSON.parse(data);
      items.forEach(item => {
        const li = createListItem(item.text, person, item.checked);
        document.getElementById("list" + person).appendChild(li);
      });
    }
  </script>
</body>
</html>
