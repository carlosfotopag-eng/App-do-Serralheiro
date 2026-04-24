
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
  <title>App do Serralheiro | Medidas Profissionais 3D</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
      background: radial-gradient(circle at 20% 30%, #1a0a2e, #0a0a1a);
      min-height: 100vh;
      padding: 8px 16px 20px;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
      perspective: 1200px;
    }

    body::before {
      content: "";
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: 
        repeating-linear-gradient(90deg, rgba(255,215,0,0.08) 0px, rgba(255,215,0,0.08) 2px, transparent 2px, transparent 10px),
        repeating-linear-gradient(180deg, rgba(100,100,150,0.05) 0px, rgba(100,100,150,0.05) 1px, transparent 1px, transparent 8px),
        radial-gradient(ellipse at 50% 50%, rgba(30,20,50,0.8), rgba(10,5,20,0.95));
      pointer-events: none;
      z-index: 0;
    }

    body::after {
      content: "";
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at 20% 30%, rgba(255,215,0,0.08), transparent 70%);
      pointer-events: none;
      z-index: 0;
    }

    .app-container {
      max-width: 650px;
      width: 100%;
      margin: 0 auto;
      position: relative;
      z-index: 2;
      transform-style: preserve-3d;
      animation: fadeInUp 0.6s ease-out;
    }

    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(30px) rotateX(10deg); }
      to { opacity: 1; transform: translateY(0) rotateX(0); }
    }

    /* Título principal - mais compacto */
    .main-header {
      text-align: center;
      margin-bottom: 12px;
    }

    h2 {
      text-align: center;
      font-weight: 800;
      font-size: 1.6rem;
      margin-bottom: 4px;
      background: linear-gradient(135deg, #FFD700, #FFA500, #FF6B6B);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow: 0 5px 15px rgba(0,0,0,0.5);
      letter-spacing: 1px;
      transform: perspective(500px) rotateX(2deg);
    }

    .subtitle {
      text-align: center;
      color: rgba(255,215,0,0.8);
      font-size: 0.65rem;
      margin-bottom: 15px;
      letter-spacing: 2px;
      text-transform: uppercase;
      font-weight: 600;
    }

    .menu {
      display: flex;
      gap: 12px;
      justify-content: center;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    .menu button {
      flex: 1;
      min-width: 100px;
      background: linear-gradient(145deg, #3a3a50, #1a1a30);
      border: none;
      padding: 12px 10px;
      border-radius: 50px;
      color: #FFD700;
      font-weight: bold;
      font-size: 0.85rem;
      cursor: pointer;
      box-shadow: 0 8px 0 #0a0a15, 0 8px 20px rgba(0,0,0,0.5), inset 0 1px 0 rgba(255,255,255,0.1);
      transition: all 0.08s linear;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      transform: translateZ(10px);
    }
    .menu button:active { transform: translateY(4px) translateZ(5px); box-shadow: 0 4px 0 #0a0a15; }

    .card {
      background: rgba(12, 18, 28, 0.85);
      backdrop-filter: blur(12px);
      border-radius: 30px;
      padding: 18px 20px 22px;
      margin-bottom: 16px;
      box-shadow: 0 25px 40px -15px rgba(0,0,0,0.6), inset 0 1px 0 rgba(255,255,255,0.08), 0 0 0 1px rgba(255,215,0,0.2);
      transform: translateZ(5px);
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .card:hover { transform: translateZ(10px) translateY(-3px); box-shadow: 0 30px 50px -15px rgba(0,0,0,0.7); }

    .card h3 {
      font-size: 1.3rem;
      font-weight: 700;
      margin-bottom: 15px;
      color: #FFD700;
      border-left: 5px solid #FFD700;
      padding-left: 15px;
      text-shadow: 0 2px 5px rgba(0,0,0,0.5);
    }

    .glass-input {
      width: 100%;
      padding: 12px 16px;
      margin: 8px 0;
      background: rgba(5, 10, 20, 0.9);
      border: 1px solid rgba(255,215,0,0.4);
      border-radius: 50px;
      font-size: 0.95rem;
      color: #FFE8C0;
      font-weight: 500;
      outline: none;
      transition: all 0.2s;
      box-shadow: inset 0 3px 8px rgba(0,0,0,0.4), 0 1px 0 rgba(255,255,255,0.05);
    }
    .glass-input:focus { border-color: #FFD700; box-shadow: 0 0 0 3px rgba(255,215,0,0.2), inset 0 3px 8px rgba(0,0,0,0.4); transform: scale(1.01); }

    .input-label {
      font-size: 0.65rem;
      color: #FFD700;
      margin-left: 16px;
      margin-top: 3px;
      display: flex;
      align-items: center;
      gap: 6px;
      font-weight: 600;
    }

    .flex-btns {
      display: flex;
      gap: 12px;
      margin: 15px 0 8px;
      flex-wrap: wrap;
      justify-content: center;
    }

    .btn-elevated {
      background: linear-gradient(145deg, #3a3a52, #1a1a32);
      border: none;
      padding: 10px 20px;
      border-radius: 50px;
      font-weight: 700;
      font-size: 0.8rem;
      color: #FFD700;
      cursor: pointer;
      box-shadow: 0 6px 0 #0a0a18, 0 5px 15px rgba(0,0,0,0.5), inset 0 1px 0 rgba(255,255,255,0.1);
      transition: all 0.08s linear;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      min-width: 130px;
    }
    .btn-elevated:active { transform: translateY(3px); box-shadow: 0 3px 0 #0a0a18; }
    .btn-success { background: linear-gradient(145deg, #8B6914, #6B4E0A); box-shadow: 0 6px 0 #4a3508; }
    .btn-outline-light { background: linear-gradient(145deg, #2a2a42, #151530); border: 1px solid rgba(255,215,0,0.3); }

    .clear-history-btn {
      background: linear-gradient(145deg, #8B1A1A, #6B0E0E);
      box-shadow: 0 6px 0 #4a0808;
      border: none;
      padding: 8px 16px;
      border-radius: 50px;
      font-weight: 700;
      font-size: 0.7rem;
      color: #FFD700;
      cursor: pointer;
      margin-top: 8px;
      width: 100%;
    }
    .clear-history-btn:active { transform: translateY(3px); box-shadow: 0 3px 0 #4a0808; }

    /* DISPLAY DIGITAL ESTILO CALCULADORA */
    .digital-display {
      background: #0a0f1a;
      border-radius: 18px;
      padding: 14px 16px;
      margin-top: 12px;
      border: 1px solid rgba(0, 255, 255, 0.3);
      box-shadow: inset 0 0 20px rgba(0, 255, 255, 0.05), 0 0 10px rgba(0, 255, 255, 0.1), inset 0 2px 5px rgba(0,0,0,0.5);
      font-family: 'Courier New', 'JetBrains Mono', monospace;
      position: relative;
      overflow: hidden;
    }

    .digital-display::before {
      content: "";
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(0, 255, 255, 0.1), transparent);
      animation: scan 3s infinite;
    }

    @keyframes scan {
      0% { left: -100%; }
      100% { left: 100%; }
    }

    .digital-line {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      padding: 8px 0;
      border-bottom: 1px dashed rgba(0, 255, 255, 0.2);
      font-size: 0.85rem;
    }
    .digital-line:last-child { border-bottom: none; }

    .digital-label {
      color: #00ffff;
      font-weight: 600;
      letter-spacing: 1px;
      text-shadow: 0 0 5px rgba(0, 255, 255, 0.5);
    }

    .digital-value {
      color: #ffd700;
      font-weight: 800;
      font-size: 0.9rem;
      font-family: 'Courier New', monospace;
      background: rgba(0, 0, 0, 0.5);
      padding: 3px 10px;
      border-radius: 30px;
      letter-spacing: 1px;
    }

    .digital-value-large {
      font-size: 1rem;
      background: linear-gradient(135deg, #1a2a3a, #0a1a2a);
      padding: 5px 12px;
      border-radius: 40px;
      border: 1px solid #00ffff33;
    }

    .digital-title {
      text-align: center;
      color: #00ffff;
      font-size: 0.65rem;
      letter-spacing: 3px;
      margin-bottom: 10px;
      text-transform: uppercase;
      font-weight: 600;
    }

    .graph-container {
      margin-top: 12px;
      padding: 10px;
      background: rgba(0,0,0,0.45);
      border-radius: 16px;
      transform: translateZ(3px);
    }

    .graph-bar {
      display: flex;
      align-items: center;
      gap: 8px;
      margin: 6px 0;
    }

    .graph-label {
      width: 70px;
      font-size: 10px;
      color: #FFD700;
      font-weight: bold;
    }

    .graph-fill {
      height: 25px;
      background: linear-gradient(90deg, #ff6b6b, #ffa502, #ffd700);
      border-radius: 12px;
      transition: width 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      display: flex;
      align-items: center;
      justify-content: flex-end;
      padding-right: 8px;
      color: white;
      font-size: 10px;
      font-weight: bold;
      box-shadow: inset 0 1px 2px rgba(255,255,255,0.3), 0 2px 5px rgba(0,0,0,0.2);
    }

    .history {
      max-height: 130px;
      overflow: auto;
      margin-top: 8px;
      font-size: 10px;
      background: rgba(0,0,0,0.6);
      border-radius: 16px;
      padding: 8px;
      font-family: monospace;
    }
    .history div { padding: 5px; border-bottom: 1px solid rgba(0, 255, 255, 0.2); color: #0ff; }

    .hidden { display: none; }

    #level {
      font-size: 44px;
      text-align: center;
      margin-top: 10px;
      font-weight: bold;
      background: linear-gradient(135deg, #FFD700, #FF6B6B, #FFA500);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }

    .level-meter {
      width: 100%;
      height: 40px;
      background: rgba(0,0,0,0.5);
      border-radius: 30px;
      margin: 10px 0;
      overflow: hidden;
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.5);
    }
    .level-fill {
      height: 100%;
      width: 50%;
      background: linear-gradient(90deg, #2ecc71, #f1c40f, #e74c3c);
      border-radius: 30px;
      transition: width 0.08s linear;
    }
    .level-markers { display: flex; justify-content: space-between; padding: 0 10px; color: rgba(255,215,0,0.7); font-size: 9px; margin-top: 3px; }

    .card::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(255,215,0,0.5), transparent);
      border-radius: 30px;
    }

    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: rgba(0,0,0,0.3); border-radius: 10px; }
    ::-webkit-scrollbar-thumb { background: linear-gradient(180deg, #FFD700, #FFA500); border-radius: 10px; }
  </style>
</head>
<body>
<div class="app-container">
  <!-- CABEÇALHO COMPACTO - SEM LOGO TRANSPARENTE -->
  <div class="main-header">
    <h2>🔨 APP DO SERRALHEIRO</h2>
    <div class="subtitle">⚡ Medições Profissionais 3D | Conversões | Nível Digital ⚡</div>
  </div>

  <div class="menu">
    <button onclick="showSection('pontos')">📏 Medição 3D</button>
    <button onclick="showSection('conversor')">🔄 Conversor</button>
    <button onclick="showSection('nivel')">🎚️ Nível 3D</button>
  </div>

  <!-- SEÇÃO MEDIÇÃO -->
  <div id="pontos" class="card">
    <h3>📐 Medição de Peças (A, B, C)</h3>
    <div class="input-label">🔹 PONTO A — Início da peça (mm)</div>
    <input type="number" id="pontoA" class="glass-input" placeholder="Ex: 150 mm" step="any">
    <div class="input-label">📏 PONTO B — Distância horizontal / base (mm)</div>
    <input type="number" id="pontoB" class="glass-input" placeholder="Ex: 300 mm" step="any">
    <div class="input-label">📐 PONTO C — Altura / desnível B→C (mm)</div>
    <input type="number" id="alturaBC" class="glass-input" placeholder="Ex: 120 mm" step="any">

    <div class="flex-btns">
      <button class="btn-elevated btn-success" onclick="saveMeasurement()">💾 Salvar Medição</button>
      <button class="btn-elevated btn-outline-light" onclick="toggleHistory()">📜 Histórico</button>
    </div>

    <div id="resultadoPontos" class="digital-display">
      <div class="digital-title">═══ DISPLAY DIGITAL ═══</div>
      <div style="text-align:center; color:#0ff8;">⏻ Aguardando dados...</div>
    </div>
    <div id="graficoVisual" class="graph-container"></div>
    <div id="historico" class="history hidden"></div>
    <button id="clearHistoryBtn" class="clear-history-btn hidden" onclick="clearHistory()">🗑️ LIMPAR HISTÓRICO</button>
  </div>

  <!-- SEÇÃO CONVERSOR -->
  <div id="conversor" class="card hidden">
    <h3>🔄 Conversor de Unidades</h3>
    <div class="input-label">📏 Milímetros (mm) → Polegadas</div>
    <input type="number" id="mm" class="glass-input" placeholder="Digite mm" step="any">
    <button class="btn-elevated" onclick="mmToInch()">Converter para Polegadas</button>
    <div id="resultadoMM" class="digital-display">
      <div class="digital-title">═══ CONVERSÃO MM → IN ═══</div>
      <div style="text-align:center; color:#0ff8;">—</div>
    </div>

    <div class="input-label" style="margin-top:10px;">📏 Polegadas (in) → Milímetros</div>
    <input type="number" id="polegadas" class="glass-input" placeholder="Digite polegadas" step="any">
    <button class="btn-elevated" onclick="inchToMm()">Converter para Milímetros</button>
    <div id="resultadoPol" class="digital-display">
      <div class="digital-title">═══ CONVERSÃO IN → MM ═══</div>
      <div style="text-align:center; color:#0ff8;">—</div>
    </div>
  </div>

  <!-- SEÇÃO NÍVEL -->
  <div id="nivel" class="card hidden">
    <h3>🎚️ Nível Digital 3D</h3>
    <div id="level">0.0°</div>
    <div class="level-meter"><div class="level-fill" id="levelFill"></div></div>
    <div class="level-markers"><span>-90°</span><span>-45°</span><span>0°</span><span>+45°</span><span>+90°</span></div>
    <div class="digital-display" style="text-align: center; font-size: 11px; margin-top: 8px;">
      <div class="digital-title">═══ SENSOR 3D ═══</div>
      📱 Incline o dispositivo para testar o nível em tempo real
    </div>
  </div>
</div>

<script>
// Elementos DOM
const pontosDiv = document.getElementById('pontos');
const conversorDiv = document.getElementById('conversor');
const nivelDiv = document.getElementById('nivel');
const pontoA = document.getElementById('pontoA');
const pontoB = document.getElementById('pontoB');
const alturaBC = document.getElementById('alturaBC');
const resultadoPontos = document.getElementById('resultadoPontos');
const historicoDiv = document.getElementById('historico');
const graficoVisual = document.getElementById('graficoVisual');
const clearHistoryBtn = document.getElementById('clearHistoryBtn');

function drawGraph(A, B, altura, angulo, hipotenusa, comprimentoTotal) {
  const maxVal = Math.max(B, altura, hipotenusa, comprimentoTotal, A || 0);
  if (maxVal === 0) return;
  
  graficoVisual.innerHTML = `
    <div style="margin-bottom: 8px; color: #FFD700; font-size: 11px; text-align:center;">📊 Gráfico Comparativo 3D (mm)</div>
    ${A ? `<div class="graph-bar"><div class="graph-label">📌 Ponto A</div><div class="graph-fill" style="width: ${(A/maxVal)*100}%">${A.toFixed(1)} mm</div></div>` : ''}
    <div class="graph-bar"><div class="graph-label">📏 Base B</div><div class="graph-fill" style="width: ${(B/maxVal)*100}%">${B.toFixed(1)} mm</div></div>
    <div class="graph-bar"><div class="graph-label">📐 Altura C</div><div class="graph-fill" style="width: ${(altura/maxVal)*100}%">${altura.toFixed(1)} mm</div></div>
    <div class="graph-bar"><div class="graph-label">🔺 Hipotenusa</div><div class="graph-fill" style="width: ${(hipotenusa/maxVal)*100}%">${hipotenusa.toFixed(1)} mm</div></div>
    <div class="graph-bar"><div class="graph-label">🧱 Total</div><div class="graph-fill" style="width: ${(comprimentoTotal/maxVal)*100}%">${comprimentoTotal.toFixed(1)} mm</div></div>
  `;
}

function computeAndUpdate() {
  let A = parseFloat(pontoA.value);
  let B = parseFloat(pontoB.value);
  let altura = parseFloat(alturaBC.value);
  
  const isValidNum = (v) => !isNaN(v) && v !== null && v !== undefined;
  let validA = isValidNum(A);
  let validB = isValidNum(B);
  let validAlt = isValidNum(altura);
  
  if (!validB || B === 0) {
    resultadoPontos.innerHTML = `<div class="digital-title">═══ DISPLAY DIGITAL ═══</div><div style="text-align:center; color:#ff6666;">⚠️ Ponto B (base) é obrigatório</div>`;
    graficoVisual.innerHTML = '';
    return;
  }
  
  if (!validAlt) {
    resultadoPontos.innerHTML = `<div class="digital-title">═══ DISPLAY DIGITAL ═══</div><div style="text-align:center; color:#ffaa66;">📏 Insira a altura B→C para calcular</div>`;
    graficoVisual.innerHTML = '';
    return;
  }
  
  let anguloRad = Math.atan(altura / B);
  let anguloDeg = anguloRad * (180 / Math.PI);
  let hipotenusa = Math.sqrt(B * B + altura * altura);
  let comprimentoTotal = (validA ? A : 0) + hipotenusa;
  
  drawGraph(validA ? A : 0, B, altura, anguloDeg, hipotenusa, comprimentoTotal);
  
  resultadoPontos.innerHTML = `
    <div class="digital-title">═══ DISPLAY DIGITAL ═══</div>
    <div class="digital-line"><span class="digital-label">📏 PONTO A</span><span class="digital-value">${validA ? A.toFixed(2) + ' mm' : '— (opcional)'}</span></div>
    <div class="digital-line"><span class="digital-label">📐 PONTO B (base)</span><span class="digital-value">${B.toFixed(2)} mm</span></div>
    <div class="digital-line"><span class="digital-label">📏 PONTO C (altura)</span><span class="digital-value">${altura.toFixed(2)} mm</span></div>
    <div class="digital-line" style="background: rgba(0,255,255,0.05); border-radius: 8px;"><span class="digital-label">🔺 ÂNGULO</span><span class="digital-value digital-value-large">${anguloDeg.toFixed(2)}°</span></div>
    <div class="digital-line"><span class="digital-label">📐 HIPOTENUSA</span><span class="digital-value">${hipotenusa.toFixed(2)} mm</span></div>
    <div class="digital-line" style="background: rgba(255,215,0,0.1); border-radius: 8px;"><span class="digital-label">🧱 TOTAL (A+BC)</span><span class="digital-value digital-value-large">${comprimentoTotal.toFixed(2)} mm</span></div>
    <div class="digital-line"><span class="digital-label">➕ AUMENTO LINEAR</span><span class="digital-value">+${hipotenusa.toFixed(2)} mm</span></div>
  `;
}

[pontoA, pontoB, alturaBC].forEach(input => {
  if (input) input.addEventListener('input', () => computeAndUpdate());
});

function saveMeasurement() {
  let A = parseFloat(pontoA.value);
  let B = parseFloat(pontoB.value);
  let altura = parseFloat(alturaBC.value);
  
  if (isNaN(B) || isNaN(altura) || B === 0) {
    alert("⚠️ Preencha B e altura corretamente");
    return;
  }
  
  let ang = Math.atan(altura / B) * (180 / Math.PI);
  let hip = Math.sqrt(B*B + altura*altura);
  let comp = (isNaN(A) ? 0 : A) + hip;
  let timestamp = new Date().toLocaleString('pt-BR');
  let entry = `[${timestamp}] A:${isNaN(A)?'—':A.toFixed(1)}mm | B:${B.toFixed(1)}mm | C:${altura.toFixed(1)}mm | ∠${ang.toFixed(1)}° | Total:${comp.toFixed(1)}mm`;
  
  let stored = JSON.parse(localStorage.getItem('serralheiro_history') || '[]');
  stored.unshift(entry);
  if (stored.length > 15) stored.pop();
  localStorage.setItem('serralheiro_history', JSON.stringify(stored));
  alert("✅ Medição salva!");
  renderHistoryList();
}

function renderHistoryList() {
  let stored = JSON.parse(localStorage.getItem('serralheiro_history') || '[]');
  if (!historicoDiv) return;
  if (stored.length === 0) {
    historicoDiv.innerHTML = '<div style="text-align:center;">📭 Nenhuma medição salva</div>';
    clearHistoryBtn.classList.add('hidden');
  } else {
    historicoDiv.innerHTML = stored.map(item => `<div>🔨 ${item}</div>`).join('');
    clearHistoryBtn.classList.remove('hidden');
  }
}

function toggleHistory() {
  if (historicoDiv.classList.contains('hidden')) {
    renderHistoryList();
    historicoDiv.classList.remove('hidden');
  } else {
    historicoDiv.classList.add('hidden');
  }
}

function clearHistory() {
  if (confirm("⚠️ Tem certeza que deseja limpar TODO o histórico?")) {
    localStorage.removeItem('serralheiro_history');
    renderHistoryList();
    if (!historicoDiv.classList.contains('hidden')) {
      historicoDiv.innerHTML = '<div style="text-align:center;">📭 Histórico vazio</div>';
    }
    alert("🗑️ Histórico limpo com sucesso!");
  }
}

function mmToInch() {
  let mmVal = parseFloat(document.getElementById('mm').value);
  if (isNaN(mmVal)) {
    document.getElementById('resultadoMM').innerHTML = `<div class="digital-title">═══ CONVERSÃO MM → IN ═══</div><div style="text-align:center; color:#ff6666;">⚠️ Digite um valor em mm</div>`;
    return;
  }
  let inches = mmVal / 25.4;
  document.getElementById('resultadoMM').innerHTML = `
    <div class="digital-title">═══ CONVERSÃO MM → IN ═══</div>
    <div class="digital-line"><span class="digital-label">📏 MILÍMETROS</span><span class="digital-value">${mmVal.toFixed(3)} mm</span></div>
    <div class="digital-line"><span class="digital-label">📐 POLEGADAS</span><span class="digital-value digital-value-large">${inches.toFixed(4)} in</span></div>
  `;
}

function inchToMm() {
  let inchVal = parseFloat(document.getElementById('polegadas').value);
  if (isNaN(inchVal)) {
    document.getElementById('resultadoPol').innerHTML = `<div class="digital-title">═══ CONVERSÃO IN → MM ═══</div><div style="text-align:center; color:#ff6666;">⚠️ Digite um valor em polegadas</div>`;
    return;
  }
  let mmResult = inchVal * 25.4;
  document.getElementById('resultadoPol').innerHTML = `
    <div class="digital-title">═══ CONVERSÃO IN → MM ═══</div>
    <div class="digital-line"><span class="digital-label">📏 POLEGADAS</span><span class="digital-value">${inchVal.toFixed(4)} in</span></div>
    <div class="digital-line"><span class="digital-label">📐 MILÍMETROS</span><span class="digital-value digital-value-large">${mmResult.toFixed(2)} mm</span></div>
  `;
}

let levelElement = document.getElementById('level');
let levelFill = document.getElementById('levelFill');

function handleOrientation(event) {
  if (!levelElement) return;
  let beta = event.beta;
  if (beta !== null && beta !== undefined) {
    let angle = beta.toFixed(1);
    levelElement.innerHTML = `${angle}°`;
    let percent = ((beta + 90) / 180) * 100;
    percent = Math.min(100, Math.max(0, percent));
    if (levelFill) levelFill.style.width = `${percent}%`;
  }
}

if (window.DeviceOrientationEvent) {
  if (typeof DeviceOrientationEvent.requestPermission === 'function') {
    const nivelCard = document.getElementById('nivel');
    if (nivelCard && !nivelCard.querySelector('.sensor-btn')) {
      const requestBtn = document.createElement('button');
      requestBtn.innerText = '🎯 Ativar Sensor 3D';
      requestBtn.className = 'btn-elevated';
      requestBtn.style.marginTop = '12px';
      requestBtn.style.width = '100%';
      requestBtn.onclick = () => {
        DeviceOrientationEvent.requestPermission()
          .then(permissionState => {
            if (permissionState === 'granted') {
              window.addEventListener('deviceorientation', handleOrientation);
              requestBtn.remove();
            } else alert('Permissão necessária');
          }).catch(console.error);
      };
      nivelCard.appendChild(requestBtn);
    } else {
      window.addEventListener('deviceorientation', handleOrientation);
    }
  } else {
    window.addEventListener('deviceorientation', handleOrientation);
  }
}

function showSection(sectionId) {
  pontosDiv.classList.add('hidden');
  conversorDiv.classList.add('hidden');
  nivelDiv.classList.add('hidden');
  const target = document.getElementById(sectionId);
  if (target) target.classList.remove('hidden');
  if (sectionId === 'pontos') computeAndUpdate();
}

window.addEventListener('DOMContentLoaded', () => {
  computeAndUpdate();
  renderHistoryList();
});

window.showSection = showSection;
window.saveMeasurement = saveMeasurement;
window.toggleHistory = toggleHistory;
window.clearHistory = clearHistory;
window.mmToInch = mmToInch;
window.inchToMm = inchToMm;
</script>
</body>
</html>
