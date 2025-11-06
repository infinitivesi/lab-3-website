# Звіт з лабораторної роботи 3

## Розробка базового вебпроєкту

### Інформація про команду
- Назва команди: -

- Учасники:
Шавирін Ярослав (кодер)

## Завдання

### Обрана предметна область

Роботи в сфері IT.

### Реалізовані вимоги

Вкажіть, які рівні завдань було виконано:

- [ да ] Рівень 1: Створено сторінки "Головна" та "Про нас"
- [ да ] Рівень 2: Додано мінімум дві додаткові статичні сторінки з меню та адаптивною версткою

## Хід виконання роботи

### Підготовка середовища розробки

Опишіть процес встановлення та налаштування:

- Версія Python = 3.12 64 біт
- Встановлення Flask = встановленний у VSCode за командою: pip install flask.
- Інші використані інструменти = VSCode

### Структура проєкту

Наведіть структуру файлів та директорій вашого проєкту:

```
lab-reports/
├── imageabout.png
├── imagehelp.png
├── imagehome.png
├── imageshop.png
└── lab03-report-ShavyrinYaroslav-IPZ21.md
lab03-flaskProject/
├── static/
│   ├── images.jpg
│   └── sad.jpg
├── templates/
│   ├── about.html
│   ├── base.html
│   ├── help.html
│   ├── home.html
│   └── shop.html
├── app.py
```

### Опис реалізованих сторінок

#### Головна сторінка

Текст, Картинка, Функціонал: Перехід на наступну сторінку, після перезапуску сторінки, картинка змінеться.

#### Сторінка "Про нас"

Текст, Картинка, Функціонал: Перехід на наступну сторінку, після перезапуску сторінки, картинка змінеться.

#### Сторінка Зворотнього зв'язку

Текст, Картинка, Функціонал: Перехід на наступну сторінку.

#### Сторінка Магазину

Текст, Картинка, Функціонал: Перехід на наступну сторінку.


## Ключові фрагменти коду

### Маршрутизація в Flask

Наведіть приклад налаштування маршрутів у файлі `app.py`:

```python
@app.route('/about')
def about():
    return render_template('about.html')
```

### Базовий шаблон
```

<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %} супер пупер крутий вебсайт {% endblock %}</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @keyframes slideDown {
            0% { max-height: 0; opacity: 0; }
            100% { max-height: 300px; opacity: 1; }
        }
        @keyframes slideUp {
            0% { max-height: 300px; opacity: 1; }
            100% { max-height: 0; opacity: 0; }
        }
        .animate-slide-down {
            animation: slideDown 0.3s ease-out forwards;
        }
        .animate-slide-up {
            animation: slideUp 0.3s ease-in forwards;
        }
        .burger-line {
            transition: all 0.3s ease-in-out;
        }
        .open .line1 {
            transform: rotate(-45deg) translate(-5px, 6px);
        }
        .open .line2 {
            opacity: 0;
        }
        .open .line3 {
            transform: rotate(45deg) translate(-5px, -6px);
        }
    </style>
</head>
<body class="bg-grey-100">
    <nav class="bg-purple-500 p-4">
        <div class="container mx-auto flex justify-between items-center">
            <a href="/" class="text-white text-2xl font-bold transition-transform duration-300 hover:scale-110">супер крутий вебсайт</a>
            <div class="hidden md:flex space-x-4">
                <a href="/" class="text-white text-xl hover:text-blue-200 transition-colors duration-300 hover:underline">Головна</a>
                <a href="/shop" class="text-white text-xl hover:text-blue-200 transition-colors duration-300 hover:underline">Магазин</a>
                <a href="/about" class="text-white text-xl hover:text-blue-200 transition-colors duration-300 hover:underline">Про нас</a>
                <a href="/help" class="text-white text-xl hover:text-blue-200 transition-colors duration-300 hover:underline">Зворотній зв'язок</a>
            </div>
            <button id="mobile-menu-button" class="md:hidden text-white w-6 h-6 relative focus:outline-none">
                <span class="burger-line block absolute h-0.5 w-6 bg-current transform transition duration-500 ease-in-out line1"></span>
                <span class="burger-line block absolute h-0.5 w-6 bg-current transform transition duration-500 ease-in-out line2"></span>
                <span class="burger-line block absolute h-0.5 w-6 bg-current transform transition duration-500 ease-in-out line3"></span>
            </button>
        </div>
        <div id="mobile-menu" class="hidden md:hidden overflow-hidden">
            <a href="/" class="block text-white hover:text-blue-200 py-2 transform transition duration-300 hover:translate-x-2">Головна</a>
            <a href="/shop" class="block text-white hover:text-blue-200 py-2 transform transition duration-300 hover:translate-x-2">Магазин</a>
            <a href="/about" class="block text-white hover:text-blue-200 py-2 transform transition duration-300 hover:translate-x-2">Про нас</a>
            <a href="/shop" class="block text-white hover:text-blue-200 py-2 transform transition duration-300 hover:translate-x-2">Зворотній зв'язок</a>
        </div>
    </nav>

    <div class="container mx-auto mt-8 p-4">
        {% block content %}{% endblock %}
    </div>

    <script>
        const mobileMenuButton = document.getElementById('mobile-menu-button');
        const mobileMenu = document.getElementById('mobile-menu');

        mobileMenuButton.addEventListener('click', () => {
            mobileMenuButton.classList.toggle('open');
            if (mobileMenu.classList.contains('hidden')) {
                mobileMenu.classList.remove('hidden');
                mobileMenu.classList.add('animate-slide-down');
                mobileMenu.classList.remove('animate-slide-up');
            } else {
                mobileMenu.classList.add('animate-slide-up');
                mobileMenu.classList.remove('animate-slide-down');
                setTimeout(() => {
                    mobileMenu.classList.add('hidden');
                }, 300);
            }
        });
    </script>
</body>
</html>
```

## Розподіл обов'язків у команді

Опишіть внесок кожного учасника команди:

- Шавирін Ярослав Олексійович: Створення нових шаблонів, створення папок та середовищ для роботи, зроблено 1 та 2 рівень завданнь.

## Скріншоти

Додайте скріншоти основних сторінок вашого вебзастосунку: 

lab-reports

### Головна сторінка

![Головна сторінка](lab-3-website/lab-reports/imagehome.png)

### Сторінка "Про нас"

![Сторінка Про нас](lab-3-website/lab-reports/imageabout.png)

### Додаткові сторінки

![Зворотній зв'язок](lab-3-website/lab-reports/imagehelp.png)

![Мазагин](lab-3-website/lab-reports/imageshop.png)


### Висновки

Опишіть:

- Що вдалося реалізувати успішно:
  
  Вдалось успішно реалізувати сайт для пошуку робіт у сфері ІТ, також успішно виконати 1 та 2 рівень завданнь. Я навчився краще працювати з GitHub та VSCode.
  
- З якими труднощами зіткнулися:
  Не вдалося реалізувати проєкт повністю на VSCode, було багато помилок але усі виправлені.

- Очікуванна оцінка:
  9-10
