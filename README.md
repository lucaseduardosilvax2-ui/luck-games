# lucke
-games
jogos para pc windows etc.
HTML
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Luck Games - Sistema de Jogos para PC</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <div class="header-content">
                <h1>🎮 Luck Games</h1>
                <p>Seu sistema completo de jogos para PC</p>
            </div>
            <div class="header-buttons">
                <button class="btn-favorites" onclick="toggleFavorites()" title="Favoritos">
                    ❤️ <span id="favCount">0</span>
                </button>
                <button class="btn-cart" onclick="toggleCart()" title="Carrinho">
                    🛒 <span id="cartCount">0</span>
                </button>
                <button class="btn-profile" onclick="toggleProfile()" title="Perfil">
                    👤
                </button>
            </div>
        </header>

        <!-- Search and Filters -->
        <section class="search-section">
            <div class="search-box">
                <input 
                    type="text" 
                    id="searchInput" 
                    placeholder="🔍 Buscar jogo..."
                    class="search-input"
                >
            </div>

            <div class="filters">
                <select id="categoryFilter" class="filter-select">
                    <option value="">Todas as Categorias</option>
                    <option value="ação">Ação</option>
                    <option value="rpg">RPG</option>
                    <option value="estratégia">Estratégia</option>
                    <option value="puzzle">Puzzle</option>
                    <option value="corrida">Corrida</option>
                    <option value="esportes">Esportes</option>
                    <option value="aventura">Aventura</option>
                    <option value="simulação">Simulação</option>
                    <option value="terror">Terror</option>
                    <option value="luta">Luta</option>
                </select>

                <select id="priceFilter" class="filter-select">
                    <option value="">Todas as Faixas de Preço</option>
                    <option value="gratuito">Gratuito</option>
                    <option value="ate50">Até R$ 50</option>
                    <option value="50a100">R$ 50 - R$ 100</option>
                    <option value="acima100">Acima de R$ 100</option>
                </select>

                <select id="sortFilter" class="filter-select">
                    <option value="nome">Ordenar por Nome</option>
                    <option value="preco-asc">Preço: Menor para Maior</option>
                    <option value="preco-desc">Preço: Maior para Menor</option>
                    <option value="nota">Melhor Avaliado</option>
                </select>
            </div>
        </section>

        <!-- Stats -->
        <section class="stats">
            <div class="stat-item">
                <span class="stat-label">Jogos Encontrados:</span>
                <span class="stat-value" id="totalGames">0</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">Filtros Ativos:</span>
                <span class="stat-value" id="activeFilters">0</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">Total de Jogos:</span>
                <span class="stat-value" id="totalAllGames">0</span>
            </div>
        </section>

        <!-- Games Grid -->
        <section class="games-grid" id="gamesContainer">
            <!-- Games will be inserted here by JavaScript -->
        </section>

        <!-- Empty State -->
        <section class="empty-state" id="emptyState" style="display: none;">
            <p>😢 Nenhum jogo encontrado com esses filtros</p>
            <button onclick="resetFilters()" class="btn-reset">Limpar Filtros</button>
        </section>
    </div>

    <!-- Favorites Modal -->
    <div class="modal" id="favoritesModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>❤️ Meus Favoritos</h2>
                <button class="close-btn" onclick="toggleFavorites()">✕</button>
            </div>
            <div class="modal-body" id="favoritesBody">
                <p style="text-align: center; color: #999;">Nenhum favorito ainda</p>
            </div>
        </div>
    </div>

    <!-- Cart Modal -->
    <div class="modal" id="cartModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>🛒 Carrinho de Compras</h2>
                <button class="close-btn" onclick="toggleCart()">✕</button>
            </div>
            <div class="modal-body" id="cartBody">
                <p style="text-align: center; color: #999;">Carrinho vazio</p>
            </div>
            <div class="modal-footer" id="cartFooter" style="display: none;">
                <div class="cart-total">
                    <span>Total:</span>
                    <span id="cartTotal">R$ 0,00</span>
                </div>
                <button class="btn-checkout">Finalizar Compra</button>
            </div>
        </div>
    </div>

    <!-- Profile Modal -->
    <div class="modal" id="profileModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>👤 Meu Perfil</h2>
                <button class="close-btn" onclick="toggleProfile()">✕</button>
            </div>
            <div class="modal-body">
                <div class="profile-section">
                    <h3>Estatísticas</h3>
                    <div class="stat-grid">
                        <div class="stat-card">
                            <span class="stat-icon">📚</span>
                            <span class="stat-text">Jogos Visitados</span>
                            <span class="stat-number" id="statsViewed">0</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-icon">❤️</span>
                            <span class="stat-text">Favoritos</span>
                            <span class="stat-number" id="statsFav">0</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-icon">🛒</span>
                            <span class="stat-text">Itens no Carrinho</span>
                            <span class="stat-number" id="statsCart">0</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-icon">💰</span>
                            <span class="stat-text">Total Gasto</span>
                            <span class="stat-number" id="statsSpent">R$ 0,00</span>
                        </div>
                    </div>
                </div>
                <div class="profile-section">
                    <h3>Ações</h3>
                    <button class="btn-action" onclick="clearAllData()">🗑️ Limpar Dados</button>
                </div>
            </div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
