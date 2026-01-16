<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Especialista Claro TV+ | Guia de Vendas 2026</title>
    <link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root { --claro-red: #ee2924; --bg: #f4f4f4; --white: #ffffff; --dark: #333; }
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Open Sans', sans-serif; background: var(--bg); color: var(--dark); }
        
        header { background: var(--white); padding: 20px; text-align: center; border-bottom: 5px solid var(--claro-red); box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
        header h1 { color: var(--claro-red); font-size: 1.2rem; margin-bottom: 5px; }
        header p { font-size: 0.85rem; color: #666; }

        .container { padding: 15px; max-width: 500px; margin: auto; }

        /* Grid de Streamings */
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 10px; }
        .st-card { background: var(--white); border-radius: 12px; padding: 15px; text-align: center; border: 1px solid #ddd; cursor: pointer; transition: 0.2s; }
        .st-card:active { transform: scale(0.95); }
        .st-card img { height: 35px; margin-bottom: 8px; object-fit: contain; }
        .st-card .badge { font-size: 0.65rem; color: var(--claro-red); font-weight: bold; text-transform: uppercase; }

        /* Modal / Página de Conteúdo */
        #page-content { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: var(--white); z-index: 100; overflow-y: auto; padding: 20px; }
        .back-btn { background: var(--claro-red); color: white; border: none; padding: 12px; width: 100%; border-radius: 8px; font-weight: bold; margin-bottom: 20px; }

        .tabs { display: flex; gap: 8px; margin-bottom: 20px; }
        .tab-btn { flex: 1; padding: 10px; border: none; background: #eee; border-radius: 6px; font-weight: bold; cursor: pointer; }
        .tab-btn.active { background: var(--claro-red); color: white; }

        /* Cards de Filmes/Séries */
        .content-item { background: #fff; border: 1px solid #eee; border-radius: 10px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .pos { background: gold; padding: 2px 6px; border-radius: 4px; font-size: 0.7rem; font-weight: bold; }
        .title { font-size: 1.1rem; font-weight: bold; color: var(--claro-red); margin: 5px 0; }
        .synopsis { font-size: 0.85rem; color: #555; margin-bottom: 10px; line-height: 1.4; }
        .pitch { background: #fff0f0; border-left: 4px solid var(--claro-red); padding: 10px; font-size: 0.85rem; margin-bottom: 12px; }
        .yt-btn { display: block; background: #ff0000; color: white; text-align: center; padding: 10px; border-radius: 6px; text-decoration: none; font-weight: bold; font-size: 0.85rem; }

        /* Tabela de Economia */
        .economy-table { margin-top: 30px; font-size: 0.8rem; width: 100%; border-collapse: collapse; }
        .economy-table td { padding: 10px; border-bottom: 1px solid #eee; }
        .economy-table tr:last-child { font-weight: bold; color: green; font-size: 1rem; }
    </style>
</head>
<body>

<header>
    <h1>ESPECIALISTA CLARO TV+</h1>
    <p>O melhor conteúdo do mundo em um só lugar.</p>
</header>

<div class="container">
    <div class="grid" id="main-grid">
        </div>
    
    <div style="margin-top: 30px; text-align: center; padding: 15px; background: #eee; border-radius: 10px;">
        <small>Dica: Use o site para mostrar ao cliente a economia real de ter todos os streamings inclusos.</small>
    </div>
</div>

<div id="page-content">
    <button class="back-btn" onclick="closeDetails()">← VOLTAR AO MENU</button>
    <div id="details-header"></div>
    
    <div class="tabs">
        <button class="tab-btn active" onclick="switchTab('ranking')">TOP 3 ATUAL</button>
        <button class="tab-btn" onclick="switchTab('future')">EM BREVE</button>
    </div>

    <div id="ranking-list"></div>
    <div id="future-list" style="display:none;"></div>
    
    <table class="economy-table" id="economy-box"></table>
</div>

<script>
    const data = {
        'Max': {
            plano: 'Standard com Anúncios',
            preco: 'R$ 29,90',
            top: [
                {t: 'Coringa: Delírio a Dois', s: 'Arthur Fleck aguarda o julgamento por seus crimes enquanto encontra o amor e a música dentro dele.', p: 'O filme que acabou de sair do cinema! Argumento imbatível para fãs de drama.'},
                {t: 'The Last of Us (T2)', s: 'Ellie e Joel enfrentam as consequências de suas escolhas em um mundo perigoso.', p: 'A maior série de 2026. Quem não tem Claro TV+ vai ficar de fora da conversa.'}
            ],
            future: 'The White Lotus: Tailândia (Fevereiro)'
        },
        'Netflix': {
            plano: 'Padrão com Anúncios',
            preco: 'R$ 20,90',
            top: [
                {t: 'His & Hers', s: 'Um suspense de tirar o fôlego baseado no best-seller internacional.', p: 'Ideal para quem gosta de maratonar séries de mistério no fim de semana.'}
            ],
            future: 'Wednesday (T2) - Fevereiro/2026'
        },
        'Apple TV+': {
            plano: 'Sem Anúncios (Premium)',
            preco: 'R$ 21,90',
            top: [
                {t: 'F1 (Brad Pitt)', s: 'Realismo absurdo em uma história de superação nas pistas mais rápidas do mundo.', p: 'Qualidade de cinema. Perfeito para demonstrar o poder da imagem na Claro.'}
            ],
            future: 'Severance (T2) - Em Breve'
        },
        'Globoplay': {
            plano: 'Premium (Sem Anúncios)',
            preco: 'R$ 54,90',
            top: [
                {t: 'Guerreiros do Sol', s: 'A nova superprodução épica original Globoplay.', p: 'Destaque que o Globoplay da Claro é o PREMIUM: sem comerciais e com tudo liberado.'}
            ],
            future: 'BBB 26 - Acompanhe 24h'
        }
    };

    function init() {
        const grid = document.getElementById('main-grid');
        Object.keys(data).forEach(key => {
            grid.innerHTML += `
                <div class="st-card" onclick="openDetails('${key}')">
                    <img src="https://via.placeholder.com/100x40?text=${key}" alt="${key}">
                    <span class="badge">Incluso</span>
                </div>
            `;
        });
    }

    function openDetails(key) {
        const item = data[key];
        document.getElementById('details-header').innerHTML = `
            <h2 style="color:var(--claro-red)">${key}</h2>
            <p style="margin-bottom:20px; font-size:0.9rem"><b>Plano:</b> ${item.plano}</p>
        `;
        
        let rankHtml = '';
        item.top.forEach((content, index) => {
            rankHtml += `
                <div class="content-item">
                    <span class="pos">#${index+1} POPULAR</span>
                    <div class="title">${content.t}</div>
                    <div class="synopsis">${content.s}</div>
                    <div class="pitch"><strong>Estratégia:</strong> ${content.p}</div>
                    <a href="https://www.youtube.com/results?search_query=${content.t}+trailer" target="_blank" class="yt-btn">VER TRAILER ▶️</a>
                </div>
            `;
        });
        document.getElementById('ranking-list').innerHTML = rankHtml;
        
        document.getElementById('future-list').innerHTML = `
            <div class="content-item">
                <div class="title">🚀 ${item.future}</div>
                <div class="pitch">Use esse lançamento para criar urgência na assinatura hoje!</div>
            </div>
        `;

        document.getElementById('economy-box').innerHTML = `
            <tr><td>Assinatura Avulsa</td><td>${item.preco}</td></tr>
            <tr><td>Na Claro TV+</td><td>R$ 0,00 Adicional</td></tr>
            <tr><td>SUA ECONOMIA</td><td>100% NESTE APP</td></tr>
        `;

        document.getElementById('page-content').style.display = 'block';
        window.scrollTo(0,0);
    }

    function closeDetails() { document.getElementById('page-content').style.display = 'none'; }

    function switchTab(type) {
        document.getElementById('ranking-list').style.display = type === 'ranking' ? 'block' : 'none';
        document.getElementById('future-list').style.display = type === 'future' ? 'block' : 'none';
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.toggle('active'));
    }

    init();
</script>
</body>
</html>
