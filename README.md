<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Квиз: Выбор бумаги для визиток</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .question {
            margin-bottom: 20px;
        }
        .options {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        .option {
            padding: 10px 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
            cursor: pointer;
            background-color: #f9f9f9;
            text-align: center;
        }
        .option.selected {
            background-color: #28a745;
            color: white;
            border-color: #28a745;
        }
        .result {
            margin-top: 20px;
            font-weight: bold;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input[type="text"], input[type="tel"] {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
        }
        button {
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body>

<h1>Квиз: Выбор бумаги для визиток</h1>

<!-- Вопрос 1: Тип бумаги -->
<div class="question">
    <h2>1. Выберите тип бумаги для печати визиток:</h2>
    <div class="options" id="paperTypeOptions">
        <div class="option" data-value="designer" onclick="selectOption(this, 'designerPaperOptions')">Дизайнерская бумага</div>
        <div class="option" data-value="coated" onclick="selectOption(this, 'designerPaperOptions')">Мелованная бумага</div>
    </div>
</div>

<!-- Вопрос 2: Тип дизайнерской бумаги -->
<div class="question hidden" id="designerPaperOptions">
    <h2>2. Выберите тип дизайнерской бумаги:</h2>
    <div class="options" id="designerPaperOptionsList">
        <div class="option" data-value="100" onclick="selectOption(this, 'printTypeOptions')">ARENA . Производитель: Fedrigoni, Италия - 100 рублей</div>
        <div class="option" data-value="200" onclick="selectOption(this, 'printTypeOptions')">COLORLAB. Производитель: Китай - 200 рублей</div>
        <div class="option" data-value="300" onclick="selectOption(this, 'printTypeOptions')">CLOUD LILY. Производитель: Китай - 300 рублей</div>
    </div>
</div>

<!-- Вопрос 3: Тип печати -->
<div class="question hidden" id="printTypeOptions">
    <h2>3. Выберите тип печати:</h2>
    <div class="options" id="printTypeOptionsList">
        <div class="option" data-value="100" onclick="selectOption(this, 'result')">Печать на бумаге 4+0 (Односторонняя) - 100 рублей</div>
        <div class="option" data-value="200" onclick="selectOption(this, 'result')">Печать на бумаге 4+4 (Двухсторонняя) - 200 рублей</div>
    </div>
</div>

<!-- Итоговая стоимость -->
<div class="result hidden" id="result">
    <h2>Итоговая стоимость: <span id="totalPrice">0</span> рублей</h2>
</div>

<!-- Форма заявки -->
<div class="form-group hidden" id="formGroup">
    <h2>Форма заявки:</h2>
    <label for="name">ФИО:</label>
    <input type="text" id="name" name="name" placeholder="Введите ваше ФИО">
    <label for="phone">Телефон:</label>
    <input type="tel" id="phone" name="phone" placeholder="Введите ваш телефон">
    <button onclick="submitForm()">Отправить</button>
</div>

<script>
    let selectedPaperType = null;
    let selectedDesignerPaper = null;
    let selectedPrintType = null;

    function selectOption(optionElement, nextQuestionId) {
        // Убираем выделение у всех кнопок в текущем вопросе
        const parent = optionElement.parentElement;
        const options = parent.querySelectorAll('.option');
        options.forEach(opt => opt.classList.remove('selected'));

        // Выделяем выбранную кнопку
        optionElement.classList.add('selected');

        // Сохраняем выбранное значение
        if (parent.id === 'paperTypeOptions') {
            selectedPaperType = optionElement.getAttribute('data-value');
        } else if (parent.id === 'designerPaperOptionsList') {
            selectedDesignerPaper = parseInt(optionElement.getAttribute('data-value'));
        } else if (parent.id === 'printTypeOptionsList') {
            selectedPrintType = parseInt(optionElement.getAttribute('data-value'));
        }

        // Показываем следующий вопрос
        if (nextQuestionId) {
            const nextQuestion = document.getElementById(nextQuestionId);
            if (nextQuestion) {
                nextQuestion.classList.remove('hidden');
            }
        }

        // Если это последний вопрос, обновляем стоимость и показываем форму
        if (nextQuestionId === 'result') {
            updatePrice();
            document.getElementById('result').classList.remove('hidden');
            document.getElementById('formGroup').classList.remove('hidden');
        }
    }

    function updatePrice() {
        const totalPrice = (selectedDesignerPaper || 0) + (selectedPrintType || 0);
        document.getElementById('totalPrice').textContent = totalPrice;
    }

    function submitForm() {
        const name = document.getElementById('name').value;
        const phone = document.getElementById('phone').value;
        const totalPrice = document.getElementById('totalPrice').textContent;

        if (name && phone && totalPrice > 0) {
            alert("Заявка отправлена!\nФИО: " + name + "\nТелефон: " + phone + "\nСтоимость: " + totalPrice + " рублей");
        } else {
            alert("Пожалуйста, заполните все поля и выберите опции.");
        }
    }
</script>

</body>
</html>
