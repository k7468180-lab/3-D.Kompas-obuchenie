<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Компас: Обучение</title>
    <style>
        :root {
            --primary-color: #6B9080;
            --hover-color: #557566;
            --bg-color: #F4F7F5;
            --text-color: #354F52;
            --card-bg: #ffffff;
            --section-bg: #EAF4F4;
        }

        * {
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.7;
            scroll-behavior: smooth;
        }

        /* === ШАПКА С ГРАДИЕНТОМ И ПОИСКОМ === */
        header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--text-color) 100%);
            box-shadow: 0 2px 15px rgba(0,0,0,0.1);
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            flex-wrap: wrap;
            gap: 15px;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 15px;
            flex: 1;
        }

        .logo-img {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            object-fit: cover;
            border: 2px solid white;
            background-color: #ddd;
        }

        .site-title {
            font-size: 1.1rem;
            font-weight: 600;
            color: white;
            white-space: nowrap;
        }

        /* === ПОИСК === */
        .search-container {
            position: relative;
            display: flex;
            align-items: center;
        }

        .search-input {
            padding: 8px 35px 8px 15px;
            border: none;
            border-radius: 25px;
            font-size: 0.9rem;
            width: 250px;
            transition: all 0.3s ease;
            background: rgba(255,255,255,0.95);
        }

        .search-input:focus {
            outline: none;
            width: 300px;
            box-shadow: 0 0 10px rgba(255,255,255,0.3);
        }

        .search-btn {
            position: absolute;
            right: 5px;
            top: 50%;
            transform: translateY(-50%);
            background: var(--primary-color);
            border: none;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }

        .search-btn:hover {
            background: var(--hover-color);
        }

        .search-results {
            position: absolute;
            top: 100%;
            right: 0;
            background: white;
            border-radius: 8px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.2);
            max-height: 400px;
            overflow-y: auto;
            z-index: 1001;
            display: none;
            min-width: 300px;
            margin-top: 10px;
        }

        .search-results.active {
            display: block;
        }

        .search-result-item {
            padding: 12px 15px;
            border-bottom: 1px solid #eee;
            cursor: pointer;
            transition: background 0.2s;
        }

        .search-result-item:hover {
            background: var(--section-bg);
        }

        .search-result-item:last-child {
            border-bottom: none;
        }

        .search-result-title {
            font-weight: 600;
            color: var(--primary-color);
            margin-bottom: 5px;
        }

        .search-result-text {
            font-size: 0.85rem;
            color: #666;
        }

        .no-results {
            padding: 15px;
            text-align: center;
            color: #999;
        }

        .hero-banner {
            position: relative;
            width: 100%;
            height: 400px;
            background: linear-gradient(rgba(107,144,128,0.85), rgba(53,79,82,0.8)), 
                        url('piato4ki/banner.jpg') center/cover no-repeat;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            color: white;
            padding: 20px;
        }

        .hero-banner > * {
            position: relative;
            z-index: 2;
            max-width: 700px;
        }

        .hero-banner h1 {
            font-size: 2.2rem;
            margin: 0 0 15px;
            font-weight: 700;
        }

        .hero-banner p {
            font-size: 1.2rem;
            margin: 0 0 25px;
            opacity: 0.95;
        }

        .nav-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 15px;
            width: 100%;
        }

        .nav-btn {
            display: block;
            background-color: rgba(255,255,255,0.95);
            color: var(--text-color);
            padding: 18px 20px;
            font-size: 1rem;
            font-weight: 600;
            text-decoration: none;
            border-radius: 12px;
            border: 2px solid transparent;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            transition: all 0.3s ease;
            cursor: pointer;
            text-align: center;
        }

        .nav-btn:hover {
            border-color: var(--primary-color);
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(107, 144, 128, 0.2);
            color: var(--primary-color);
        }

        .nav-btn:active {
            transform: scale(0.98);
        }

        .content-section {
            padding: 70px 20px;
            background-color: var(--card-bg);
            border-top: 1px solid #e0e0e0;
        }

        .content-section:nth-child(even) {
            background-color: var(--section-bg);
        }

        .container {
            max-width: 850px;
            margin: 0 auto;
        }

        .content-section h2 {
            font-size: 1.9rem;
            color: var(--primary-color);
            margin: 0 0 25px;
            padding-bottom: 12px;
            border-bottom: 3px solid var(--primary-color);
            display: inline-block;
        }

        .content-section h3 {
            color: var(--text-color);
            margin: 35px 0 18px;
            font-size: 1.35rem;
        }

        .content-section h4 {
            color: var(--text-color);
            margin: 25px 0 12px;
            font-size: 1.15rem;
            font-weight: 600;
        }

        .content-section p {
            font-size: 1.05rem;
            margin: 0 0 18px;
            text-align: justify;
        }

        .simple-link {
            color: var(--primary-color);
            text-decoration: none;
            font-weight: 600;
            border-bottom: 1px dashed var(--primary-color);
            transition: all 0.2s;
            display: inline-block;
        }

        .simple-link:hover {
            border-bottom-style: solid;
            color: var(--hover-color);
        }

        .screenshot {
            display: block;
            max-width: 100%;
            height: auto;
            margin: 25px auto;
            border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            border: 1px solid #e0e0e0;
            transition: transform 0.3s ease;
        }

        .screenshot:hover {
            transform: translateY(-4px);
        }

        .screenshot-caption {
            text-align: center;
            font-size: 0.9rem;
            color: #666;
            margin: -15px auto 25px;
            font-style: italic;
        }

        .step-list {
            list-style: none;
            padding: 0;
            margin: 20px 0;
            counter-reset: step;
        }

        .step-list li {
            counter-increment: step;
            padding: 12px 12px 12px 50px;
            position: relative;
            margin: 12px 0;
            background: var(--section-bg);
            border-radius: 10px;
            border-left: 3px solid var(--primary-color);
        }

        .step-list li::before {
            content: counter(step);
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            width: 26px;
            height: 26px;
            background: var(--primary-color);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 0.85rem;
        }

        .success-box {
            margin-top: 35px;
            padding: 25px;
            background: var(--section-bg);
            border-radius: 12px;
            text-align: center;
            font-weight: 600;
            border: 1px solid rgba(107,144,128,0.2);
        }

        .warning-box {
            background: #fff3cd;
            border-left: 4px solid #ffc107;
            padding: 15px 20px;
            margin: 20px 0;
            border-radius: 0 8px 8px 0;
            font-size: 0.95rem;
        }

        .param-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            font-size: 0.95rem;
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }

        .param-table th {
            background: var(--primary-color);
            color: white;
            padding: 12px 15px;
            text-align: left;
            font-weight: 600;
        }

        .param-table td {
            padding: 10px 15px;
            border-bottom: 1px solid #eee;
        }

        .param-table tr:last-child td {
            border-bottom: none;
        }

        .param-table tr:hover {
            background: var(--section-bg);
        }

        /* === ПЛАВАЮЩЕЕ ВИДЕО === */
        .floating-video {
            position: fixed;
            top: 90px;
            right: -400px;
            width: 380px;
            z-index: 999;
            background: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.15);
            padding: 10px;
            opacity: 0;
            visibility: hidden;
            transition: right 0.4s ease, opacity 0.3s ease, visibility 0.3s ease, transform 0.3s ease;
            pointer-events: none;
        }

        .floating-video.visible {
            opacity: 1;
            visibility: visible;
            pointer-events: auto;
        }

        .floating-video.active {
            right: 30px;
        }

        .floating-video.centered {
            position: absolute;
            top: 90px;
            left: 50%;
            transform: translateX(-50%);
            right: auto;
            opacity: 1;
            visibility: visible;
            pointer-events: auto;
        }

        .floating-video:hover {
            transform: scale(1.02);
        }

        .floating-video video {
            width: 100%;
            border-radius: 8px;
            display: block;
            background: #000;
        }

        .floating-video .video-caption {
            text-align: center;
            font-size: 0.85rem;
            color: #666;
            margin: 10px 0 0;
            font-style: italic;
        }

        .video-start-placeholder {
            display: none;
            width: 100%;
            max-width: 380px;
            margin: 30px auto;
            background: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            padding: 10px;
        }

        .video-start-placeholder video {
            width: 100%;
            border-radius: 8px;
            display: block;
            background: #000;
        }

        .video-start-placeholder .video-caption {
            text-align: center;
            font-size: 0.85rem;
            color: #666;
            margin: 10px 0 0;
            font-style: italic;
        }

        .specs-box {
            background: var(--section-bg);
            padding: 15px 20px;
            border-radius: 10px;
            margin: 20px 0;
            border-left: 3px solid var(--primary-color);
        }

        .specs-box strong {
            color: var(--primary-color);
        }

        /* === ИСТОЧНИКИ === */
        .sources-section {
            background: var(--section-bg);
            padding: 40px 20px;
            border-top: 2px solid var(--primary-color);
        }

        .sources-container {
            max-width: 850px;
            margin: 0 auto;
        }

        .sources-section h2 {
            color: var(--primary-color);
            margin: 0 0 20px;
            font-size: 1.5rem;
        }

        .sources-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .sources-list li {
            margin: 10px 0;
            padding: 10px;
            background: white;
            border-radius: 8px;
            border-left: 3px solid var(--primary-color);
        }

        .sources-list a {
            color: var(--text-color);
            text-decoration: none;
            word-break: break-all;
            transition: color 0.2s;
        }

        .sources-list a:hover {
            color: var(--primary-color);
            text-decoration: underline;
        }

        footer {
            text-align: center;
            padding: 30px;
            background-color: var(--text-color);
            color: #AEBDC0;
            font-size: 0.9rem;
        }

        /* === АДАПТИВНОСТЬ === */
        @media (max-width: 1400px) {
            .floating-video { width: 340px; right: 20px; }
        }

        @media (max-width: 1200px) {
            .floating-video { width: 300px; right: 15px; top: 90px; }
            .search-input { width: 200px; }
            .search-input:focus { width: 230px; }
        }

        @media (max-width: 768px) {
            .floating-video { display: none !important; }
            .video-start-placeholder { display: block !important; }
            header { 
                flex-direction: column; 
                gap: 12px; 
                text-align: center;
                padding: 1rem;
            }
            .logo-container {
                flex-direction: column;
                width: 100%;
            }
            .search-container {
                width: 100%;
                max-width: 400px;
            }
            .search-input {
                width: 100%;
            }
            .search-input:focus {
                width: 100%;
            }
            .search-results {
                left: 0;
                right: 0;
                min-width: auto;
            }
            .hero-banner { 
                height: 350px;
                padding: 15px;
            }
            .hero-banner h1 { 
                font-size: 1.6rem;
                margin-bottom: 10px;
            }
            .hero-banner p {
                font-size: 1rem;
                margin-bottom: 20px;
            }
            .nav-grid { 
                grid-template-columns: 1fr;
                gap: 10px;
            }
            .nav-btn {
                padding: 15px;
                font-size: 0.95rem;
            }
            .content-section { 
                padding: 40px 15px;
            }
            .content-section h2 { 
                font-size: 1.5rem;
            }
            .content-section h3 {
                font-size: 1.2rem;
            }
            .param-table { 
                font-size: 0.85rem;
            }
            .param-table th, 
            .param-table td { 
                padding: 8px 10px;
            }
            .screenshot {
                margin: 20px auto;
            }
            .step-list li {
                padding: 10px 10px 10px 45px;
                font-size: 0.95rem;
            }
            .step-list li::before {
                width: 22px;
                height: 22px;
                font-size: 0.75rem;
                left: 10px;
            }
            .sources-section {
                padding: 30px 15px;
            }
            .sources-list li {
                padding: 8px;
                font-size: 0.9rem;
            }
        }

        @media (max-width: 480px) {
            .site-title {
                font-size: 1rem;
            }
            .hero-banner h1 {
                font-size: 1.4rem;
            }
            .content-section h2 {
                font-size: 1.3rem;
            }
            .specs-box {
                padding: 12px 15px;
                font-size: 0.9rem;
            }
        }

        /* Подсветка найденного текста */
        .highlight {
            background: yellow;
            padding: 2px;
            border-radius: 3px;
        }
    </style>
