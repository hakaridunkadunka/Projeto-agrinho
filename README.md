<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Equilíbrio Sustentável – Dados do IBGE</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background: #f0f4f1;
            color: #1a2e1f;
            line-height: 1.7;
            scroll-behavior: smooth;
            overflow-x: hidden;
        }

        /* ===== ANIMAÇÕES FLUIDAS ===== */
        .fade-up {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.8s ease, transform 0.8s ease;
        }
        .fade-up.visivel {
            opacity: 1;
            transform: translateY(0);
        }

        .fade-in {
            opacity: 0;
            transition: opacity 0.9s ease;
        }
        .fade-in.visivel {
            opacity: 1;
        }

        .hero {
            background: linear-gradient(160deg, #1b3b2b 0%, #2d5a3f 30%, #3a6b4a 60%, #5c8a66 100%);
            color: #f6faf7;
            padding: 5rem 2rem 4rem;
            text-align: center;
            position: relative;
            overflow: hidden;
            min-height: 70vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .hero::before {
            content: "";
            position: absolute;
            top: -30%;
            left: -20%;
            width: 140%;
            height: 160%;
            background: radial-gradient(ellipse at 40% 60%, rgba(144, 190, 140, 0.15) 0%, transparent 60%),
                radial-gradient(ellipse at 70% 30%, rgba(210, 230, 180, 0.1) 0%, transparent 55%);
            pointer-events: none;
            animation: moverFundo 14s infinite alternate ease-in-out;
        }

        @keyframes moverFundo {
            0% { transform: scale(1) rotate(0deg); }
            100% { transform: scale(1.05) rotate(1deg); }
        }

        .hero-content {
            position: relative;
            z-index: 1;
            max-width: 850px;
        }

        .ibge-badge {
            display: inline-block;
            background: rgba(255, 255, 255, 0.12);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 255, 255, 0.25);
            border-radius: 50px;
            padding: 0.55rem 1.6rem;
            font-size: 0.9rem;
            font-weight: 600;
            letter-spacing: 0.04em;
            text-transform: uppercase;
            margin-bottom: 2rem;
            color: #d4edda;
            transition: all 0.4s;
        }

        .ibge-badge span {
            font-weight: 800;
            color: #ffffff;
        }

        .hero h1 {
            font-size: clamp(2.2rem, 5.5vw, 3.8rem);
            font-weight: 700;
            letter-spacing: -0.02em;
            margin-bottom: 1.2rem;
            text-shadow: 0 2px 18px rgba(0, 0, 0, 0.3);
            transition: transform 0.3s;
        }

        .hero h1 em {
            font-style: normal;
            color: #b9e6c5;
            text-decoration: underline;
            text-decoration-color: #6ca57c;
            text-underline-offset: 0.15em;
            text-decoration-thickness: 3px;
        }

        .hero-subtitle {
            font-size: 1.25rem;
            font-weight: 400;
            opacity: 0.9;
            margin-bottom: 2.5rem;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            color: #e2f0e4;
        }

        .btn-scroll {
            background: #f6faf7;
            color: #1b3b2b;
            border: none;
            padding: 0.9rem 2.2rem;
            font-size: 1rem;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            letter-spacing: 0.03em;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
            box-shadow: 0 8px 28px rgba(0, 0, 0, 0.18);
        }

        .btn-scroll:hover {
            background: #e5f0e6;
            transform: translateY(-3px);
            box-shadow: 0 14px 34px rgba(0, 0, 0, 0.22);
        }

        .container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 3.5rem 1.5rem;
        }

        .section-title {
            font-size: 2rem;
            font-weight: 700;
            color: #1b3b2b;
            margin-bottom: 0.6rem;
            position: relative;
            display: inline-block;
        }

        .section-title::after {
            content: "";
            display: block;
            width: 60px;
            height: 4px;
            background: #4a8c5c;
            margin-top: 0.4rem;
            border-radius: 4px;
            transition: width 0.3s;
        }

        .section-title:hover::after {
            width: 100%;
        }

        .intro-text {
            font-size: 1.15rem;
            color: #2c472f;
            margin-bottom: 2.5rem;
            max-width: 800px;
        }

        /* Grid pilares */
        .grid-pilares {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 1.8rem;
            margin: 2.5rem 0 3rem;
        }

        .card-pilar {
            background: #ffffff;
            border-radius: 18px;
            padding: 2rem 1.5rem;
            box-shadow: 0 10px 30px rgba(30, 60, 30, 0.08);
            border-top: 5px solid #4a8c5c;
            transition: transform 0.25s ease, box-shadow 0.25s ease;
        }

        .card-pilar:hover {
            transform: translateY(-8px);
            box-shadow: 0 18px 40px rgba(30, 60, 30, 0.18);
        }

        .data-highlight {
            background: #eaf4ec;
            border-left: 6px solid #2d5a3f;
            border-radius: 0 14px 14px 0;
            padding: 1.8rem 2rem;
            margin: 2.5rem 0;
            font-weight: 500;
            transition: background 0.3s;
        }

        .data-highlight:hover {
            background: #d9ebdc;
        }

        .metric-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 1.5rem;
            margin: 2rem 0 3rem;
        }

        .metric-box {
            background: #ffffff;
            border-radius: 30px;
            padding: 1.5rem 1rem;
            text-align: center;
            box-shadow: 0 6px 22px rgba(30, 60, 30, 0.09);
            transition: transform 0.3s;
            cursor: default;
        }

        .metric-box:hover {
            transform: translateY(-4px);
        }

        .metric-number {
            font-size: 2.4rem;
            font-weight: 800;
            color: #1b3b2b;
        }

        /* Linha do tempo */
        .timeline {
            margin: 3rem 0;
            position: relative;
            padding-left: 2rem;
            border-left: 3px dashed #4a8c5c;
        }

        .timeline-item {
            margin-bottom: 2rem;
            position: relative;
            padding-left: 2rem;
        }

        .timeline-item::before {
            content: "●";
            position: absolute;
            left: -2.7rem;
            top: 0.2rem;
            font-size: 1.6rem;
            color: #2d5a3f;
            background: #f0f4f1;
            padding: 0 0.3rem;
        }

        /* Barras de progresso */
        .barra-info {
            margin: 1.2rem 0;
            display: flex;
            align-items: center;
            gap: 1rem;
        }
        .barra-label {
            width: 180px;
            font-weight: 600;
        }
        .barra-fundo {
            flex: 1;
            height: 20px;
            background: #d9e2da;
            border-radius: 20px;
            overflow: hidden;
        }
        .barra-preenchimento {
            height: 100%;
            width: 0%;
            background: #2d5a3f;
            border-radius: 20px;
            transition: width 1.2s ease;
        }

        .ods-strip {
            background: #1b3b2b;
            color: #f0f7f1;
            padding: 2.8rem 1.5rem;
            border-radius: 22px;
            margin: 2.5rem 0;
            text-align: center;
            transition: transform 0.3s;
        }

        .publication-list {
            list-style: none;
            padding: 0;
            margin: 2rem 0;
        }

        .publication-list li {
            background: #ffffff;
            margin-bottom: 1rem;
            padding: 1.2rem 1.6rem;
            border-radius: 12px;
            box-shadow: 0 4px 14px rgba(20, 50, 20, 0.06);
            display: flex;
            align-items: baseline;
            gap: 0.9rem;
            transition: background 0.2s, transform 0.2s;
        }

        .publication-list li:hover {
            background: #f2f8f3;
            transform: translateX(6px);
        }

        .publication-list li::before {
            content: "📘";
            font-size: 1.2rem;
            flex-shrink: 0;
        }

        footer {
            background: #1a2e1f;
            color: #bfd6c5;
            text-align: center;
            padding: 2.2rem 1.5rem;
            font-size: 0.95rem;
        }

        /* Gráfico de pizza simples (CSS) */
        .grafico-pizza {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background: conic-gradient(#2d5a3f 0deg 240deg, #a3c4aa 240deg 360deg);
            margin: 1rem auto;
        }

        @media (max-width: 600px) {
            .barra-info {
                flex-direction: column;
                align-items: flex-start;
            }
            .barra-label {
                width: auto;
            }
            .timeline {
                padding-left: 1.2rem;
            }
        }
    </style>
</head>
<body>

    <!-- HERO -->
    <section class="hero fade-in">
        <div class="hero-content">
            <div class="ibge-badge">Fonte oficial · <span>IBGE</span></div>
            <h1>Equilíbrio <em>Sustentável</em></h1>
            <p class="hero-subtitle">
                Os Indicadores de Desenvolvimento Sustentável do IBGE revelam como o Brasil integra crescimento econômico, justiça social e proteção ambiental – com dados oficiais e atualizados.
            </p>
            <a href="#conteudo" class="btn-scroll">Explorar indicadores ▼</a>
        </div>
    </section>

    <!-- CONTEÚDO PRINCIPAL -->
    <div class="container" id="conteudo">

        <!-- O QUE SÃO IDS -->
        <div class="fade-up">
            <h2 class="section-title">O que são os IDS?</h2>
            <p class="intro-text">
                Desde <strong>2002</strong>, o IBGE publica os <strong>Indicadores de Desenvolvimento Sustentável (IDS)</strong>, um conjunto de mais de 60 indicadores que acompanham o progresso do Brasil rumo aos Objetivos de Desenvolvimento Sustentável (ODS) da ONU. As dimensões ambiental, social, econômica e institucional são analisadas com base em pesquisas como PNAD, PNSB, Censo Agro e Contas Econômicas Ambientais.
            </p>
        </div>

        <!-- PILARES -->
        <div class="grid-pilares">
            <div class="card-pilar fade-up">
                <h3>🌿 Ambiental</h3>
                <p>Cobertura vegetal nativa, emissões de gases de efeito estufa, recursos hídricos e biodiversidade. O IBGE monitora a perda de vegetação e a qualidade das águas.</p>
            </div>
            <div class="card-pilar fade-up">
                <h3>👥 Social</h3>
                <p>Acesso a saneamento, saúde, educação e redução das desigualdades. A PNAD Contínua e a PNSB fornecem retratos detalhados da qualidade de vida.</p>
            </div>
            <div class="card-pilar fade-up">
                <h3>📊 Econômico</h3>
                <p>Uso de recursos naturais, eficiência energética e padrões de consumo. As Contas Econômicas Ambientais integram economia e meio ambiente.</p>
            </div>
            <div class="card-pilar fade-up">
                <h3>🏛️ Institucional</h3>
                <p>Governança, participação social e marcos legais. O IBGE avalia a existência de conselhos municipais de meio ambiente e planos diretores.</p>
            </div>
        </div>

        <!-- DADOS RECENTES -->
        <div class="fade-up">
            <div class="data-highlight">
                <strong>🌎 Saneamento básico (PNSB 2020):</strong> Cerca de <strong>66% dos municípios</strong> possuem coleta de esgoto, porém apenas <strong>46,3% dos domicílios</strong> têm acesso à rede coletora (PNAD 2022). No Norte, esse índice cai para menos de 15%. Universalizar o saneamento é meta do ODS 6.
            </div>
        </div>

        <!-- INDICADORES EM BARRAS -->
        <div class="fade-up">
            <h2 class="section-title">Indicadores-chave do Brasil</h2>
            <div class="barra-info">
                <span class="barra-label">🌳 Cobertura vegetal nativa</span>
                <div class="barra-fundo"><div class="barra-preenchimento" data-width="58" style="width: 0%;"> </div></div>
                <span><strong>58%</strong> do território</span>
            </div>
            <div class="barra-info">
                <span class="barra-label">💡 Energia renovável na matriz</span>
                <div class="barra-fundo"><div class="barra-preenchimento" data-width="45" style="width: 0%;"> </div></div>
                <span><strong>45%</strong> (hidro, eólica, biomassa)</span>
            </div>
            <div class="barra-info">
                <span class="barra-label">🚰 Acesso à água potável</span>
                <div class="barra-fundo"><div class="barra-preenchimento" data-width="84" style="width: 0%;"> </div></div>
                <span><strong>84,1%</strong> dos domicílios</span>
            </div>
            <div class="barra-info">
                <span class="barra-label">🗑️ Coleta de lixo adequada</span>
                <div class="barra-fundo"><div class="barra-preenchimento" data-width="91" style="width: 0%;"> </div></div>
                <span><strong>91,6%</strong> dos domicílios urbanos</span>
            </div>
            <p style="font-size:0.85rem; color:#4a6b4f;">Fonte: IDS 2022, PNAD Contínua, Balanço Energético Nacional (IBGE/EPE)</p>
        </div>

        <!-- LINHA DO TEMPO -->
        <div class="fade-up">
            <h2 class="section-title">Evolução dos IDS</h2>
            <div class="timeline">
                <div class="timeline-item"><strong>2002</strong> – Primeira edição dos IDS, com 50 indicadores.</div>
                <div class="timeline-item"><strong>2010</strong> – Inclusão das Contas Econômicas Ambientais.</div>
                <div class="timeline-item"><strong>2017</strong> – Alinhamento total aos 17 ODS da ONU.</div>
                <div class="timeline-item"><strong>2023</strong> – Plataforma ODS Brasil reúne dados de todas as unidades federativas.</div>
            </div>
        </div>

        <!-- ODS EM DESTAQUE -->
        <div class="ods-strip fade-up">
            <h2>📍 Monitoramento dos ODS</h2>
            <p>
                O IBGE coordena a produção de indicadores para os 17 Objetivos de Desenvolvimento Sustentável. Exemplos de metas acompanhadas: erradicação da pobreza (ODS 1), fome zero (ODS 2), energia limpa (ODS 7), ação climática (ODS 13) e vida na água (ODS 14). A plataforma <strong>odsbrasil.gov.br</strong> é mantida pelo Instituto.
            </p>
            <div class="metric-grid" style="justify-items:center;">
                <div class="metric-box"><span class="metric-number">17</span> ODS</div>
                <div class="metric-box"><span class="metric-number">169</span> metas</div>
                <div class="metric-box"><span class="metric-number">231</span> indicadores globais</div>
            </div>
        </div>

        <!-- PUBLICAÇÕES -->
        <div class="fade-up">
            <h2 class="section-title">Publicações do IBGE</h2>
            <ul class="publication-list">
                <li><strong>Indicadores de Desenvolvimento Sustentável (IDS)</strong> – Edição mais recente com séries históricas.</li>
                <li><strong>Contas Econômicas Ambientais</strong> – Água, energia, emissões e uso da terra.</li>
                <li><strong>Pesquisa Nacional de Saneamento Básico (PNSB)</strong> – Infraestrutura de água e esgoto.</li>
                <li><strong>Censo Agropecuário</strong> – Práticas agrícolas e sustentabilidade no campo.</li>
                <li><strong>Plataforma ODS Brasil</strong> – Painel interativo com indicadores municipais.</li>
            </ul>
        </div>

        <p style="font-size:0.9rem; color:#4a6b4f; text-align:center; margin-top:2rem;">
            Todas as informações são baseadas exclusivamente em dados do <strong>IBGE</strong>.
        </p>
    </div>

    <footer>
        <p>🌱 <strong>Equilíbrio Sustentável</strong> · Dados oficiais do IBGE · Brasil, 2026</p>
    </footer>

    <!-- SCRIPT PARA ANIMAÇÕES E INTERATIVIDADE -->
    <script>
        (function() {
            // Aplica classe 'visivel' quando elementos entram na viewport
            const elementos = document.querySelectorAll('.fade-up, .fade-in');
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visivel');
                    }
                });
            }, { threshold: 0.2 });

            elementos.forEach(el => observer.observe(el));

            // Anima as barras de progresso quando visíveis
            const barras = document.querySelectorAll('.barra-preenchimento');
            const observerBarras = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const barra = entry.target;
                        const largura = barra.getAttribute('data-width') + '%';
                        barra.style.width = largura;
                    }
                });
            }, { threshold: 0.5 });

            barras.forEach(barra => observerBarras.observe(barra));

            // Hero já visível (força animação inicial)
            document.querySelector('.hero').classList.add('visivel');
        })();
    </script>
</body>
</html>

