<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Misión Conocimiento: Tema 5 - La Tierra, nuestro planeta</title>
  <link href="https://googleapis.com" rel="stylesheet">
  <style>
    :root {
      --bg-gradient: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
      --card-bg: #ffffff;
      --primary: #0284c7;
      --primary-hover: #0369a1;
      --success: #10b981;
      --warning: #f59e0b;
      --danger: #ef4444;
      --text-main: #1e293b;
      --text-muted: #64748b;
      --radius: 24px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Nunito', sans-serif;
      background: var(--bg-gradient);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 16px;
      color: var(--text-main);
    }

    .app-container {
      background: var(--card-bg);
      width: 100%;
      max-width: 740px;
      border-radius: var(--radius);
      box-shadow: 0 24px 60px rgba(0, 0, 0, 0.35);
      overflow: hidden;
      display: flex;
      flex-direction: column;
      animation: fadeIn 0.4s ease-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(15px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Barra de estado superior */
    .status-bar {
      background: #0f172a;
      color: #fff;
      padding: 14px 24px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
    }

    .game-badge {
      font-family: 'Fredoka', sans-serif;
      font-size: 1.1rem;
      font-weight: 600;
      color: #38bdf8;
      letter-spacing: 0.4px;
    }

    .stats {
      display: flex;
      gap: 14px;
      align-items: center;
      font-weight: 800;
      font-size: 1.05rem;
    }

    .stat-pill {
      background: rgba(255, 255, 255, 0.12);
      padding: 6px 14px;
      border-radius: 999px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .progress-container {
      width: 100%;
      height: 7px;
      background: #334155;
    }

    .progress-bar {
      height: 100%;
      background: linear-gradient(90deg, #38bdf8, #10b981);
      width: 0%;
      transition: width 0.4s ease;
    }

    /* Cuerpo principal */
    .main-content {
      padding: 30px 28px;
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    /* Pantalla de inicio */
    .hero-icon {
      font-size: 4.5rem;
      margin-bottom: 10px;
      animation: float 3s ease-in-out infinite;
    }

    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-8px); }
    }

    h1 {
      font-family: 'Fredoka', sans-serif;
      font-size: 2.1rem;
      color: #0f172a;
      margin-bottom: 6px;
    }

    .topic-tag {
      background: #e0f2fe;
      color: #0369a1;
      font-weight: 800;
      font-size: 0.9rem;
      padding: 5px 14px;
      border-radius: 999px;
      margin-bottom: 14px;
    }

    .subtitle {
      font-size: 1.08rem;
      color: var(--text-muted);
      margin-bottom: 24px;
      max-width: 560px;
      line-height: 1.5;
    }

    .mission-selector {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
      width: 100%;
    }

    @media (max-width: 600px) {
      .mission-selector {
        grid-template-columns: 1fr;
      }
    }

    .mission-card {
      border: 3px solid #e2e8f0;
      border-radius: 20px;
      padding: 20px;
      cursor: pointer;
      transition: all 0.25s ease;
      background: #f8fafc;
      text-align: left;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .mission-card:hover {
      border-color: var(--primary);
      background: #f0f9ff;
      transform: translateY(-4px);
      box-shadow: 0 12px 24px rgba(2, 132, 199, 0.15);
    }

    .mission-card .m-icon {
      font-size: 2.5rem;
    }

    .mission-card h3 {
      font-family: 'Fredoka', sans-serif;
      font-size: 1.25rem;
      color: #0f172a;
    }

    .mission-card p {
      font-size: 0.95rem;
      color: var(--text-muted);
      line-height: 1.4;
    }

    /* Escena de juego */
    .turn-tag {
      background: #e0f2fe;
      color: #0369a1;
      font-weight: 800;
      font-size: 0.85rem;
      padding: 5px 14px;
      border-radius: 999px;
      margin-bottom: 14px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .scene-visual {
      width: 112px;
      height: 112px;
      background: linear-gradient(135deg, #e0f2fe, #bae6fd);
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 3.8rem;
      margin-bottom: 18px;
      box-shadow: 0 10px 25px rgba(56, 189, 248, 0.28);
      border: 4px solid #fff;
    }

    .story-text {
      font-size: 1.18rem;
      line-height: 1.55;
      color: #1e293b;
      font-weight: 700;
      margin-bottom: 24px;
      max-width: 610px;
    }

    /* Botones de opciones */
    .options-grid {
      display: flex;
      flex-direction: column;
      gap: 12px;
      width: 100%;
    }

    .option-btn {
      background: #f8fafc;
      border: 2.5px solid #cbd5e1;
      border-radius: 16px;
      padding: 16px 20px;
      font-family: 'Nunito', sans-serif;
      font-size: 1.05rem;
      font-weight: 700;
      color: #1e293b;
      text-align: left;
      cursor: pointer;
      transition: all 0.2s ease;
      display: flex;
      align-items: center;
      gap: 14px;
    }

    .option-btn:hover:not(:disabled) {
      border-color: var(--primary);
      background: #f0f9ff;
      transform: translateX(4px);
    }

    .option-btn:active:not(:disabled) {
      transform: scale(0.99);
    }

    .option-letter {
      background: var(--primary);
      color: white;
      width: 34px;
      height: 34px;
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-weight: 800;
      flex-shrink: 0;
    }

    /* Caja de retroalimentación */
    .feedback-box {
      width: 100%;
      border-radius: 18px;
      padding: 20px;
      margin-top: 6px;
      text-align: left;
      animation: popIn 0.3s ease;
    }

    @keyframes popIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }

    .feedback-correct {
      background: #ecfdf5;
      border: 2.5px solid #10b981;
      color: #065f46;
    }

    .feedback-partial {
      background: #fffbeb;
      border: 2.5px solid #f59e0b;
      color: #92400e;
    }

    .feedback-wrong {
      background: #fef2f2;
      border: 2.5px solid #ef4444;
      color: #991b1b;
    }

    .feedback-header {
      font-family: 'Fredoka', sans-serif;
      font-size: 1.25rem;
      margin-bottom: 6px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .feedback-text {
      font-size: 1.05rem;
      line-height: 1.5;
      margin-bottom: 16px;
    }

    .next-btn {
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 14px;
      padding: 15px 28px;
      font-family: 'Fredoka', sans-serif;
      font-size: 1.15rem;
      cursor: pointer;
      width: 100%;
      transition: background 0.2s;
      box-shadow: 0 4px 14px rgba(2, 132, 199, 0.3);
    }

    .next-btn:hover {
      background: var(--primary-hover);
    }

    /* Pantalla final */
    .medal-display {
      font-size: 5.2rem;
      margin: 8px 0;
      animation: popIn 0.5s ease;
    }

    .final-score-box {
      background: #f1f5f9;
      border-radius: 18px;
      padding: 18px 28px;
      margin: 18px 0;
      display: flex;
      gap: 28px;
      justify-content: center;
      flex-wrap: wrap;
    }

    .score-item span {
      display: block;
      font-size: 0.88rem;
      color: var(--text-muted);
      font-weight: 800;
    }

    .score-item strong {
      font-family: 'Fredoka', sans-serif;
      font-size: 1.85rem;
      color: var(--primary);
    }

    .hidden {
      display: none !important;
    }
  </style>
</head>
<body>

<div class="app-container">
  <!-- Barra superior de estado -->
  <div class="status-bar">
    <div class="game-badge">🌍 Misión Conocimiento: Tema 5</div>
    <div class="stats">
      <div class="stat-pill" title="Puntos de Saber">⭐ <span id="score-val">0</span> pts</div>
      <div class="stat-pill" title="Energía / Vidas" id="lives-val">❤️❤️❤️</div>
    </div>
  </div>
  <div class="progress-container">
    <div class="progress-bar" id="progress-bar"></div>
  </div>

  <!-- PANTALLA DE INICIO -->
  <div class="main-content" id="start-screen">
    <div class="hero-icon">🌎🧭</div>
    <div class="topic-tag">TEMA 5: La Tierra, nuestro planeta</div>
    <h1>Misión Conocimiento</h1>
    <p class="subtitle">¡Bienvenido/a al equipo científico de 6º! Elige una aventura de investigación y resuelve los retos aplicando tus conocimientos sobre nuestro planeta.</p>
    
    <div class="mission-selector">
      <div class="mission-card" onclick="startGame(0)">
        <div class="m-icon">🌋</div>
        <h3>Misión 1: El Volcán Dormido</h3>
        <p>Explora el interior terrestre: capas de la geosfera, energía interna, terremotos, rocas y minerales.</p>
      </div>
      <div class="mission-card" onclick="startGame(1)">
        <div class="m-icon">🛰️</div>
        <h3>Misión 2: Guardianes del Planeta</h3>
        <p>Investiga desde el espacio: atmósfera, hidrosfera, biosfera, rotación, traslación y eclipses.</p>
      </div>
    </div>
  </div>

  <!-- PANTALLA DE JUEGO -->
  <div class="main-content hidden" id="game-screen">
