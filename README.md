<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RPG System & Character Sheet Manager</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        fantasy: {
                            gold: '#d97706',
                            darkGold: '#b45309',
                            parchment: '#fef3c7',
                            darkBg: '#121214',
                            cardBg: '#1a1a1e',
                            border: '#3f3f46'
                        }
                    }
                }
            }
        }
    </script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600;700;900&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        h1, h2, h3, .font-cinzel { font-family: 'Cinzel', serif; }
    </style>
</head>
<body class="bg-gray-900 text-gray-100 min-h-screen transition-colors duration-300">
    <!-- Header Navigation & Main Controls -->
    <header class="bg-gray-950 border-b border-gray-800 sticky top-0 z-50 shadow-md">
        <div class="max-w-7xl mx-auto px-4 py-3 flex flex-wrap justify-between items-center gap-4">
            <div class="flex items-center space-x-3">
                <span class="text-2xl">🪙⚔️</span>
                <h1 class="text-xl md:text-2xl font-bold bg-gradient-to-r from-amber-400 to-amber-600 bg-clip-text text-transparent font-cinzel">
                    Crônicas do Multiverso RPG
                </h1>
            </div>
            <!-- Tab Navigation -->
            <nav class="flex flex-wrap gap-2">
                <button onclick="switchTab('economy')" id="btn-tab-economy" class="px-4 py-2 rounded-lg font-medium text-sm transition-all bg-amber-600 text-white shadow">
                    💰 Economia & Câmbio
                </button>
                <button onclick="switchTab('sheet')" id="btn-tab-sheet" class="px-4 py-2 rounded-lg font-medium text-sm transition-all bg-gray-800 text-gray-300 hover:bg-gray-700">
                    📜 Ficha do Herói
                </button>
                <button onclick="switchTab('trade')" id="btn-tab-trade" class="px-4 py-2 rounded-lg font-medium text-sm transition-all bg-gray-800 text-gray-300 hover:bg-gray-700">
                    🏛️ Comércio & Negócios
                </button>
                <button onclick="switchTab('manager')" id="btn-tab-manager" class="px-4 py-2 rounded-lg font-medium text-sm transition-all bg-gray-800 text-gray-300 hover:bg-gray-700">
                    📚 Gerenciador de Fichas
                </button>
                <button onclick="switchTab('campaigns')" id="btn-tab-campaigns" class="px-4 py-2 rounded-lg font-medium text-sm transition-all bg-gray-800 text-gray-300 hover:bg-gray-700">
                    🛡️ Campanhas (Mesa)
                </button>
            </nav>
            <div class="flex items-center space-x-3">
                <button onclick="toggleTheme()" class="p-2 rounded-full bg-gray-800 text-amber-400 hover:bg-gray-700 transition" title="Alternar Tema">
                    🌙
                </button>
            </div>
        </div>
    </header>
    <!-- Main Container -->
    <main class="max-w-7xl mx-auto px-4 py-6">
        <!-- ================= TAB 1: ECONOMIA ================= -->
        <div id="tab-economy" class="space-y-6">
            <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl backdrop-blur">
                <div class="flex justify-between items-center mb-6">
                    <div>
                        <h2 class="text-2xl font-bold font-cinzel text-amber-400">Tesouro & Moedas</h2>
                        <p class="text-sm text-gray-400">Conversão oficial: 50 Cobre (PC) = 1 Prata (PP) | 100 Prata (PP) = 1 Ouro (PO) | 1.000 Ouro (PO) = 1 Platina (PL)</p>
                    </div>
                    <button onclick="optimizeCoins()" class="px-4 py-2 bg-amber-600 hover:bg-amber-500 text-white text-sm font-semibold rounded-xl shadow transition flex items-center gap-2">
                        <span>✨ Otimizar Moedas (Consolidar)</span>
                    </button>
                </div>
                <!-- Moedas Grid -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="bg-gray-900 border border-cyan-800/50 rounded-xl p-4 flex flex-col justify-between shadow-inner">
                        <div class="flex justify-between items-center mb-2">
                            <span class="font-bold text-cyan-400 flex items-center gap-1">💎 Platina (PL)</span>
                            <span class="text-xs text-gray-500">1.000 PO</span>
                        </div>
                        <input type="number" id="coin-pl" min="0" value="0" oninput="updateCoins()" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-3 text-xl font-bold text-cyan-300 focus:outline-none focus:border-cyan-500">
                    </div>
                    <div class="bg-gray-900 border border-amber-800/50 rounded-xl p-4 flex flex-col justify-between shadow-inner">
                        <div class="flex justify-between items-center mb-2">
                            <span class="font-bold text-amber-400 flex items-center gap-1">🟡 Ouro (PO)</span>
                            <span class="text-xs text-gray-500">100 PP</span>
                        </div>
                        <input type="number" id="coin-po" min="0" value="0" oninput="updateCoins()" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-3 text-xl font-bold text-amber-300 focus:outline-none focus:border-amber-500">
                    </div>
                    <div class="bg-gray-900 border border-gray-600/50 rounded-xl p-4 flex flex-col justify-between shadow-inner">
                        <div class="flex justify-between items-center mb-2">
                            <span class="font-bold text-gray-300 flex items-center gap-1">⚪ Prata (PP)</span>
                            <span class="text-xs text-gray-500">50 PC</span>
                        </div>
                        <input type="number" id="coin-pp" min="0" value="0" oninput="updateCoins()" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-3 text-xl font-bold text-gray-200 focus:outline-none focus:border-gray-400">
                    </div>
                    <div class="bg-gray-900 border border-orange-900/50 rounded-xl p-4 flex flex-col justify-between shadow-inner">
                        <div class="flex justify-between items-center mb-2">
                            <span class="font-bold text-orange-400 flex items-center gap-1">🟤 Cobre (PC)</span>
                            <span class="text-xs text-gray-500">Base</span>
                        </div>
                        <input type="number" id="coin-pc" min="0" value="0" oninput="updateCoins()" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-3 text-xl font-bold text-orange-300 focus:outline-none focus:border-orange-500">
                    </div>
                </div>
                <div class="mt-6 p-4 bg-gray-900/90 rounded-xl border border-gray-700 flex flex-wrap justify-between items-center gap-4">
                    <div>
                        <span class="text-sm text-gray-400">Valor Total Equivalente em Cobre (PC):</span>
                        <div id="total-copper-val" class="text-2xl font-extrabold text-amber-400">0 PC</div>
                    </div>
                    <div>
                        <span class="text-sm text-gray-400">Peso Total Estimado:</span>
                        <div id="total-weight-val" class="text-lg font-bold text-gray-300">0.0 kg (0 lb)</div>
                    </div>
                </div>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl">
                    <h3 class="text-xl font-bold font-cinzel text-amber-400 mb-4">Adicionar / Deduzir Moedas</h3>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-1">Descrição da Transação</label>
                            <input type="text" id="trans-desc" placeholder="Ex: Recompensa de Missão" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2.5 text-gray-100 focus:outline-none focus:border-amber-500">
                        </div>
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-300 mb-1">Tipo de Moeda</label>
                                <select id="trans-coin-type" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2.5 text-gray-100 focus:outline-none focus:border-amber-500">
                                    <option value="pc">Cobre (PC)</option>
                                    <option value="pp">Prata (PP)</option>
                                    <option value="po">Ouro (PO)</option>
                                    <option value="pl">Platina (PL)</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-300 mb-1">Quantidade</label>
                                <input type="number" id="trans-amount" value="10" min="1" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2.5 text-gray-100 focus:outline-none focus:border-amber-500">
                            </div>
                        </div>
                        <div class="flex gap-3 pt-2">
                            <button onclick="processTransaction('add')" class="flex-1 bg-green-700 hover:bg-green-600 text-white font-semibold py-2.5 px-4 rounded-xl shadow transition">➕ Adicionar Tesouro</button>
                            <button onclick="processTransaction('sub')" class="flex-1 bg-red-700 hover:bg-red-600 text-white font-semibold py-2.5 px-4 rounded-xl shadow transition">➖ Gastar / Pagar</button>
                        </div>
                    </div>
                </div>
                <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl flex flex-col justify-between">
                    <div>
                        <div class="flex justify-between items-center mb-4">
                            <h3 class="text-xl font-bold font-cinzel text-amber-400">Histórico de Transações</h3>
                            <button onclick="clearHistory()" class="text-xs text-red-400 hover:underline">Limpar Histórico</button>
                        </div>
                        <div id="transaction-history" class="space-y-2 max-h-56 overflow-y-auto pr-2 text-sm text-gray-300">
                            <p class="text-gray-500 italic">Nenhuma transação registrada recentemente.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- ================= TAB 2: FICHA DO PERSONAGEM ================= -->
        <div id="tab-sheet" class="hidden space-y-6">
            <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-4 shadow-xl flex flex-wrap items-center justify-between gap-4">
                <div class="flex items-center gap-3 flex-1 min-w-[280px]">
                    <span class="font-bold text-amber-400">Herói Ativo:</span>
                    <select id="active-character-select" onchange="switchActiveCharacter(this.value)" class="flex-1 bg-gray-900 border border-gray-700 rounded-lg p-2.5 text-gray-100 font-semibold focus:outline-none focus:border-amber-500">
                    </select>
                </div>
                <div class="flex gap-2">
                    <button onclick="createNewCharacter()" class="px-4 py-2 bg-amber-600 hover:bg-amber-500 text-white text-sm font-semibold rounded-xl shadow transition">⚔️ Novo Herói</button>
                    <button onclick="duplicateActiveCharacter()" class="px-4 py-2 bg-gray-700 hover:bg-gray-600 text-white text-sm font-semibold rounded-xl shadow transition">📋 Duplicar</button>
                    <button onclick="deleteActiveCharacter()" class="px-4 py-2 bg-red-800 hover:bg-red-700 text-white text-sm font-semibold rounded-xl shadow transition">🗑️ Excluir</button>
                </div>
            </div>
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <div class="lg:col-span-2 space-y-6">
                    <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-4">
                        <h3 class="text-xl font-bold font-cinzel text-amber-400 border-b border-gray-700 pb-2">Informações Pessoais</h3>
                        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Nome</label>
                                <input type="text" id="char-name" oninput="updateCharInfo('name', this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Idade</label>
                                <input type="text" id="char-age" oninput="updateCharInfo('age', this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Raça</label>
                                <select id="char-race" onchange="onRaceChange(this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                                </select>
                            </div>
                        </div>
                        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Classe</label>
                                <select id="char-class" onchange="onClassChange(this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                                </select>
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Divindade (Opcional)</label>
                                <select id="char-deity" onchange="onDeityChange(this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                                </select>
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Título</label>
                                <select id="char-title" onchange="onTitleChange(this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                                </select>
                            </div>
                        </div>
                        <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Profissão</label>
                                <input type="text" id="char-profession" oninput="updateCharInfo('profession', this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Altura</label>
                                <input type="text" id="char-height" oninput="updateCharInfo('height', this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Peso</label>
                                <input type="text" id="char-weight" oninput="updateCharInfo('weight', this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100">
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 mb-1">Rank</label>
                                <input type="text" id="char-rank" oninput="updateCharInfo('rank', this.value)" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100 text-center font-bold text-amber-400">
                            </div>
                        </div>
                        <div>
                            <label class="block text-xs font-medium text-gray-400 mb-1">História do Herói</label>
                            <textarea id="char-history" oninput="updateCharInfo('history', this.value)" rows="2" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-2 text-gray-100 text-sm"></textarea>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-4">
                            <h3 class="text-xl font-bold font-cinzel text-amber-400 border-b border-gray-700 pb-2">Status de Batalha</h3>
                            <div class="grid grid-cols-2 gap-4">
                                <div class="bg-gray-900 p-3 rounded-xl border border-gray-700 text-center">
                                    <span class="text-xs text-gray-400 block">HP (Vida)</span>
                                    <span id="stat-hp" class="text-xl font-bold text-red-400">20 / 20</span>
                                </div>
                                <div class="bg-gray-900 p-3 rounded-xl border border-gray-700 text-center">
                                    <span class="text-xs text-gray-400 block">MANA</span>
                                    <span id="stat-mana" class="text-xl font-bold text-blue-400">10 / 10</span>
                                </div>
                                <div class="bg-gray-900 p-3 rounded-xl border border-gray-700 text-center">
                                    <span class="text-xs text-gray-400 block">SANIDADE</span>
                                    <span id="stat-san" class="text-xl font-bold text-purple-400">5</span>
                                </div>
                                <div class="bg-gray-900 p-3 rounded-xl border border-gray-700 text-center">
                                    <span class="text-xs text-gray-400 block">DEFESA FÍSICA</span>
                                    <span id="stat-def" class="text-xl font-bold text-emerald-400">10</span>
                                </div>
                            </div>
                        </div>
                        <!-- SETOR DE ATRIBUTOS COM BÔNUS CALCULADOS -->
                        <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-4">
                            <div class="flex justify-between items-center border-b border-gray-700 pb-2">
                                <h3 class="text-xl font-bold font-cinzel text-amber-400">Atributos do Herói</h3>
                                <span class="text-xs px-2.5 py-1 bg-amber-600/35 border border-amber-600/50 text-amber-300 rounded font-semibold">Livres: <span id="stat-free-points">5</span></span>
                            </div>
                            <div id="attributes-container" class="space-y-3 max-h-64 overflow-y-auto pr-1">
                                <!-- Renderizado via JS -->
                            </div>
                        </div>
                    </div>
                    <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-4">
                        <div class="flex justify-between items-center border-b border-gray-700 pb-2">
                            <h3 class="text-xl font-bold font-cinzel text-amber-400">⚡ Habilidades</h3>
                            <button onclick="openAddSkillModal()" class="text-xs px-3 py-1.5 bg-amber-600 hover:bg-amber-500 text-white rounded-lg font-semibold shadow">➕ Criar Habilidade</button>
                        </div>
                        <div id="skills-list" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                            <!-- Renderizado via JS -->
                        </div>
                    </div>
                    <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-4">
                        <div class="flex justify-between items-center border-b border-gray-700 pb-2">
                            <h3 class="text-xl font-bold font-cinzel text-amber-400">✨ Magias</h3>
                            <button onclick="openAddSpellModal()" class="text-xs px-3 py-1.5 bg-amber-600 hover:bg-amber-500 text-white rounded-lg font-semibold shadow">➕ Criar Magia</button>
                        </div>
                        <div id="spells-list" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                            <!-- Renderizado via JS -->
                        </div>
                    </div>
                    <!-- INVENTÁRIO COM ABAS SEPARADAS -->
                    <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-4">
                        <div class="flex justify-between items-center border-b border-gray-700 pb-2">
                            <h3 class="text-xl font-bold font-cinzel text-amber-400">🎒 Inventário do Herói</h3>
                            <div class="flex gap-2">
                                <button onclick="openEquipmentLibraryModal()" class="text-xs px-3 py-1.5 bg-gray-700 hover:bg-gray-600 text-amber-400 rounded-lg font-semibold shadow border border-amber-600/30">📖 Biblioteca de Itens</button>
                                <button onclick="openAddItemModal()" class="text-xs px-3 py-1.5 bg-amber-600 hover:bg-amber-500 text-white rounded-lg font-semibold shadow">➕ Item Manual</button>
                            </div>
                        </div>                    
                        <!-- Sub-abas do Inventário -->
                        <div class="flex flex-wrap gap-2 pt-1 border-b border-gray-700 pb-3">
                            <button onclick="switchInventorySubTab('weapons')" id="inv-tab-weapons" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-amber-600 text-white">⚔️ Armas</button>
                            <button onclick="switchInventorySubTab('armors')" id="inv-tab-armors" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-900 text-gray-300 hover:bg-gray-700">🛡️ Armaduras e Escudos</button>
                            <button onclick="switchInventorySubTab('resources')" id="inv-tab-resources" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-900 text-gray-300 hover:bg-gray-700">🪵 Recursos Diversos</button>
                            <button onclick="switchInventorySubTab('consumables')" id="inv-tab-consumables" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-900 text-gray-300 hover:bg-gray-700">🧪 Consumíveis</button>
                        </div>
                        <!-- Conteúdo do Inventário -->
                        <div id="inventory-content-container" class="space-y-3 min-h-[160px]">
                            <!-- Renderizado via JS -->
                        </div>
                    </div>
                </div>
                <div class="space-y-6">
                    <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-4">
                        <h3 class="text-lg font-bold font-cinzel text-amber-400 border-b border-gray-700 pb-2">Guia do Multiverso</h3>
                        <div class="space-y-3 text-xs text-gray-300">
                            <div class="p-3 bg-gray-900 rounded-xl border border-gray-700">
                                <span class="font-bold text-amber-400 block mb-1">🎒 Inventário Organizado</span>
                                <p>Gerencie armas, armaduras, recursos e consumíveis divididos por categorias temáticas.</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- ================= TAB: COMÉRCIO & NEGÓCIOS ================= -->
        <div id="tab-trade" class="hidden space-y-6">
            <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-6">
                <div class="flex flex-wrap justify-between items-center gap-4 border-b border-gray-700 pb-4">
                    <div>
                        <h2 class="text-2xl font-bold font-cinzel text-amber-400">Sistema de Comércio & Carreira Mercantil</h2>
                        <p class="text-sm text-gray-400">Evolua sua carreira como Funcionário (Vendedor) ou Dono de Negócio (Comerciante) para acumular fama, bônus de Carisma e lucros.</p>
                    </div>
                    <div class="bg-gray-900 px-4 py-2 rounded-xl border border-gray-700 flex items-center gap-3">
                        <span class="text-xs text-gray-400">Herói Selecionado:</span>
                        <span id="trade-active-char-name" class="font-bold text-amber-400 text-sm">Nenhum</span>
                    </div>
                </div>
                <!-- Seletor de Caminho de Carreira -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-gray-900 border border-gray-700 rounded-xl p-5 space-y-4 shadow-inner flex flex-col justify-between">
                        <div class="space-y-3">
                            <div class="flex justify-between items-center">
                                <h3 class="text-lg font-bold font-cinzel text-amber-400">💼 Vendedor (Funcionário)</h3>
                                <select id="trade-seller-level" onchange="updateTradeCareer('seller', this.value)" class="bg-gray-950 border border-gray-700 rounded-lg p-2 text-xs text-amber-300 font-semibold focus:outline-none">
                                    <option value="1">Nível 1 - Novato</option>
                                    <option value="2">Nível 2 - Caixeiro-Viajante</option>
                                    <option value="3">Nível 3 - Especialista</option>
                                    <option value="4">Nível 4 - Negociador Estrela</option>
                                    <option value="5">Nível 5 - Lenda das Vendas</option>
                                </select>
                            </div>
                            <p class="text-xs text-gray-400">Progride acumulando fama através do contato direto com clientes, lábia e comissões.</p>                          
                            <div id="seller-details-box" class="p-3 bg-gray-950 rounded-lg border border-gray-800 space-y-2 text-xs text-gray-300">
                                <!-- Preenchido via JS -->
                            </div>
                        </div>
                        <button onclick="simulateTradeAction('seller')" class="w-full py-2 bg-amber-600 hover:bg-amber-500 text-white font-semibold text-xs rounded-lg shadow transition">Trabalhar como Vendedor (+ Fama)</button>
                    </div>
                    <div class="bg-gray-900 border border-gray-700 rounded-xl p-5 space-y-4 shadow-inner flex flex-col justify-between">
                        <div class="space-y-3">
                            <div class="flex justify-between items-center">
                                <h3 class="text-lg font-bold font-cinzel text-amber-400">🏛️ Comerciante (Dono)</h3>
                                <select id="trade-merchant-level" onchange="updateTradeCareer('merchant', this.value)" class="bg-gray-950 border border-gray-700 rounded-lg p-2 text-xs text-amber-300 font-semibold focus:outline-none">
                                    <option value="1">Nível 1 - Lojista de Esquina</option>
                                    <option value="2">Nível 2 - Empreendedor</option>
                                    <option value="3">Nível 3 - Marca Regional</option>
                                    <option value="4">Nível 4 - Magnata</option>
                                    <option value="5">Nível 5 - Imperador do Comércio</option>
                                </select>
                            </div>
                            <p class="text-xs text-gray-400">Progride expandindo negócios, contratando vendedores e ditando o valor da economia.</p>                         
                            <div id="merchant-details-box" class="p-3 bg-gray-950 rounded-lg border border-gray-800 space-y-2 text-xs text-gray-300">
                                <!-- Preenchido via JS -->
                            </div>
                        </div>
                        <button onclick="simulateTradeAction('merchant')" class="w-full py-2 bg-amber-600 hover:bg-amber-500 text-white font-semibold text-xs rounded-lg shadow transition">Gerenciar Negócio / Coletar Lucros</button>
                    </div>
                </div>
            </div>
        </div>
        <!-- ================= TAB 3: GERENCIADOR DE FICHAS ================= -->
        <div id="tab-manager" class="hidden space-y-6">
            <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl">
                <div class="flex flex-wrap justify-between items-center gap-4 mb-6">
                    <div>
                        <h2 class="text-2xl font-bold font-cinzel text-amber-400">Repositório de Heróis</h2>
                        <p class="text-sm text-gray-400">Gerencie, busque e acesse todas as suas fichas criadas no navegador.</p>
                    </div>
                    <div class="flex gap-3">
                        <button onclick="createNewCharacter(); switchTab('sheet');" class="px-4 py-2 bg-amber-600 hover:bg-amber-500 text-white font-semibold rounded-xl shadow transition">➕ Criar Novo Herói</button>
                    </div>
                </div>
                <div class="mb-6">
                    <input type="text" id="manager-search" oninput="renderCharacterManager()" placeholder="🔍 Pesquisar herói por nome, raça ou classe..." class="w-full bg-gray-900 border border-gray-700 rounded-xl p-3 text-gray-100 focus:outline-none focus:border-amber-500">
                </div>
                <div id="manager-character-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                </div>
            </div>
        </div>
        <!-- ================= TAB 4: CAMPANHAS ================= -->
        <div id="tab-campaigns" class="hidden space-y-6">
            <div class="bg-gray-800/80 border border-gray-700 rounded-2xl p-6 shadow-xl space-y-6">
                <div class="flex flex-wrap justify-between items-center gap-4 border-b border-gray-700 pb-4">
                    <div>
                        <h2 class="text-2xl font-bold font-cinzel text-amber-400">Campanhas na Nuvem (Mesa de RPG)</h2>
                        <p class="text-sm text-gray-400">Crie ou participe de uma campanha para o Mestre e os jogadores visualizarem as fichas em tempo real.</p>
                    </div>
                    <div class="flex gap-3">
                        <button onclick="openCreateCampaignModal()" class="px-4 py-2 bg-amber-600 hover:bg-amber-500 text-white font-semibold rounded-xl shadow transition">🏰 Criar Campanha (Mestre)</button>
                        <button onclick="openJoinCampaignModal()" class="px-4 py-2 bg-gray-700 hover:bg-gray-600 text-white font-semibold rounded-xl shadow transition">🔗 Entrar com Código</button>
                    </div>
                </div>
                <div id="active-campaign-panel" class="space-y-6">
                    <div class="text-center py-12 text-gray-500">
                        <span class="text-4xl block mb-2">📜</span>
                        <p class="text-lg font-medium">Nenhuma campanha conectada no momento.</p>
                    </div>
                </div>
            </div>
        </div>
    </main>
    <!-- Modals -->
    <div id="modal-xp" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-gray-900 border border-gray-700 rounded-2xl p-6 max-w-md w-full shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <h3 class="text-lg font-bold font-cinzel text-amber-400">Calculadora de XP de Combate</h3>
                <button onclick="closeXPCalculatorModal()" class="text-gray-400 hover:text-white font-bold">✕</button>
            </div>
            <div class="space-y-3">
                <div>
                    <label class="block text-xs font-medium text-gray-400 mb-1">Nível da Criatura / Inimigo</label>
                    <input type="number" id="xp-calc-level" value="5" min="1" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2.5 text-gray-100">
                </div>
                <div>
                    <label class="block text-xs font-medium text-gray-400 mb-1">Vida (HP) Total da Criatura</label>
                    <input type="number" id="xp-calc-hp" value="50" min="1" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2.5 text-gray-100">
                </div>
                <div>
                    <label class="block text-xs font-medium text-gray-400 mb-1">Raridade / Categoria</label>
                    <select id="xp-calc-rarity" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2.5 text-gray-100">
                        <option value="1.0">Comum (Multiplicador 1.0)</option>
                        <option value="1.2">Incomum (Multiplicador 1.2)</option>
                        <option value="1.5">Rara / Besta (Multiplicador 1.5)</option>
                        <option value="2.0">Mini Boss (Multiplicador 2.0)</option>
                        <option value="3.0">Boss (Multiplicador 3.0)</option>
                    </select>
                </div>
                <div class="bg-gray-950 p-3 rounded-xl border border-gray-800 text-center">
                    <span class="text-xs text-gray-400 block">XP Calculado:</span>
                    <span id="xp-calc-result" class="text-2xl font-extrabold text-amber-400">250 XP</span>
                </div>
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="calculateXPResult()" class="flex-1 bg-gray-800 hover:bg-gray-700 text-gray-200 py-2.5 rounded-xl font-semibold">Calcular</button>
                <button onclick="applyCalculatedXP()" class="flex-1 bg-amber-600 hover:bg-amber-500 text-white py-2.5 rounded-xl font-semibold">Adicionar à Ficha</button>
            </div>
        </div>
    </div>
    <!-- Modal Detalhes da Magia -->
    <div id="modal-spell-details" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-gray-900 border border-gray-700 rounded-2xl p-6 max-w-md w-full shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <h3 class="text-lg font-bold font-cinzel text-amber-400">Detalhes da Magia</h3>
                <button onclick="closeSpellModal()" class="text-gray-400 hover:text-white font-bold">✕</button>
            </div>
            <div id="spell-modal-content"></div>
            <div class="pt-2 flex justify-end">
                <button onclick="closeSpellModal()" class="px-4 py-2 bg-amber-600 hover:bg-amber-500 text-white rounded-xl text-xs font-semibold">Fechar</button>
            </div>
        </div>
    </div>
    <!-- Modal Detalhes da Habilidade -->
    <div id="modal-skill-details" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-gray-900 border border-gray-700 rounded-2xl p-6 max-w-md w-full shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <h3 class="text-lg font-bold font-cinzel text-amber-400">Detalhes da Habilidade</h3>
                <button onclick="closeSkillModal()" class="text-gray-400 hover:text-white font-bold">✕</button>
            </div>
            <div id="skill-modal-content"></div>
            <div class="pt-2 flex justify-end">
                <button onclick="closeSkillModal()" class="px-4 py-2 bg-amber-600 hover:bg-amber-500 text-white rounded-xl text-xs font-semibold">Fechar</button>
            </div>
        </div>
    </div>
    <!-- Modal Adicionar Item ao Inventário -->
    <div id="modal-add-item" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-gray-900 border border-gray-700 rounded-2xl p-6 max-w-md w-full shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <h3 class="text-lg font-bold font-cinzel text-amber-400">Adicionar Item Manual</h3>
                <button onclick="closeModal('modal-add-item')" class="text-gray-400 hover:text-white font-bold">✕</button>
            </div>
            <div class="space-y-3 text-xs">
                <div>
                    <label class="block text-gray-400 mb-1">Categoria do Item</label>
                    <select id="newItem-category" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2 text-gray-100">
                        <option value="weapons">⚔️ Arma</option>
                        <option value="armors">🛡️ Armadura / Escudo / Acessório</option>
                        <option value="resources">🪵 Recurso Diverso / Ferramenta</option>
                        <option value="consumables">🧪 Consumível</option>
                    </select>
                </div>
                <div>
                    <label class="block text-gray-400 mb-1">Nome do Item</label>
                    <input type="text" id="newItem-name" placeholder="Ex: Espada Curta de Ferro" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2 text-gray-100">
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-gray-400 mb-1">Atributo Chave / Tipo</label>
                        <input type="text" id="newItem-type" placeholder="Força / Corte" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2 text-gray-100">
                    </div>
                    <div>
                        <label class="block text-gray-400 mb-1">Dano / Efeito</label>
                        <input type="text" id="newItem-effect" placeholder="1d6 + 1" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2 text-gray-100">
                    </div>
                </div>
                <div>
                    <label class="block text-gray-400 mb-1">Descrição / Utilidade</label>
                    <textarea id="newItem-desc" rows="2" placeholder="Detalhes do equipamento..." class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2 text-gray-100"></textarea>
                </div>
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="closeModal('modal-add-item')" class="flex-1 bg-gray-800 hover:bg-gray-700 text-gray-200 py-2.5 rounded-xl font-semibold text-xs">Cancelar</button>
                <button onclick="saveNewInventoryItem()" class="flex-1 bg-amber-600 hover:bg-amber-500 text-white py-2.5 rounded-xl font-semibold text-xs">Salvar Item</button>
            </div>
        </div>
    </div>
    <!-- Modal Biblioteca de Equipamentos -->
    <div id="modal-equipment-library" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-gray-900 border border-gray-700 rounded-2xl p-6 max-w-2xl w-full shadow-2xl space-y-4 max-h-[85vh] flex flex-col">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <div>
                    <h3 class="text-lg font-bold font-cinzel text-amber-400">📖 Biblioteca de Equipamentos</h3>
                    <p class="text-xs text-gray-400">Selecione itens oficiais do acervo para adicionar diretamente à sua ficha.</p>
                </div>
                <button onclick="closeModal('modal-equipment-library')" class="text-gray-400 hover:text-white font-bold">✕</button>
            </div>        
            <div class="flex flex-wrap gap-2 pb-2 border-b border-gray-800">
                <button onclick="switchLibraryCategory('weapons')" id="lib-tab-weapons" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-amber-600 text-white">⚔️ Armas</button>
                <button onclick="switchLibraryCategory('armors')" id="lib-tab-armors" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-950 text-gray-300 hover:bg-gray-800">🛡️ Armaduras e Escudos</button>
                <button onclick="switchLibraryCategory('resources')" id="lib-tab-resources" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-950 text-gray-300 hover:bg-gray-800">🪵 Recursos e Ferramentas</button>
                <button onclick="switchLibraryCategory('consumables')" id="lib-tab-consumables" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-950 text-gray-300 hover:bg-gray-800">🧪 Consumíveis</button>
            </div>
            <div class="mb-3">
                <input type="text" id="library-search" oninput="renderLibraryItems()" placeholder="🔍 Pesquisar na biblioteca..." class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2 text-xs text-gray-100 focus:outline-none focus:border-amber-500">
            </div>
            <div id="library-items-container" class="space-y-2 overflow-y-auto pr-1 flex-1 min-h-[260px] max-h-[40vh]">
                <!-- Renderizado dinamicamente -->
            </div>
            <div class="pt-2 flex justify-end border-t border-gray-800">
                <button onclick="closeModal('modal-equipment-library')" class="px-4 py-2 bg-gray-800 hover:bg-gray-700 text-gray-200 rounded-xl text-xs font-semibold">Fechar</button>
            </div>
        </div>
    </div>
    <!-- Modal Criar Campanha -->
    <div id="modal-campaign-create" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-gray-900 border border-gray-700 rounded-2xl p-6 max-w-md w-full shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <h3 class="text-lg font-bold font-cinzel text-amber-400">Criar Nova Campanha (Mestre)</h3>
                <button onclick="closeModal('modal-campaign-create')" class="text-gray-400 hover:text-white font-bold">✕</button>
            </div>
            <div class="space-y-3 text-xs">
                <div>
                    <label class="block text-gray-400 mb-1">Nome da Campanha</label>
                    <input type="text" id="new-campaign-name" placeholder="Ex: As Crônicas de Eldoria" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2.5 text-gray-100">
                </div>
                <div>
                    <label class="block text-gray-400 mb-1">Sinopse / Descrição</label>
                    <textarea id="new-campaign-desc" rows="3" placeholder="Resumo da aventura..." class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2.5 text-gray-100"></textarea>
                </div>
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="closeModal('modal-campaign-create')" class="flex-1 bg-gray-800 hover:bg-gray-700 text-gray-200 py-2.5 rounded-xl font-semibold text-xs">Cancelar</button>
                <button onclick="createCampaignAction()" class="flex-1 bg-amber-600 hover:bg-amber-500 text-white py-2.5 rounded-xl font-semibold text-xs">Criar Mesa</button>
            </div>
        </div>
    </div>
    <!-- Modal Entrar em Campanha -->
    <div id="modal-campaign-join" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-gray-900 border border-gray-700 rounded-2xl p-6 max-w-md w-full shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <h3 class="text-lg font-bold font-cinzel text-amber-400">Entrar em Campanha Existente</h3>
                <button onclick="closeModal('modal-campaign-join')" class="text-gray-400 hover:text-white font-bold">✕</button>
            </div>
            <div class="space-y-3 text-xs">
                <div>
                    <label class="block text-gray-400 mb-1">Código / ID da Campanha</label>
                    <input type="text" id="join-campaign-id" placeholder="Ex: MESA-98762" class="w-full bg-gray-950 border border-gray-700 rounded-lg p-2.5 text-gray-100">
                </div>
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="closeModal('modal-campaign-join')" class="flex-1 bg-gray-800 hover:bg-gray-700 text-gray-200 py-2.5 rounded-xl font-semibold text-xs">Cancelar</button>
                <button onclick="joinCampaignAction()" class="flex-1 bg-amber-600 hover:bg-amber-500 text-white py-2.5 rounded-xl font-semibold text-xs">Conectar</button>
            </div>
        </div>
    </div>
    <!-- App Logic Script -->
    <script>
        // Global state initialization to fix ReferenceError
        let characters = JSON.parse(localStorage.getItem('rpg_characters')) || [];
        let transactionHistory = JSON.parse(localStorage.getItem('rpg_history')) || [];
        let activeCharacterId = characters.length > 0 ? characters[0].id : null;
        let activeInvSubTab = 'weapons';
        let activeLibraryCategory = 'weapons';
        const DEITIES_DATABASE = {
            "chronar": { title: "Deus do Tempo", desc: "Senhor das eras e da temporalidade." },
            "elyndra": { title: "Deusa da Vida", desc: "Protetora da flora, fauna e da vitalidade." },
            "morvakar": { title: "Deus da Morte", desc: "Guardião do repouso eterno e do submundo." },
            "vaelthor": { title: "Deus da Guerra", desc: "Patrono dos campos de batalha e da bravura." },
            "seraphyne": { title: "Deusa da Magia", desc: "Fonte suprema das artes arcanas e do éter." }
        };
        const RACES_DATABASE = {
            "Humanos": { desc: "Estatura média entre 1,50m e 1,90m.", ability: "Adaptabilidade: Uma vez por combate, pode repetir um teste ou ataque falho recebendo +2 de bônus.", attrs: { Força: 1, Agilidade: 1, Intelecto: 1, Carisma: 1, Vigor: -1, Sanidade: -1, Éter: -1 } },
            "Meio-Elfos": { desc: "Estrutura humana com refinamento élfico.", ability: "Forja Precisa: Recebe +3 de dano nas armas forjadas através da alquimia ou magia.", attrs: { Força: -1, Agilidade: 1, Intelecto: 3, Carisma: -1, Vigor: -1, Sanidade: -1, Éter: 1 } },
            "Fadas": { desc: "Seres diminutos de 30 a 50cm com asas translúcidas.", ability: "Asas Encantadas: Aumenta deslocamento em +3m e recebe +2 em testes de esquiva no ar.", attrs: { Força: -1, Agilidade: -1, Intelecto: 2, Carisma: -1, Vigor: -1, Sanidade: 2, Éter: 4 } },
            "Elfos": { desc: "Esbeltos, ágeis e de postura irrepreensível.", ability: "Sentidos Aguçados: +2 fixo em Percepção e +2 na Iniciativa.", attrs: { Força: -1, Agilidade: 1, Intelecto: 4, Carisma: 3, Vigor: -1, Sanidade: 1, Éter: 3 } },
            "Orcs": { desc: "Corpulentos e musculosos (1,90m a 2,20m) com presas.", ability: "Golpe Devastador: Ataques corpo a corpo críticos adicionam +1 dado de dano extra.", attrs: { Força: 4, Agilidade: 1, Intelecto: -1, Carisma: 1, Vigor: 4, Sanidade: -1, Éter: -1 } },
            "Gigantes": { desc: "Mais de sete metros de altura, pele cinzenta de granito.", ability: "Passo Sísmico: Golpeia o chão causando 1d8+Força de impacto em 3 metros ao redor.", attrs: { Força: 4, Agilidade: -6, Intelecto: -1, Carisma: 1, Vigor: 4, Sanidade: -3, Éter: 1 } },
            "Anões": { desc: "Baixos (1,20m a 1,40m) mas densos e barbudos.", ability: "Pele de Pedra: Recebe Redução de Dano igual ao Vigor contra corte, perfuração e impacto.", attrs: { Força: 3, Agilidade: -1, Intelecto: 3, Carisma: 1, Vigor: -1, Sanidade: 1, Éter: -8 } },
            "Dragonatos": { desc: "Humanoides cobertos por escamas espessas.", ability: "Sopro Dragônico: Expele energia elemental em cone de 4,5m causando 1d12+Magia.", attrs: { Força: 1, Agilidade: 1, Intelecto: 3, Carisma: -1, Vigor: 1, Sanidade: 1, Éter: 4 } },
            "Kitsune": { desc: "Elegante figura humana com orelhas felpudas e caudas.", ability: "Ilusão Natural: Cria cópia ilusória, concedendo +4 em Defesa/Esquiva (gasta 5 mana).", attrs: { Força: -8, Agilidade: 3, Intelecto: 1, Carisma: 3, Vigor: -1, Sanidade: 1, Éter: 4 } },
            "Aasimar": { desc: "Humanoides de traços simétricos e brilho opalescente.", ability: "Luz Divina: Restaura 2d4+2 HP ou causa dano radiante (2x/dia).", attrs: { Força: 1, Agilidade: 1, Intelecto: -1, Carisma: 1, Vigor: 1, Sanidade: 0, Éter: -2 } },
            "Tieflings": { desc: "Exibem chifres curvados e cauda muscular.", ability: "Chama Infernal: Envolve armas em fogo sombrio (+1d6 dano em crítico).", attrs: { Força: -1, Agilidade: 1, Intelecto: 1, Carisma: -1, Vigor: 1, Sanidade: 3, Éter: 4 } },
            "Meios-Orcs": { desc: "Físico forte e imponente de 1,80m a 2,00m.", ability: "Tenacidade Vigorosa: +2 em testes de Vigor e +3 de Vida máxima.", attrs: { Força: 2, Agilidade: 1, Intelecto: 3, Carisma: -4, Vigor: 1, Sanidade: -1, Éter: -6 } },
            "Meios-Gigantes": { desc: "Medem entre 2,20m e 2,50m de altura.", ability: "Estatura Imponente: +3 em testes de Força para empurrar, agarrar ou mover objetos.", attrs: { Força: 3, Agilidade: -3, Intelecto: 3, Carisma: -2, Vigor: 3, Sanidade: 3, Éter: -1 } },
            "Vampiros": { desc: "Tez extremamente pálida e elegância sobrenatural.", ability: "Sangue Dominante: Força teste de resistência no alvo e +2 Agilidade/Carisma.", attrs: { Força: -8, Agilidade: 5, Intelecto: -1, Carisma: 1, Vigor: 1, Sanidade: 1, Éter: 1 } },
            "Onis": { desc: "Gigantescos (2,10m a 2,60m) de pele colorida vibrante.", ability: "Peso Morto: +2 dano físico bruto em golpe corpo a corpo.", attrs: { Força: 3, Vigor: 1, Agilidade: 1, Sanidade: 0, Intelecto: 1, Carisma: -4, Éter: -4 } },
            "Seres Espirituais": { desc: "Silhuetas humanoides compostas por núcleo elemental.", ability: "Centelha Primordial: Manipula quantidade inofensiva de seu elemento de origem.", attrs: { Força: -1, Agilidade: 1, Intelecto: 3, Carisma: 1, Vigor: -1, Sanidade: -1, Éter: 4 } },
            "Errante": { desc: "Carcaças reanimadas por magia necrótica.", ability: "Fôlego do Túmulo: Imune a afogamento/veneno; ignora dor do primeiro ferimento.", attrs: { Força: 0, Agilidade: 0, Intelecto: 3, Carisma: -8, Vigor: 1, Sanidade: 1, Éter: 1 } },
            "Demonio Maior": { desc: "Humanos perfeitos com chifres discretos.", ability: "Ressonância Abissal: Força teste mental em raio de 6m, causando perda de Sanidade.", attrs: { Força: 1, Agilidade: 0, Intelecto: 1, Carisma: -3, Vigor: 1, Sanidade: -3, Éter: 2 } }
        };
        const CLASSES_DATABASE = {
            "Bárbaro": { 
                startingSkill: "Avanço Intimidador (Nvl 1): Empurra um inimigo até 3 metros para trás.", 
                startingSpell: { name: "Golpe Brutal", level: 1, type: "Físico", damage: "1d12 + Físico", desc: "O impacto do golpe é tão violento que desequilibra o alvo, reduzindo o deslocamento dele pela metade no próximo turno.", range: "Corpo a corpo (1,5m)", cost: "4 de Mana" } 
            },
            "Demolidor": { 
                startingSkill: "Identificar Fissura (Nvl 1): O próximo ataque aliado contra o alvo ignora resistências físicas.", 
                startingSpell: { name: "Romper Defesa", level: 1, type: "Físico / Tático", damage: "1d8 + Físico", desc: "Identifica falhas na armadura do inimigo usando o Intelectual. Ignora resistência física do alvo neste ataque.", range: "Corpo a corpo (1,5m)", cost: "5 de Mana" } 
            },
            "Necromante": { 
                startingSkill: "Sussurro do Além (Nvl 1): Extrai informação simples de cadáver recente.", 
                startingSpell: { name: "Toque do Túmulo", level: 1, type: "Magia Sombria", damage: "1d8 + Magia", desc: "Dano necrótico. O Necromante drena a vitalidade do alvo, curando a si mesmo o equivalente à metade do dano causado.", range: "Corpo a corpo (Toque)", cost: "6 de Mana" } 
            },
            "Monge": { 
                startingSkill: "Postura da Folha ao Vento (Nvl 1): Ignora terrenos difíceis e não provoca ataques de oportunidade.", 
                startingSpell: { name: "Palma Serena", level: 1, type: "Físico / Marcial", damage: "1d6 + Físico", desc: "Atinge pontos de pressão do alvo. O inimigo atingido sofre desvantagem em seu próximo ataque.", range: "Corpo a corpo (1,5m)", cost: "4 de Mana" } 
            },
            "Druida": { 
                startingSkill: "Crescimento Rasteiro (Nvl 1): Reduz o movimento de inimigos pela metade em área.", 
                startingSpell: { name: "Chicote de Espinhos", level: 1, type: "Magia da Natureza", damage: "1d8 + Magia", desc: "Cria uma vinha espinhosa que atinge o alvo e pode puxá-lo até 3 metros na direção do Druida.", range: "9 metros", cost: "5 de Mana" } 
            },
            "Paladino": { 
                startingSkill: "Égide do Protetor (Nvl 1): Redireciona para si o próximo ataque que acertaria um aliado.", 
                startingSpell: { name: "Golpe Iluminado", level: 1, type: "Físico / Divino", damage: "Dano da Arma + 1d6 Divindade", desc: "A arma brilha com poder sagrado. O alvo atingido irradia luz, impedindo que fique furtivo ou invisível por 1 turno.", range: "Corpo a corpo (1,5m)", cost: "5 de Mana" } 
            },
            "Escritor Rúnico": { 
                startingSkill: "Sigilo de Alerta (Nvl 1): Runa que explode em clarão de luz, cegando intrusos.", 
                startingSpell: { name: "Runa da Combustão", level: 1, type: "Magia Arcana", damage: "2d6 Fogo", desc: "Inscreve rapidamente uma runa no ar ou chão. Ela explode quando o alvo se aproxima ou é acionada pelo Escritor.", range: "6 metros", cost: "6 de Mana" } 
            },
            "Xamã": { 
                startingSkill: "Totem da Nevoeiro Dissipado (Nvl 1): Dissipa fumaça, gases e ilusões ao redor.", 
                startingSpell: { name: "Rajada Espiritual", level: 1, type: "Magia Espiritual", damage: "1d8 + Magia", desc: "Evoca um espírito ancestral que causa dano de frio e empurra o alvo 1,5m para trás.", range: "12 metros", cost: "5 de Mana" } 
            },
            "Mago": { 
                startingSkill: "Manipulação Menor (Nvl 1): Move pequenos objetos com a mente à distância.", 
                startingSpell: { name: "Dardo Arcano", level: 1, type: "Magia Arcana", damage: "1d10 + Magia", desc: "Dispara um feixe de pura lógica mágica. O ataque nunca erra se o alvo estiver visível e fora de cobertura total.", range: "18 metros", cost: "5 de Mana" } 
            },
            "Bardo": { 
                startingSkill: "Acorde Dissonante (Nvl 1): Nota estridente que causa surdez temporária e bloqueia reações.", 
                startingSpell: { name: "Acorde Dissonante", level: 1, type: "Magia Ilusória", damage: "1d6 + Magia", desc: "Emite um som mágico e estridente. O alvo sofre dano psíquico e fica atordoado temporariamente, perdendo sua reação.", range: "12 metros", cost: "5 de Mana" } 
            },
            "Engenheiro": { 
                startingSkill: "Gancho Magnético/Retrátil (Nvl 1): Puxa o personagem ou desarma item do inimigo.", 
                startingSpell: { name: "Granada Básica", level: 1, type: "Tecnológico", damage: "1d6 + Intelectual", desc: "Arremessa um explosivo caseiro que atinge uma pequena área. Inimigos na área sofrem dano de fragmentação.", range: "9 metros", cost: "6 de Mana" } 
            },
            "Clérigo": { 
                startingSkill: "Presença Apaziguadora (Nvl 1): Estabiliza imediatamente aliado sangrando.", 
                startingSpell: { name: "Chama Sagrada", level: 1, type: "Magia Divina", damage: "1d8 + Divindade", desc: "Faz chamas celestiais caírem sobre o inimigo. Se o alvo for uma criatura maligna/profana, causa 1d4 de dano extra.", range: "12 metros", cost: "5 de Mana" } 
            },
            "Bruxo": { 
                startingSkill: "Falso Vislumbre (Nvl 1): Manipula mente do alvo para criar aberturas.", 
                startingSpell: { name: "Raio Agonizante", level: 1, type: "Magia Oculta", damage: "1d10 + Magia", desc: "Dispara um feixe de energia corrompida. O alvo afetado não pode receber cura até o fim do seu próximo turno.", range: "18 metros", cost: "6 de Mana" } 
            },
            "Ladino": { 
                startingSkill: "Truque de Fumaça (Nvl 1): Arremessa bomba de fumaça bloqueando linha de visão.", 
                startingSpell: { name: "Corte Venenoso", level: 1, type: "Físico / Furtivo", damage: "Dano da Arma + 1d4", desc: "Um ataque rápido em pontos vitais. Causa sangramento ou envenenamento, infligindo 1d4 de dano no início do turno do alvo.", range: "Corpo a corpo (1,5m)", cost: "4 de Mana" } 
            },
            "Besta": { 
                startingSkill: "Faro Predatório (Nvl 1): Fareja sangue e rastreia alvos invisíveis.", 
                startingSpell: { name: "Presas Predatórias", level: 1, type: "Físico / Selvagem", damage: "1d8 + Vigor", desc: "Um ataque feroz usando garras ou presas. Se o ataque acertar, a Besta pode tentar agarrar o oponente como ação livre.", range: "Corpo a corpo (1,5m)", cost: "4 de Mana" } 
            },
            "Cavaleiro": { 
                startingSkill: "Ordem de Manobra (Nvl 1): Permite aliado se mover imediatamente com reação.", 
                startingSpell: { name: "Grito de Comando", level: 1, type: "Físico / Tático", damage: "Dano da Arma + 2", desc: "Um ataque coordenado que inspira os aliados. O aliado mais próximo ganha +1 na rolagem de ataque do seu próximo turno.", range: "Corpo a corpo (1,5m)", cost: "5 de Mana" } 
            },
            "Arqueiro": { 
                startingSkill: "Flecha Ancoradora (Nvl 1): Prende o alvo ao chão ou parede com uma flecha.", 
                startingSpell: { name: "Flecha Penetrante", level: 1, type: "Distância / Físico", damage: "Dano da Arma + Intelectual", desc: "Usando cálculos táticos, dispara uma flecha que ignora os bônus de cobertura leve e média do inimigo.", range: "24 metros", cost: "4 de Mana" } 
            },
            "Atirador Arcano": { 
                startingSkill: "Disparo Ilusório (Nvl 1): Projétil de luz pura que emite sons para despistar.", 
                startingSpell: { name: "Flecha Imbuída", level: 1, type: "Distância / Magia", damage: "Dano da Arma + 1d6 Magia", desc: "Funde magia ao projétil físico. A flecha causa dano elemental (fogo, frio ou raio) além do dano perfurante.", range: "24 metros", cost: "6 de Mana" } 
            },
            "Guerreiro": { 
                startingSkill: "Desarmar Tático (Nvl 1): Faz a arma do inimigo voar de suas mãos.", 
                startingSpell: { name: "Golpe Cíclico", level: 1, type: "Físico", damage: "Dano da Arma", desc: "Um ataque fluido. Após acertar o golpe, o Guerreiro assume postura defensiva, ganhando +2 de Defesa até o próximo turno.", range: "Corpo a corpo (1,5m)", cost: "5 de Mana" } 
            },
            "Pugilista": { 
                startingSkill: "Punho Repulsor Arcane (Nvl 1): Onda de choque de curto alcance.", 
                startingSpell: { name: "Soco Cinético", level: 1, type: "Físico / Magia", damage: "1d6 Físico + 1d4 Magia", desc: "Canaliza energia mística nos punhos. A força explosiva do impacto empurra o alvo 3 metros para trás.", range: "Corpo a corpo (1,5m)", cost: "5 de Mana" } 
            },
            "Alquimista": { 
                startingSkill: "Frasco Viscoso (Nvl 1): Gosma pegajosa que reduz movimento e pode ser inflamada.", 
                startingSpell: { name: "Frasco Ácido", level: 1, type: "Tecnológico / Químico", damage: "1d6 + Intelectual", desc: "Lança um frasco instável. O ácido corrói a armadura, diminuindo em 1 a Defesa do alvo até que ele seja limpo.", range: "9 metros", cost: "6 de Mana" } 
            },
            "Domador das Bestas": { 
                startingSkill: "Comando de Fustigar (Nvl 1): Ordena animal perturbar alvo, deixando-o Distraído.", 
                startingSpell: { name: "Ordem de Caça", level: 1, type: "Comando / Físico", damage: "1d6 + Carismático", desc: "O Domador marca um alvo. Sua fera ganha vantagem para atacar este alvo e causa dano extra baseado na sinergia.", range: "12 metros", cost: "5 de Mana" } 
            },
            "Forjador": { 
                startingSkill: "Ajuste Estrutural de Combate (Nvl 1): Aumenta defesa de aliado ou penetração de arma.", 
                startingSpell: { name: "Aço Aquecido", level: 1, type: "Suporte / Físico", damage: "Dano da Arma + 1d4 Fogo", desc: "Sobreaquece a própria arma ou a de um aliado. O próximo acerto dessa arma causa dano de fogo bônus e pode derreter escudos.", range: "Toque", cost: "5 de Mana" } 
            }
        };
        const SELLER_RANKS = {
            1: { title: "Novato", bonusCarisma: 1, effect: "Clientes locais toleram sua presença, mas ainda duvidam das suas promessas.", funds: "Salário base negociável." },
            2: { title: "Caixeiro-Viajante", bonusCarisma: 2, effect: "Algumas pessoas na cidade já o reconhecem pelo nome.", funds: "Salário base negociável + 5% de comissão por venda." },
            3: { title: "Especialista", bonusCarisma: 3, effect: "NPCs pedem para ser atendidos especificamente por você.", funds: "Salário base negociável + 10% de comissão." },
            4: { title: "Negociador Estrela", bonusCarisma: 4, effect: "Aristocratas e comerciantes ricos exigem sua consultoria pessoal.", funds: "Salário base negociável + 20% de comissão e bônus de metas." },
            5: { title: "Lenda das Vendas", bonusCarisma: 5, effect: "Sua palavra é garantia. Você pode vender gelo no deserto.", funds: "Salário alto + 35% de comissão. Acesso a clientes da realeza." }
        };
        const MERCHANT_RANKS = {
            1: { title: "Lojista de Esquina", bonusCarisma: 1, effect: "Conhecido apenas no próprio bairro. Mantém o negócio funcionando.", funds: "Lucro básico de loja local." },
            2: { title: "Empreendedor", bonusCarisma: 2, effect: "Fornecedores confiam em você e oferecem descontos iniciais.", funds: "Lucros moderados de expansão comercial." },
            3: { title: "Marca Regional", bonusCarisma: 3, effect: "O nome da sua empresa atrai clientes de outras cidades.", funds: "Pode gerenciar até 3 Vendedores. Lucros expressivos." },
            4: { title: "Magnata", bonusCarisma: 4, effect: "Líderes políticos convidam você para banquetes buscando favores.", funds: "Múltiplas filiais pelo reino. Riqueza substancial." },
            5: { title: "Imperador do Comércio", bonusCarisma: 5, effect: "Monopólio mercadológico. Sua marca dita o valor da moeda local.", funds: "Fundos praticamente ilimitados." }
        };
        // Helper function to get the currently active character object
        function getCharacter() {
            let char = characters.find(c => c.id === activeCharacterId);
            if (!char && characters.length > 0) {
                activeCharacterId = characters[0].id;
                char = characters[0];
            }
            if (!char) {
                char = createNewCharacterTemplate("Herói Principal");
                characters.push(char);
                activeCharacterId = char.id;
            }
            return char;
        }
        // Helper function to save characters and history to localStorage
        function saveToStorage() {
            localStorage.setItem('rpg_characters', JSON.stringify(characters));
            localStorage.setItem('rpg_history', JSON.stringify(transactionHistory));
        }
        const EQUIPMENT_LIBRARY = {
            weapons: [
                { name: "Clava de Madeira", type: "Arma de Contusão (Força)", effect: "1d6 + 1", desc: "Bastão de madeira maciça, simples e resistente." },
                { name: "Maça de Ferro Leve", type: "Arma de Contusão (Força)", effect: "1d6 + 2", desc: "Cabeça de ferro em cabo curto. Golpes sólidos e confiáveis." },
                { name: "Espada Curta de Ferro", type: "Arma de Corte (Força)", effect: "1d6 + 1", desc: "Lâmina reta e compacta. Boa para golpes diretos." },
                { name: "Machado de Lenhador", type: "Arma de Corte (Força)", effect: "1d8", desc: "Lâmina pesada em cabo médio. Corta bem e causa impacto forte." },
                { name: "Lança de Madeira com Ponta de Ferro", type: "Arma de Perfuração (Força)", effect: "1d6 + 1", desc: "Haste longa com ponta de ferro. Mantém inimigos à distância." },
                { name: "Martelo de Pedra", type: "Arma de Contusão (Força)", effect: "1d8", desc: "Cabeça de pedra polida fixada em cabo. Impacto pesado." },
                { name: "Porrete com Pregos", type: "Arma de Contusão/Corte (Força)", effect: "1d6 + 2", desc: "Clava de madeira com pregos afiados cravados. Brutal e simples." },
                { name: "Machado de Batalha Leve", type: "Arma de Corte (Força)", effect: "1d8", desc: "Lâmina dupla pequena. Equilíbrio entre peso e poder de corte." },
                { name: "Tridente Simples", type: "Arma de Perfuração (Força)", effect: "1d6 + 1", desc: "Três pontas de ferro em haste curta. Versátil e firme." },
                { name: "Espada de Treinamento", type: "Arma de Corte (Força)", effect: "1d6 + 1", desc: "Feita em aço mais macio. Usada por recrutas, mas funcional." },
                { name: "Adaga de Punhal", type: "Arma de Perfuração (Agilidade)", effect: "1d4 + 2", desc: "Pequena, afiada e fácil de esconder. Rápida no arremesso." },
                { name: "Arco Curto de Madeira", type: "Arma à Distância (Agilidade)", effect: "1d6", desc: "Arco simples de madeira flexível. Fácil de manusear e transportar." },
                { name: "Foice Curta", type: "Arma de Corte (Agilidade)", effect: "1d6 + 1", desc: "Lâmina curva e leve. Rápida para cortes rápidos." },
                { name: "Funda de Couro", type: "Arma à Distância (Agilidade)", effect: "1d4 + 1", desc: "Tira de couro para lançar pedras. Silenciosa e discreta." },
                { name: "Luvas de Couro com Pontas", type: "Arma de Corpo a Corpo (Agilidade)", effect: "1d4 + 2", desc: "Couro resistente com pontas de osso. Aumenta o impacto dos socos." },
                { name: "Dardos de Madeira", type: "Arma à Distância (Agilidade)", effect: "1d4 + 1", desc: "Pequenas lanças leves. Disparam rápido e com precisão modesta." },
                { name: "Adaga de Arremesso", type: "Arma de Perfuração (Agilidade)", effect: "1d4 + 1", desc: "Equilibrada para lançamentos. Afiada em uma ponta." },
                { name: "Bastão Curto", type: "Arma de Contusão (Agilidade)", effect: "1d6", desc: "Bastão de madeira leve. Usado para desvios e golpes rápidos." },
                { name: "Chicote de Couro", type: "Arma de Longo Alcance (Agilidade)", effect: "1d4 + 1", desc: "Tira de couro flexível. Pode desarmar inimigos." },
                { name: "Arpão Leve", type: "Arma à Distância (Agilidade)", effect: "1d6", desc: "Ponta de osso em haste curta. Boa em áreas fechadas." },
                { name: "Vara de Madeira Gravada", type: "Foco/Arma Simples (Intelecto)", effect: "1d4 +1 em avaliação", desc: "Vara lisa com marcas e medidas. Auxilia cálculos e projéteis." },
                { name: "Lança-Chamas Portátil Simples", type: "Dispositivo (Intelecto)", effect: "1d6 Fogo (1 uso)", desc: "Frasco com óleo e pavio acionável manualmente. Queima curta e perigosa." },
                { name: "Besta de Mão Ajustável", type: "Dispositivo de Arremesso (Intelecto)", effect: "1d6 (sem penalidade até 6m)", desc: "Pequena besta montada. Ajusta força do disparo." },
                { name: "Frasco de Ácido Fraco", type: "Arma Química (Intelecto)", effect: "1d3 + 1", desc: "Mistura corrosiva básica. Causa dano contínuo leve." },
                { name: "Vara de Sinalização", type: "Ferramenta (Intelecto)", effect: "1d4 e luz", desc: "Vara com espelhos e lentes. Cria luz ou sinais visuais." },
                { name: "Rede de Aço com Peso", type: "Dispositivo (Intelecto)", effect: "Desvantagem de movimento", desc: "Rede leve com pesos nas pontas para prender inimigos." },
                { name: "Dardos Envenenados Básicos", type: "Arma Química (Intelecto)", effect: "1d4 e desv. Força", desc: "Dardos com veneno não letal feito de plantas." },
                { name: "Estilingue de Precisão Aprimorada", type: "Dispositivo (Intelecto)", effect: "1d4 + 1 (ignora 1 def)", desc: "Estilingue com mira improvisada." },
                { name: "Vara de Salgueiro", type: "Foco Arcano (Magia)", effect: "1d4 mágico", desc: "Madeira flexível que conduz magia leve." },
                { name: "Cajado de Pinho Simples", type: "Foco Arcano (Magia)", effect: "1d6 mágico (-1 mana Nvl 1)", desc: "Madeira de pinho com cristal comum incrustado." },
                { name: "Varinha de Faia com Pedra Branca", type: "Foco Arcano (Magia)", effect: "1d4 + 1 mágico", desc: "Varinha pequena com pedra fosca." },
                { name: "Bastão de Carvalho com Runas", type: "Foco Arcano (Magia)", effect: "1d6 (+1 defesa)", desc: "Bastão resistente com runas básicas gravadas." },
                { name: "Varinha de Osso Polido", type: "Foco Arcano (Magia)", effect: "1d4 (ilusão +1 turno)", desc: "Osso liso que ressoa com magia sutil." },
                { name: "Cristal de Mão", type: "Foco Arcano (Magia)", effect: "1d4 + 1 mágico", desc: "Cristal pequeno que segura na palma." },
                { name: "Cajado de Videira Seca", type: "Foco Arcano (Magia)", effect: "1d6 (natureza +1 dano)", desc: "Enraíza levemente no chão ao conjurar." },
                { name: "Varinha de Ametista Bruta", type: "Foco Arcano (Magia)", effect: "1d4 (vantagem 1º atk)", desc: "Cristal bruto que brilha ao conjurar." }
            ],
            armors: [
                { name: "Túnica de Couro Cru", type: "Armadura Leve (Força)", effect: "Defesa +1", desc: "Couro simplesmente curtido, oferece proteção básica." },
                { name: "Escudo de Madeira", type: "Escudo (Força)", effect: "Defesa +2", desc: "Feito de madeira grossa, bloqueia golpes leves." },
                { name: "Cinto de Couro Reforçado", type: "Acessório (Força)", effect: "Força +1", desc: "Couro grosso com fivela de ferro, apoia a postura." },
                { name: "Botas de Marcha", type: "Calçado (Força)", effect: "Resistência +1", desc: "Couro grosso e solado reforçado para terrenos difíceis." },
                { name: "Braçadeiras de Couro", type: "Proteção de Braço (Força)", effect: "Defesa +1", desc: "Couro duro enrolado nos antebraços para amortecer golpes." },
                { name: "Escudo de Vime", type: "Escudo (Força)", effect: "Defesa +1", desc: "Entrançado de ramos, leve, mas quebra fácil." },
                { name: "Capa de Lã Grossa", type: "Vestimenta (Força)", effect: "Resistência +1", desc: "Lã espessa, protege do frio e arranhões leves." },
                { name: "Perneiras de Couro", type: "Proteção de Perna (Força)", effect: "Defesa +1", desc: "Couro duro cobrindo canelas, reduz feridas de impacto." },
                { name: "Bolsa de Cintura Reforçada", type: "Acessório (Força)", effect: "Capacidade +2", desc: "Couro grosso para carregar mais itens sem desconforto." },
                { name: "Faixa de Cabeça de Couro", type: "Acessório (Força)", effect: "Força +1 (testes físicos)", desc: "Absorve suor e mantém foco em esforços físicos." },
                { name: "Roupas de Tecido Leve", type: "Vestimenta (Agilidade)", effect: "Furtividade +1", desc: "Tecido fino e macio. Não atrapalha movimentos." },
                { name: "Botas de Couro Macio", type: "Calçado (Agilidade)", effect: "Furtividade +1", desc: "Solado fino e silencioso. Menos ruído ao andar." },
                { name: "Capa Escura", type: "Vestimenta (Agilidade)", effect: "Furtividade +2 (sombras)", desc: "Tecido escuro e leve. Ajuda a se esconder em sombras." },
                { name: "Cinto de Ferramentas Leves", type: "Acessório (Agilidade)", effect: "Destreza +1", desc: "Bolsos com ferramentas simples para fechaduras." },
                { name: "Luvas de Tecido Ajustadas", type: "Acessório (Agilidade)", effect: "Escalar +1", desc: "Tecido fino que não escorrega. Melhor pegada." },
                { name: "Mochila Leve de Couro", type: "Mochila (Agilidade)", effect: "Movimento normal", desc: "Pequena e leve. Não atrapalha movimentos rápidos." },
                { name: "Capuz de Tecido", type: "Acessório (Agilidade)", effect: "Furtividade +1", desc: "Cobre o rosto parcialmente. Dificulta reconhecimento." },
                { name: "Calçados de Solado de Lã", type: "Calçado (Agilidade)", effect: "Furtividade +1", desc: "Quase sem ruído em pisos lisos." },
                { name: "Faixas de Tecido nas Pernas", type: "Acessório (Agilidade)", effect: "Saltos +1", desc: "Ajudam em movimentos rápidos e saltos." },
                { name: "Bolsas de Cintura Pequenas", type: "Acessório (Agilidade)", effect: "Sacar rápido", desc: "Acessa itens rapidamente sem gastar movimento." },
                { name: "Capa de Tecido Encantado Leve", type: "Vestimenta (Magia)", effect: "Vantagem contra medo", desc: "Protege contra influências sobrenaturais fracas." },
                { name: "Amuleto de Proteção Menor", type: "Talismã (Magia)", effect: "+1 Defesa Mágica", desc: "Pedra com símbolo protetor simples." },
                { name: "Manto de Resistência Menor", type: "Vestimenta (Magia)", effect: "Reduz 1 dano elemental", desc: "Tratado com ervas protetoras." }
            ],
            resources: [
                { name: "Caderno de Anotações e Carvão", type: "Ferramenta (Intelecto)", effect: "Vantagem em lembrar", desc: "Registra observações e mapas." },
                { name: "Kit de Ferramentas de Oficial", type: "Ferramenta (Intelecto)", effect: "Vantagem em reparos", desc: "Alicates, lâminas e chaves para armadilhas." },
                { name: "Lupa de Vidro", type: "Ferramenta (Intelecto)", effect: "Vantagem em percepção", desc: "Examine pequenos detalhes e inscrições." },
                { name: "Mapa da Região + Caneta", type: "Documento (Intelecto)", effect: "+1 Navegação", desc: "Mapa desenhado com estradas e vilarejos." },
                { name: "Livro de Curiosidades Locais", type: "Livro (Intelecto)", effect: "Vantagem em conhecimento", desc: "Contém lendas, plantas e costumes." },
                { name: "Kit de Primeiros Socorros", type: "Médico (Intelecto)", effect: "Cura 1d4+1 PV", desc: "Curativos e ervas para ferimentos leves." },
                { name: "Régua e Compasso de Bolso", type: "Ferramenta (Intelecto)", effect: "Vantagem em estruturas", desc: "Instrumentos de medição." },
                { name: "Óculos de Lentes Simples", type: "Acessório (Intelecto)", effect: "Leitura e detecção", desc: "Melhora leitura e percepção à distância." },
                { name: "Frascos Vazios e Etiquetas", type: "Kit Químico (Intelecto)", effect: "Coleta substâncias", desc: "Frascos rotulados para amostras." },
                { name: "Tábua de Cálculos de Bolso", type: "Ferramenta (Intelecto)", effect: "Vantagem em lógica", desc: "Tabelas e fórmulas para contagens." },
                { name: "Bolsa de Componentes Básicos", type: "Kit Mágico (Magia)", effect: "Componentes ilimitados", desc: "Ervas e pós necessários para magias simples." },
                { name: "Diário de Estudos Arcanos", type: "Grimório (Magia)", effect: "+1 Identificar magias", desc: "Anotações sobre limites arcanos." },
                { name: "Livro de Magias Básicas", type: "Grimório (Magia)", effect: "Recupera 1 magia", desc: "Contém 4 magias simples de nível 1." }
            ],
            consumables: [
                { name: "Vela Aromática de Concentração", type: "Consumível (Magia)", effect: "Vantagem ao estudar (1h)", desc: "Ajuda a manter foco durante estudos." },
                { name: "Pó de Iluminação", type: "Consumível (Magia)", effect: "Luz sem chama (3 usos)", desc: "Acende como uma tocha por 1 hora." },
                { name: "Frasco de Água Benta Menor", type: "Consumível (Magia)", effect: "1d6 dano sombrio", desc: "Água abençoada contra criaturas sombrias." },
                { name: "Pó de Fumaça", type: "Mistura Química (Intelecto)", effect: "Névoa em pequena área", desc: "Saco que rompe ao impacto, obscurece visão." }
            ]
        };
        window.openEquipmentLibraryModal = function() {
            renderLibraryItems();
            document.getElementById('modal-equipment-library').classList.remove('hidden');
        };
        window.switchLibraryCategory = function(cat) {
            activeLibraryCategory = cat;
            ['weapons', 'armors', 'resources', 'consumables'].forEach(c => {
                const btn = document.getElementById(`lib-tab-${c}`);
                if (btn) {
                    btn.className = c === cat ? "px-3 py-1.5 rounded-lg text-xs font-semibold bg-amber-600 text-white" : "px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-950 text-gray-300 hover:bg-gray-800";
                }
            });
            renderLibraryItems();
        };
        window.renderLibraryItems = function() {
            const query = (document.getElementById('library-search').value || '').toLowerCase();
            const container = document.getElementById('library-items-container');
            const items = EQUIPMENT_LIBRARY[activeLibraryCategory] || [];
            const filtered = items.filter(i => i.name.toLowerCase().includes(query) || i.type.toLowerCase().includes(query) || i.desc.toLowerCase().includes(query));
            if (filtered.length === 0) {
                container.innerHTML = '<p class="text-gray-500 italic text-xs text-center py-6">Nenhum item encontrado na biblioteca.</p>';
                return;
            }
            container.innerHTML = filtered.map(item => `
                <div class="p-3 bg-gray-950 rounded-xl border border-gray-800 flex justify-between items-center gap-3">
                    <div class="space-y-1">
                        <div class="flex items-center gap-2">
                            <span class="font-bold text-amber-400 text-xs">${item.name}</span>
                            <span class="text-[10px] bg-gray-900 text-gray-300 px-2 py-0.5 rounded border border-gray-800">${item.type}</span>
                        </div>
                        <p class="text-[11px] text-gray-300"><strong class="text-amber-500">Efeito:</strong> ${item.effect}</p>
                        <p class="text-[11px] text-gray-400">${item.desc}</p>
                    </div>
                    <button onclick="addItemFromLibrary('${activeLibraryCategory}', '${item.name.replace(/'/g, "\\'")}')" class="px-3 py-1.5 bg-amber-600 hover:bg-amber-500 text-white font-semibold text-xs rounded-lg shadow whitespace-nowrap">➕ Pegar</button>
                </div>
            `).join('');
        };
        window.addItemFromLibrary = function(cat, itemName) {
            const itemTemplate = EQUIPMENT_LIBRARY[cat].find(i => i.name === itemName);
            if (!itemTemplate) return;
            const char = getCharacter();
            if (!char.inventory[cat]) char.inventory[cat] = [];
            char.inventory[cat].push(JSON.parse(JSON.stringify(itemTemplate)));
            saveToStorage();
            renderInventoryItems();
            alert(`"${itemTemplate.name}" adicionado ao inventário com sucesso!`);
        };
        window.switchTab = function(tabName) {
            ['economy', 'sheet', 'trade', 'manager', 'campaigns'].forEach(t => {
                const tabEl = document.getElementById(`tab-${t}`);
                if (tabEl) tabEl.classList.add('hidden');
                const btn = document.getElementById(`btn-tab-${t}`);
                if (btn) {
                    btn.className = "px-4 py-2 rounded-lg font-medium text-sm transition-all bg-gray-800 text-gray-300 hover:bg-gray-700";
                }
            });
            const targetTab = document.getElementById(`tab-${tabName}`);
            if (targetTab) targetTab.classList.remove('hidden');          
            const activeBtn = document.getElementById(`btn-tab-${tabName}`);
            if (activeBtn) {
                activeBtn.className = "px-4 py-2 rounded-lg font-medium text-sm transition-all bg-amber-600 text-white shadow";
            }
            if (tabName === 'manager') renderCharacterManager();
            if (tabName === 'trade') renderTradeTab();
        };
        window.toggleTheme = function() {
            const html = document.documentElement;
            html.classList.toggle('dark');
        };
        window.switchInventorySubTab = function(subTab) {
            activeInvSubTab = subTab;
            ['weapons', 'armors', 'resources', 'consumables'].forEach(st => {
                const btn = document.getElementById(`inv-tab-${st}`);
                if (btn) {
                    btn.className = st === subTab ? "px-3 py-1.5 rounded-lg text-xs font-semibold bg-amber-600 text-white" : "px-3 py-1.5 rounded-lg text-xs font-semibold bg-gray-900 text-gray-300 hover:bg-gray-700";
                }
            });
            renderInventoryItems();
        };
        window.updateCoins = function() {
            const char = getCharacter();
            char.coins.pl = parseInt(document.getElementById('coin-pl').value) || 0;
            char.coins.po = parseInt(document.getElementById('coin-po').value) || 0;
            char.coins.pp = parseInt(document.getElementById('coin-pp').value) || 0;
            char.coins.pc = parseInt(document.getElementById('coin-pc').value) || 0;
            const totalPC = (char.coins.pl * 5000000) + (char.coins.po * 5000) + (char.coins.pp * 50) + char.coins.pc;
            document.getElementById('total-copper-val').innerText = totalPC.toLocaleString() + ' PC';
            const totalCoinsCount = char.coins.pl + char.coins.po + char.coins.pp + char.coins.pc;
            const totalLb = totalCoinsCount / 50;
            const totalKg = totalLb * 0.453592;
            document.getElementById('total-weight-val').innerText = `${totalKg.toFixed(2)} kg (${totalLb.toFixed(1)} lb)`;
            saveToStorage();
        };
        function loadCoinInputs() {
            const char = getCharacter();
            document.getElementById('coin-pl').value = char.coins.pl || 0;
            document.getElementById('coin-po').value = char.coins.po || 0;
            document.getElementById('coin-pp').value = char.coins.pp || 0;
            document.getElementById('coin-pc').value = char.coins.pc || 0;
            updateCoins();
        }
        window.optimizeCoins = function() {
            const char = getCharacter();
            let totalPC = (char.coins.pl * 5000000) + (char.coins.po * 5000) + (char.coins.pp * 50) + char.coins.pc;
            char.coins.pl = Math.floor(totalPC / 5000000);
            totalPC %= 5000000;
            char.coins.po = Math.floor(totalPC / 5000);
            totalPC %= 5000;
            char.coins.pp = Math.floor(totalPC / 50);
            char.coins.pc = totalPC % 50;
            loadCoinInputs();
            saveToStorage();
            alert("Moedas consolidadas com sucesso!");
        };
        function createNewCharacterTemplate(name) {
            return {
                id: 'char_' + Math.random().toString(36).substr(2, 9),
                name: name || "Novo Herói",
                age: "25",
                race: "Humanos",
                characterClass: "Guerreiro",
                deity: "",
                title: "Nenhum",
                profession: "Aventureiro",
                height: "1.75m",
                weight: "70kg",
                rank: "F",
                history: "Um aventureiro novato em busca de glória.",
                level: 0,
                xp: 0,
                freePoints: 5,
                attributes: { Força: 1, Agilidade: 1, Intelecto: 1, Carisma: 1, Vigor: 1, Sanidade: 1, Éter: 1 },
                skills: [CLASSES_DATABASE["Guerreiro"].startingSkill],
                spells: [CLASSES_DATABASE["Guerreiro"].startingSpell],
                inventory: {
                    weapons: [{ name: "Espada Curta de Ferro", type: "Arma de Corte (Força)", effect: "1d6 + 1", desc: "Lâmina reta e compacta. Boa para golpes diretos." }],
                    armors: [{ name: "Túnica de Couro Cru", type: "Armadura Leve (Força)", effect: "Defesa +1", desc: "Couro simplesmente curtido, oferece proteção básica." }],
                    resources: [{ name: "Caderno de Anotações e Carvão", type: "Ferramenta (Intelecto)", effect: "Vantagem em lembrar informações", desc: "Registra observações e mapas." }],
                    consumables: [{ name: "Kit de Primeiros Socorros", type: "Médico (Intelecto)", effect: "Recupera 1d4+1 PV", desc: "Trata ferimentos leves." }]
                },
                coins: { pl: 0, po: 10, pp: 50, pc: 100 }
            };
        }
        window.processTransaction = function(type) {
            const desc = document.getElementById('trans-desc').value.trim() || "Transação sem descrição";
            const coinType = document.getElementById('trans-coin-type').value;
            const amount = parseInt(document.getElementById('trans-amount').value) || 0;
            const char = getCharacter();
            if (amount <= 0) return;
            if (type === 'sub') {
                if (char.coins[coinType] < amount) {
                    alert("Saldo insuficiente nesta moeda!");
                    return;
                }
                char.coins[coinType] -= amount;
            } else {
                char.coins[coinType] += amount;
            }
            loadCoinInputs();
            transactionHistory.unshift({ date: new Date().toLocaleTimeString(), desc: `${type === 'add' ? '+' : '-'} ${amount} ${coinType.toUpperCase()} (${desc})` });
            if (transactionHistory.length > 20) transactionHistory.pop();
            renderHistory();
            saveToStorage();
        };
        function renderHistory() {
            const histEl = document.getElementById('transaction-history');
            if (transactionHistory.length === 0) {
                histEl.innerHTML = '<p class="text-gray-500 italic">Nenhuma transação registrada recentemente.</p>';
                return;
            }
            histEl.innerHTML = transactionHistory.map(h => `<div class="p-2 bg-gray-900 rounded border border-gray-800 flex justify-between"><span>${h.desc}</span><span class="text-xs text-gray-500">${h.date}</span></div>`).join('');
        }
        window.clearHistory = function() {
            transactionHistory = [];
            renderHistory();
            saveToStorage();
        };
        window.switchActiveCharacter = function(id) {
            activeCharacterId = id;
            loadActiveCharacterToUI();
            saveToStorage();
        };
        window.createNewCharacter = function() {
            const newChar = createNewCharacterTemplate("Herói " + (characters.length + 1));
            characters.push(newChar);
            activeCharacterId = newChar.id;
            loadActiveCharacterToUI();
            saveToStorage();
        };
        window.duplicateActiveCharacter = function() {
            const current = getCharacter();
            const copy = JSON.parse(JSON.stringify(current));
            copy.id = 'char_' + Math.random().toString(36).substr(2, 9);
            copy.name = current.name + " (Cópia)";
            characters.push(copy);
            activeCharacterId = copy.id;
            loadActiveCharacterToUI();
            saveToStorage();
        };
        window.deleteActiveCharacter = function() {
            if (characters.length <= 1) {
                alert("Você precisa manter pelo menos uma ficha no sistema.");
                return;
            }
            if (confirm("Deseja realmente excluir este herói?")) {
                characters = characters.filter(c => c.id !== activeCharacterId);
                activeCharacterId = characters[0].id;
                loadActiveCharacterToUI();
                saveToStorage();
            }
        };
        function loadActiveCharacterToUI() {
            const char = getCharacter();
            if (!char.inventory) {
                char.inventory = { weapons: [], armors: [], resources: [], consumables: [] };
            }
            if (!char.trade) {
                char.trade = { sellerLevel: 1, merchantLevel: 1 };
            }
            const activeSelect = document.getElementById('active-character-select');
            if (activeSelect) {
                activeSelect.innerHTML = characters.map(c => `<option value="${c.id}" ${c.id === activeCharacterId ? 'selected' : ''}>${c.name} (Nível ${c.level} - ${c.characterClass})</option>`).join('');
            }
            const setValueIfExist = (id, val) => {
                const el = document.getElementById(id);
                if (el) el.value = val;
            };
            const setTextIfExist = (id, val) => {
                const el = document.getElementById(id);
                if (el) el.innerText = val;
            };
            setValueIfExist('char-name', char.name || '');
            setValueIfExist('char-age', char.age || '');
            setValueIfExist('char-profession', char.profession || '');
            setValueIfExist('char-height', char.height || '');
            setValueIfExist('char-weight', char.weight || '');
            setValueIfExist('char-rank', char.rank || 'F');
            setValueIfExist('char-history', char.history || '');
            const raceEl = document.getElementById('char-race');
            if (raceEl) raceEl.innerHTML = Object.keys(RACES_DATABASE).map(r => `<option value="${r}" ${char.race === r ? 'selected' : ''}>${r}</option>`).join('');
            const classEl = document.getElementById('char-class');
            if (classEl) classEl.innerHTML = Object.keys(CLASSES_DATABASE).map(cls => `<option value="${cls}" ${char.characterClass === cls ? 'selected' : ''}>${cls}</option>`).join('');
            const deityEl = document.getElementById('char-deity');
            if (deityEl) deityEl.innerHTML = `<option value="">Nenhuma / Sem Divindade</option>` + Object.keys(DEITIES_DATABASE).map(d => `<option value="${d}" ${char.deity === d ? 'selected' : ''}>${d.toUpperCase()} (${DEITIES_DATABASE[d].title})</option>`).join('');
            const titleEl = document.getElementById('char-title');
            if (titleEl) titleEl.innerHTML = `<option value="Nenhum">Nenhum Título Ativo</option><option value="Rastreador de Sangue Frio" ${char.title === 'Rastreador de Sangue Frio' ? 'selected' : ''}>Rastreador de Sangue Frio</option>`;
            setTextIfExist('stat-level', char.level || 0);
            const currentMaxXP = getXPRequiredForLevel(char.level);
            setTextIfExist('stat-xp-text', `${char.xp || 0} / ${currentMaxXP}`);         
            const xpBar = document.getElementById('stat-xp-bar');
            if (xpBar) xpBar.style.width = Math.min(100, Math.round(((char.xp || 0) / currentMaxXP) * 100)) + '%';
            const freePointsEl = document.getElementById('stat-free-points');
            if (freePointsEl) freePointsEl.innerText = char.freePoints || 0;
            loadCoinInputs();
            renderAttributes();
            renderSkills();
            renderSpells();
            renderInventoryItems();
            calculateSecondaryStats();
            renderTradeTab();
        }
        window.renderTradeTab = function() {
            const char = getCharacter();
            if (!char.trade) char.trade = { sellerLevel: 1, merchantLevel: 1 };
            document.getElementById('trade-active-char-name').innerText = char.name;
            document.getElementById('trade-seller-level').value = char.trade.sellerLevel;
            document.getElementById('trade-merchant-level').value = char.trade.merchantLevel;
            const sData = SELLER_RANKS[char.trade.sellerLevel];
            document.getElementById('seller-details-box').innerHTML = `
                <p><strong class="text-amber-400">Título:</strong> ${sData.title}</p>
                <p><strong class="text-amber-400">Bônus de Carisma:</strong> +${sData.bonusCarisma}</p>
                <p><strong class="text-amber-400">Efeito da Fama:</strong> ${sData.effect}</p>
                <p><strong class="text-amber-400">Fundos / Comissão:</strong> ${sData.funds}</p>
            `;
            const mData = MERCHANT_RANKS[char.trade.merchantLevel];
            document.getElementById('merchant-details-box').innerHTML = `
                <p><strong class="text-amber-400">Título:</strong> ${mData.title}</p>
                <p><strong class="text-amber-400">Bônus de Carisma:</strong> +${mData.bonusCarisma}</p>
                <p><strong class="text-amber-400">Efeito da Fama:</strong> ${mData.effect}</p>
                <p><strong class="text-amber-400">Fundos / Lucro:</strong> ${mData.funds}</p>
            `;
        };
        window.updateTradeCareer = function(type, val) {
            const char = getCharacter();
            if (!char.trade) char.trade = { sellerLevel: 1, merchantLevel: 1 };
            if (type === 'seller') char.trade.sellerLevel = parseInt(val);
            if (type === 'merchant') char.trade.merchantLevel = parseInt(val);
            saveToStorage();
            renderTradeTab();
        };
        window.simulateTradeAction = function(type) {
            const char = getCharacter();
            if (type === 'seller') {
                const sData = SELLER_RANKS[char.trade.sellerLevel];
                alert(`Você realizou turnos de vendas como ${sData.title}! Sua lábia e reputação atraíram novos clientes.`);
            } else {
                const mData = MERCHANT_RANKS[char.trade.merchantLevel];
                alert(`Você gerenciou seu negócio como ${mData.title}! O empreendimento gerou lucros e fortaleceu sua marca na região.`);
            }
        };
        window.updateCharInfo = function(field, val) {
            getCharacter()[field] = val;
            saveToStorage();
        };
        window.onRaceChange = function(newRace) {
            getCharacter().race = newRace;
            saveToStorage();
            loadActiveCharacterToUI();
        };
        window.onClassChange = function(newClassName) {
            const char = getCharacter();
            const oldClassName = char.characterClass;          
            if (CLASSES_DATABASE[oldClassName]?.startingSkill) {
                const idx = char.skills.indexOf(CLASSES_DATABASE[oldClassName].startingSkill);
                if (idx > -1) char.skills.splice(idx, 1);
            }
            if (CLASSES_DATABASE[oldClassName]?.startingSpell) {
                const oldSpellName = CLASSES_DATABASE[oldClassName].startingSpell.name;
                const idxSpell = char.spells.findIndex(sp => typeof sp === 'object' ? sp.name === oldSpellName : sp === oldSpellName);
                if (idxSpell > -1) char.spells.splice(idxSpell, 1);
            }
            char.characterClass = newClassName;
            if (CLASSES_DATABASE[newClassName]?.startingSkill) {
                char.skills.unshift(CLASSES_DATABASE[newClassName].startingSkill);
            }
            if (CLASSES_DATABASE[newClassName]?.startingSpell) {
                char.spells.unshift(CLASSES_DATABASE[newClassName].startingSpell);
            }
            saveToStorage();
            loadActiveCharacterToUI();
        };
        window.onDeityChange = function(newDeity) {
            getCharacter().deity = newDeity;
            saveToStorage();
        };
        window.onTitleChange = function(newTitle) {
            getCharacter().title = newTitle;
            saveToStorage();
        };
        function renderAttributes() {
            const container = document.getElementById('attributes-container');
            if (!container) return;           
            const char = getCharacter();
            const attrNames = ["Força", "Agilidade", "Intelecto", "Carisma", "Vigor", "Sanidade", "Éter"];
            // Tabela exata de bônus de modificador de atributos fornecida
            function getAttributeModifier(val) {
                if (val >= 10) return 6;
                if (val >= 8 && val <= 9) return 5;
                if (val >= 6 && val <= 7) return 4;
                if (val >= 4 && val <= 5) return 3;
                if (val >= 2 && val <= 3) return 2;
                if (val === 1) return 1;
                if (val === 0) return 0;
                if (val === -1) return -1;
                if (val >= -3 && val <= -2) return -2;
                if (val >= -5 && val <= -4) return -3;
                if (val >= -7 && val <= -6) return -4;
                if (val >= -9 && val <= -8) return -5;
                if (val <= -10) return -6;
                return 0;
            }
            container.innerHTML = attrNames.map(attr => {
                const raceBonus = (RACES_DATABASE[char.race]?.attrs[attr]) || 0;
                const totalVal = (char.attributes[attr] || 0) + raceBonus;
                const modVal = getAttributeModifier(totalVal);
                const modStr = modVal >= 0 ? `+${modVal}` : `${modVal}`;
                return `
                    <div class="bg-gray-900 p-3 rounded-xl border border-gray-700 flex justify-between items-center">
                        <div>
                            <span class="font-bold text-gray-200 block text-sm">${attr}</span>
                            <span class="text-[11px] text-gray-400">Base: ${char.attributes[attr]} | Raça: ${raceBonus >= 0 ? '+' + raceBonus : raceBonus}</span>
                        </div>
                        <div class="flex items-center gap-3">
                            <span class="text-xs px-2 py-0.5 rounded bg-amber-600/20 border border-amber-600/40 text-amber-300 font-bold" title="Bônus de Rolagem">Bônus: ${modStr}</span>
                            <div class="flex items-center gap-1">
                                <button onclick="modifyAttribute('${attr}', -1)" class="w-7 h-7 bg-gray-800 hover:bg-gray-700 rounded text-amber-400 font-bold">-</button>
                                <span class="text-lg font-bold text-amber-400 w-8 text-center">${totalVal}</span>
                                <button onclick="modifyAttribute('${attr}', 1)" class="w-7 h-7 bg-gray-800 hover:bg-gray-700 rounded text-amber-400 font-bold">+</button>
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }
        window.modifyAttribute = function(attr, delta) {
            const char = getCharacter();
            if (delta > 0 && char.freePoints <= 0) {
                alert("Você não possui pontos livres disponíveis para distribuir.");
                return;
            }
            if (delta < 0 && char.attributes[attr] <= 0) return;
            char.attributes[attr] += delta;
            char.freePoints -= delta;
            saveToStorage();
            loadActiveCharacterToUI();
        };
        function calculateSecondaryStats() {
            const char = getCharacter();
            const vigor = (char.attributes["Vigor"] || 0) + (RACES_DATABASE[char.race]?.attrs["Vigor"] || 0);
            const ether = (char.attributes["Éter"] || 0) + (RACES_DATABASE[char.race]?.attrs["Éter"] || 0);
            const sanidade = (char.attributes["Sanidade"] || 0) + (RACES_DATABASE[char.race]?.attrs["Sanidade"] || 0);
            const forca = (char.attributes["Força"] || 0) + (RACES_DATABASE[char.race]?.attrs["Força"] || 0);
            const lvl = char.level || 0;
            const maxHP = Math.round(vigor * (lvl / 2) + 20);
            const maxMana = Math.round(ether * (lvl / 2) + 10);
            const totalSan = Math.round(sanidade * lvl + 5);
            const defesa = forca + vigor + 10;
            document.getElementById('stat-hp').innerText = `${maxHP} / ${maxHP}`;
            document.getElementById('stat-mana').innerText = `${maxMana} / ${maxMana}`;
            document.getElementById('stat-san').innerText = totalSan;
            document.getElementById('stat-def').innerText = defesa;
        }
        function renderInventoryItems() {
            const char = getCharacter();
            const container = document.getElementById('inventory-content-container');
            const items = char.inventory[activeInvSubTab] || [];
            if (items.length === 0) {
                container.innerHTML = '<p class="text-gray-500 italic text-xs text-center py-6">Nenhum item nesta categoria.</p>';
                return;
            }
            container.innerHTML = items.map((item, idx) => `
                <div class="p-3 bg-gray-900 rounded-xl border border-gray-700 flex justify-between items-start gap-3">
                    <div class="space-y-1">
                        <div class="flex items-center gap-2">
                            <span class="font-bold text-amber-400 text-sm">${item.name}</span>
                            <span class="text-[10px] bg-gray-800 text-gray-300 px-2 py-0.5 rounded border border-gray-700">${item.type}</span>
                        </div>
                        <p class="text-xs text-gray-300"><strong class="text-amber-500">Efeito/Dano:</strong> ${item.effect}</p>
                        <p class="text-xs text-gray-400">${item.desc}</p>
                    </div>
                    <button onclick="removeInventoryItem('${activeInvSubTab}', ${idx})" class="text-red-400 hover:text-red-300 font-bold text-xs p-1">✕</button>
                </div>
            `).join('');
        }
        window.openAddItemModal = function() {
            document.getElementById('newItem-name').value = '';
            document.getElementById('newItem-type').value = '';
            document.getElementById('newItem-effect').value = '';
            document.getElementById('newItem-desc').value = '';
            document.getElementById('modal-add-item').classList.remove('hidden');
        };
        window.saveNewInventoryItem = function() {
            const cat = document.getElementById('newItem-category').value;
            const name = document.getElementById('newItem-name').value.trim();
            if (!name) { alert("Insira o nome do item."); return; }            
            const itemObj = {
                name: name,
                type: document.getElementById('newItem-type').value.trim() || "Geral",
                effect: document.getElementById('newItem-effect').value.trim() || "Nenhum",
                desc: document.getElementById('newItem-desc').value.trim() || "Sem descrição."
            };
            const char = getCharacter();
            if (!char.inventory[cat]) char.inventory[cat] = [];
            char.inventory[cat].push(itemObj);
            saveToStorage();
            renderInventoryItems();
            closeModal('modal-add-item');
        };
        window.removeInventoryItem = function(cat, idx) {
            const char = getCharacter();
            if (char.inventory[cat]) {
                char.inventory[cat].splice(idx, 1);
                saveToStorage();
                renderInventoryItems();
            }
        };
        function renderSkills() {
            const char = getCharacter();
            const listEl = document.getElementById('skills-list');
            if (!listEl) return;
            if (!char.skills || char.skills.length === 0) {
                listEl.innerHTML = '<p class="text-gray-500 italic text-xs">Nenhuma habilidade cadastrada.</p>';
                return;
            }
            listEl.innerHTML = char.skills.map((s, idx) => {
                const sName = typeof s === 'object' ? s.name : s;
                const hasDetails = typeof s === 'object' && s.desc;
                return `
                    <div class="p-2.5 bg-gray-900 rounded-xl border border-gray-700 flex justify-between items-center gap-2">
                        <div class="flex items-center gap-2">
                            <span class="text-gray-200 text-xs font-bold">${sName}</span>
                            ${hasDetails ? `<button onclick="openSkillModal(${idx})" class="text-[10px] bg-amber-600/35 border border-amber-600/50 text-amber-300 px-1.5 py-0.5 rounded hover:bg-amber-600/50">Detalhes</button>` : ''}
                        </div>
                        <button onclick="removeItem('skills', ${idx})" class="text-red-400 font-bold text-xs">✕</button>
                    </div>
                `;
            }).join('');
        }
        window.openSkillModal = function(idx) {
            const char = getCharacter();
            const s = char.skills[idx];
            if (!s || typeof s !== 'object') return;
            document.getElementById('skill-modal-content').innerHTML = `
                <h3 class="text-xl font-bold font-cinzel text-amber-400 mb-2">${s.name}</h3>
                <div class="space-y-2 text-xs text-gray-300">
                    <p><strong class="text-amber-400">Nível:</strong> ${s.level}</p>
                    <p><strong class="text-amber-400">Tipo:</strong> ${s.type}</p>
                    <p><strong class="text-amber-400">Alcance:</strong> ${s.range}</p>
                    <p><strong class="text-amber-400">Dano / Efeito:</strong> ${s.damage}</p>
                    <div class="p-3 bg-gray-950 rounded-lg border border-gray-800 mt-3">
                        <strong class="text-amber-400 block mb-1">Descrição Completa:</strong>
                        <p class="text-gray-200 leading-relaxed">${s.desc}</p>
                    </div>
                </div>
            `;
            document.getElementById('modal-skill-details').classList.remove('hidden');
        };
        window.closeSkillModal = function() {
            document.getElementById('modal-skill-details').classList.add('hidden');
        };
        function renderSpells() {
            const char = getCharacter();
            const listEl = document.getElementById('spells-list');
            if (!listEl) return;
            if (!char.spells || char.spells.length === 0) {
                listEl.innerHTML = '<p class="text-gray-500 italic text-xs">Nenhuma magia cadastrada.</p>';
                return;
            }
            listEl.innerHTML = char.spells.map((sp, idx) => {
                const spName = typeof sp === 'object' ? sp.name : sp;
                const hasDetails = typeof sp === 'object' && sp.desc;
                return `
                    <div class="p-2.5 bg-gray-900 rounded-xl border border-gray-700 flex justify-between items-center gap-2">
                        <div class="flex items-center gap-2">
                            <span class="text-gray-200 text-xs font-bold">${spName}</span>
                            ${hasDetails ? `<button onclick="openSpellModal(${idx})" class="text-[10px] bg-amber-600/35 border border-amber-600/50 text-amber-300 px-1.5 py-0.5 rounded hover:bg-amber-600/50">Detalhes</button>` : ''}
                        </div>
                        <button onclick="removeItem('spells', ${idx})" class="text-red-400 font-bold text-xs">✕</button>
                    </div>
                `;
            }).join('');
        }
        window.openSkillModal = function(idx) {
            const char = getCharacter();
            const s = char.skills[idx];
            if (!s || typeof s !== 'object') return;
            document.getElementById('skill-modal-content').innerHTML = `
                <h3 class="text-xl font-bold font-cinzel text-amber-400 mb-2">${s.name}</h3>
                <div class="space-y-2 text-xs text-gray-300">
                    <p><strong class="text-amber-400">Nível:</strong> ${s.level}</p>
                    <p><strong class="text-amber-400">Tipo:</strong> ${s.type}</p>
                    <p><strong class="text-amber-400">Alcance:</strong> ${s.range}</p>
                    <p><strong class="text-amber-400">Dano / Efeito:</strong> ${s.damage}</p>
                    <div class="p-3 bg-gray-950 rounded-lg border border-gray-800 mt-3">
                        <strong class="text-amber-400 block mb-1">Descrição Completa:</strong>
                        <p class="text-gray-200 leading-relaxed">${s.desc}</p>
                    </div>
                </div>
            `;
            document.getElementById('modal-skill-details').classList.remove('hidden');
        };
        window.closeSkillModal = function() {
            document.getElementById('modal-skill-details').classList.add('hidden');
        };
        window.renderSpells = function() {
            const char = getCharacter();
            const listEl = document.getElementById('spells-list');
            if (!char.spells || char.spells.length === 0) {
                listEl.innerHTML = '<p class="text-gray-500 italic text-xs">Nenhuma magia cadastrada.</p>';
                return;
            }
            listEl.innerHTML = char.spells.map((sp, idx) => {
                const spName = typeof sp === 'object' ? sp.name : sp;
                const hasDetails = typeof sp === 'object' && sp.desc;
                return `
                    <div class="p-2.5 bg-gray-900 rounded-xl border border-gray-700 flex justify-between items-center gap-2">
                        <div class="flex items-center gap-2">
                            <span class="text-gray-200 text-xs font-bold">${spName}</span>
                            ${hasDetails ? `<button onclick="openSpellModal(${idx})" class="text-[10px] bg-amber-600/35 border border-amber-600/50 text-amber-300 px-1.5 py-0.5 rounded hover:bg-amber-600/50">Detalhes</button>` : ''}
                        </div>
                        <button onclick="removeItem('spells', ${idx})" class="text-red-400 font-bold text-xs">✕</button>
                    </div>
                `;
            }).join('');
        };
        window.openSpellModal = function(idx) {
            const char = getCharacter();
            const sp = char.spells[idx];
            if (!sp || typeof sp !== 'object') return;
            document.getElementById('spell-modal-content').innerHTML = `
                <h3 class="text-xl font-bold font-cinzel text-amber-400 mb-2">${sp.name}</h3>
                <div class="space-y-2 text-xs text-gray-300">
                    <p><strong class="text-amber-400">Nível:</strong> ${sp.level}</p>
                    <p><strong class="text-amber-400">Tipo:</strong> ${sp.type}</p>
                    <p><strong class="text-amber-400">Alcance:</strong> ${sp.range}</p>
                    <p><strong class="text-amber-400">Dano:</strong> ${sp.damage}</p>
                    <p><strong class="text-amber-400">Custo de Mana:</strong> ${sp.cost}</p>
                    <div class="p-3 bg-gray-950 rounded-lg border border-gray-800 mt-3">
                        <strong class="text-amber-400 block mb-1">Descrição Completa:</strong>
                        <p class="text-gray-200 leading-relaxed">${sp.desc}</p>
                    </div>
                </div>
            `;
            document.getElementById('modal-spell-details').classList.remove('hidden');
        };
        window.closeSpellModal = function() {
            document.getElementById('modal-spell-details').classList.add('hidden');
        };
        window.removeItem = function(type, idx) {
            const char = getCharacter();
            char[type].splice(idx, 1);
            saveToStorage();
            loadActiveCharacterToUI();
        };
        function getXPRequiredForLevel(lvl) {
            if (lvl < 5) return 60;
            if (lvl < 10) return 180;
            if (lvl < 15) return 360;
            if (lvl < 20) return 600;
            if (lvl < 25) return 900;
            if (lvl < 30) return 1260;
            if (lvl < 35) return 1680;
            if (lvl < 40) return 2160;
            if (lvl < 45) return 2700;
            if (lvl < 50) return 3300;
            if (lvl < 55) return 3960;
            if (lvl < 60) return 4680;
            if (lvl < 65) return 5460;
            if (lvl < 70) return 6300;
            if (lvl < 75) return 7200;
            if (lvl < 80) return 8160;
            if (lvl < 85) return 9180;
            if (lvl < 90) return 10260;
            if (lvl < 95) return 11400;
            return 12600;
        }
        window.openXPCalculatorModal = function() {
            calculateXPResult();
            document.getElementById('modal-xp').classList.remove('hidden');
        };
        window.closeXPCalculatorModal = function() {
            document.getElementById('modal-xp').classList.add('hidden');
        };
        window.calculateXPResult = function() {
            const lvl = parseInt(document.getElementById('xp-calc-level').value) || 1;
            const hp = parseInt(document.getElementById('xp-calc-hp').value) || 10;
            const rarity = parseFloat(document.getElementById('xp-calc-rarity').value) || 1.0;
            const totalXP = Math.round((lvl * hp) * rarity);
            document.getElementById('xp-calc-result').innerText = totalXP + ' XP';
            return totalXP;
        };
        window.applyCalculatedXP = function() {
            const xpVal = calculateXPResult();
            addXP(xpVal);
            closeXPCalculatorModal();
        };
        window.addXP = function(amount) {
            const char = getCharacter();
            char.xp = (char.xp || 0) + amount;
            let reqXP = getXPRequiredForLevel(char.level);
            while (char.xp >= reqXP) {
                char.xp -= reqXP;
                char.level++;
                char.freePoints += 1;
                reqXP = getXPRequiredForLevel(char.level);
                alert(`Parabéns! ${char.name} subiu para o Nível ${char.level}! (+1 Atributo ganho)`);
            }
            saveToStorage();
            loadActiveCharacterToUI();
        };
        function renderCharacterManager() {
            const query = (document.getElementById('manager-search').value || '').toLowerCase();
            const grid = document.getElementById('manager-character-grid');
            const filtered = characters.filter(c => c.name.toLowerCase().includes(query) || c.race.toLowerCase().includes(query) || c.characterClass.toLowerCase().includes(query));
            if (filtered.length === 0) {
                grid.innerHTML = '<p class="text-gray-500 italic col-span-full text-center py-8">Nenhum herói encontrado.</p>';
                return;
            }
            grid.innerHTML = filtered.map(c => `
                <div class="bg-gray-900 border border-gray-700 rounded-2xl p-5 shadow-lg flex flex-col justify-between space-y-4">
                    <div>
                        <div class="flex justify-between items-start mb-2">
                            <h3 class="text-lg font-bold font-cinzel text-amber-400">${c.name}</h3>
                            <span class="px-2 py-0.5 bg-amber-600/20 text-amber-400 text-xs font-semibold rounded border border-amber-600/30">Lvl ${c.level}</span>
                        </div>
                        <p class="text-xs text-gray-400">Raça: <span class="text-gray-200">${c.race}</span> | Classe: <span class="text-gray-200">${c.characterClass}</span></p>
                        <p class="text-xs text-gray-400 mt-1">Rank: <span class="text-amber-400 font-bold">${c.rank}</span> | Título: <span class="text-gray-200">${c.title}</span></p>
                    </div>
                    <div class="flex gap-2 pt-2 border-t border-gray-800">
                        <button onclick="switchActiveCharacter('${c.id}'); switchTab('sheet');" class="flex-1 py-2 bg-amber-600 hover:bg-amber-500 text-white text-xs font-semibold rounded-lg shadow">📜 Abrir Ficha</button>
                        <button onclick="activeCharacterId = '${c.id}'; duplicateActiveCharacter(); renderCharacterManager();" class="px-3 py-2 bg-gray-800 hover:bg-gray-700 text-gray-300 text-xs rounded-lg">📋</button>
                        <button onclick="activeCharacterId = '${c.id}'; deleteActiveCharacter(); renderCharacterManager();" class="px-3 py-2 bg-red-900/40 hover:bg-red-900 text-red-300 text-xs rounded-lg">🗑️</button>
                    </div>
                </div>
            `).join('');
        }
        window.openCreateCampaignModal = function() {
            document.getElementById('modal-campaign-create').classList.remove('hidden');
        };
        window.openJoinCampaignModal = function() {
            document.getElementById('modal-campaign-join').classList.remove('hidden');
        };
        window.createCampaignAction = function() {
            const name = document.getElementById('new-campaign-name').value.trim();
            if (!name) { alert("Insira um nome para a campanha."); return; }
            const code = "MESA-" + Math.floor(10000 + Math.random() * 90000);
            alert(`Campanha "${name}" criada com sucesso!\nCódigo de acesso: ${code}`);
            closeModal('modal-campaign-create');
        };
        window.joinCampaignAction = function() {
            const code = document.getElementById('join-campaign-id').value.trim();
            if (!code) { alert("Insira o código da campanha."); return; }
            alert(`Conectado com sucesso à mesa [${code}]!`);
            closeModal('modal-campaign-join');
        };
        window.closeModal = function(id) {
            const modal = document.getElementById(id);
            if (modal) modal.classList.add('hidden');
        };
        window.onload = function() {
            if (characters.length === 0) {
                const initialChar = createNewCharacterTemplate("Herói Principal");
                characters.push(initialChar);
                activeCharacterId = initialChar.id;
                saveToStorage();
            }
            loadActiveCharacterToUI();
            renderHistory();
        };
    </script>
</body>
</html>
