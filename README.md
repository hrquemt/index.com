<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Magia e Mistério: Um RPG de Hogwarts</title>
    <meta name="description" content="Um sistema de RPG de mesa criado por Henrique Moraes Tamiozzo, ambientado no universo de Hogwarts. Encontre regras, magias, bestiário e mais.">
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Uncial+Antiqua&family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            background-image: url('https://www.transparenttextures.com/patterns/old-paper.png');
            background-color: #fdf5e6;
            font-family: 'Inter', sans-serif;
            color: #4a2c2a;
        }
        h1, h2, h3, h4, h5, h6 {
            font-family: 'Uncial Antiqua', cursive;
            color: #5d4037;
            letter-spacing: 1px;
        }
        .nav-link {
            transition: all 0.3s ease;
            border-bottom: 2px solid transparent;
            padding: 8px; /* Adicionado padding para área de clique maior */
        }
        /* Adicionado estilo de foco visível para acessibilidade de teclado */
        .nav-link:hover, .nav-link:focus {
            color: #c89c4ca1;
            border-bottom-color: #c89c4ca1;
            outline: none; /* Remove o outline padrão para usar o nosso */
        }
        .skip-link {
            position: absolute;
            top: -40px;
            left: 0;
            background: #5d4037;
            color: white;
            padding: 8px;
            z-index: 100;
            transition: top 0.3s;
        }
        .skip-link:focus {
            top: 0;
        }
        .card {
            background-color: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(210, 180, 140, 0.5);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        .accordion-button::after {
            content: ' ▼';
            font-size: 0.8em;
            transition: transform 0.3s ease;
        }
        .accordion-button[aria-expanded="true"]::after {
            transform: rotate(180deg);
        }
        .modal {
            display: none; /* Será controlado por 'hidden' no JS */
            position: fixed;
            z-index: 100;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.8);
            justify-content: center;
            align-items: center;
        }
        .modal.is-open {
            display: flex;
        }
        .modal-content {
            margin: auto;
            display: block;
            max-width: 90%;
            max-height: 90vh;
        }
        .modal-close {
            position: absolute;
            top: 10px;
            right: 25px;
            color: #f1f1f1;
            font-size: 40px;
            font-weight: bold;
            transition: 0.3s;
            cursor: pointer;
            background: none;
            border: none;
        }
        .modal-close:hover, .modal-close:focus {
            color: #bbb;
            outline: 2px solid #fff; /* Foco visível */
        }
        .sr-only {
            position: absolute;
            width: 1px;
            height: 1px;
            padding: 0;
            margin: -1px;
            overflow: hidden;
            clip: rect(0, 0, 0, 0);
            white-space: nowrap;
            border-width: 0;
        }
        /* Garante melhor contraste na navegação */
        nav { background-color: #5d4037; }
        /* Melhorando o contraste do texto no Header */
        header .text-gray-200 { color: #E5E7EB; }
        header .text-gray-300 { color: #D1D5DB; }
        /* Melhorando a legibilidade das tabelas */
        table { border-collapse: collapse; }
        th, td { border: 1px solid rgba(200, 156, 76, 0.5); padding: 8px 12px; }
        th { background-color: rgba(93, 64, 55, 0.1); }
    </style>
</head>
<body class="antialiased">

    <a href="#main-content" class="skip-link">Pular para o conteúdo principal</a>

    <div id="imageModal" class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle" hidden>
        <button class="modal-close" id="modalCloseButton">
            <span aria-hidden="true">&times;</span>
            <span class="sr-only">Fechar modal</span>
        </button>
        <img class="modal-content" id="modalImage" alt="">
        <h3 id="modalTitle" class="sr-only">Visualização de Imagem Ampliada</h3>
    </div>

    <header class="text-center py-10 px-4" style="background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('https://images.unsplash.com/photo-1618941329383-df59b36715d0?q=80&w=1932&auto=format&fit=crop') center/cover;">
        <img src="https://images.ctfassets.net/usf1vwtuqyxm/3d9lS5n2p19iQLVh1sML2b/7931f8b31a33a579133a1714015f4058/HogwartsCrest_WB_F4.png?w=914&q=70&fm=webp" alt="Brasão de Hogwarts" class="mx-auto h-32 w-auto mb-4">
        <h1 class="text-5xl md:text-7xl font-bold text-white shadow-lg">Magia e Mistério</h1>
        <h2 class="text-2xl md:text-3xl text-gray-200 mt-2">O RPG de Hogwarts</h2>
        <p class="text-lg text-gray-300 italic mt-6">Criado por Henrique Moraes Tamiozzo</p>
    </header>

    <nav class="bg-[#5d4037] text-white sticky top-0 z-50 shadow-lg">
        <div class="container mx-auto px-4">
            <div class="flex justify-center items-center py-3 space-x-4 md:space-x-8 overflow-x-auto">
                <a href="#sistema" class="nav-link text-sm md:text-base whitespace-nowrap">Sistema</a>
                <a href="#magias" class="nav-link text-sm md:text-base whitespace-nowrap">Magias</a>
                <a href="#bestiario" class="nav-link text-sm md:text-base whitespace-nowrap">Bestiário</a>
                <a href="#varinhas" class="nav-link text-sm md:text-base whitespace-nowrap">Varinhas</a>
                <a href="#regras" class="nav-link text-sm md:text-base whitespace-nowrap">Regras Avançadas</a>
                <a href="#mapas" class="nav-link text-sm md:text-base whitespace-nowrap">Mapas</a>
            </div>
        </div>
    </nav>

    <main id="main-content" class="container mx-auto p-4 md:p-8">

        <section id="sistema" class="mb-16 scroll-mt-20">
            <h2 class="text-4xl text-center mb-8 border-b-2 border-[#c89c4c] pb-2">Sistema e Criação de Personagem</h2>
             <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div class="card p-6 rounded-lg lg:col-span-1">
                    <h3 class="text-2xl mb-4">Atributos</h3>
                    <p class="mb-4">Distribua 10 pontos entre eles.</p>
                    <ul class="space-y-2 list-inside list-disc">
                        <li>Coragem</li>
                        <li>Conhecimento</li>
                        <li>Empatia</li>
                        <li>Enganação</li>
                        <li>Magia</li>
                        <li>Resistência</li>
                    </ul>
                </div>
                <div class="card p-6 rounded-lg lg:col-span-1">
                    <h3 class="text-2xl mb-4">Perícias</h3>
                    <p class="mb-4">Habilidades especializadas do seu personagem.</p>
                    <ul class="space-y-2 list-inside list-disc">
                        <li>Duelos</li>
                        <li>Poções</li>
                        <li>Feitiçaria</li>
                        <li>Herbologia</li>
                        <li>Defesa Contra as Artes das Trevas</li>
                    </ul>
                </div>
                <div class="card p-6 rounded-lg md:col-span-2 lg:col-span-1">
                    <h3 class="text-2xl mb-4">Sistema de Dados</h3>
                    <p>Todas as ações principais usam o <strong>