styles.css

CSS
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    padding: 20px;
    color: #333;
}

.container {
    max-width: 1400px;
    margin: 0 auto;
}

/* Header */
.header {
    background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
    color: white;
    padding: 30px 20px;
    border-radius: 15px;
    margin-bottom: 40px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 20px;
}

.header-content h1 {
    font-size: 2.5em;
    margin-bottom: 5px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.header-content p {
    font-size: 1em;
    opacity: 0.9;
}

.header-buttons {
    display: flex;
    gap: 15px;
}

.btn-favorites, .btn-cart, .btn-profile {
    background: rgba(255, 255, 255, 0.2);
    color: white;
    border: 2px solid white;
    padding: 10px 15px;
    border-radius: 10px;
    cursor: pointer;
    font-size: 1.1em;
    transition: all 0.3s ease;
    font-weight: bold;
}

.btn-favorites:hover, .btn-cart:hover, .btn-profile:hover {
    background: white;
    color: #667eea;
    transform: scale(1.05);
}

/* Search Section */
.search-section {
    background: white;
    padding: 30px;
    border-radius: 15px;
    margin-bottom: 30px;
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.search-box {
    margin-bottom: 20px;
}

.search-input {
    width: 100%;
    padding: 15px 20px;
    font-size: 1em;
    border: 2px solid #e0e0e0;
    border-radius: 10px;
    transition: all 0.3s ease;
}

.search-input:focus {
    outline: none;
    border-color: #667eea;
    box-shadow: 0 0 10px rgba(102, 126, 234, 0.3);
}

.filters {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 15px;
}

.filter-select {
    padding: 12px 15px;
    border: 2px solid #e0e0e0;
    border-radius: 10px;
    font-size: 1em;
    background-color: white;
    cursor: pointer;
    transition: all 0.3s ease;
}

.filter-select:hover {
    border-color: #667eea;
}

.filter-select:focus {
    outline: none;
    border-color: #667eea;
    box-shadow: 0 0 10px rgba(102, 126, 234, 0.3);
}

/* Stats */
.stats {
    display: flex;
    gap: 20px;
    margin-bottom: 30px;
    flex-wrap: wrap;
}

.stat-item {
    background: white;
    padding: 15px 25px;
    border-radius: 10px;
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
    display: flex;
    align-items: center;
    gap: 10px;
    flex: 1;
    min-width: 200px;
}

.stat-label {
    font-weight: 600;
    color: #666;
}

.stat-value {
    font-size: 1.5em;
    font-weight: bold;
    color: #667eea;
}

/* Games Grid */
.games-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 25px;
    margin-bottom: 40px;
}

.game-card {
    background: white;
    border-radius: 15px;
    overflow: hidden;
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    position: relative;
}

.game-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
}

.game-badge {
    position: absolute;
    top: 10px;
    right: 10px;
    background: rgba(0, 0, 0, 0.7);
    color: white;
    padding: 5px 10px;
    border-radius: 20px;
    font-size: 0.9em;
    font-weight: bold;
    z-index: 10;
}

