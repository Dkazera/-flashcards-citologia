# -flashcards-citologia
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Flashcards · Citologia ACAFE</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --blue: #4ab8e8;
    --blue-dark: #1a6080;
    --blue-light: #cbe8f5;
    --bg: #f4f6f8;
    --card-bg: #ffffff;
    --text: #1a1e24;
    --text-muted: #5a6270;
    --border: #dde2e8;
    --red: #c0392b;
    --dark: #3d4a56;
    --green: #27ae60;
    --cyan: #2eaed4;
    --radius: 12px;
    --shadow: 0 2px 16px rgba(0,0,0,0.08);
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 24px 16px 48px;
    color: var(--text);
  }

  /* Header */
  header {
    width: 100%;
    max-width: 680px;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .logo {
    font-size: 13px;
    font-weight: 600;
    color: var(--blue-dark);
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }
  .logo span { color: var(--blue); }
  .deck-info {
    font-size: 12px;
    color: var(--text-muted);
    font-family: 'DM Mono', monospace;
  }

  /* Progress */
  .progress-wrap {
    width: 100%;
    max-width: 680px;
    margin-bottom: 6px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .progress-label {
    font-size: 12px;
    color: var(--text-muted);
  }
  .progress-bar {
    width: 100%;
    max-width: 680px;
    height: 4px;
    background: var(--border);
    border-radius: 99px;
    margin-bottom: 20px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: var(--blue);
    border-radius: 99px;
    transition: width 0.4s ease;
  }

  /* Card container */
  .card-container {
    width: 100%;
    max-width: 680px;
    perspective: 1200px;
    margin-bottom: 16px;
  }
  .card {
    width: 100%;
    min-height: 260px;
    position: relative;
    transform-style: preserve-3d;
    transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    cursor: pointer;
    border-radius: var(--radius);
  }
  .card.flipped { transform: rotateY(180deg); }
  .card-face {
    position: absolute;
    width: 100%;
    min-height: 260px;
    backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
    border-radius: var(--radius);
    padding: 32px 28px 28px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: var(--card-bg);
    box-shadow: var(--shadow);
    border: 0.5px solid var(--border);
  }
  .card-back-face {
    transform: rotateY(180deg);
  }
  .card-tag {
    position: absolute;
    top: 14px;
    left: 16px;
    font-size: 11px;
    font-weight: 600;
    padding: 3px 10px;
    border-radius: 99px;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }
  .card-hint {
    position: absolute;
    bottom: 14px;
    right: 16px;
    font-size: 11px;
    color: var(--text-muted);
    opacity: 0.6;
  }
  .front-question {
    font-size: 20px;
    font-weight: 500;
    text-align: center;
    line-height: 1.5;
    color: var(--text);
    max-width: 540px;
  }
  .back-subtitle {
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--blue);
    margin-bottom: 14px;
  }
  .back-answer {
    font-size: 16px;
    text-align: center;
    line-height: 1.65;
    color: var(--text);
    max-width: 560px;
  }

  /* Show answer button */
  .show-btn {
    width: 100%;
    max-width: 680px;
    padding: 15px;
    background: var(--dark);
    color: #fff;
    border: none;
    border-radius: var(--radius);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    font-weight: 500;
    cursor: pointer;
    transition: background 0.15s, transform 0.1s;
    margin-bottom: 0;
  }
  .show-btn:hover { background: #4a5868; }
  .show-btn:active { transform: scale(0.99); }

  /* Rating buttons */
  .rating-section {
    width: 100%;
    max-width: 680px;
    display: none;
    flex-direction: column;
    gap: 0;
    border-radius: var(--radius);
    overflow: hidden;
    box-shadow: var(--shadow);
  }
  .rating-section.visible { display: flex; }
  .rating-buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }
  .rate-btn {
    padding: 14px 8px;
    border: none;
    cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    font-weight: 600;
    color: #fff;
    transition: filter 0.15s, transform 0.1s;
  }
  .rate-btn:hover { filter: brightness(1.12); }
  .rate-btn:active { transform: scale(0.98); }
  .rate-btn.r-red   { background: var(--red); }
  .rate-btn.r-dark  { background: var(--dark); }
  .rate-btn.r-green { background: var(--green); }
  .rate-btn.r-cyan  { background: var(--cyan); }
  .rating-subs {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }
  .rate-sub {
    padding: 4px 8px;
    text-align: center;
    font-size: 10px;
    font-family: 'DM Mono', monospace;
    color: rgba(255,255,255,0.8);
  }
  .rate-sub.r-red   { background: #a52d22; }
  .rate-sub.r-dark  { background: #303d48; }
  .rate-sub.r-green { background: #1e8449; }
  .rate-sub.r-cyan  { background: #2090b0; }

  /* Navigation */
  .nav-row {
    width: 100%;
    max-width: 680px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 20px;
  }
  .nav-btn {
    display: flex;
    align-items: center;
    gap: 6px;
    padding: 9px 16px;
    background: var(--card-bg);
    border: 0.5px solid var(--border);
    border-radius: 99px;
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    color: var(--text-muted);
    cursor: pointer;
    transition: background 0.15s, color 0.15s;
  }
  .nav-btn:hover { background: var(--blue-light); color: var(--blue-dark); border-color: var(--blue); }
  .shuffle-btn {
    padding: 9px 16px;
    background: var(--card-bg);
    border: 0.5px solid var(--border);
    border-radius: 99px;
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    color: var(--text-muted);
    cursor: pointer;
    transition: background 0.15s;
  }
  .shuffle-btn:hover { background: var(--blue-light); color: var(--blue-dark); border-color: var(--blue); }

  /* Stats row */
  .stats-row {
    width: 100%;
    max-width: 680px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
    margin-top: 20px;
  }
  .stat-card {
    background: var(--card-bg);
    border: 0.5px solid var(--border);
    border-radius: 10px;
    padding: 12px 10px;
    text-align: center;
  }
  .stat-label {
    font-size: 10px;
    color: var(--text-muted);
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    margin-bottom: 4px;
  }
  .stat-value {
    font-size: 22px;
    font-weight: 600;
    font-family: 'DM Mono', monospace;
    color: var(--text);
  }
  .stat-value.red   { color: var(--red); }
  .stat-value.dark  { color: var(--dark); }
  .stat-value.green { color: var(--green); }
  .stat-value.cyan  { color: var(--cyan); }

  /* Tag color classes */
  .tag-membrane { background: #fde9e0; color: #b54a1a; }
  .tag-org      { background: #e0f0fd; color: #1a5a8a; }
  .tag-energia  { background: #e4f5e8; color: #1a7a35; }
  .tag-nucleo   { background: #ede0fd; color: #5a1aa0; }
  .tag-divisao  { background: #fdf5e0; color: #8a6a00; }
  .tag-comp     { background: #e0fdf5; color: #006a50; }

  /* Complete screen */
  .complete-screen {
    display: none;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 40px 20px;
    background: var(--card-bg);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    width: 100%;
    max-width: 680px;
    gap: 12px;
  }
  .complete-screen.visible { display: flex; }
  .complete-emoji { font-size: 48px; margin-bottom: 8px; }
  .complete-title { font-size: 24px; font-weight: 600; }
  .complete-sub { color: var(--text-muted); font-size: 15px; }
  .restart-btn {
    margin-top: 16px;
    padding: 12px 28px;
    background: var(--blue);
    color: #fff;
    border: none;
    border-radius: 99px;
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
  }
  .restart-btn:hover { background: var(--cyan); }

  @media (max-width: 480px) {
    .front-question { font-size: 17px; }
    .back-answer { font-size: 14px; }
    .stats-row { grid-template-columns: repeat(2, 1fr); }
  }
</style>
</head>
<body>

<header>
  <div class="logo">Citologia <span>·</span> ACAFE Medicina</div>
  <div class="deck-info" id="deckinfo">1 / 40</div>
</header>

<div class="progress-wrap">
  <span class="progress-label" id="progresslabel">Progresso</span>
  <span class="progress-label" id="progresspct">0%</span>
</div>
<div class="progress-bar">
  <div class="progress-fill" id="progressfill" style="width:0%"></div>
</div>

<!-- Main card -->
<div class="card-container" id="cardcontainer">
  <div class="card" id="card" onclick="flipCard()">
    <div class="card-face card-front-face">
      <span class="card-tag" id="cardtag"></span>
      <p class="front-question" id="fronttext"></p>
      <span class="card-hint">clique para revelar</span>
    </div>
    <div class="card-face card-back-face">
      <span class="card-tag" id="backctag"></span>
      <p class="back-subtitle" id="backsubtitle"></p>
      <p class="back-answer" id="backtext"></p>
    </div>
  </div>
</div>

<!-- Show answer button -->
<button class="show-btn" id="showbtn" onclick="flipCard()">Mostrar resposta</button>

<!-- Rating section -->
<div class="rating-section" id="ratingsection">
  <div class="rating-buttons">
    <button class="rate-btn r-red"   onclick="rate(0)">Novamente</button>
    <button class="rate-btn r-dark"  onclick="rate(1)">Difícil</button>
    <button class="rate-btn r-green" onclick="rate(2)">Bom</button>
    <button class="rate-btn r-cyan"  onclick="rate(3)">Fácil</button>
  </div>
  <div class="rating-subs">
    <span class="rate-sub r-red">&lt;10min(s)</span>
    <span class="rate-sub r-dark">8dia(s)</span>
    <span class="rate-sub r-green">3,7mês(es)</span>
    <span class="rate-sub r-cyan">9,1mês(es)</span>
  </div>
</div>

<!-- Complete screen -->
<div class="complete-screen" id="completescreen">
  <div class="complete-emoji">🎉</div>
  <p class="complete-title">Baralho concluído!</p>
  <p class="complete-sub" id="completesub"></p>
  <button class="restart-btn" onclick="restart()">Estudar novamente</button>
</div>

<!-- Navigation -->
<div class="nav-row">
  <button class="nav-btn" onclick="prevCard()">← Anterior</button>
  <button class="shuffle-btn" onclick="shuffleCards()">↺ Embaralhar</button>
  <button class="nav-btn" onclick="nextCard()">Próxima →</button>
</div>

<!-- Stats -->
<div class="stats-row">
  <div class="stat-card">
    <div class="stat-label">Novamente</div>
    <div class="stat-value red" id="s0">0</div>
  </div>
  <div class="stat-card">
    <div class="stat-label">Difícil</div>
    <div class="stat-value dark" id="s1">0</div>
  </div>
  <div class="stat-card">
    <div class="stat-label">Bom</div>
    <div class="stat-value green" id="s2">0</div>
  </div>
  <div class="stat-card">
    <div class="stat-label">Fácil</div>
    <div class="stat-value cyan" id="s3">0</div>
  </div>
</div>

<script>
const all = [
  {tag:"Teoria Celular",tc:"tag-comp",front:"Quais são os 3 princípios da teoria celular moderna?",back:"Teoria Celular",ans:"(1) Todo ser vivo é formado por células; (2) A célula é a menor unidade viva; (3) Toda célula origina-se de outra preexistente (Omnis cellula e cellula)."},
  {tag:"Membrana",tc:"tag-membrane",front:"O que é o modelo do mosaico fluido e quem o propôs?",back:"Membrana Plasmática",ans:"Modelo proposto por Singer e Nicolson (1972): bicamada fosfolipídica anfipática em estado fluido, com proteínas integrais e periféricas que se movem lateralmente."},
  {tag:"Procariotos",tc:"tag-comp",front:"Qual é o tamanho dos ribossomos em procariotos vs. eucariotos?",back:"Ribossomos",ans:"Procariotos: 70S (50S + 30S). Eucariotos: 80S (60S + 40S). Mitocôndrias e cloroplastos têm ribossomos 70S (origem endossimbiótica)."},
  {tag:"Endossimbiose",tc:"tag-org",front:"Cite 4 evidências da teoria endossimbiótica de Lynn Margulis.",back:"Teoria Endossimbiótica",ans:"(1) DNA circular sem histonas; (2) Ribossomos 70S bacterianos; (3) Autoduplicação independente; (4) Membrana dupla; (5) Sensibilidade a antibióticos antibacterianos."},
  {tag:"Membrana",tc:"tag-membrane",front:"Qual a função do colesterol na membrana plasmática animal?",back:"Colesterol",ans:"Atua como amortecedor de fluidez: evita que a membrana fique fluida demais em altas temperaturas e quebradiça em baixas temperaturas. Exclusivo de células animais."},
  {tag:"Membrana",tc:"tag-membrane",front:"O que é o glicocálix e quais são suas funções?",back:"Glicocálix",ans:"Zona de carboidratos (glicoproteínas e glicolipídios) na face extracelular. Funções: reconhecimento celular (sistema ABO), proteção mecânica, retenção de nutrientes e adesão celular."},
  {tag:"Transporte",tc:"tag-membrane",front:"Qual a diferença entre difusão simples e difusão facilitada?",back:"Transporte Passivo",ans:"Difusão simples: passagem direta pela bicamada (O₂, CO₂, hormônios esteroides). Difusão facilitada: exige proteínas transportadoras (GLUT para glicose). Ambas a favor do gradiente, sem ATP."},
  {tag:"Transporte",tc:"tag-membrane",front:"Como funciona a bomba Na⁺/K⁺ ATPase?",back:"Transporte Ativo",ans:"Hidrolisa 1 ATP para bombear 3 Na⁺ para fora e 2 K⁺ para dentro. Mantém potencial negativo interno, regula volume osmótico e cria gradiente de Na⁺ para cotransportes."},
  {tag:"Transporte",tc:"tag-membrane",front:"O que ocorre com célula animal e vegetal em meio hipotônico?",back:"Osmose",ans:"Célula animal: sofre lise (plasmoptise) por falta de parede rígida. Célula vegetal: torna-se túrgida, mas não rompe devido à pressão de turgor da parede celular."},
  {tag:"Transporte",tc:"tag-membrane",front:"O que é a endocitose mediada por receptores? Dê um exemplo.",back:"Endocitose",ans:"Ingestão seletiva de moléculas via receptores específicos na membrana. Exemplo: captação de LDL mediada por receptores de clatrina."},
  {tag:"Citoesqueleto",tc:"tag-org",front:"Quais são os 3 tipos de filamentos do citoesqueleto e seus diâmetros?",back:"Citoesqueleto",ans:"Microtúbulos (~25 nm, tubulina); Filamentos intermediários (~10 nm, queratina/vimentina/laminas); Microfilamentos (~7 nm, actina)."},
  {tag:"Citoesqueleto",tc:"tag-org",front:"Qual proteína forma os microtúbulos? Cite 2 funções.",back:"Microtúbulos",ans:"Dímeros de alfa e beta-tubulina. Funções: fuso mitótico/meiótico, trilhos para cinesina (anterógrado) e dineína (retrógrado), eixos de cílios e flagelos."},
  {tag:"Citoesqueleto",tc:"tag-org",front:"Qual o papel dos microfilamentos de actina?",back:"Microfilamentos",ans:"Contração muscular (com miosina), motilidade ameboide (pseudópodes), anel contrátil na citocinese animal, ciclose vegetal e sustentação das microvilosidades."},
  {tag:"Organelas",tc:"tag-org",front:"Qual a diferença funcional entre RER e REL?",back:"Retículo Endoplasmático",ans:"RER: síntese de proteínas de exportação e glicosilação inicial (tem ribossomos). REL: síntese de lipídios e hormônios esteroides, desintoxicação (P450) e armazenamento de Ca²⁺."},
  {tag:"Golgi",tc:"tag-org",front:"O que é o complexo de Golgi e qual sua polaridade?",back:"Complexo de Golgi",ans:"Sáculos empilhados (dictiossomos). Face cis: recebe vesículas do RER. Face trans: brota vesículas de secreção e lisossomos. Processa, concentra e empacota proteínas."},
  {tag:"Lisossomos",tc:"tag-org",front:"Como os lisossomos mantêm seu pH ácido (~4,5)?",back:"Lisossomos",ans:"Por bombas de prótons (H⁺ ATPase) ativas na membrana lisossomal que acidificam o interior, ativando as ~40 hidrolases ácidas presentes."},
  {tag:"Lisossomos",tc:"tag-org",front:"Qual a diferença entre heterofagia e autofagia?",back:"Lisossomos",ans:"Heterofagia: digestão de material exógeno capturado por endocitose. Autofagia: digestão de organelas velhas/danificadas da própria célula (ex: mitocôndrias disfuncionais)."},
  {tag:"Patologia",tc:"tag-comp",front:"O que é a Doença de Tay-Sachs?",back:"Doenças Lisossômicas",ans:"Deficiência genética (autossômica recessiva) da Hexosaminidase A. Acúmulo do gangliosídeo GM2 nos neurônios → neurodegeneração progressiva, cegueira e óbito precoce."},
  {tag:"Peroxissomos",tc:"tag-org",front:"Qual a função dos peroxissomos e da catalase?",back:"Peroxissomos",ans:"Oxidam substratos orgânicos (beta-oxidação de ácidos graxos longos) gerando H₂O₂. A catalase neutraliza: 2H₂O₂ → 2H₂O + O₂. Abundantes em hepatócitos e rins."},
  {tag:"Glioxissomos",tc:"tag-org",front:"O que são glioxissomos e onde são encontrados?",back:"Glioxissomos",ans:"Peroxissomos modificados exclusivos de plantas (sementes em germinação). Contêm enzimas do ciclo do glioxilato, convertendo lipídios em carboidratos para o embrião."},
  {tag:"Centríolos",tc:"tag-org",front:"Qual o papel do centrossomo? Onde está ausente?",back:"Centríolos",ans:"Centro organizador de microtúbulos; coordena o fuso mitótico. Centríolos = 9 tripletos (9×3). Ausentes em angiospermas e gimnospermas (divisão acêntrica)."},
  {tag:"Respiração",tc:"tag-energia",front:"Quais são as 4 etapas da respiração aeróbia e onde ocorrem?",back:"Respiração Celular",ans:"(1) Glicólise – citosol; (2) Descarboxilação oxidativa – matriz; (3) Ciclo de Krebs – matriz; (4) Cadeia respiratória/fosforilação oxidativa – cristas mitocondriais."},
  {tag:"Glicólise",tc:"tag-energia",front:"Qual o balanço líquido da glicólise?",back:"Glicólise",ans:"1 glicose → 2 piruvatos. Balanço líquido: 2 ATP (fosforilação em nível de substrato) + 2 NADH. Ocorre no citosol, sem consumo de O₂."},
  {tag:"Respiração",tc:"tag-energia",front:"Qual o papel do O₂ na cadeia respiratória?",back:"Cadeia Respiratória",ans:"O O₂ é o aceptor final de elétrons. No complexo IV, recebe elétrons exaustos e combina-se com H⁺ da matriz formando água celular (H₂O). Sem O₂, a cadeia para completamente."},
  {tag:"ATP Sintase",tc:"tag-energia",front:"Como a ATP Sintase produz ATP? (Mecanismo de Mitchell)",back:"Fosforilação Oxidativa",ans:"Prótons acumulados no espaço intermembranas retornam à matriz pelo canal da ATP Sintase. O fluxo de H⁺ induz rotação mecânica na subunidade catalítica: ADP + Pi → ATP."},
  {tag:"Bioenergética",tc:"tag-energia",front:"Qual a diferença entre inibidores e desacopladores da cadeia respiratória?",back:"Inibidores vs. Desacopladores",ans:"Inibidores (cianeto, CO): bloqueiam transferência de elétrons no complexo IV → sem ATP. Desacopladores (termogenina, DNP): vazamento de H⁺ sem passar pela ATP Sintase → energia vira calor."},
  {tag:"Fermentação",tc:"tag-energia",front:"Qual a diferença entre fermentação lática e alcoólica?",back:"Fermentação",ans:"Lática: piruvato → lactato (lactato desidrogenase). Ocorre em músculo e bactérias láticas. Alcoólica: piruvato → acetaldeído + CO₂ → etanol. Realizada por leveduras."},
  {tag:"Fotossíntese",tc:"tag-energia",front:"De onde vem o O₂ liberado na fotossíntese?",back:"Fotossíntese",ans:"Exclusivamente da água, pela fotólise: 2H₂O → O₂ + 4H⁺ + 4e⁻ (Reação de Hill). O O₂ NÃO vem do CO₂."},
  {tag:"Fotossíntese",tc:"tag-energia",front:"Onde ocorrem as fases clara e escura da fotossíntese?",back:"Fotossíntese",ans:"Fase clara (fotoquímica): membrana dos tilacoides – gera ATP e NADPH. Fase escura (Calvin): estroma do cloroplasto – fixa CO₂ e produz glicose."},
  {tag:"Núcleo",tc:"tag-nucleo",front:"O que é o corpúsculo de Barr?",back:"Cromatina",ans:"Heterocromatina que representa um dos cromossomos X inativado aleatoriamente nas células somáticas de fêmeas de mamíferos. Visível como cromatina densa no núcleo."},
  {tag:"Núcleo",tc:"tag-nucleo",front:"Qual a função do nucléolo?",back:"Núcleo Celular",ans:"Local de síntese intensa de RNA ribossômico (rRNA) e montagem das subunidades dos ribossomos. Células cancerígenas apresentam nucléolos gigantes e múltiplos."},
  {tag:"RNA",tc:"tag-nucleo",front:"O que é o splicing alternativo?",back:"Processamento do RNA",ans:"Combinações diferentes de éxons do mesmo pré-mRNA geram múltiplos mRNAs maduros. Explica como ~20.000 genes humanos produzem mais de 100.000 proteínas distintas."},
  {tag:"DNA",tc:"tag-nucleo",front:"Quais são as propriedades do código genético?",back:"Código Genético",ans:"(1) Degenerado/redundante: vários códons para o mesmo aminoácido. (2) Universal: mesmos códons em praticamente todos os seres vivos. Códon de iniciação: AUG (Metionina)."},
  {tag:"Ciclo Celular",tc:"tag-divisao",front:"Quais as fases da interfase e o que ocorre em cada uma?",back:"Ciclo Celular",ans:"G1: crescimento e síntese de proteínas. S: replicação do DNA e duplicação dos centríolos. G2: checagem do DNA replicado e síntese de tubulinas para o fuso."},
  {tag:"Mitose",tc:"tag-divisao",front:"Por que a metáfase é usada para o cariótipo?",back:"Mitose",ans:"Fase de máxima condensação cromossômica, com cromossomos alinhados na placa metafásica. A colchicina (destrói microtúbulos) paralisa a divisão nessa fase."},
  {tag:"Citocinese",tc:"tag-divisao",front:"Qual a diferença da citocinese em células animais e vegetais?",back:"Citocinese",ans:"Animal: centrípeta, por anel contrátil de actina e miosina. Vegetal: centrífuga, por depósito de vesículas de pectina do Golgi formando o fragmoplasto."},
  {tag:"Meiose",tc:"tag-divisao",front:"O que é o crossing-over e em qual fase da meiose ocorre?",back:"Meiose I — Prófase I",ans:"Troca recíproca de segmentos de DNA entre cromátides não-irmãs de homólogos. Ocorre no Paquíteno da Prófase I. Os pontos de permutação são chamados quiasmas."},
  {tag:"Meiose",tc:"tag-divisao",front:"Qual a principal diferença entre Anáfase I e Anáfase II da meiose?",back:"Meiose",ans:"Anáfase I: separa cromossomos homólogos — NÃO divide o centrômero. Anáfase II: divide o centrômero e separa cromátides-irmãs (idêntica à mitose)."},
  {tag:"Aneuploidias",tc:"tag-comp",front:"Quais os cariótipos da Síndrome de Down, Klinefelter e Turner?",back:"Aneuploidias",ans:"Down: 47, XX/XY, +21. Klinefelter: 47, XXY (masculino). Turner: 45, X0 (feminino) — única monossomia viável em humanos."},
  {tag:"Paredes",tc:"tag-comp",front:"Qual a parede celular de bactérias, plantas, fungos e algas?",back:"Parede Celular",ans:"Bactérias: peptidoglicano (mureína). Plantas: celulose. Fungos: quitina. Algas: celulose ou sílica. Células animais não possuem parede celular."},
];

let cards = [...all];
let idx = 0;
let flipped = false;
let scores = [0,0,0,0];
let answered = 0;

function shuffle(a){
  for(let i=a.length-1;i>0;i--){
    const j=Math.floor(Math.random()*(i+1));
    [a[i],a[j]]=[a[j],a[i]];
  }
  return a;
}

function render(){
  const c = cards[idx];
  // reset flip
  const card = document.getElementById('card');
  card.classList.remove('flipped');
  flipped = false;

  // front
  document.getElementById('fronttext').textContent = c.front;
  document.getElementById('cardtag').textContent = c.tag;
  document.getElementById('cardtag').className = 'card-tag ' + c.tc;

  // back
  document.getElementById('backctag').textContent = c.tag;
  document.getElementById('backctag').className = 'card-tag ' + c.tc;
  document.getElementById('backsubtitle').textContent = c.back;
  document.getElementById('backtext').textContent = c.ans;

  // progress
  const pct = Math.round((idx / cards.length) * 100);
  document.getElementById('progressfill').style.width = pct + '%';
  document.getElementById('progresspct').textContent = pct + '%';
  document.getElementById('deckinfo').textContent = (idx+1) + ' / ' + cards.length;

  // buttons
  document.getElementById('showbtn').style.display = 'block';
  document.getElementById('ratingsection').classList.remove('visible');
  document.getElementById('completescreen').classList.remove('visible');
  document.getElementById('cardcontainer').style.display = 'block';

  updateStats();
}

function flipCard(){
  if(flipped) return;
  flipped = true;
  document.getElementById('card').classList.add('flipped');
  setTimeout(()=>{
    document.getElementById('showbtn').style.display = 'none';
    document.getElementById('ratingsection').classList.add('visible');
  }, 250);
}

function rate(n){
  scores[n]++;
  answered++;
  flipped = false;
  if(idx < cards.length - 1){
    idx++;
    render();
  } else {
    showComplete();
  }
  updateStats();
}

function showComplete(){
  document.getElementById('cardcontainer').style.display = 'none';
  document.getElementById('showbtn').style.display = 'none';
  document.getElementById('ratingsection').classList.remove('visible');
  document.getElementById('completescreen').classList.add('visible');
  document.getElementById('progressfill').style.width = '100%';
  document.getElementById('progresspct').textContent = '100%';
  const total = scores.reduce((a,b)=>a+b,0);
  const pct = total > 0 ? Math.round((scores[2]+scores[3])/total*100) : 0;
  document.getElementById('completesub').textContent =
    'Você respondeu ' + total + ' cartas. ' + pct + '% marcadas como Bom ou Fácil.';
}

function restart(){
  idx=0; flipped=false; scores=[0,0,0,0]; answered=0;
  render();
}

function nextCard(){
  flipped=false;
  idx=(idx+1)%cards.length;
  render();
}
function prevCard(){
  flipped=false;
  idx=(idx-1+cards.length)%cards.length;
  render();
}
function shuffleCards(){
  cards=shuffle([...all]);
  idx=0; flipped=false; scores=[0,0,0,0]; answered=0;
  render();
}

function updateStats(){
  document.getElementById('s0').textContent=scores[0];
  document.getElementById('s1').textContent=scores[1];
  document.getElementById('s2').textContent=scores[2];
  document.getElementById('s3').textContent=scores[3];
}

render();
</script>
</body>
</html>
