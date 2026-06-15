<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Человекомашинные интерфейсы | Экзамен</title>
<style>
  /* RESET & БАЗА */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    background: radial-gradient(circle at 20% 30%, #0a0f1e, #03050b);
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, 'SF Pro Text', sans-serif;
    color: #eef5ff;
    line-height: 1.5;
    padding: 2rem 1rem;
  }

  /* АНИМИРОВАННЫЙ НЕОНОВЫЙ ГЛОБАЛЬНЫЙ КОНТЕЙНЕР */
  .glow-bg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    z-index: 0;
    background: radial-gradient(ellipse at 40% 50%, rgba(0, 255, 255, 0.08), transparent 70%);
    animation: pulseGlow 8s infinite alternate;
  }

  @keyframes pulseGlow {
    0% { opacity: 0.3; }
    100% { opacity: 0.8; }
  }

  .container {
    max-width: 1400px;
    margin: 0 auto;
    position: relative;
    z-index: 2;
  }

  /* ЗАГОЛОВОК — ЛОМАЮЩИЙ ГЛАЗА */
  .hero {
    text-align: center;
    margin-bottom: 4rem;
    position: relative;
  }

  .hero h1 {
    font-size: 4.8rem;
    font-weight: 900;
    background: linear-gradient(135deg, #f0f, #0ff, #f90, #f0f);
    background-size: 300% 300%;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    animation: textShift 6s ease infinite;
    text-shadow: 0 0 15px rgba(0,255,255,0.5);
    letter-spacing: -0.02em;
  }

  @keyframes textShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  .hero .sub {
    font-size: 1.3rem;
    margin-top: 1rem;
    opacity: 0.9;
    backdrop-filter: blur(4px);
    background: rgba(255,255,255,0.05);
    display: inline-block;
    padding: 0.5rem 2rem;
    border-radius: 80px;
    border: 1px solid rgba(0,255,255,0.4);
    box-shadow: 0 0 20px rgba(0,255,255,0.2);
  }

  /* СЕТКА КАРТОЧЕК — ОЧЕНЬ СОЧНАЯ */
  .questions-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(360px, 1fr));
    gap: 2rem;
  }

  /* КАРТОЧКА ВОПРОСА */
  .question-card {
    background: rgba(12, 20, 35, 0.7);
    backdrop-filter: blur(12px);
    border-radius: 2rem;
    padding: 1.5rem;
    border: 1px solid rgba(0, 255, 255, 0.3);
    transition: all 0.4s cubic-bezier(0.2, 0.9, 0.4, 1.1);
    box-shadow: 0 10px 25px -5px rgba(0,0,0,0.5), 0 0 0 0 rgba(0,255,255,0);
    position: relative;
    overflow: hidden;
  }

  .question-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0, 255, 255, 0.2), transparent);
    transition: left 0.7s;
    z-index: 0;
  }

  .question-card:hover::before {
    left: 100%;
  }

  .question-card:hover {
    transform: translateY(-8px) scale(1.01);
    border-color: #0ff;
    box-shadow: 0 20px 35px -12px rgba(0,255,255,0.3), 0 0 20px rgba(0,255,255,0.4);
    background: rgba(18, 28, 45, 0.85);
  }

  .card-header {
    display: flex;
    align-items: center;
    gap: 0.8rem;
    margin-bottom: 1.2rem;
    border-bottom: 2px dashed rgba(0,255,255,0.5);
    padding-bottom: 0.6rem;
  }

  .q-num {
    font-size: 2rem;
    font-weight: 800;
    background: linear-gradient(145deg, #0ff, #f0f);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    text-shadow: 0 0 5px cyan;
  }

  .q-tag {
    background: rgba(0, 255, 255, 0.2);
    padding: 0.2rem 0.7rem;
    border-radius: 50px;
    font-size: 0.7rem;
    font-weight: bold;
    letter-spacing: 1px;
    backdrop-filter: blur(4px);
    border: 0.5px solid cyan;
  }

  .question-text {
    font-size: 1rem;
    font-weight: 500;
    margin-bottom: 1.5rem;
    line-height: 1.4;
    color: #f0fcff;
    text-shadow: 0 0 2px rgba(0,0,0,0.5);
    display: -webkit-box;
    -webkit-line-clamp: 4;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  /* КНОПКА-ССЫЛКА (БЕШЕНЫЙ ДИЗАЙН) */
  .btn-link {
    display: inline-flex;
    align-items: center;
    gap: 0.6rem;
    background: linear-gradient(95deg, #0a0f2a, #101a30);
    padding: 0.7rem 1.3rem;
    border-radius: 40px;
    text-decoration: none;
    font-weight: 600;
    color: #0ff;
    border: 1px solid rgba(0,255,255,0.6);
    transition: 0.2s;
    backdrop-filter: blur(8px);
    font-size: 0.85rem;
    letter-spacing: 0.5px;
  }

  .btn-link:hover {
    background: #0ff;
    color: #000;
    box-shadow: 0 0 20px #0ff;
    border-color: #fff;
    gap: 0.9rem;
  }

  .btn-link::after {
    content: '➡️';
    transition: transform 0.2s;
  }

  .btn-link:hover::after {
    transform: translateX(5px);
  }

  /* ФУТЕР С ТРЭШ-АНИМАЦИЕЙ */
  .footer {
    margin-top: 4rem;
    text-align: center;
    padding: 2rem;
    border-top: 1px solid rgba(0,255,255,0.3);
    font-size: 0.85rem;
    background: rgba(0,0,0,0.3);
    border-radius: 80px;
    backdrop-filter: blur(8px);
  }

  /* АДАПТИВ */
  @media (max-width: 760px) {
    .hero h1 { font-size: 2.5rem; }
    .questions-grid { grid-template-columns: 1fr; }
    .question-card { padding: 1.2rem; }
  }

  /* СКРОЛЛБАР — ДЛЯ КРАСОТЫ */
  ::-webkit-scrollbar {
    width: 10px;
    background: #010101;
  }
  ::-webkit-scrollbar-thumb {
    background: linear-gradient(#0ff, #f0f);
    border-radius: 10px;
  }
</style>
</head>
<body>
<div class="glow-bg"></div>
<div class="container">
  <div class="hero">
    <h1>⚡ ЧЕЛОВЕКО-МАШИННЫЕ ⚡<br>ИНТЕРФЕЙСЫ</h1>
    <div class="sub">🔥 20 взрывных вопросов к экзамену 🔥</div>
    <div style="margin-top: 1.2rem; font-size: 0.9rem;">✨ кликай по карточкам — ссылки ведут на детальные страницы ✨</div>
  </div>

  <div class="questions-grid">
    <!-- 1 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">01</span><span class="q-tag">ARCH</span></div>
      <div class="question-text">Архитектурные парадигмы веб-фронтенда: MPA, SPA, SSR, SSG. Различия рендеринга, SEO, TTI.</div>
      <a href="#q1" class="btn-link">Погрузиться в парадигмы</a>
    </div>
    <!-- 2 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">02</span><span class="q-tag">DOM</span></div>
      <div class="question-text">Модель DOM и события: фазы захвата/всплытия, делегирование событий — задачи и суть.</div>
      <a href="#q2" class="btn-link">Исследовать DOM</a>
    </div>
    <!-- 3 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">03</span><span class="q-tag">HCI LAWS</span></div>
      <div class="question-text">Закон Фиттса и закон Хика. Применение в UI для меню и интерактивных элементов.</div>
      <a href="#q3" class="btn-link">Законы → оптимизация</a>
    </div>
    <!-- 4 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">04</span><span class="q-tag">GOMS/KLM</span></div>
      <div class="question-text">Модель GOMS и KLM: сравнение альтернативных дизайнов на примере конвертера температур.</div>
      <a href="#q4" class="btn-link">Анализ GOMS</a>
    </div>
    <!-- 5 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">05</span><span class="q-tag">COGNITIVE</span></div>
      <div class="question-text">Когнитивная нагрузка, закон Миллера 7±2, стратегии снижения: группировка, прогрессивное раскрытие.</div>
      <a href="#q5" class="btn-link">Разгрузить мозг</a>
    </div>
    <!-- 6 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">06</span><span class="q-tag">USABILITY</span></div>
      <div class="question-text">Критерии юзабилити: скорость, ошибки, обучение, удовлетворение. SUS, SEQ методы измерения.</div>
      <a href="#q6" class="btn-link">Измерить юзабилити</a>
    </div>
    <!-- 7 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">07</span><span class="q-tag">ORM</span></div>
      <div class="question-text">Object‑relational impedance mismatch. ORM: Hibernate, SQLAlchemy. Антипаттерны: N+1, божественная сущность.</div>
      <a href="#q7" class="btn-link">ORM глубина</a>
    </div>
    <!-- 8 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">08</span><span class="q-tag">SERIALIZATION</span></div>
      <div class="question-text">Сравнение Java Serialization / Python pickle vs XML/JSON. Недостатки бинарной и текстовой сериализации.</div>
      <a href="#q8" class="btn-link">Сериализация данных</a>
    </div>
    <!-- 9 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">09</span><span class="q-tag">AUTH</span></div>
      <div class="question-text">Идентификация, аутентификация, авторизация. Сессии (stateful) vs JWT (stateless): плюсы/минусы.</div>
      <a href="#q9" class="btn-link">Сессии и JWT</a>
    </div>
    <!-- 10 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">10</span><span class="q-tag">OAUTH2</span></div>
      <div class="question-text">OAuth 2.0: роли (владелец ресурса, клиент, сервер), Authorization Code Flow. Решаемая проблема безопасности.</div>
      <a href="#q10" class="btn-link">OAuth 2.0 поток</a>
    </div>
    <!-- 11 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">11</span><span class="q-tag">OPENAPI</span></div>
      <div class="question-text">Спецификация OpenAPI и экосистема Swagger: Editor, UI, Codegen — задачи и решения.</div>
      <a href="#q11" class="btn-link">Документация API</a>
    </div>
    <!-- 12 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">12</span><span class="q-tag">API PROTOCOLS</span></div>
      <div class="question-text">REST vs GraphQL vs gRPC: сильные стороны, слабости, сценарии (публичное API, микросервисы, выборки).</div>
      <a href="#q12" class="btn-link">Выбрать протокол</a>
    </div>
    <!-- 13 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">13</span><span class="q-tag">DESIGN SYS</span></div>
      <div class="question-text">Дизайн-системы (Material, HIG). WCAG: контрастность, скринридеры, клавиатура — примеры реализации.</div>
      <a href="#q13" class="btn-link">Доступность и дизайн</a>
    </div>
    <!-- 14 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">14</span><span class="q-tag">COMPOSITION</span></div>
      <div class="question-text">Законы композиции: целостность, доминанта, уравновешенность. Правило 60‑30‑10 для цвета.</div>
      <a href="#q14" class="btn-link">Визуал композиция</a>
    </div>
    <!-- 15 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">15</span><span class="q-tag">ISLANDS/RSC</span></div>
      <div class="question-text">Islands Architecture и React Server Components: решение проблем производительности SPA.</div>
      <a href="#q15" class="btn-link">Новый фронтенд</a>
    </div>
    <!-- 16 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">16</span><span class="q-tag">SECURITY</span></div>
      <div class="question-text">XSS, CSRF, SQL‑инъекции. Защита: экранирование, CSRF‑токены — механизмы фреймворков.</div>
      <a href="#q16" class="btn-link">Веб-безопасность</a>
    </div>
    <!-- 17 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">17</span><span class="q-tag">MICROFRONTEND</span></div>
      <div class="question-text">Микрофронтенды: iframe, Web Components, Module Federation. Проблемы и цели архитектуры.</div>
      <a href="#q17" class="btn-link">Микро-интеграция</a>
    </div>
    <!-- 18 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">18</span><span class="q-tag">BACKEND TOOLS</span></div>
      <div class="question-text">Middleware и pipeline обработки запроса. Внедрение зависимостей (DI) для тестируемости и гибкости.</div>
      <a href="#q18" class="btn-link">Middleware+DI</a>
    </div>
    <!-- 19 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">19</span><span class="q-tag">TYPOGRAPHY</span></div>
      <div class="question-text">Типы шрифтов (serif, sans‑serif, моно). Параметры: размер, длина строки, интерлиньяж, контраст.</div>
      <a href="#q19" class="btn-link">Типографика UI</a>
    </div>
    <!-- 20 -->
    <div class="question-card">
      <div class="card-header"><span class="q-num">20</span><span class="q-tag">PERCEPTION</span></div>
      <div class="question-text">F‑образный паттерн сканирования, эффект последовательной позиции (начала и конца списка). Навигация.</div>
      <a href="#q20" class="btn-link">Восприятие в HCI</a>
    </div>
  </div>

  <div class="footer">
    <span>🌀 ЧЕЛОВЕК → МАШИНА → ИНТЕРФЕЙСЫ 🌀<br>готовься с безумным вниманием — каждый вопрос перевернёт твой мозг. Нажми на ссылку — откроется страница с глубоким разбором.</span>
  </div>
</div>
</body>
</html>