.game-badge.favorite {
    background: #e74c3c;
}

.btn-fav {
    position: absolute;
    top: 10px;
    left: 10px;
    background: rgba(255, 255, 255, 0.9);
    border: none;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    font-size: 1.2em;
    cursor: pointer;
    transition: all 0.3s ease;
    z-index: 10;
}

.btn-fav:hover {
    transform: scale(1.1);
    background: white;
}

.game-image {
    width: 100%;
    height: 200px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 4em;
    color: white;
    position: relative;
    overflow: hidden;
}

.game-image::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
}

.game-card:hover .game-image::before {
    background: rgba(0, 0, 0, 0.3);
}

.game-content {
    padding: 20px;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
}

.game-title {
    font-size: 1.3em;
    font-weight: bold;
    margin-bottom: 8px;
    color: #1e3c72;
}

.game-category {
    display: inline-block;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.85em;
    margin-bottom: 12px;
    width: fit-content;
}

.game-info {
    font-size: 0.95em;
    color: #666;
    margin-bottom: 8px;
}

.game-rating {
    display: flex;
    align-items: center;
    gap: 5px;
    margin-bottom: 12px;
    font-weight: 600;
}

.stars {
    color: #ffc107;
}

.game-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
    padding-top: 15px;
    border-top: 1px solid #e0e0e0;
}

.game-price {
    font-size: 1.3em;
    font-weight: bold;
    color: #27ae60;
}

.game-price.free {
    color: #e74c3c;
}

.btn-cart-add {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    border: none;
    padding: 8px 15px;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-weight: bold;
}

