# Html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RPG Party - Sem Login</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- TELA INICIAL -->
    <div id="tela-inicial" class="tela-container">
        <div class="container-inicial">
            <h1>🎲 RPG Party</h1>
            <p class="subtitulo">Aventuras em grupo, sem complicações</p>
            
            <div class="form-inicial">
                <div class="input-group">
                    <label for="apelido">Seu Apelido:</label>
                    <input type="text" id="apelido" placeholder="Digite seu nome ou apelido" maxlength="20">
                </div>

                <div class="button-group">
                    <button id="btn-criar-party" class="btn btn-primary">
                        ✨ Criar Party
                    </button>
                </div>

                <div class="divisor">OU</div>

                <div class="input-group">
                    <label for="codigo-party">Entrar em uma Party:</label>
                    <input type="text" id="codigo-party" placeholder="Digite o código da party" maxlength="6">
                    <button id="btn-entrar-party" class="btn btn-secondary">
                        Entrar
                    </button>
                </div>
            </div>

            <div id="erro-msg" class="erro-msg"></div>
        </div>
    </div>

    <!-- PARTY ROOM -->
    <div id="party-room" class="tela-container hidden">
        <div class="header-party">
            <div class="header-esquerda">
                <button id="btn-escudo-mestre" class="btn btn-mestre hidden">
                    🛡️ Escudo do Mestre
                </button>
            </div>
            
            <div class="header-centro">
                <h2 id="titulo-party">Party</h2>
            </div>

            <div class="header-direita">
                <div class="codigo-party">
                    <span>Código: <strong id="codigo-display"></strong></span>
                    <button id="btn-copiar-codigo" class="btn-pequeno">📋</button>
                </div>
                <button id="btn-sair" class="btn btn-danger">Sair</button>
            </div>
        </div>

        <div class="party-content">
            <!-- COLUNA ESQUERDA (4 seções) -->
            <div class="coluna-esquerda">
                
                <!-- 1. JOGADORES -->
                <div class="secao jogadores-secao">
                    <h3>👥 Jogadores</h3>
                    <div id="lista-jogadores" class="lista-jogadores"></div>
                </div>

                <!-- 2. DADOS -->
                <div class="secao dados-secao">
                    <h3>🎲 Dados</h3>
                    <div class="botoes-dados">
                        <button class="btn-dado" data-lados="4">d4</button>
                        <button class="btn-dado" data-lados="8">d8</button>
                        <button class="btn-dado" data-lados="10">d10</button>
                        <button class="btn-dado" data-lados="12">d12</button>
                        <button class="btn-dado" data-lados="20">d20</button>
                        <button class="btn-dado" data-lados="100">d100</button>
                    </div>
                </div>

                <!-- 3. RESULTADO DOS DADOS -->
                <div class="secao resultado-secao">
                    <h3>📊 Resultado</h3>
                    <div id="resultado-dados" class="resultado-dados">
                        <p class="placeholder">Lance um dado para ver o resultado</p>
                    </div>
                </div>

                <!-- 4. ANOTAÇÕES -->
                <div class="secao anotacoes-secao">
                    <h3>📝 Anotações</h3>
                    <textarea id="anotacoes-jogadores" class="textarea-grande" placeholder="Suas anotações aqui..."></textarea>
                </div>
            </div>

            <!-- COLUNA DIREITA (IMAGENS - GRANDE) -->
            <div class="coluna-direita">
                <div class="secao imagens-secao">
                    <h3>🖼️ Imagens</h3>
                    <div id="area-imagens" class="area-imagens">
                        <p class="placeholder">Imagens aparecerão aqui</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- ESCUDO DO MESTRE (Modal) -->
    <div id="modal-escudo" class="modal hidden">
        <div class="modal-content modal-grande">
            <div class="modal-header">
                <h2>🛡️ Escudo do Mestre</h2>
                <button id="btn-fechar-escudo" class="btn-fechar">&times;</button>
            </div>

            <div class="modal-tabs">
                <button class="tab-btn ativo" data-tab="anotacoes-mestre">📝 Anotações</button>
                <button class="tab-btn" data-tab="imagens-publicas">🖼️ Imagens Públicas</button>
                <button class="tab-btn" data-tab="imagens-privadas">🔒 Imagens Privadas</button>
                <button class="tab-btn" data-tab="mapa">🗺️ Mapa</button>
                <button class="tab-btn" data-tab="fichas">📄 Fichas</button>
            </div>

            <div class="modal-body">
                
                <!-- TAB 1: ANOTAÇÕES MESTRE -->
                <div id="anotacoes-mestre" class="tab-content ativo">
                    <h3>Suas Anotações Privadas</h3>
                    <textarea id="textarea-anotacoes-mestre" class="textarea-grande" placeholder="Escreva suas anotações secretas aqui..."></textarea>
                </div>

                <!-- TAB 2: IMAGENS PÚBLICAS -->
                <div id="imagens-publicas" class="tab-content">
                    <h3>Imagens Públicas</h3>
                    <div class="imagem-upload">
                        <label>Upload de Imagem:</label>
                        <input type="file" id="upload-imagem-publica" accept="image/*">
                        <div id="preview-publica" class="preview-imagem"></div>
                    </div>
                    <div class="imagem-controls">
                        <label>Controles:</label>
                        <div class="controles-flex">
                            <div>
                                <label>Posição X:</label>
                                <input type="range" id="pos-x-publica" min="0" max="100" value="0">
                                <span id="valor-x-publica">0</span>
                            </div>
                            <div>
                                <label>Posição Y:</label>
                                <input type="range" id="pos-y-publica" min="0" max="100" value="0">
                                <span id="valor-y-publica">0</span>
                            </div>
                            <div>
                                <label>Tamanho (%):</label>
                                <input type="range" id="tamanho-publica" min="10" max="200" value="100">
                                <span id="valor-tamanho-publica">100</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- TAB 3: IMAGENS PRIVADAS -->
                <div id="imagens-privadas" class="tab-content">
                    <h3>Imagens Privadas (Apenas você vê)</h3>
                    <div class="imagem-upload">
                        <label>Upload de Imagem Privada:</label>
                        <input type="file" id="upload-imagem-privada" accept="image/*">
                        <div id="preview-privada" class="preview-imagem"></div>
                    </div>
                </div>

                <!-- TAB 4: MAPA -->
                <div id="mapa" class="tab-content">
                    <h3>Mapa (Grid Automático)</h3>
                    <div class="imagem-upload">
                        <label>Upload do Mapa:</label>
                        <input type="file" id="upload-mapa" accept="image/*">
                        <p class="info-texto">O mapa anterior será substituído automaticamente</p>
                    </div>
                    <div id="preview-mapa" class="preview-imagem-grande"></div>
                </div>

                <!-- TAB 5: FICHAS -->
                <div id="fichas" class="tab-content">
                    <h3>Fichas</h3>
                    
                    <div class="fichas-container">
                        <div class="ficha-tipo">
                            <h4>⚔️ Ficha de Inimigo</h4>
                            <div class="form-ficha">
                                <input type="text" id="inimigo-nome" placeholder="Nome do inimigo" maxlength="30">
                                <input type="number" id="inimigo-poder" placeholder="Poder" min="0">
                                <input type="number" id="inimigo-dano" placeholder="Dano" min="0">
                                <textarea id="inimigo-complementos" placeholder="Complementos adicionais" rows="3"></textarea>
                                <button id="btn-criar-inimigo" class="btn btn-primary">Criar Ficha de Inimigo</button>
                            </div>
                            <div id="lista-inimigos" class="lista-fichas"></div>
                        </div>

                        <div class="ficha-tipo">
                            <h4>🧙 Ficha de NPC</h4>
                            <div class="form-ficha">
                                <input type="text" id="npc-nome" placeholder="Nome do NPC" maxlength="30">
                                <input type="number" id="npc-idade" placeholder="Idade" min="0" max="150">
                                <textarea id="npc-complemento" placeholder="Descrição/Complementos" rows="3"></textarea>
                                <button id="btn-criar-npc" class="btn btn-primary">Criar Ficha de NPC</button>
                            </div>
                            <div id="lista-npcs" class="lista-fichas"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
