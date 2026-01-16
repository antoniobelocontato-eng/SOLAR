<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HUB TV+ | PAINEL EXPERT</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        :root { --claro-red: #ee2924; --bg-dark: #0b0d10; --card-bg: #161a1f; --text-gray: #a0a0a0; }
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Inter', sans-serif; background: var(--bg-dark); color: #fff; overflow-x: hidden; }

        header { padding: 40px 25px; background: linear-gradient(to bottom, #1e0505, var(--bg-dark)); text-align: center; }
        header h1 { font-size: 26px; font-weight: 900; }
        header h1 span { color: var(--claro-red); }

        .container { padding: 20px; max-width: 1200px; margin: auto; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px; }
        .st-card { 
            background: var(--card-bg); border-radius: 20px; padding: 25px 15px; text-align: center;
            border: 1px solid rgba(255,255,255,0.05); cursor: pointer; transition: 0.3s;
        }

        #details-page { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: var(--bg-dark); z-index: 1000; overflow-y: auto; }
        .nav-header { padding: 15px 20px; display: flex; align-items: center; justify-content: space-between; background: #000; border-bottom: 2px solid var(--claro-red); }
        .home-btn { color: var(--claro-red); font-weight: 800; cursor: pointer; }

        /* ABAS DINÂMICAS - ESTILO IMAGE_154FC2.JPG */
        .tabs-scroll { display: flex; gap: 10px; padding: 20px; overflow-x: auto; scrollbar-width: none; background: #161a1f; }
        .tab { 
            background: #fff; color: #000; padding: 10px 20px; border-radius: 25px; 
            font-size: 11px; font-weight: 800; white-space: nowrap; cursor: pointer; border: 2px solid transparent;
            transition: 0.3s; text-align: center; min-width: 150px;
        }
        .tab.active { background: #ffff00 !important; border-color: #ffaa00; box-shadow: 0 0 15px rgba(255,255,0,0.5); }

        /* LAYOUT 3 COLUNAS */
        .ranking-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; padding: 15px; }
        .rank-column { border-right: 1px dashed #444; padding: 0 5px; }
        .rank-column:last-child { border-right: none; }
        .rank-label { background: var(--claro-red); text-align: center; font-size: 12px; font-weight: 800; padding: 8px; border-radius: 5px; margin-bottom: 10px; }
        
        .poster-container { background: #222; border-radius: 15px; aspect-ratio: 2/3; background-size: cover; border: 2px solid var(--claro-red); margin-bottom: 10px; }
        .synopsis-box { background: #fff; color: #000; padding: 10px; border-radius: 10px; font-size: 10px; font-weight: 700; height: 100px; margin-bottom: 10px; }
        .btn-trailer { background: #fff; color: #000; text-align: center; padding: 8px; border-radius: 8px; font-weight: 800; font-size: 10px; text-decoration: none; border: 2px solid #00ff00; display: block; }
        .movie-name-footer { background: var(--claro-red); text-align: center; padding: 10px; font-size: 11px; font-weight: 800; margin-top: 10px; border-radius: 5px; }
    </style>
</head>
<body>

<div id="home-view">
    <header><h1>HUB TV+ |<span> PAINEL</span></h1></header>
    <div class="container"><div class="grid" id="main-grid"></div></div>
</div>

<div id="details-page">
    <div class="nav-header">
        <span class="home-btn" onclick="closeDetails()">🏠 HOME</span>
        <span id="st-name-header" style="font-weight:900;">STREAMING</span>
        <span></span>
    </div>
    <div class="tabs-scroll">
        <div class="tab active" id="tab-1" onclick="updateRanking('FILMES MÊS', 'tab-1')">TOP Filmes no último mês</div>
        <div class="tab" id="tab-2" onclick="updateRanking('FILMES SEMANA', 'tab-2')">TOP Filmes na última semana</div>
        <div class="tab" id="tab-3" onclick="updateRanking('SÉRIES', 'tab-3')">TOP Séries no último mês</div>
        <div class="tab" id="tab-4" onclick="updateRanking('LANÇAMENTOS', 'tab-4')">Próximos Lançamentos</div>
    </div>
    <div class="ranking-grid" id="ranking-content"></div>
</div>

<script>
    const streamings = ['Netflix', 'Max', 'Disney+', 'Prime Video', 'Apple TV+', 'Globoplay'];
    function init() {
        const grid = document.getElementById('main-grid');
        streamings.forEach(st => {
            grid.innerHTML += `<div class="st-card" onclick="openDetails('${st}')"><h3>${st}</h3><span style="font-size:9px; color:var(--claro-red)">INCLUSO</span></div>`;
        });
    }
    function openDetails(name) {
        document.getElementById('st-name-header').innerText = name.toUpperCase();
        updateRanking('FILMES MÊS', 'tab-1');
        document.getElementById('details-page').style.display = 'block';
    }
    function updateRanking(cat, tabId) {
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById(tabId).classList.add('active');
        let html = '';
        for(let i=1; i<=3; i++) {
            html += `
                <div class="rank-column">
                    <div class="rank-label">${i}º lugar</div>
                    <div class="poster-container" style="background-image: url('https://via.placeholder.com/400x600')"></div>
                    <div class="synopsis-box">SINOPSE: Conteúdo bombando na Claro TV+ em Jan/2026.</div>
                    <a href="#" class="btn-trailer">LINK TRAILER</a>
                    <div class="movie-name-footer">NOME DO FILME</div>
                </div>`;
        }
        document.getElementById('ranking-content').innerHTML = html;
    }
    function closeDetails() { document.getElementById('details-page').style.display = 'none'; }
    init();
</script>
</body>
</html>