</head>
<body>

    <header>
        <div class="logo-container">
            <img src="piato4ki/avatar.jpg" alt="Автор" class="logo-img">
            <div class="site-title">Создание 3-д моделей, легко и доступно</div>
        </div>
        <div class="search-container">
            <input type="text" class="search-input" id="searchInput" placeholder="Поиск по сайту...">
            <button class="search-btn" id="searchBtn">🔍</button>
            <div class="search-results" id="searchResults"></div>
        </div>
    </header>

    <!-- ✅ ПЛАВАЮЩЕЕ ВИДЕО (десктоп) -->
    <div class="floating-video" id="floatingVideo">
        <video 
            src="piato4ki/vidos.speed-8x.mp4" 
            autoplay 
            muted 
            loop 
            playsinline
            controlslist="nodownload"
            preload="metadata"
            controls>
            Ваш браузер не поддерживает видео.
        </video>
        <div class="video-caption">Видео-инструкция: создание фиджет-игрушки (20 мин, ускорено 8×)</div>
    </div>

    <section class="hero-banner">
        <div>
            <h1>пошаговая инструкция по 3-д компасу</h1>
            <p>Здесь мы подробно разберём программу КОМПАС-3D. Выберите тему, чтобы начать обучение:</p>
            
            <div class="nav-grid">
                <a href="#install" class="nav-btn">Установка программы</a>
                <a href="#create" class="nav-btn">Создание 3D моделей</a>
                <a href="#print" class="nav-btn">Печать на принтере</a>
            </div>
        </div>
    </section>

    <!-- РАЗДЕЛ 1: Установка -->
    <section id="install" class="content-section">
        <div class="container">
            <h2>1. Установка программы</h2>
            
            <p>Если вы совсем недавно обзавелись 3D-принтером, но уже поняли, что распечатывать готовые чужие файлы вам скучно, значит, этот цикл публикаций создан специально для вас. В своих материалах я постараюсь помочь вам освоить создание авторских 3D-моделей.</p>
            
            <p><strong>КОМПАС-3D Home</strong> — это интуитивно понятная даже новичку платформа для трёхмерного проектирования, при этом обладающая функционалом, сопоставимым с профессиональными решениями.</p>
            
            <p>Данный продукт разработан отечественной компанией <strong>АСКОН</strong> на базе профессионального пакета <strong>КОМПАС-3D</strong>, который успешно присутствует на рынке уже более четверти века.</p>
            
            <p>Интерфейс и вся сопроводительная документация, включая руководства и справочные материалы, полностью переведены на русский язык, что, несомненно, облегчит процесс освоения программы.</p>

            <p>Для начала работы вы можете загрузить бесплатную пробную версию <strong>КОМПАС-3D Home</strong>, рассчитанную на 60 дней использования. Сделать это можно на официальном ресурсе <strong>kompas.ru</strong>.</p>
            
            <p>🔗 Прямая ссылка для загрузки:<br>
            <a href="http://kompas.ru/kompas-3d-home/download/" target="_blank" class="simple-link">http://kompas.ru/kompas-3d-home/download/</a></p>
            
            <p>Заполнив простую регистрационную форму, вы получите на указанный e-mail ссылку на архив с дистрибутивом. Скачайте файл, распакуйте его и запустите установку. Уверен, этот этап не вызовет у вас сложностей.</p>
            
            <p>После активации вы увидите стартовый экран программы.</p>
            
            <img src="piato4ki/foto1.png" alt="Стартовый экран" class="screenshot">
            <div class="screenshot-caption">Фото 1: Стартовый экран КОМПАС-3D</div>

            <h3>Создание детали</h3>
            <p>Для начала работы над новым объектом просто нажмите на иконку с надписью 'деталь' на стартовой странице.</p>
            
            <h3>Эскиз — фундамент любой модели</h3>
            <p>Базой для любой операции служит эскиз. Чертежи размещаются на рабочих плоскостях или поверхностях существующей геометрии.</p>
            <p>Чтобы начать построение, активируйте кнопку <strong>«Эскиз»</strong> на панели «Текущее состояние» и укажите нужную плоскость.</p>
            <p>После этого программа переключится в режим редактирования эскиза: изображение ориентируется параллельно экрану, а в углу появится индикатор текущего режима.</p>
            
            <img src="piato4ki/foto2.png" alt="Режим эскиза" class="screenshot">
            <div class="screenshot-caption">Фото 2: Интерфейс режима эскиза</div>

            <h3>Рисуем прямоугольник</h3>
            <p>Выберите инструмент <strong>«Прямоугольник»</strong> на вкладке «Геометрия» или «Элементы тела».</p>
            
            <img src="piato4ki/foto3.png" alt="Инструмент Прямоугольник" class="screenshot">
            <div class="screenshot-caption">Фото 3: Выбор инструмента</div>
            
            <p>Вы можете задать габариты двумя способами: кликнуть мышью в двух произвольных точках или ввести точные значения с клавиатуры. Наберите высоту <strong>50 мм</strong>, подтвердите ввод клавишей <strong>Enter</strong>, затем укажите ширину <strong>50 мм</strong> и снова нажмите <strong>Enter</strong>. Щёлкните в любом месте рабочей области, чтобы разместить фигуру.</p>
            
            <p>Теперь можно завершить работу с эскизом. Для этого повторно нажмите кнопку <strong>«Эскиз»</strong> на панели состояния или воспользуйтесь значком выхода в правом верхнем углу.</p>

            <h3>Операция выдавливания</h3>
            <p>Когда эскиз готов, можно приступить к созданию объёма. Активируйте команду <strong>«Элемент выдавливания»</strong> на панели «Элементы тела».</p>
            
            <img src="piato4ki/foto4.png" alt="Операция выдавливания" class="screenshot">
            <div class="screenshot-caption">Фото 4: Команда выдавливания</div>
            
            <p>Задайте глубину: перетащите маркеры в окне предпросмотра или введите значение <strong>50 мм</strong> вручную, подтвердив клавишей <strong>Enter</strong>. Для завершения операции нажмите <strong>«Создать объект»</strong> или используйте комбинацию <strong>Ctrl+Enter</strong>.</p>
            
            <img src="piato4ki/foto5.png" alt="Готовый куб" class="screenshot">
            <div class="screenshot-caption">Фото 5: Результат выдавливания</div>
            
            <p>В результате у вас появится куб (или параллелепипед — в зависимости от введённых параметров).</p>

            <h3>Сохранение проекта</h3>
            <p>Не забудьте сохранить результат: нажмите кнопку <strong>«Сохранить»</strong> на стандартной панели или используйте горячие клавиши <strong>Ctrl+S</strong>. Укажите удобную папку для размещения файла.</p>

            <h3>Экспорт для 3D-печати</h3>
            <p>Чтобы отправить модель на печать, её необходимо экспортировать в формат <strong>STL</strong>.</p>
            <p>Для этого в меню <strong>«Файл»</strong> выберите пункт <strong>«Сохранить как...»</strong>. В диалоговом окне в списке «Тип файла» укажите формат <strong>Stl</strong>.</p>
            <p>Затем кликните по стрелке рядом с кнопкой <strong>«Сохранить»</strong> и в выпадающем меню выберите <strong>«Сохранить с параметрами»</strong>.</p>
            <p>Откроется окно «Параметры экспорта в Stl». В данном случае настройки можно оставить без изменений — просто подтвердите действие, нажав <strong>Ок</strong>.</p>
            
            <img src="piato4ki/foto6.jpg" alt="Параметры экспорта" class="screenshot">
            <div class="screenshot-caption">Фото 6: Окно параметров экспорта</div>
            
            <p>В следующем диалоге выберите вариант <strong>«Текстовый»</strong> и нажмите кнопку <strong>«Начать запись»</strong>.</p>
            
            <div class="success-box">
                🎉 Поздравляем! Ваша первая авторская модель, готовая к 3D-печати, создана!
            </div>
        </div>
    </section>

    <!-- РАЗДЕЛ 2: Создание моделей (с видео) -->
    <section id="create" class="content-section">
        <div class="container">
            <h2>2. Создание простых 3D моделей</h2>
            
            <!-- ✅ СТАТИЧНОЕ ВИДЕО В НАЧАЛЕ РАЗДЕЛА (для мобильных и начальной позиции) -->
            <div class="video-start-placeholder" id="videoPlaceholder">
                <video 
                    src="piato4ki/vidos.speed-8x.mp4" 
                    autoplay 
                    muted 
                    loop 
                    playsinline
                    controlslist="nodownload"
                    preload="metadata"
                    controls>
                    Ваш браузер не поддерживает видео.
                </video>
                <div class="video-caption">Видео-инструкция: создание фиджет-игрушки (20 мин, ускорено 8×)</div>
            </div>
            
            <h3>КОМПАС-3D для новичков: Создаём фиджет-игрушку с подвижной сферой</h3>
            
            <h4>Что будем делать</h4>
            <p>Создадим игрушку-антистресс из двух частей: <strong>корпус</strong> и <strong>подвижная сфера внутри</strong>. Для этого нам понадобятся три заготовки: корпус, сфера и спираль (для создания узора).</p>
            
            <div class="specs-box">
                <strong>Габариты модели:</strong><br>
                • Высота: 70 мм<br>
                • Диаметр корпуса: 40 мм<br>
                • Диаметр спирали: 36 мм<br>
                • Диаметр сферы: 38 мм
            </div>
            
            <h3>ШАГ 1: Подготовка</h3>
            <ol class="step-list">
                <li>Запустите <strong>КОМПАС-3D</strong></li>
                <li>Нажмите <strong>«Файл» → «Создать» → «Деталь»</strong></li>
                <li>Вы попали в рабочее пространство. Справа или слева вы видите <strong>Дерево построения</strong> — там будут появляться все ваши действия.</li>
            </ol>
            
            <h3>ШАГ 2: Создаём спираль (основу узора)</h3>
            
            <h4>2.1. Вызываем команду</h4>
            <ul>
                <li>Перейдите: <strong>«Моделирование» → «Элементы каркаса» → «Спираль цилиндрическая»</strong></li>
                <li>Совет: Если не нашли, введите «спираль» в поиске команд (значок лупы вверху)</li>
            </ul>
            
            <h4>2.2. Настраиваем спираль</h4>
            <p>В появившейся панели справа:</p>
            
            <table class="param-table">
                <thead>
                    <tr>
                        <th>Параметр</th>
                        <th>Значение</th>
                        <th>Зачем</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td><strong>Базовая плоскость</strong></td>
                        <td>Выберите синюю плоскость</td>
                        <td>Где рисовать спираль</td>
                    </tr>
                    <tr>
                        <td><strong>Координаты</strong></td>
                        <td>X=0, Y=0</td>
                        <td>Чтобы спираль встала ровно в центр</td>
                    </tr>
                    <tr>
                        <td><strong>Диаметр</strong></td>
                        <td>36 мм</td>
                        <td>Чуть меньше корпуса</td>
                    </tr>
                    <tr>
                        <td><strong>Количество витков</strong></td>
                        <td>0.7–1.5</td>
                        <td>Меньше витков = меньше дефектов при печати</td>
                    </tr>
                    <tr>
                        <td><strong>Высота (шаг)</strong></td>
                        <td>70 мм</td>
                        <td>По высоте игрушки</td>
                    </tr>
                </tbody>
            </table>
            
            <p>Нажмите <strong>«Создать объект»</strong> (зелёная галочка) или <code>Ctrl+Enter</code></p>
            
            <h4>2.3. Рисуем «лепесток» спирали</h4>
            <ol class="step-list">
                <li>Нажмите кнопку <strong>«Эскиз»</strong> (значок карандаша)</li>
                <li>Кликните по <strong>синей плоскости</strong> — она повернётся к вам «лицом»</li>
                <li>В панели <strong>«Геометрия»</strong> выберите <strong>«Прямоугольник по центру и вершине»</strong></li>
                <li>Поставьте центр прямоугольника на <strong>горизонтальную ось</strong> (появится значок привязки)</li>
                <li>Вторую точку зафиксируйте на <strong>вертикальной оси</strong> — так лепесток будет симметричным</li>
            </ol>
            
            <h4>2.4. Добавляем окружность и размеры</h4>
            <ol class="step-list">
                <li>Выберите инструмент <strong>«Окружность»</strong> и поставьте её в центр прямоугольника</li>
                <li>Нажмите <strong>«Авторазмер»</strong> (в разделе «Черчение» → «Размеры»)</li>
                <li>Проставьте размеры:
                    <ul>
                        <li>Диаметр окружности: <strong>6 мм</strong></li>
                        <li>Расстояние от центра до края прямоугольника: <strong>15 мм</strong></li>
                        <li>Толщина прямоугольника: <strong>4 мм</strong></li>
                    </ul>
                </li>
            </ol>
            
            <h4>2.5. Копируем лепестки по кругу</h4>
            <ol class="step-list">
                <li>Зажмите <code>Shift</code> и выделите все контуры (прямоугольник + окружность)</li>
                <li>Выберите: <strong>«Черчение» → «Копия» → «Копия по окружности»</strong></li>
                <li>Настройки:
                    <ul>
                        <li><strong>Центр копирования</strong>: начало координат (0;0)</li>
                        <li><strong>Режим</strong>: «Заданное количество на окружности»</li>
                        <li><strong>Количество</strong>: 5 или 7 (нечётное число)</li>
                    </ul>
                </li>
            </ol>
            
            <div class="warning-box">
                <strong>Важно:</strong> При чётном числе контуры пересекаются в одной точке — КОМПАС не сможет сделать их объёмными.
            </div>
            
            <ol class="step-list" start="4">
                <li>Нажмите «Создать объект» — эскиз готов</li>
            </ol>
            
            <h4>2.6. Делаем спираль объёмной</h4>
            <ol class="step-list">
                <li>Выберите: <strong>«Моделирование» → «Добавить элемент» → «Элемент по траектории»</strong></li>
                <li>В панели настроек:
                    <ul>
                        <li><strong>Сечение</strong>: ваш эскиз с лепестками (выбрано автоматически)</li>
                        <li><strong>Траектория</strong>: кликните по спирали, которую создали в шаге 2.2</li>
                    </ul>
                </li>
                <li>Нажмите «Создать объект» — спираль готова.</li>
            </ol>
            
            <p><strong>Скройте лишнее</strong>: в Дереве построения нажмите на значок видимости (глаз) рядом со спиралью и эскизом — они исчезнут из вида, но останутся в файле.</p>
            
            <!-- ✅ ФОТО 9 -->
            <img src="piato4ki/foto9.png" alt="Спираль готова" class="screenshot">
            <div class="screenshot-caption">Фото 9: Готовая спираль</div>
            
            <h3>ШАГ 3: Создаём корпус</h3>
            
            <h4>3.1. Новый эскиз</h4>
            <ol class="step-list">
                <li>Убедитесь, что спираль скрыта</li>
                <li>Нажмите <strong>«Эскиз»</strong> → выберите <strong>зелёную плоскость</strong></li>
            </ol>
            
            <h4>3.2. Рисуем контур корпуса</h4>
            <p>Нарисуйте половину профиля корпуса (как на разрезе):</p>
            <ol class="step-list">
                <li><strong>«Отрезок»</strong>: вертикальная линия внизу</li>
                <li><strong>«Дуга по двум точкам»</strong>: плавный изгиб корпуса</li>
                <li><strong>«Отрезок»</strong>: верхняя граница</li>
            </ol>
            
            <h4>3.3. Добавляем ограничения и размеры</h4>
            <table class="param-table">
                <thead>
                    <tr>
                        <th>Действие</th>
                        <th>Инструмент</th>
                        <th>Значение</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Сделать отрезки равными</td>
                        <td>«Ограничения» → «Равенство»</td>
                        <td>—</td>
                    </tr>
                    <tr>
                        <td>Задать высоту корпуса</td>
                        <td>«Авторазмер»</td>
                        <td>70 мм</td>
                    </tr>
                    <tr>
                        <td>Задать толщину стенки</td>
                        <td>«Авторазмер»</td>
                        <td>7 мм</td>
                    </tr>
                    <tr>
                        <td>Отступ дуги от центра</td>
                        <td>«Авторазмер» (горизонтальный)</td>
                        <td>10 мм</td>
                    </tr>
                    <tr>
                        <td>Радиус корпуса</td>
                        <td>«Авторазмер» (радиус)</td>
                        <td>20 мм (диаметр 40 мм)</td>
                    </tr>
                    <tr>
                        <td>Выровнять отрезки</td>
                        <td>«Ограничения» → «Выравнивание»</td>
                        <td>—</td>
                    </tr>
                </tbody>
            </table>
            
            <h4>3.4. Осевая линия для вращения</h4>
            <ol class="step-list">
                <li>Выберите: <strong>«Черчение» → «Автоосевая»</strong></li>
                <li>Проведите вертикальную линию через начало координат (зажмите <code>Shift</code> для строгой вертикали)</li>
            </ol>
            
            <h4>3.5. Создаём объём</h4>
            <ol class="step-list">
                <li>Выберите: <strong>«Моделирование» → «Добавить элемент» → «Элемент вращения»</strong></li>
                <li>Убедитесь, что спираль скрыта (иначе тела «склеятся»)</li>
                <li>Нажмите «Создать объект» — корпус готов</li>
            </ol>
            
            <p>Скройте корпус в Дереве построения, чтобы он не мешал.</p>
            
            <!-- ✅ ФОТО 10 -->
            <img src="piato4ki/foto10.png" alt="Корпус готов" class="screenshot">
            <div class="screenshot-caption">Фото 10: Готовый корпус</div>
            
            <h3>ШАГ 4: Создаём сферу (подвижная часть)</h3>
            
            <h4>4.1. Новый эскиз</h4>
            <ol class="step-list">
                <li>Нажмите <strong>«Эскиз»</strong> → выберите <strong>зелёную плоскость</strong></li>
            </ol>
            
            <h4>4.2. Рисуем полуокружность</h4>
            <ol class="step-list">
                <li>Выберите <strong>«Дуга»</strong> (базовый инструмент)</li>
                <li>Поставьте центр дуги на вертикальную ось</li>
                <li>Начало и конец дуги тоже привяжите к вертикали</li>
                <li>Углы: начальный <strong>90°</strong>, конечный <strong>270°</strong></li>
            </ol>
            
            <h4>4.3. Размеры</h4>
            <ul>
                <li>Радиус дуги: <strong>19 мм</strong> (диаметр сферы = 38 мм)</li>
                <li>Отступ центра сферы от низа: <strong>35 мм</strong> (середина высоты 70 мм)</li>
            </ul>
            
            <h4>4.4. Делаем шар</h4>
            <ol class="step-list">
                <li>Добавьте осевую линию (как в шаге 3.4)</li>
                <li>Выберите <strong>«Элемент вращения»</strong> → нажмите «Создать объект»</li>
            </ol>
            
            <p>В Дереве построения у вас теперь три тела: <strong>Спираль</strong>, <strong>Корпус</strong>, <strong>Сфера</strong></p>
            
            <!-- ✅ ФОТО 11 -->
            <img src="piato4ki/foto11.png" alt="Сфера готова" class="screenshot">
            <div class="screenshot-caption">Фото 11: Готовая сфера</div>
            
            <h3>ШАГ 5: Булевы операции</h3>
            
            <div class="warning-box">
                <strong>Совет:</strong> Переключите вид Дерева с «Истории построения» на <strong>«Структурное представление»</strong>. Так вы увидите именно тела, а не шаги их создания.
            </div>
            
            <h4>5.1. Вырезаем узор на корпусе</h4>
            <ol class="step-list">
                <li>Скройте сферу и вторую спираль (оставьте видны только <strong>Корпус</strong> и <strong>Спираль-1</strong>)</li>
                <li>Выберите: <strong>«Моделирование» → «Булевы операции» → «Вычитание»</strong></li>
                <li>Настройки:
                    <ul>
                        <li><strong>Главное тело</strong>: Корпус (кликните по нему)</li>
                        <li><strong>Вычитаемое тело</strong>: Спираль-1</li>
                    </ul>
                </li>
                <li>Нажмите «Создать объект» — в корпусе появился спиральный узор.</li>
            </ol>
            
            <h4>5.2. Делаем подвижную сферу</h4>
            <ol class="step-list">
                <li>Скройте корпус, покажите <strong>Сферу</strong> и <strong>Спираль-2</strong> (копию спирали)</li>
                <li>Выберите: <strong>«Булевы операции» → «Пересечение»</strong></li>
                <li>Выделите сферу и спираль (порядок не важен)</li>
                <li>Нажмите «Создать объект» — сфера теперь со спиральным узором.</li>
            </ol>
            
            <!-- ✅ ФОТО 12 -->
            <img src="piato4ki/foto12.png" alt="Булевы операции" class="screenshot">
            <div class="screenshot-caption">Фото 12: Результат булевых операций</div>
            
            <h3>ШАГ 6: Добавляем зазор (чтобы сфера двигалась)</h3>
            
            <div class="warning-box">
                <strong>Важно:</strong> Без этого шага сфера застрянет в корпусе.
            </div>
            
            <ol class="step-list">
                <li>Скройте сферу, оставьте видимым только <strong>Корпус</strong></li>
                <li>Выберите: <strong>«Моделирование» → «Грани» → «Сместить грани»</strong></li>
                <li>Выделите <strong>внутренние грани корпуса</strong>, которые касаются сферы (удерживайте <code>Ctrl</code> для множественного выбора)</li>
                <li>В панели настроек:
                    <ul>
                        <li>Нажмите <strong>«Сменить направление»</strong>, чтобы отступ шёл внутрь</li>
                        <li>Значение смещения: <strong>0.3 мм</strong> (оптимальный зазор для 3D-печати)</li>
                    </ul>
                </li>
                <li>Нажмите «Создать объект»</li>
            </ol>
            
            <p>Покажите сферу — теперь между деталями есть небольшой промежуток.</p>
            
            <h3>ШАГ 7: Сохраняем в STL для печати</h3>
            
            <h4>7.1. Сохраняем корпус</h4>
            <ol class="step-list">
                <li>Скройте сферу, оставьте видимым только <strong>Корпус</strong></li>
                <li><strong>«Файл» → «Сохранить как...»</strong></li>
                <li>Тип файла: <strong>«Файлы стереолитографии (*.stl)»</strong></li>
                <li>Нажмите на <strong>стрелочку рядом с кнопкой «Сохранить»</strong> → <strong>«Сохранить с параметрами»</strong></li>
                <li>В окне настроек:
                    <ul>
                        <li><strong>Точность (допуск)</strong>: <strong>0.01 мм</strong> (для гладких поверхностей)</li>
                        <li>Формат: <strong>Двоичный</strong> (меньше размер файла)</li>
                    </ul>
                </li>
                <li>Нажмите <strong>«Экспортировать»</strong></li>
            </ol>
            
            <h4>7.2. Сохраняем сферу</h4>
            <ol class="step-list">
                <li>Скройте корпус, покажите <strong>Сферу</strong></li>
                <li>Повторите шаги 2–6 выше</li>
                <li>Готово. У вас два STL-файла: <code>корпус.stl</code> и <code>сфера.stl</code></li>
            </ol>
            
            <div class="success-box">
                <strong>Готово. Что дальше?</strong><br><br>
                1. Загрузите STL-файлы в слайсер (Cura, PrusaSlicer и др.)<br>
                2. Настройте печать (материал: PLA, высота слоя: 0.15–0.2 мм)<br>
                3. Распечатайте обе детали<br>
                4. Соберите: сфера должна свободно вращаться внутри корпуса<br><br>
                <em>Важно: Всегда сохраняйте исходный файл .m3d — в нём можно редактировать модель. STL-файл предназначен только для печати.</em>
            </div>
        </div>
    </section>

    <!-- РАЗДЕЛ 3: Печать -->
    <section id="print" class="content-section">
        <div class="container">
            <h2>3. Печать на 3D принтере</h2>
            
            <h3>ЭТАП 1: Поиск и загрузка 3D-моделей</h3>
            
            <h4>Вариант А: Скачивание готовых STL-моделей</h4>
            <p>Посетите библиотеки 3D-моделей:</p>
            <ul>
                <li><a href="https://www.thingiverse.com" target="_blank" class="simple-link">Thingiverse</a></li>
                <li><a href="https://www.printables.com" target="_blank" class="simple-link">Printables</a></li>
                <li><a href="https://cults3d.com" target="_blank" class="simple-link">Cults3D</a></li>
            </ul>
            <p>В поиске введите название модели (например, «fidget cube», «gear», «bracket»)</p>
            <p>Выберите модель с высоким рейтингом и положительными отзывами</p>
            <p>Нажмите кнопку Download → скачайте файл в формате .STL</p>
            
            <h4>Вариант Б: Создание собственной модели в КОМПАС-3D</h4>
            <ul class="step-list">
                <li>На стартовой странице нажмите «Создать деталь»</li>
                <li>Постройте эскиз на одной из плоскостей (кнопка «Эскиз» → выбор плоскости)</li>
                <li>Используйте инструменты геометрии: «Прямоугольник», «Окружность», «Отрезок»</li>
                <li>Примените операцию «Выдавливание» для создания объёма</li>
                <li>Добавьте дополнительные элементы: «Вырезать», «Скругление», «Массив»</li>
                <li>Сохраните модель: Файл → Сохранить (формат .m3d — родной формат КОМПАС)</li>
            </ul>
            
            <h3>ЭТАП 2: Импорт модели в КОМПАС-3D (если модель скачана)</h3>
            
            <div class="warning-box">
                <strong>Важно:</strong> КОМПАС-3D — это САПР для проектирования, а не слайсер. Он используется для подготовки и экспорта модели, а не для непосредственной печати.
            </div>
            
            <h4>Шаг 2.1: Открытие STL-файла</h4>
            <ul class="step-list">
                <li>Запустите КОМПАС-3D</li>
                <li>Перейдите: Файл → Открыть</li>
                <li>В типе файлов выберите «Файлы стереолитографии (*.stl)»</li>
                <li>Найдите скачанный файл и откройте его</li>
            </ul>
            
            <h4>Шаг 2.2: Проверка и редактирование модели</h4>
            <p>Убедитесь, что модель загрузилась корректно</p>
            <p>При необходимости:</p>
            <ul>
                <li>Масштабируйте: Инструменты → Редактирование детали → Масштабирование</li>
                <li>Ориентируйте: Вид → Ориентация → выберите нужный ракурс</li>
                <li>Проверьте геометрию: Сервис → Проверка модели (на наличие разрывов)</li>
            </ul>
            
            <h3>ЭТАП 3: Экспорт модели в STL для 3D-печати</h3>
            <p><strong>Это критически важный этап — от настроек экспорта зависит качество печати.</strong></p>
            
            <h4>Шаг 3.1: Вызов команды экспорта</h4>
            <ul class="step-list">
                <li>Убедитесь, что открыта деталь (не сборка и не чертёж)</li>
                <li>Перейдите: Файл → Сохранить как...</li>
                <li>В поле «Тип файла» выберите «Файлы стереолитографии (*.stl)»</li>
            </ul>
            
            <h4>Шаг 3.2: Настройка параметров экспорта</h4>
            <p>Нажмите на стрелку ▼ рядом с кнопкой «Сохранить»</p>
            <p>Выберите «Сохранить с параметрами»</p>
            <p>Откроется окно «Параметры экспорта в STL»:</p>
            
            <table class="param-table">
                <thead>
                    <tr>
                        <th>Параметр</th>
                        <th>Рекомендуемое значение</th>
                        <th>Пояснение</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Формат файла</td>
                        <td>Текстовый (ASCII) или Двоичный</td>
                        <td>Двоичный — меньше размер, Текстовый — легче редактировать</td>
                    </tr>
                    <tr>
                        <td>Единицы измерения</td>
                        <td>Миллиметры (мм)</td>
                        <td>Стандарт для 3D-печати</td>
                    </tr>
                    <tr>
                        <td>Точность (допуск)</td>
                        <td>0.01–0.05 мм</td>
                        <td>Чем меньше — тем выше детализация, но больше размер файла</td>
                    </tr>
                    <tr>
                        <td>Разбиение на треугольники</td>
                        <td>Автоматически / Высокое качество</td>
                        <td>Обеспечивает плавные поверхности</td>
                    </tr>
                    <tr>
                        <td>Экспортировать</td>
                        <td>Только видимые компоненты / Вся деталь</td>
                        <td>Выбирайте в зависимости от задачи</td>
                    </tr>
                </tbody>
            </table>
            
            <p>Нажмите ОК для подтверждения</p>
            
            <h4>Шаг 3.3: Сохранение файла</h4>
            <ul class="step-list">
                <li>Укажите папку для сохранения (рекомендуется создать отдельную папку STL_Export)</li>
                <li>Дайте файлу понятное имя (например, MyPart_v1.stl)</li>
                <li>Нажмите Сохранить</li>
            </ul>
            
            <h3>ЭТАП 4: Подготовка к печати в слайсере</h3>
            
            <div class="warning-box">
                <strong>Важно:</strong> КОМПАС-3D не управляет принтером напрямую. Для печати необходим слайсер — программа, преобразующая STL в G-код (инструкции для принтера).
            </div>
            
            <p><strong>Популярные слайсеры:</strong></p>
            <ul>
                <li>Cura (бесплатный, самый популярный)</li>
                <li>PrusaSlicer (открытый, много настроек)</li>
                <li>Simplify3D (платный, профессиональный)</li>
            </ul>
            
            <h4>Шаг 4.1: Импорт STL в слайсер</h4>
            <ul class="step-list">
                <li>Запустите слайсер (например, Cura)</li>
                <li>Перетащите файл .stl в рабочую область или используйте Файл → Открыть</li>
                <li>Модель появится на виртуальном столе</li>
            </ul>
            
            <!-- ✅ НОВОЕ ФОТО 7 (PNG) -->
            <img src="piato4ki/foto7.png" alt="Модель в слайсере" class="screenshot">
            <div class="screenshot-caption">Фото 7: Модель на виртуальном столе в слайсере</div>
            
            <h4>Шаг 4.2: Настройка параметров печати</h4>
            <p>Основные параметры (пример для PLA-пластика):</p>
            
            <table class="param-table">
                <thead>
                    <tr>
                        <th>Параметр</th>
                        <th>Значение</th>
                        <th>Комментарий</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Высота слоя</td>
                        <td>0.15–0.2 мм</td>
                        <td>Баланс качества и скорости</td>
                    </tr>
                    <tr>
                        <td>Заполнение (Infill)</td>
                        <td>15–25%</td>
                        <td>Для декоративных деталей; 50–100% — для прочных</td>
                    </tr>
                    <tr>
                        <td>Толщина стенок</td>
                        <td>1.2–1.6 мм (3–4 периметра)</td>
                        <td>Обеспечивает прочность</td>
                    </tr>
                    <tr>
                        <td>Скорость печати</td>
                        <td>40–60 мм/с</td>
                        <td>Медленнее = качественнее</td>
                    </tr>
                    <tr>
                        <td>Температура сопла</td>
                        <td>200–210 °C (для PLA)</td>
                        <td>Зависит от производителя пластика</td>
                    </tr>
                    <tr>
                        <td>Температура стола</td>
                        <td>50–60 °C (для PLA)</td>
                        <td>Улучшает адгезию</td>
                    </tr>
                    <tr>
                        <td>Поддержки (Supports)</td>
                        <td>Вкл., если есть свесы >45°</td>
                        <td>Тип: Tree (древовидные) — экономнее</td>
                    </tr>
                    <tr>
                        <td>Адгезия к столу</td>
                        <td>Brim или Skirt</td>
                        <td>Предотвращает отрыв модели</td>
                    </tr>
                </tbody>
            </table>
            
            <h4>Шаг 4.3: Слайсинг и сохранение G-кода</h4>
            <ul class="step-list">
                <li>Нажмите кнопку «Slice» (Нарезать)</li>
                <li>Дождитесь расчёта траекторий</li>
                <li>Просмотрите предпросмотр: убедитесь, что все слои корректны</li>
                <li>Нажмите «Save to File» и сохраните файл с расширением .gcode</li>
            </ul>
            
            <h3>ЭТАП 5: Печать на 3D-принтере</h3>
            
            <h4>Шаг 5.1: Подготовка принтера</h4>
            <ul class="step-list">
                <li>Включите принтер и дождитесь нагрева</li>
                <li>Очистите печатную платформу (протрите изопропиловым спиртом)</li>
                <li>Загрузите пластик: подайте нить в экструдер до появления капли из сопла</li>
                <li>Откалибруйте стол (если требуется): зазор между соплом и столом ≈ толщина листа бумаги</li>
            </ul>
            
            <!-- ✅ НОВОЕ ФОТО 8 -->
            <img src="piato4ki/foto8.jpg" alt="Калибровка стола принтера" class="screenshot">
            <div class="screenshot-caption">Фото 8: Калибровка печатного стола</div>
            
            <h4>Шаг 5.2: Запуск печати</h4>
            <p><strong>Способ А: Через SD-карту</strong></p>
            <ul>
                <li>Скопируйте .gcode-файл на microSD-карту</li>
                <li>Вставьте карту в принтер</li>
                <li>В меню принтера выберите Print from SD → ваш файл → Start</li>
            </ul>
            
            <p><strong>Способ Б: Через USB / Wi-Fi</strong></p>
            <ul>
                <li>Подключите принтер к компьютеру кабелем или по сети</li>
                <li>В слайсере нажмите «Print via USB» (если поддерживается)</li>
                <li>Следите за началом печати через интерфейс принтера</li>
            </ul>
            
            <h4>Шаг 5.3: Контроль процесса</h4>
            <ul class="step-list">
                <li>Первые 5–10 минут наблюдайте за печатью: убедитесь, что первый слой ложится ровно</li>
                <li>Не открывайте дверцу (если принтер с камерой) — перепады температуры могут вызвать отслоение</li>
                <li>При необходимости используйте вентилятор для обдува (для PLA)</li>
            </ul>
            
            <h4>Шаг 5.4: Завершение и постобработка</h4>
            <ul class="step-list">
                <li>После окончания печати дождитесь остывания стола (особенно для ABS)</li>
                <li>Аккуратно снимите модель шпателем</li>
                <li>Удалите поддержки (кусачками, ножом)</li>
                <li>При необходимости:
                    <ul>
                        <li>Обработайте наждачной бумагой (зерно 200–800)</li>
                        <li>Покрасьте или покройте грунтовкой</li>
                        <li>Склейте детали (если модель печаталась частями)</li>
                    </ul>
                </li>
            </ul>
            
            <div class="success-box">
                Готово! Ваша модель успешно напечатана.
            </div>
        </div>
    </section>

    <!-- === ИСТОЧНИКИ ИНФОРМАЦИИ === -->
    <section class="sources-section">
        <div class="sources-container">
            <h2>📚 Источники информации:</h2>
            <ul class="sources-list">
                <li><a href="https://rutube.ru/video/07606f6dcfdfc78d1bc17864afdcaca4/?r=wd" target="_blank">https://rutube.ru/video/07606f6dcfdfc78d1bc17864afdcaca4/?r=wd</a></li>
                <li><a href="https://www.ixbt.com/live/sw/kak-sozdat-prostye-figury-v-kompas-3d-kvadrat-treugolnik-krug.html#toc_header1" target="_blank">https://www.ixbt.com/live/sw/kak-sozdat-prostye-figury-v-kompas-3d-kvadrat-treugolnik-krug.html</a></li>
                <li><a href="https://fluidcourse.ru/kompasmetodichka#module-2-exercise-5" target="_blank">https://fluidcourse.ru/kompasmetodichka#module-2-exercise-5</a></li>
                <li><a href="https://pikabu.ru/story/3d_pechat_dlya_chaynikov_chast_1_vvodnaya_10272914" target="_blank">https://pikabu.ru/story/3d_pechat_dlya_chaynikov_chast_1_vvodnaya_10272914</a></li>
            </ul>
        </div>
    </section>

    <footer>
        <p>&copy; 2023 Обучение 3D Компас. Все права защищены.</p>
    </footer>

    <!-- ✅ СКРИПТ ДЛЯ «УМНОГО» ПЛАВАЮЩЕГО ВИДЕО И ПОИСКА -->
    <script>
        // === ПЛАВАЮЩЕЕ ВИДЕО ===
        document.addEventListener('DOMContentLoaded', function() {
            const floatingVideo = document.getElementById('floatingVideo');
            const videoPlaceholder = document.getElementById('videoPlaceholder');
            const section2 = document.getElementById('create');
            
            const isMobile = window.innerWidth <= 768;
            
            if (isMobile) {
                floatingVideo.style.display = 'none';
                videoPlaceholder.style.display = 'block';
                return;
            }
            
            videoPlaceholder.style.display = 'none';
            
            let section2Top = 0;
            let section2Height = 0;
            let videoActive = false;
            let videoCentered = false;
            
            function updateSectionMetrics() {
                const rect = section2.getBoundingClientRect();
                section2Top = window.scrollY + rect.top;
                section2Height = section2.offsetHeight;
            }
            
            function updateVideo() {
                updateSectionMetrics();
                
                const scrollY = window.scrollY;
                const windowHeight = window.innerHeight;
                const sectionBottom = section2Top + section2Height;
                const stickPoint = section2Top + 150;
                
                const inSection = scrollY + windowHeight * 0.3 >= section2Top && 
                                 scrollY <= sectionBottom - windowHeight * 0.3;
                
                if (!inSection) {
                    floatingVideo.classList.remove('visible', 'active', 'centered');
                    videoActive = false;
                    videoCentered = false;
                    return;
                }
                
                floatingVideo.classList.add('visible');
                videoActive = true;
                
                if (scrollY < stickPoint) {
                    if (!videoCentered) {
                        floatingVideo.classList.add('centered');
                        floatingVideo.classList.remove('active');
                        videoCentered = true;
                    }
                } else {
                    if (videoCentered) {
                        floatingVideo.classList.remove('centered');
                        floatingVideo.classList.add('active');
                        videoCentered = false;
                    }
                }
            }
            
            window.addEventListener('load', updateVideo);
            window.addEventListener('scroll', updateVideo, { passive: true });
            window.addEventListener('resize', () => {
                updateSectionMetrics();
                updateVideo();
                
                const isMobileNow = window.innerWidth <= 768;
                if (isMobileNow) {
                    floatingVideo.style.display = 'none';
                    videoPlaceholder.style.display = 'block';
                } else {
                    floatingVideo.style.display = 'block';
                    videoPlaceholder.style.display = 'none';
                    updateVideo();
                }
            });
            
            setTimeout(updateVideo, 300);
            
            // === ПОИСК ПО САЙТУ ===
            const searchInput = document.getElementById('searchInput');
            const searchBtn = document.getElementById('searchBtn');
            const searchResults = document.getElementById('searchResults');
            
            function performSearch() {
                const query = searchInput.value.trim().toLowerCase();
                
                if (query.length < 2) {
                    searchResults.classList.remove('active');
                    return;
                }
                
                // Собираем все заголовки и параграфы
                const elements = document.querySelectorAll('h2, h3, h4, p, li');
                const results = [];
                
                elements.forEach(el => {
                    const text = el.textContent.toLowerCase();
                    if (text.includes(query) && !el.closest('.search-results') && !el.closest('header')) {
                        const parentSection = el.closest('section') || el.closest('div');
                        const title = el.closest('section')?.querySelector('h2')?.textContent || 'Раздел';
                        const preview = el.textContent.substring(0, 150) + '...';
                        
                        results.push({
                            element: el,
                            title: title,
                            preview: preview,
                            text: el.textContent
                        });
                    }
                });
                
                // Удаляем дубликаты
                const uniqueResults = results.filter((result, index, self) => 
                    index === self.findIndex(r => r.element === result.element)
                );
                
                // Показываем результаты
                displayResults(uniqueResults.slice(0, 10)); // Максимум 10 результатов
            }
            
            function displayResults(results) {
                if (results.length === 0) {
                    searchResults.innerHTML = '<div class="no-results">Ничего не найдено</div>';
                    searchResults.classList.add('active');
                    return;
                }
                
                let html = '';
                results.forEach((result, index) => {
                    html += `
                        <div class="search-result-item" data-index="${index}">
                            <div class="search-result-title">${result.title}</div>
                            <div class="search-result-text">${result.preview}</div>
                        </div>
                    `;
                });
                
                searchResults.innerHTML = html;
                searchResults.classList.add('active');
                
                // Добавляем обработчики кликов
                searchResults.querySelectorAll('.search-result-item').forEach((item, index) => {
                    item.addEventListener('click', () => {
                        results[index].element.scrollIntoView({ behavior: 'smooth', block: 'center' });
                        searchResults.classList.remove('active');
                        searchInput.value = '';
                        
                        // Подсветка найденного текста
                        highlightText(results[index].element, searchInput.value.trim());
                    });
                });
            }
            
            function highlightText(element, query) {
                if (!query) return;
                
                const text = element.textContent;
                const regex = new RegExp(`(${query})`, 'gi');
                element.innerHTML = text.replace(regex, '<span class="highlight">$1</span>');
                
                // Убираем подсветку через 3 секунды
                setTimeout(() => {
                    element.textContent = text;
                }, 3000);
            }
            
            // Обработчики событий для поиска
            searchBtn.addEventListener('click', performSearch);
            
            searchInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    performSearch();
                }
            });
            
            searchInput.addEventListener('input', () => {
                if (searchInput.value.trim().length >= 2) {
                    performSearch();
                } else {
                    searchResults.classList.remove('active');
                }
            });
            
            // Закрытие поиска при клике вне
            document.addEventListener('click', (e) => {
                if (!e.target.closest('.search-container')) {
                    searchResults.classList.remove('active');
                }
            });
        });
    </script>

</body>
</html>