.btn-cart-add:hover {
    transform: scale(1.05);
    box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

/* Empty State */
.empty-state {
    text-align: center;
    padding: 60px 20px;
    background: white;
    border-radius: 15px;
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.empty-state p {
    font-size: 1.5em;
    color: #666;
    margin-bottom: 20px;
}

.btn-reset {
    padding: 12px 30px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    border: none;
    border-radius: 10px;
    font-size: 1em;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn-reset:hover {
    transform: scale(1.05);
}

/* Modal */
.modal {
    display: none;
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.modal-content {
    background-color: white;
    margin: 5% auto;
    padding: 0;
    border-radius: 15px;
    width: 90%;
    max-width: 600px;
    max-height: 80vh;
    display: flex;
    flex-direction: column;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
}

.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    border-bottom: 1px solid #e0e0e0;
}

.modal-header h2 {
    font-size: 1.5em;
    color: #1e3c72;
}

.close-btn {
    background: none;
    border: none;
    font-size: 1.5em;
    cursor: pointer;
    color: #666;
    transition: all 0.3s ease;
}

.close-btn:hover {
    color: #e74c3c;
    transform: scale(1.2);
}

.modal-body {
    overflow-y: auto;
    padding: 20px;
    flex-grow: 1;
}

.modal-footer {
    padding: 20px;
    border-top: 1px solid #e0e0e0;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.cart-total {
    display: flex;
    justify-content: space-between;
    font-size: 1.3em;
    font-weight: bold;
    margin-bottom: 10px;
}

.btn-checkout {
    background: linear-gradient(135deg, #27ae60 0%, #229954 100%);
    color: white;
    border: none;
    padding: 12px 20px;
    border-radius: 10px;
    cursor: pointer;
    font-size: 1em;
    transition: all 0.3s ease;
    font-weight: bold;
}

.btn-checkout:hover {
    transform: scale(1.05);
}

/* Profile Stats Grid */
.profile-section {
    margin-bottom: 30px;
}

.profile-section h3 {
    font-size: 1.3em;
    color: #1e3c72;
    margin-bottom: 15px;
}

.stat-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
}

.stat-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.stat-icon {
    font-size: 2em;
}

.stat-text {
    font-size: 0.9em;
    opacity: 0.9;
}

.stat-number {
    font-size: 1.5em;
    font-weight: bold;
}

.btn-action {
    background: #e74c3c;
    color: white;
    border: none;
    padding: 12px 20px;
    border-radius: 10px;
    cursor: pointer;
    font-size: 1em;
    transition: all 0.3s ease;
    font-weight: bold;
    width: 100%;
}

.btn-action:hover {
    background: #c0392b;
    transform: scale(1.02);
}

/* Favorites Grid */
.favorites-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 15px;
}

.favorite-item {
    background: white;
    border: 2px solid #667eea;
    border-radius: 10px;
    padding: 15px;
    text-align: center;
    position: relative;
}

.favorite-item-emoji {
    font-size: 2.5em;
    margin-bottom: 10px;
}

.favorite-item-title {
    font-weight: bold;
    color: #1e3c72;
    font-size: 0.9em;
    margin-bottom: 10px;
}

.favorite-item-price {
    color: #667eea;
    font-weight: bold;
    margin-bottom: 10px;
}

.btn-remove {
    background: #e74c3c;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
    font-size: 0.8em;
}

/* Cart Items */
.cart-items {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.cart-item {
    background: white;
    border: 1px solid #e0e0e0;
    border-radius: 10px;
    padding: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.cart-item-info {
    flex-grow: 1;
}

.cart-item-title {
    font-weight: bold;
    color: #1e3c72;
    margin-bottom: 5px;
}

.cart-item-price {
    color: #667eea;
    font-weight: bold;
}

.btn-remove-cart {
    background: #e74c3c;
    color: white;
    border: none;
    padding: 5px 15px;
    border-radius: 5px;
    cursor: pointer;
}

/* Responsive */
@media (max-width: 768px) {
    .header {
        flex-direction: column;
        text-align: center;
    }

    .header-content h1 {
        font-size: 1.8em;
    }

    .games-grid {
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
        gap: 15px;
    }

    .filters {
        grid-template-columns: 1fr;
    }

    .stats {
        flex-direction: column;
    }

    .stat-item {
        min-width: auto;
    }

    .modal-content {
        width: 95%;
        margin: 20% auto;
    }

    .favorites-grid {
        grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
    }
}
script.js

js
// Database of Games - Expandido com 48 jogos!
const games = [
    // Ação (7)
    { id: 1, title: "Elden Ring", category: "ação", price: 299.90, rating: 4.8, description: "Jogo de ação e aventura de mundo aberto", emoji: "⚔️" },
    { id: 2, title: "Dark Souls III", category: "ação", price: 199.90, rating: 4.7, description: "Ação desafiadora e viciante", emoji: "☠️" },
    { id: 3, title: "Cyberpunk 2077", category: "ação", price: 179.90, rating: 4.5, description: "Ação em cidade futurista", emoji: "🤖" },
    { id: 4, title: "Valorant", category: "ação", price: 0, rating: 4.5, description: "Shooter tático competitivo gratuito", emoji: "🎯" },
    { id: 5, title: "Counter-Strike 2", category: "ação", price: 0, rating: 4.7, description: "Shooter tático gratuito lendário", emoji: "💣" },
    { id: 6, title: "Warframe", category: "ação", price: 0, rating: 4.4, description: "Ação cooperativa de ficção científica", emoji: "🔫" },
    { id: 7, title: "Apex Legends", category: "ação", price: 0, rating: 4.5, description: "Battle royale de herói gratuito", emoji: "🎮" },

    // RPG (8)
    { id: 8, title: "Baldur's Gate 3", category: "rpg", price: 249.90, rating: 4.9, description: "RPG de fantasia com histórias ricas", emoji: "🧙" },
    { id: 9, title: "The Witcher 3", category: "rpg", price: 89.90, rating: 4.8, description: "RPG com história memorável", emoji: "🧔" },
    { id: 10, title: "Final Fantasy VII Remake", category: "rpg", price: 249.90, rating: 4.7, description: "RPG clássico reimaginado", emoji: "💫" },
    { id: 11, title: "Lost Ark", category: "rpg", price: 0, rating: 4.3, description: "MMORPG de ação isométrico", emoji: "⚔️" },
    { id: 12, title: "Path of Exile", category: "rpg", price: 0, rating: 4.6, description: "RPG de ação dark gratuito", emoji: "💀" },
    { id: 13, title: "Neverwinter", category: "rpg", price: 0, rating: 4.2, description: "MMO de Dungeons & Dragons gratuito", emoji: "🐉" },
    { id: 14, title: "Diablo IV", category: "rpg", price: 249.90, rating: 4.5, description: "RPG de ação dark e épico", emoji: "👿" },
    { id: 15, title: "Dragon's Dogma 2", category: "rpg", price: 299.90, rating: 4.6, description: "RPG de ação medieval com dragões", emoji: "🐲" },

    // Estratégia (8)
    { id: 16, title: "StarCraft II", category: "estratégia", price: 0, rating: 4.6, description: "Estratégia em tempo real clássico", emoji: "🚀" },
    { id: 17, title: "Dota 2", category: "estratégia", price: 0, rating: 4.7, description: "MOBA estratégico competitivo", emoji: "👹" },
    { id: 18, title: "League of Legends", category: "estratégia", price: 0, rating: 4.6, description: "MOBA mais popular do mundo", emoji: "⚡" },
    { id: 19, title: "Age of Empires IV", category: "estratégia", price: 199.90, rating: 4.4, description: "Estratégia histórica clássica", emoji: "🏰" },
    { id: 20, title: "Civilization VI", category: "estratégia", price: 149.90, rating: 4.6, description: "Estratégia por turnos épica", emoji: "🗺️" },
    { id: 21, title: "Total War: Warhammer III", category: "estratégia", price: 249.90, rating: 4.4, description: "Estratégia com batalhas épicas", emoji: "⚔️" },
    { id: 22, title: "Company of Heroes 3", category: "estratégia", price: 199.90, rating: 4.3, description: "Estratégia militar tática", emoji: "🪖" },
    { id: 23, title: "They Are Billions", category: "estratégia", price: 29.90, rating: 4.5, description: "Estratégia de construção e defesa", emoji: "🧟" },

    // Puzzle (5)
    { id: 24, title: "Portal 2", category: "puzzle", price: 49.90, rating: 4.9, description: "Puzzle criativo e inovador", emoji: "🟠" },
    { id: 25, title: "Tetris Effect Connected", category: "puzzle", price: 29.90, rating: 4.5, description: "Puzzle clássico com visual moderno", emoji: "🟨" },
    { id: 26, title: "The Witness", category: "puzzle", price: 39.90, rating: 4.4, description: "Puzzle atmosférico de exploração", emoji: "👁️" },
    { id: 27, title: "Braid", category: "puzzle", price: 14.90, rating: 4.6, description: "Puzzle de plataforma com manipulação de tempo", emoji: "⏰" },
    { id: 28, title: "Portal Remastered", category: "puzzle", price: 9.90, rating: 4.7, description: "Puzzle clássico remaster", emoji: "🟢" },

    // Corrida (5)
    { id: 29, title: "Forza Motorsport 5", category: "corrida", price: 199.90, rating: 4.7, description: "Simulador de corrida premium", emoji: "🏎️" },
    { id: 30, title: "Need for Speed Unbound", category: "corrida", price: 199.90, rating: 4.3, description: "Corrida urbana com estilo", emoji: "🏁" },
    { id: 31, title: "Gran Turismo Sport", category: "corrida", price: 99.90, rating: 4.5, description: "Simulador de corrida realista", emoji: "🏍️" },
    { id: 32, title: "Assetto Corsa Competizione", category: "corrida", price: 89.90, rating: 4.6, description: "Simulador de corrida profissional", emoji: "🏆" },
    { id: 33, title: "F1 24", category: "corrida", price: 249.90, rating: 4.4, description: "Simulador de Fórmula 1", emoji: "🏁" },

    // Esportes (5)
    { id: 34, title: "FIFA 24", category: "esportes", price: 249.90, rating: 4.2, description: "Simulador de futebol mais popular do mundo", emoji: "⚽" },
    { id: 35, title: "NBA 2K24", category: "esportes", price: 229.90, rating: 4.1, description: "Simulador de basquete oficial", emoji: "🏀" },
    { id: 36, title: "Pro Evolution Soccer 2024", category: "esportes", price: 179.90, rating: 4.3, description: "Simulador de futebol alternativo", emoji: "⚾" },
    { id: 37, title: "WWE 2K24", category: "esportes", price: 249.90, rating: 4.4, description: "Simulador de luta livre profissional", emoji: "🥊" },
    { id: 38, title: "Mario Kart 8 Deluxe", category: "esportes", price: 299.90, rating: 4.9, description: "Corrida arcade com personagens Nintendo", emoji: "🍄" },

    // Aventura (4)
    { id: 39, title: "The Legend of Zelda: Tears of the Kingdom", category: "aventura", price: 299.90, rating: 4.9, description: "Aventura épica em mundo aberto", emoji: "🗡️" },
    { id: 40, title: "Grounded", category: "aventura", price: 79.90, rating: 4.4, description: "Aventura de sobrevivência no quintal", emoji: "🐛" },
    { id: 41, title: "Uncharted: Legacy of Thieves", category: "aventura", price: 99.90, rating: 4.6, description: "Aventura de ação cinematográfica", emoji: "💎" },
    { id: 42, title: "Tomb Raider (2024)", category: "aventura", price: 249.90, rating: 4.5, description: "Aventura de exploração e ação", emoji: "🏺" },

    // Simulação (4)
    { id: 43, title: "Microsoft Flight Simulator", category: "simulação", price: 99.90, rating: 4.8, description: "Simulador de voo ultra realista", emoji: "✈️" },
    { id: 44, title: "Stardew Valley", category: "simulação", price: 39.90, rating: 4.9, description: "Simulador de fazenda relaxante", emoji: "🌾" },
    { id: 45, title: "Cities: Skylines", category: "simulação", price: 49.90, rating: 4.7, description: "Simulador de construção de cidades", emoji: "🏙️" },
    { id: 46, title: "Planet Coaster", category: "simulação", price: 99.90, rating: 4.6, description: "Simulador de parque de diversões", emoji: "🎡" },

    // Terror (3)
    { id: 47, title: "Phasmophobia", category: "terror", price: 39.90, rating: 4.7, description: "Caça de fantasmas cooperativa", emoji: "👻" },
    { id: 48, title: "Outlast", category: "terror", price: 29.90, rating: 4.4, description: "Horror de sobrevivência intenso", emoji: "😨" },
];

// State
let filteredGames = [...games];
let favorites = JSON.parse(localStorage.getItem('favorites')) || [];
let cart = JSON.parse(localStorage.getItem('cart')) || [];
let stats = JSON.parse(localStorage.getItem('stats')) || { viewed: 0, spent: 0 };

// Initialize
function init() {
    document.getElementById('totalAllGames').textContent = games.length;
    applyFilters();
    updateCounters();
}

// Get price range
function getPriceRange(price) {
    if (price === 0) return 'gratuito';
    if (price <= 50) return 'ate50';
    if (price <= 100) return '50a100';
    return 'acima100';
}

// Apply filters
function applyFilters() {
    const searchValue = document.getElementById('searchInput').value.toLowerCase();
    const categoryValue = document.getElementById('categoryFilter').value;
    const priceValue = document.getElementById('priceFilter').value;
    const sortValue = document.getElementById('sortFilter').value;

    filteredGames = games.filter(game => {
        const matchSearch = game.title.toLowerCase().includes(searchValue) || 
                          game.description.toLowerCase().includes(searchValue);
        const matchCategory = !categoryValue || game.category === categoryValue;
        const matchPrice = !priceValue || getPriceRange(game.price) === priceValue;
        return matchSearch && matchCategory && matchPrice;
    });

    switch(sortValue) {
        case 'nome':
            filteredGames.sort((a, b) => a.title.localeCompare(b.title));
            break;
        case 'preco-asc':
            filteredGames.sort((a, b) => a.price - b.price);
            break;
        case 'preco-desc':
            filteredGames.sort((a, b) => b.price - a.price);
            break;
        case 'nota':
            filteredGames.sort((a, b) => b.rating - a.rating);
            break;
    }

    renderGames();
    updateStats();
}

// Render games
function renderGames() {
    const container = document.getElementById('gamesContainer');
    const emptyState = document.getElementById('emptyState');

    if (filteredGames.length === 0) {
        container.style.display = 'none';
        emptyState.style.display = 'block';
        return;
    }

    container.style.display = 'grid';
    emptyState.style.display = 'none';

    container.innerHTML = filteredGames.map(game => {
        const isFav = favorites.some(f => f.id === game.id);
        return `
            <div class="game-card">
                <button class="btn-fav" onclick="toggleFavorite(${game.id}, event)" title="Adicionar aos favoritos">
                    ${isFav ? '❤️' : '🤍'}
                </button>
                <div class="game-image" onclick="selectGame(${game.id})">${game.emoji}</div>
                <div class="game-content">
                    <h3 class="game-title">${game.title}</h3>
                    <span class="game-category">${capitalizeFirst(game.category)}</span>
                    <p class="game-info">${game.description}</p>
                    <div class="game-rating">
                        <span class="stars">⭐</span>
                        <span>${game.rating}</span>
                    </div>
                    <div class="game-footer">
                        <div class="game-price ${game.price === 0 ? 'free' : ''}">
                            ${game.price === 0 ? 'GRÁTIS' : `R$ ${game.price.toFixed(2).replace('.', ',')}`}
                        </div>
                        <button class="btn-cart-add" onclick="addToCart(${game.id})">🛒</button>
                    </div>
                </div>
            </div>
        `;
    }).join('');
}

// Toggle favorite
function toggleFavorite(id, event) {
    event.stopPropagation();
    const game = games.find(g => g.id === id);
    const index = favorites.findIndex(f => f.id === id);
    
    if (index > -1) {
        favorites.splice(index, 1);
    } else {
        favorites.push(game);
    }
    
    localStorage.setItem('favorites', JSON.stringify(favorites));
    updateCounters();
    renderGames();
}

// Add to cart
function addToCart(id) {
    const game = games.find(g => g.id === id);
    const existsInCart = cart.some(item => item.id === id);
    
    if (!existsInCart) {
        cart.push(game);
        localStorage.setItem('cart', JSON.stringify(cart));
        updateCounters();
        alert(`${game.title} adicionado ao carrinho!`);
    } else {
        alert(`${game.title} já está no carrinho!`);
    }
}

// Remove from cart
function removeFromCart(id) {
    cart = cart.filter(item => item.id !== id);
    localStorage.setItem('cart', JSON.stringify(cart));
    updateCounters();
    renderCart();
}

// Update stats
function updateStats() {
    document.getElementById('totalGames').textContent = filteredGames.length;
    
    let activeFilters = 0;
    if (document.getElementById('searchInput').value) activeFilters++;
    if (document.getElementById('categoryFilter').value) activeFilters++;
    if (document.getElementById('priceFilter').value) activeFilters++;
    
    document.getElementById('activeFilters').textContent = activeFilters;
}

// Update counters
function updateCounters() {
    document.getElementById('favCount').textContent = favorites.length;
    document.getElementById('cartCount').textContent = cart.length;
    renderFavorites();
    renderCart();
    updateProfileStats();
}

// Render favorites
function renderFavorites() {
    const body = document.getElementById('favoritesBody');
    
    if (favorites.length === 0) {
        body.innerHTML = '<p style="text-align: center; color: #999;">Nenhum favorito ainda</p>';
        return;
    }
    
    body.innerHTML = `
        <div class="favorites-grid">
            ${favorites.map(game => `
                <div class="favorite-item">
                    <div class="favorite-item-emoji">${game.emoji}</div>
                    <div class="favorite-item-title">${game.title}</div>
                    <div class="favorite-item-price">${game.price === 0 ? 'GRÁTIS' : `R$ ${game.price.toFixed(2).replace('.', ',')}`}</div>
                    <button class="btn-remove" onclick="toggleFavorite(${game.id}, event)">Remover</button>
                </div>
            `).join('')}
        </div>
    `;
}

// Render cart
function renderCart() {
    const body = document.getElementById('cartBody');
    const footer = document.getElementById('cartFooter');
    
    if (cart.length === 0) {
        body.innerHTML = '<p style="text-align: center; color: #999;">Carrinho vazio</p>';
        footer.style.display = 'none';
        return;
    }
    
    const total = cart.reduce((sum, game) => sum + game.price, 0);
    
    body.innerHTML = `
        <div class="cart-items">
            ${cart.map(game => `
                <div class="cart-item">
                    <div class="cart-item-info">
                        <div class="cart-item-title">${game.emoji} ${game.title}</div>
                        <div class="cart-item-price">${game.price === 0 ? 'GRÁTIS' : `R$ ${game.price.toFixed(2).replace('.', ',')}`}</div>
                    </div>
                    <button class="btn-remove-cart" onclick="removeFromCart(${game.id})">Remover</button>
                </div>
            `).join('')}
        </div>
    `;
    
    footer.style.display = 'flex';
    document.getElementById('cartTotal').textContent = `R$ ${total.toFixed(2).replace('.', ',')}`;
}

// Update profile stats
function updateProfileStats() {
    document.getElementById('statsViewed').textContent = stats.viewed;
    document.getElementById('statsFav').textContent = favorites.length;
    document.getElementById('statsCart').textContent = cart.length;
    document.getElementById('statsSpent').textContent = `R$ ${stats.spent.toFixed(2).replace('.', ',')}`;
}

// Select game
function selectGame(id) {
    const game = games.find(g => g.id === id);
    stats.viewed++;
    localStorage.setItem('stats', JSON.stringify(stats));
    updateCounters();
    alert(`${game.emoji} ${game.title}\n\n⭐ Avaliação: ${game.rating}/5\n💰 Preço: ${game.price === 0 ? 'GRÁTIS' : `R$ ${game.price.toFixed(2).replace('.', ',')}`}\n\n${game.description}`);
}

// Toggle modals
function toggleFavorites() {
    const modal = document.getElementById('favoritesModal');
    modal.style.display = modal.style.display === 'block' ? 'none' : 'block';
}

function toggleCart() {
    const modal = document.getElementById('cartModal');
    modal.style.display = modal.style.display === 'block' ? 'none' : 'block';
}

function toggleProfile() {
    const modal = document.getElementById('profileModal');
    modal.style.display = modal.style.display === 'block' ? 'none' : 'block';
}

// Reset filters
function resetFilters() {
    document.getElementById('searchInput').value = '';
    document.getElementById('categoryFilter').value = '';
    document.getElementById('priceFilter').value = '';
    document.getElementById('sortFilter').value = 'nome';
    applyFilters();
}

// Clear all data
function clearAllData() {
    if (confirm('Tem certeza que quer apagar todos os dados?')) {
        favorites = [];
        cart = [];
        stats = { viewed: 0, spent: 0 };
        localStorage.removeItem('favorites');
        localStorage.removeItem('cart');
        localStorage.removeItem('stats');
        updateCounters();
        alert('Dados apagados com sucesso!');
    }
}

// Helper function
function capitalizeFirst(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
}

// Event listeners
document.getElementById('searchInput').addEventListener('input', applyFilters);
document.getElementById('categoryFilter').addEventListener('change', applyFilters);
document.getElementById('priceFilter').addEventListener('change', applyFilters);
document.getElementById('sortFilter').addEventListener('change', applyFilters);

// Close modals when clicking outside
window.addEventListener('click', (event) => {
    const favModal = document.getElementById('favoritesModal');
    const cartModal = document.getElementById('cartModal');
    const profileModal = document.getElementById('profileModal');
    
    if (event.target === favModal) favModal.style.display = 'none';
    if (event.target === cartModal) cartModal.style.display = 'none';
    if (event.target === profileModal) profileModal.style.display = 'none';
});

// Initial render
window.addEventListener('DOMContentLoaded', init);
README.md

git clone https://github.com/lucaseduardosilvax2-ui/luck-games.git
cd luck-games
