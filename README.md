# Maqvend<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MaqVendas - Sistema de Propostas</title>
    <!-- PWA -->
    <link rel="manifest" href="manifest.json">
    <meta name="theme-color" content="#2563eb">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="MaqVendas">
    <link rel="apple-touch-icon" href="icons/icon-152x152.png">
    <link rel="apple-touch-icon" sizes="192x192" href="icons/icon-192x192.png">
    <link rel="apple-touch-icon" sizes="512x512" href="icons/icon-512x512.png">
    <!-- Styles & Scripts -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="stylesheet" href="styles.css">
    <!-- Biblioteca para gerar PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
</head>
<body>
    <!-- Tela de Login -->
    <div id="login-screen" class="screen active">
        <div class="login-container">
            <div class="login-logo">
                <i class="fas fa-industry"></i>
                <h1>MaqVendas</h1>
                <p>Sistema de Propostas</p>
            </div>
            <div id="login-form">
                <div class="form-group">
                    <label for="login-email">Email</label>
                    <input type="email" id="login-email" placeholder="seu.email@empresa.com.br">
                </div>
                <div class="form-group">
                    <label for="login-senha">Senha</label>
                    <input type="password" id="login-senha" placeholder="Digite sua senha">
                </div>
                <button type="button" class="btn-login" id="btn-entrar">
                    <i class="fas fa-sign-in-alt"></i> Entrar
                </button>
                <div class="forgot-password">
                    <a href="#" id="btn-esqueci-senha">Esqueci minha senha</a>
                </div>
            </div>
            <div id="login-error" class="error-message"></div>
            <div id="login-success" class="success-message"></div>
        </div>
    </div>

    <!-- Menu Principal -->
    <div id="menu-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <i class="fas fa-industry"></i>
                <span>MaqVendas</span>
            </div>
            <div class="header-right">
                <span id="usuario-logado"></span>
                <button id="btn-logout" class="btn-logout" title="Sair">
                    <i class="fas fa-sign-out-alt"></i>
                </button>
            </div>
        </header>
        
        <main class="menu-grid">
            <div class="menu-item" id="menu-clientes">
                <i class="fas fa-users"></i>
                <span>Clientes</span>
            </div>
            <div class="menu-item" id="menu-maquinas">
                <i class="fas fa-cogs"></i>
                <span>Máquinas</span>
            </div>
            <div class="menu-item" id="menu-propostas">
                <i class="fas fa-file-invoice-dollar"></i>
                <span>Propostas</span>
            </div>
            <div class="menu-item" id="menu-catalogos">
                <i class="fas fa-book-open"></i>
                <span>Catálogos</span>
            </div>
            <div class="menu-item" id="menu-relatorios">
                <i class="fas fa-chart-bar"></i>
                <span>Relatórios</span>
            </div>
            <div class="menu-item" id="menu-posvenda">
                <i class="fas fa-tools"></i>
                <span>Pós-Venda</span>
            </div>
        </main>
    </div>

    <!-- Módulo Clientes -->
    <div id="clientes-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-clientes"><i class="fas fa-arrow-left"></i></button>
                <span>Clientes</span>
            </div>
            <div class="header-right">
                <button id="btn-novo-cliente" class="btn-add">
                    <i class="fas fa-plus"></i>
                </button>
            </div>
        </header>
        
        <div class="search-bar">
            <i class="fas fa-search"></i>
            <input type="text" id="busca-cliente" placeholder="Buscar cliente...">
        </div>
        
        <div id="lista-clientes" class="lista-cards"></div>
        
        <!-- Modal Cliente -->
        <div id="modal-cliente" class="modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2 id="modal-cliente-titulo">Novo Cliente</h2>
                    <button class="btn-close-modal" id="fechar-modal-cliente"><i class="fas fa-times"></i></button>
                </div>
                <form id="form-cliente">
                    <input type="hidden" id="cliente-id">
                    <div class="form-group">
                        <label>Razão Social *</label>
                        <input type="text" id="cliente-razao" required>
                    </div>
                    <div class="form-group">
                        <label>Nome Fantasia</label>
                        <input type="text" id="cliente-fantasia">
                    </div>
                    <div class="form-group">
                        <label>CNPJ</label>
                        <input type="text" id="cliente-cnpj" placeholder="00.000.000/0000-00">
                    </div>
                    <div class="form-group">
                        <label>Telefone</label>
                        <input type="text" id="cliente-telefone" placeholder="(00) 00000-0000">
                    </div>
                    <div class="form-group">
                        <label>Email</label>
                        <input type="email" id="cliente-email">
                    </div>
                    <div class="form-group">
                        <label>Cidade</label>
                        <input type="text" id="cliente-cidade">
                    </div>
                    <div class="form-group">
                        <label>Estado</label>
                        <select id="cliente-estado">
                            <option value="">Selecione...</option>
                            <option value="AC">AC</option><option value="AL">AL</option><option value="AP">AP</option>
                            <option value="AM">AM</option><option value="BA">BA</option><option value="CE">CE</option>
                            <option value="DF">DF</option><option value="ES">ES</option><option value="GO">GO</option>
                            <option value="MA">MA</option><option value="MT">MT</option><option value="MS">MS</option>
                            <option value="MG">MG</option><option value="PA">PA</option><option value="PB">PB</option>
                            <option value="PR">PR</option><option value="PE">PE</option><option value="PI">PI</option>
                            <option value="RJ">RJ</option><option value="RN">RN</option><option value="RS">RS</option>
                            <option value="RO">RO</option><option value="RR">RR</option><option value="SC">SC</option>
                            <option value="SP">SP</option><option value="SE">SE</option><option value="TO">TO</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Contato</label>
                        <input type="text" id="cliente-contato">
                    </div>
                    <div class="form-actions">
                        <button type="button" class="btn-cancel" id="cancelar-cliente">Cancelar</button>
                        <button type="submit" class="btn-save">Salvar</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Módulo Máquinas -->
    <div id="maquinas-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-maquinas"><i class="fas fa-arrow-left"></i></button>
                <span>Máquinas</span>
            </div>
            <div class="header-right">
                <button id="btn-sincronizar-catalogos" class="btn-add" style="background:#10b981;margin-right:8px;" title="Criar máquinas a partir dos catálogos">
                    <i class="fas fa-sync"></i>
                </button>
                <button id="btn-nova-maquina" class="btn-add">
                    <i class="fas fa-plus"></i>
                </button>
            </div>
        </header>
        
        <div class="search-bar">
            <i class="fas fa-search"></i>
            <input type="text" id="busca-maquina" placeholder="Buscar máquina...">
        </div>
        
        <div id="lista-maquinas" class="lista-cards"></div>
        
        <!-- Modal Máquina -->
        <div id="modal-maquina" class="modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2 id="modal-maquina-titulo">Nova Máquina</h2>
                    <button class="btn-close-modal" id="fechar-modal-maquina"><i class="fas fa-times"></i></button>
                </div>
                <form id="form-maquina">
                    <input type="hidden" id="maquina-id">
                    <div class="form-group">
                        <label>Modelo *</label>
                        <input type="text" id="maquina-modelo" required>
                    </div>
                    <div class="form-group">
                        <label>Fabricante</label>
                        <input type="text" id="maquina-fabricante">
                    </div>
                    <div class="form-group">
                        <label>Categoria</label>
                        <select id="maquina-categoria">
                            <option value="">Selecione...</option>
                            <option value="Escavadeira">Escavadeira</option>
                            <option value="Mini Escavadeira">Mini Escavadeira</option>
                            <option value="Carregadeira">Carregadeira</option>
                            <option value="Mini Carregadeira">Mini Carregadeira</option>
                            <option value="Retroescavadeira">Retroescavadeira</option>
                            <option value="Rolo Compactador">Rolo Compactador</option>
                            <option value="Empilhadeira">Empilhadeira</option>
                            <option value="Trator">Trator</option>
                            <option value="Outro">Outro</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Ano</label>
                        <input type="number" id="maquina-ano" min="1950" max="2030">
                    </div>
                    <div class="form-group">
                        <label>Preço (R$)</label>
                        <input type="text" id="maquina-preco" placeholder="0,00">
                    </div>
                    <div class="form-group">
                        <label>Descrição</label>
                        <textarea id="maquina-descricao" rows="3"></textarea>
                    </div>
                    <div class="form-group">
                        <label>Condição</label>
                        <select id="maquina-condicao">
                            <option value="Nova">Nova</option>
                            <option value="Usada">Usada</option>
                            <option value="Recondicionada">Recondicionada</option>
                        </select>
                    </div>
                    <div class="form-actions">
                        <button type="button" class="btn-cancel" id="cancelar-maquina">Cancelar</button>
                        <button type="submit" class="btn-save">Salvar</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Módulo Propostas -->
    <div id="propostas-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-propostas"><i class="fas fa-arrow-left"></i></button>
                <span>Propostas</span>
            </div>
            <div class="header-right">
                <button id="btn-nova-proposta" class="btn-add">
                    <i class="fas fa-plus"></i>
                </button>
            </div>
        </header>
        
        <div class="search-bar">
            <i class="fas fa-search"></i>
            <input type="text" id="busca-proposta" placeholder="Buscar proposta...">
        </div>
        
        <div class="filter-tabs">
            <button class="filter-tab active" data-status="todas">Todas</button>
            <button class="filter-tab" data-status="Pendente">Pendentes</button>
            <button class="filter-tab" data-status="Aprovada">Aprovadas</button>
            <button class="filter-tab" data-status="Reprovada">Reprovadas</button>
        </div>
        
        <div id="lista-propostas" class="lista-cards"></div>
        
        <!-- Modal Proposta -->
        <div id="modal-proposta" class="modal">
            <div class="modal-content modal-large">
                <div class="modal-header">
                    <h2 id="modal-proposta-titulo">Nova Proposta</h2>
                    <button class="btn-close-modal" id="fechar-modal-proposta"><i class="fas fa-times"></i></button>
                </div>
                <form id="form-proposta">
                    <input type="hidden" id="proposta-id">
                    <div class="form-group">
                        <label>Empresa Emissora *</label>
                        <select id="proposta-empresa" required>
                            <option value="">Selecione a empresa...</option>
                            <option value="CF Comex">CF Comex Equipamentos e Serviços Ltda</option>
                            <option value="Enjoy Comex">Enjoy Comex Ltda</option>
                        </select>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label>Cliente *</label>
                            <div class="autocomplete-wrap" style="position:relative;">
                                <input type="text" id="proposta-cliente-busca" placeholder="Digite para buscar cliente..." autocomplete="off" required>
                                <input type="hidden" id="proposta-cliente">
                                <div id="proposta-cliente-lista" class="autocomplete-list"></div>
                            </div>
                        </div>
                        <div class="form-group">
                            <label>Data</label>
                            <input type="date" id="proposta-data">
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Máquina *</label>
                        <select id="proposta-maquina" required>
                            <option value="">Selecione...</option>
                        </select>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label>Valor (R$) *</label>
                            <input type="text" id="proposta-valor" placeholder="0,00" required>
                        </div>
                        <div class="form-group">
                            <label>Condição Pagamento</label>
                            <select id="proposta-pagamento">
                                <option value="À Vista">À Vista</option>
                                <option value="30 dias">30 dias</option>
                                <option value="30/60 dias">30/60 dias</option>
                                <option value="30/60/90 dias">30/60/90 dias</option>
                                <option value="Financiamento">Financiamento</option>
                                <option value="Outro">Outro</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Validade da Proposta</label>
                        <input type="number" id="proposta-validade" value="15" min="1"> dias
                    </div>
                    <div class="form-group">
                        <label>Observações</label>
                        <textarea id="proposta-obs" rows="3"></textarea>
                    </div>
                    <div class="form-group">
                        <label>Status</label>
                        <select id="proposta-status">
                            <option value="Pendente">Pendente</option>
                            <option value="Aprovada">Aprovada</option>
                            <option value="Reprovada">Reprovada</option>
                        </select>
                    </div>
                    <div class="form-actions" style="flex-wrap: wrap; gap: 8px;">
                        <button type="button" class="btn-cancel" id="cancelar-proposta">Cancelar</button>
                        <button type="button" id="btn-gerar-pdf" class="btn-pdf">
                            <i class="fas fa-file-pdf"></i> PDF
                        </button>
                        <button type="button" id="btn-whatsapp" style="background:#25D366;color:#fff;border:none;padding:12px 16px;border-radius:8px;cursor:pointer;font-weight:600;">
                            <i class="fab fa-whatsapp"></i> WhatsApp
                        </button>
                        <button type="button" id="btn-email" style="background:#EA4335;color:#fff;border:none;padding:12px 16px;border-radius:8px;cursor:pointer;font-weight:600;">
                            <i class="fas fa-envelope"></i> Email
                        </button>
                        <button type="submit" class="btn-save">Salvar</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Módulo Catálogos -->
    <div id="catalogos-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-catalogos"><i class="fas fa-arrow-left"></i></button>
                <span>Catálogos</span>
            </div>
            <div class="header-right">
                <button id="btn-importar-catalogos" class="btn-add" style="background:#10b981;margin-right:8px;" title="Importar vários PDFs">
                    <i class="fas fa-upload"></i>
                </button>
                <button id="btn-novo-catalogo" class="btn-add">
                    <i class="fas fa-plus"></i>
                </button>
            </div>
        </header>
        
        <div class="search-bar">
            <i class="fas fa-search"></i>
            <input type="text" id="busca-catalogo" placeholder="Buscar catálogo...">
        </div>
        
        <div id="lista-catalogos" class="lista-cards catalogos-grid"></div>
        
        <!-- Modal Importação em Lote -->
        <div id="modal-importar" class="modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>📦 Importar Catálogos em Lote</h2>
                    <button class="btn-close-modal" id="fechar-modal-importar"><i class="fas fa-times"></i></button>
                </div>
                <div style="padding:20px">
                    <p style="margin-bottom:15px;color:#666">Selecione vários arquivos PDF para importar de uma vez:</p>
                    <input type="file" id="arquivos-importar" accept=".pdf" multiple style="padding:15px;width:100%;border:2px dashed #ccc;border-radius:8px;margin-bottom:15px;">
                    <div id="lista-importar" style="max-height:300px;overflow-y:auto;margin-bottom:15px;"></div>
                    <label style="display:flex;align-items:center;gap:10px;margin-bottom:15px;cursor:pointer;padding:10px;background:#f0fdf4;border-radius:8px;border:1px solid #10b981;">
                        <input type="checkbox" id="criar-maquinas" checked style="width:20px;height:20px;">
                        <span style="color:#166534;font-weight:500;"><i class="fas fa-cogs"></i> Criar máquinas automaticamente na aba Máquinas</span>
                    </label>
                    <div id="progresso-importar" style="display:none;margin-bottom:15px;">
                        <div style="background:#e5e7eb;border-radius:8px;height:20px;overflow:hidden;">
                            <div id="barra-progresso" style="background:#2563eb;height:100%;width:0%;transition:width 0.3s;"></div>
                        </div>
                        <p id="texto-progresso" style="text-align:center;margin-top:8px;color:#666;"></p>
                    </div>
                    <button id="btn-iniciar-importacao" class="btn-save" style="width:100%">
                        <i class="fas fa-cloud-upload-alt"></i> Iniciar Importação
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Modal Catálogo -->
        <div id="modal-catalogo" class="modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2 id="modal-catalogo-titulo">Novo Catálogo</h2>
                    <button class="btn-close-modal" id="fechar-modal-catalogo"><i class="fas fa-times"></i></button>
                </div>
                <form id="form-catalogo">
                    <input type="hidden" id="catalogo-id">
                    <input type="hidden" id="catalogo-url">
                    <div class="form-group">
                        <label>Título *</label>
                        <input type="text" id="catalogo-titulo" required>
                    </div>
                    <div class="form-group">
                        <label>Fabricante</label>
                        <input type="text" id="catalogo-fabricante">
                    </div>
                    <div class="form-group">
                        <label>Arquivo PDF *</label>
                        <input type="file" id="catalogo-arquivo" accept=".pdf" style="padding: 10px;">
                        <div id="arquivo-info" style="font-size: 13px; color: #666; margin-top: 8px;"></div>
                    </div>
                    <div class="form-group">
                        <label>Descrição</label>
                        <textarea id="catalogo-descricao" rows="3"></textarea>
                    </div>
                    <div class="form-actions">
                        <button type="button" class="btn-cancel" id="cancelar-catalogo">Cancelar</button>
                        <button type="submit" class="btn-save">Salvar</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Módulo Relatórios -->
    <div id="relatorios-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-relatorios"><i class="fas fa-arrow-left"></i></button>
                <span>Relatórios</span>
            </div>
        </header>
        
        <div class="relatorios-container">
            <div class="relatorio-card" id="rel-resumo">
                <i class="fas fa-chart-pie"></i>
                <h3>Resumo Geral</h3>
                <p>Visão geral do sistema</p>
            </div>
            <div class="relatorio-card" id="rel-propostas-periodo">
                <i class="fas fa-calendar-alt"></i>
                <h3>Propostas por Período</h3>
                <p>Filtrar por data</p>
            </div>
            <div class="relatorio-card" id="rel-vendedor">
                <i class="fas fa-user-tie"></i>
                <h3>Por Vendedor</h3>
                <p>Performance individual</p>
            </div>
            <div class="relatorio-card" id="rel-status">
                <i class="fas fa-tasks"></i>
                <h3>Por Status</h3>
                <p>Aprovadas, Pendentes, etc</p>
            </div>
        </div>
        
        <div id="relatorio-resultado" class="relatorio-resultado"></div>
    </div>

    <!-- Módulo Pós-Venda -->
    <div id="posvenda-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-posvenda"><i class="fas fa-arrow-left"></i></button>
                <span>Pós-Venda</span>
            </div>
        </header>
        
        <div class="posvenda-container">
            <div class="posvenda-card" id="posvenda-inspecao">
                <i class="fas fa-clipboard-check"></i>
                <h3>Inspeção de Recebimento</h3>
                <p>Formulário do técnico</p>
            </div>
            <div class="posvenda-card" id="posvenda-entrega">
                <i class="fas fa-truck-loading"></i>
                <h3>Entrega Técnica</h3>
                <p>Checklist de entrega</p>
            </div>
            <div class="posvenda-card" id="posvenda-revisao">
                <i class="fas fa-wrench"></i>
                <h3>Revisão / Manutenção</h3>
                <p>Serviços realizados</p>
            </div>
        </div>
        
        <div id="lista-ordens" class="lista-container" style="margin-top: 20px;"></div>
    </div>

    <!-- Tela Inspeção de Recebimento -->
    <div id="inspecao-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-inspecao"><i class="fas fa-arrow-left"></i></button>
                <span>Inspeção de Recebimento</span>
            </div>
            <div class="header-right">
                <button id="btn-nova-inspecao" class="btn-add">
                    <i class="fas fa-plus"></i>
                </button>
            </div>
        </header>
        
        <div class="search-bar">
            <i class="fas fa-search"></i>
            <input type="text" id="busca-inspecao" placeholder="Buscar inspeção...">
        </div>
        
        <div id="lista-inspecoes" class="lista-container"></div>
        
        <!-- Modal Nova Inspeção -->
        <div id="modal-inspecao" class="modal">
            <div class="modal-content modal-large">
                <div class="modal-header">
                    <h2 id="modal-inspecao-titulo">Nova Inspeção de Recebimento</h2>
                    <button class="modal-close" id="fechar-modal-inspecao">&times;</button>
                </div>
                <form id="form-inspecao">
                    <input type="hidden" id="inspecao-id">
                    
                    <div class="form-section">
                        <h3><i class="fas fa-info-circle"></i> Informações Gerais</h3>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Data *</label>
                                <input type="date" id="inspecao-data" required>
                            </div>
                            <div class="form-group">
                                <label>Técnico *</label>
                                <select id="inspecao-tecnico" required>
                                    <option value="">Selecione...</option>
                                    <option value="Orlando">Orlando</option>
                                    <option value="Vinicius">Vinicius</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Cliente *</label>
                                <div class="autocomplete-wrap" style="position:relative;">
                                    <input type="text" id="inspecao-cliente-busca" placeholder="Digite para buscar cliente..." autocomplete="off" required>
                                    <input type="hidden" id="inspecao-cliente">
                                    <div id="inspecao-cliente-lista" class="autocomplete-list"></div>
                                </div>
                            </div>
                            <div class="form-group">
                                <label>Máquina *</label>
                                <select id="inspecao-maquina" required>
                                    <option value="">Selecione...</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-group">
                            <label>Número de Série</label>
                            <input type="text" id="inspecao-serie">
                        </div>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-clipboard-list"></i> Checklist de Inspeção</h3>
                        <div id="checklist-inspecao" class="checklist-container">
                            
                            <div class="checklist-category">
                                <h4>🔧 Sistema do Motor</h4>
                                <div class="checklist-item">
                                    <label>Nível de óleo do motor</label>
                                    <select name="motor_oleo"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Nível anticongelante</label>
                                    <select name="motor_anticongelante"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Cor e som do escapamento</label>
                                    <select name="motor_escapamento"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>⚙️ Operação da Máquina</h4>
                                <div class="checklist-item">
                                    <label>Operação de deslocamento</label>
                                    <select name="op_deslocamento"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Operação de direção</label>
                                    <select name="op_direcao"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Dispositivo de trabalho (elevação/escavação)</label>
                                    <select name="op_dispositivo"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>💧 Sistema Hidráulico</h4>
                                <div class="checklist-item">
                                    <label>Mangueiras e conexões</label>
                                    <select name="hid_mangueiras"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Manopla do dispositivo de trabalho</label>
                                    <select name="hid_manopla"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Cilindro hidráulico (haste do pistão)</label>
                                    <select name="hid_cilindro"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Nível de óleo hidráulico</label>
                                    <select name="hid_nivel"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>🏗️ Quadro / Estrutura</h4>
                                <div class="checklist-item">
                                    <label>Dispositivo de trabalho (posição limite)</label>
                                    <select name="quadro_limite"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>🚪 Sistema de Portas / Cabine</h4>
                                <div class="checklist-item">
                                    <label>Vidros (sem rachaduras/arranhões)</label>
                                    <select name="cabine_vidros"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Fechaduras das portas</label>
                                    <select name="cabine_fechaduras"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Assento (ajuste normal)</label>
                                    <select name="cabine_assento"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>⚡ Sistema Elétrico</h4>
                                <div class="checklist-item">
                                    <label>Bateria (carga normal)</label>
                                    <select name="eletrico_bateria"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Ar condicionado / Aquecedor</label>
                                    <select name="eletrico_ac"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Limpador de para-brisa</label>
                                    <select name="eletrico_limpador"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Luzes e instrumentos</label>
                                    <select name="eletrico_luzes"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Cabos e conectores</label>
                                    <select name="eletrico_cabos"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>👁️ Aparência Geral</h4>
                                <div class="checklist-item">
                                    <label>Vazamentos (óleo, água, ar)</label>
                                    <select name="aparencia_vazamentos"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Pintura</label>
                                    <select name="aparencia_pintura"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Limpeza geral (sem poeira/detritos)</label>
                                    <select name="aparencia_limpeza"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Peças de fixação (parafusos)</label>
                                    <select name="aparencia_fixacao"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Sistema do acelerador</label>
                                    <select name="aparencia_acelerador"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>📦 Acessórios Anexados</h4>
                                <div class="checklist-item">
                                    <label>Documentos/Manuais</label>
                                    <select name="acessorios_docs"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Ferramentas</label>
                                    <select name="acessorios_ferramentas"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Manual do motor</label>
                                    <select name="acessorios_motor"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>📋 Outros</h4>
                                <div class="checklist-item">
                                    <label>Outras verificações</label>
                                    <select name="outros"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                        </div>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-camera"></i> Fotos (máx. 10)</h3>
                        <input type="file" id="inspecao-fotos" accept="image/*" multiple style="padding: 10px;">
                        <div id="preview-fotos-inspecao" class="fotos-preview"></div>
                        <small>Selecione até 10 fotos</small>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-video"></i> Vídeo (máx. 30s)</h3>
                        <input type="file" id="inspecao-video" accept="video/*" style="padding: 10px;">
                        <div id="preview-video-inspecao" class="video-preview"></div>
                        <small>Vídeo de até 30 segundos</small>
                    </div>
                    
                    <div class="form-group">
                        <label>Observações</label>
                        <textarea id="inspecao-obs" rows="3"></textarea>
                    </div>
                    
                    <div class="form-actions">
                        <button type="button" class="btn-cancel" id="cancelar-inspecao">Cancelar</button>
                        <button type="submit" class="btn-save">Salvar Inspeção</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Tela Entrega Técnica -->
    <div id="entrega-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-entrega"><i class="fas fa-arrow-left"></i></button>
                <span>Entrega Técnica</span>
            </div>
            <div class="header-right">
                <button id="btn-nova-entrega" class="btn-add">
                    <i class="fas fa-plus"></i>
                </button>
            </div>
        </header>
        
        <div class="search-bar">
            <i class="fas fa-search"></i>
            <input type="text" id="busca-entrega" placeholder="Buscar entrega...">
        </div>
        
        <div id="lista-entregas" class="lista-container"></div>
        
        <!-- Modal Nova Entrega -->
        <div id="modal-entrega" class="modal">
            <div class="modal-content modal-large">
                <div class="modal-header">
                    <h2 id="modal-entrega-titulo">Nova Entrega Técnica</h2>
                    <button class="modal-close" id="fechar-modal-entrega">&times;</button>
                </div>
                <form id="form-entrega">
                    <input type="hidden" id="entrega-id">
                    
                    <div class="form-section">
                        <h3><i class="fas fa-info-circle"></i> Informações Gerais</h3>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Data *</label>
                                <input type="date" id="entrega-data" required>
                            </div>
                            <div class="form-group">
                                <label>Técnico *</label>
                                <select id="entrega-tecnico" required>
                                    <option value="">Selecione...</option>
                                    <option value="Orlando">Orlando</option>
                                    <option value="Vinicius">Vinicius</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Cliente *</label>
                                <div class="autocomplete-wrap" style="position:relative;">
                                    <input type="text" id="entrega-cliente-busca" placeholder="Digite para buscar cliente..." autocomplete="off" required>
                                    <input type="hidden" id="entrega-cliente">
                                    <div id="entrega-cliente-lista" class="autocomplete-list"></div>
                                </div>
                            </div>
                            <div class="form-group">
                                <label>Máquina *</label>
                                <select id="entrega-maquina" required>
                                    <option value="">Selecione...</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Número de Série</label>
                                <input type="text" id="entrega-serie">
                            </div>
                            <div class="form-group">
                                <label>Horímetro</label>
                                <input type="text" id="entrega-horimetro">
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-clipboard-list"></i> Checklist de Entrega</h3>
                        <div id="checklist-entrega" class="checklist-container">
                            
                            <div class="checklist-category">
                                <h4>🔧 Sistema do Motor</h4>
                                <div class="checklist-item">
                                    <label>Nível de óleo do motor</label>
                                    <select name="ent_motor_oleo"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Nível anticongelante</label>
                                    <select name="ent_motor_anticongelante"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Cor e som do escapamento</label>
                                    <select name="ent_motor_escapamento"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>⚙️ Operação da Máquina</h4>
                                <div class="checklist-item">
                                    <label>Operação de deslocamento</label>
                                    <select name="ent_op_deslocamento"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Operação de direção</label>
                                    <select name="ent_op_direcao"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Dispositivo de trabalho (elevação/escavação)</label>
                                    <select name="ent_op_dispositivo"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>💧 Sistema Hidráulico</h4>
                                <div class="checklist-item">
                                    <label>Mangueiras e conexões</label>
                                    <select name="ent_hid_mangueiras"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Manopla do dispositivo de trabalho</label>
                                    <select name="ent_hid_manopla"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Cilindro hidráulico (haste do pistão)</label>
                                    <select name="ent_hid_cilindro"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Nível de óleo hidráulico</label>
                                    <select name="ent_hid_nivel"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>🏗️ Quadro / Estrutura</h4>
                                <div class="checklist-item">
                                    <label>Dispositivo de trabalho (posição limite)</label>
                                    <select name="ent_quadro_limite"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>🚪 Sistema de Portas / Cabine</h4>
                                <div class="checklist-item">
                                    <label>Vidros (sem rachaduras/arranhões)</label>
                                    <select name="ent_cabine_vidros"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Fechaduras das portas</label>
                                    <select name="ent_cabine_fechaduras"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Assento (ajuste normal)</label>
                                    <select name="ent_cabine_assento"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>⚡ Sistema Elétrico</h4>
                                <div class="checklist-item">
                                    <label>Bateria (carga normal)</label>
                                    <select name="ent_eletrico_bateria"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Ar condicionado / Aquecedor</label>
                                    <select name="ent_eletrico_ac"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Limpador de para-brisa</label>
                                    <select name="ent_eletrico_limpador"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Luzes e instrumentos</label>
                                    <select name="ent_eletrico_luzes"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Cabos e conectores</label>
                                    <select name="ent_eletrico_cabos"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>👁️ Aparência Geral</h4>
                                <div class="checklist-item">
                                    <label>Vazamentos (óleo, água, ar)</label>
                                    <select name="ent_aparencia_vazamentos"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Pintura</label>
                                    <select name="ent_aparencia_pintura"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Limpeza geral (sem poeira/detritos)</label>
                                    <select name="ent_aparencia_limpeza"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Peças de fixação (parafusos)</label>
                                    <select name="ent_aparencia_fixacao"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Sistema do acelerador</label>
                                    <select name="ent_aparencia_acelerador"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>📦 Acessórios Anexados</h4>
                                <div class="checklist-item">
                                    <label>Documentos/Manuais</label>
                                    <select name="ent_acessorios_docs"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Ferramentas</label>
                                    <select name="ent_acessorios_ferramentas"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Manual do motor</label>
                                    <select name="ent_acessorios_motor"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>🎓 Treinamento do Operador</h4>
                                <div class="checklist-item">
                                    <label>Instruções de operação</label>
                                    <select name="ent_treino_operacao"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Instruções de segurança</label>
                                    <select name="ent_treino_seguranca"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                                <div class="checklist-item">
                                    <label>Manutenção básica explicada</label>
                                    <select name="ent_treino_manutencao"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                            <div class="checklist-category">
                                <h4>📋 Outros</h4>
                                <div class="checklist-item">
                                    <label>Outras verificações</label>
                                    <select name="ent_outros"><option value="">-</option><option value="OK">OK</option><option value="NG">NG</option></select>
                                </div>
                            </div>

                        </div>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-camera"></i> Fotos (máx. 10)</h3>
                        <input type="file" id="entrega-fotos" accept="image/*" multiple style="padding: 10px;">
                        <div id="preview-fotos-entrega" class="fotos-preview"></div>
                        <small>Selecione até 10 fotos</small>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-video"></i> Vídeo (máx. 30s)</h3>
                        <input type="file" id="entrega-video" accept="video/*" style="padding: 10px;">
                        <div id="preview-video-entrega" class="video-preview"></div>
                        <small>Vídeo de até 30 segundos</small>
                    </div>
                    
                    <div class="form-group">
                        <label>Assinatura do Técnico</label>
                        <canvas id="assinatura-tecnico-entrega" width="300" height="100" style="border:1px solid #ccc; border-radius:6px; background:#fff;"></canvas>
                        <button type="button" class="btn-secondary" onclick="limparAssinatura('assinatura-tecnico-entrega')">Limpar</button>
                    </div>

                    <div class="form-group">
                        <label>Assinatura do Cliente</label>
                        <canvas id="assinatura-cliente" width="300" height="100" style="border:1px solid #ccc; border-radius:6px; background:#fff;"></canvas>
                        <button type="button" class="btn-secondary" onclick="limparAssinatura('assinatura-cliente')">Limpar</button>
                    </div>
                    
                    <div class="form-group">
                        <label>Observações</label>
                        <textarea id="entrega-obs" rows="3"></textarea>
                    </div>
                    
                    <div class="form-actions">
                        <button type="button" class="btn-cancel" id="cancelar-entrega">Cancelar</button>
                        <button type="submit" class="btn-save">Salvar Entrega</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Tela Revisão/Manutenção -->
    <div id="revisao-screen" class="screen">
        <header class="header">
            <div class="header-left">
                <button class="btn-back" id="voltar-revisao"><i class="fas fa-arrow-left"></i></button>
                <span>Revisão / Manutenção</span>
            </div>
            <div class="header-right">
                <button id="btn-nova-revisao" class="btn-add">
                    <i class="fas fa-plus"></i>
                </button>
            </div>
        </header>
        
        <div class="search-bar">
            <i class="fas fa-search"></i>
            <input type="text" id="busca-revisao" placeholder="Buscar revisão...">
        </div>
        
        <div id="lista-revisoes" class="lista-container"></div>
        
        <!-- Modal Nova Revisão -->
        <div id="modal-revisao" class="modal">
            <div class="modal-content modal-large">
                <div class="modal-header">
                    <h2 id="modal-revisao-titulo">Nova Revisão / Manutenção</h2>
                    <button class="modal-close" id="fechar-modal-revisao">&times;</button>
                </div>
                <form id="form-revisao">
                    <input type="hidden" id="revisao-id">
                    
                    <div class="form-section">
                        <h3><i class="fas fa-info-circle"></i> Informações Gerais</h3>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Data *</label>
                                <input type="date" id="revisao-data" required>
                            </div>
                            <div class="form-group">
                                <label>Tipo *</label>
                                <select id="revisao-tipo" required>
                                    <option value="">Selecione...</option>
                                    <option value="Revisão Programada">Revisão Programada</option>
                                    <option value="Manutenção Corretiva">Manutenção Corretiva</option>
                                    <option value="Manutenção Preventiva">Manutenção Preventiva</option>
                                    <option value="Garantia">Garantia</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Técnico *</label>
                                <select id="revisao-tecnico" required>
                                    <option value="">Selecione...</option>
                                    <option value="Orlando">Orlando</option>
                                    <option value="Vinicius">Vinicius</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Cliente *</label>
                                <div class="autocomplete-wrap" style="position:relative;">
                                    <input type="text" id="revisao-cliente-busca" placeholder="Digite para buscar cliente..." autocomplete="off" required>
                                    <input type="hidden" id="revisao-cliente">
                                    <div id="revisao-cliente-lista" class="autocomplete-list"></div>
                                </div>
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Máquina *</label>
                                <select id="revisao-maquina" required>
                                    <option value="">Selecione...</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Horímetro Atual</label>
                                <input type="text" id="revisao-horimetro">
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-clipboard-list"></i> Serviços Realizados</h3>
                        <div id="checklist-revisao" class="checklist-container">
                            
                            <div class="form-group">
                                <label>Nº da Ordem de Serviço</label>
                                <input type="text" id="revisao-os" placeholder="Ex: 0020">
                            </div>
                            
                            <div class="form-group">
                                <label>Descrição da Solicitação (palavras do cliente) *</label>
                                <textarea id="revisao-solicitacao" rows="3" required placeholder="Descreva o problema relatado pelo cliente..."></textarea>
                            </div>
                            
                            <div class="form-group">
                                <label>Aplicação Detalhada (atividade principal)</label>
                                <input type="text" id="revisao-aplicacao" placeholder="Ex: Mineração, Construção Civil, Agricultura...">
                            </div>
                            
                            <div class="form-group">
                                <label>Serviços Realizados *</label>
                                <textarea id="revisao-servicos" rows="6" required placeholder="Descreva detalhadamente todos os serviços realizados..."></textarea>
                            </div>
                            
                            <div class="form-row">
                                <div class="form-group">
                                    <label>Equipamento ficou operacional?</label>
                                    <select id="revisao-operacional">
                                        <option value="">Selecione...</option>
                                        <option value="SIM">SIM</option>
                                        <option value="NAO">NÃO</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <label>Se NÃO, motivo:</label>
                                    <input type="text" id="revisao-motivo-nao" placeholder="Motivo...">
                                </div>
                            </div>

                            <h4 style="margin-top:20px; color:#374151;">📅 Registro de Atendimentos</h4>
                            <div id="atendimentos-container">
                                <div class="atendimento-item">
                                    <div class="form-row">
                                        <div class="form-group">
                                            <label>Data</label>
                                            <input type="date" class="atend-data">
                                        </div>
                                        <div class="form-group">
                                            <label>Horário Início</label>
                                            <input type="time" class="atend-inicio">
                                        </div>
                                        <div class="form-group">
                                            <label>Horário Fim</label>
                                            <input type="time" class="atend-fim">
                                        </div>
                                    </div>
                                    <div class="form-row">
                                        <div class="form-group">
                                            <label>Tipo</label>
                                            <select class="atend-tipo">
                                                <option value="Serv.">Serviço</option>
                                                <option value="Desl.">Deslocamento</option>
                                            </select>
                                        </div>
                                        <div class="form-group">
                                            <label>KM Rodados</label>
                                            <input type="number" class="atend-km" placeholder="0">
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <button type="button" class="btn-secondary" onclick="adicionarAtendimento()">
                                <i class="fas fa-plus"></i> Adicionar Atendimento
                            </button>

                            <div class="form-row" style="margin-top:20px;">
                                <div class="form-group">
                                    <label>Data/Hora Abertura OS</label>
                                    <input type="datetime-local" id="revisao-abertura">
                                </div>
                                <div class="form-group">
                                    <label>Data/Hora Fechamento OS</label>
                                    <input type="datetime-local" id="revisao-fechamento">
                                </div>
                            </div>

                        </div>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-camera"></i> Fotos (máx. 10)</h3>
                        <input type="file" id="revisao-fotos" accept="image/*" multiple style="padding: 10px;">
                        <div id="preview-fotos-revisao" class="fotos-preview"></div>
                        <small>Selecione até 10 fotos</small>
                    </div>
                    
                    <div class="form-section">
                        <h3><i class="fas fa-video"></i> Vídeo (máx. 30s)</h3>
                        <input type="file" id="revisao-video" accept="video/*" style="padding: 10px;">
                        <div id="preview-video-revisao" class="video-preview"></div>
                        <small>Vídeo de até 30 segundos</small>
                    </div>
                    
                    <div class="form-group">
                        <label>Peças Utilizadas</label>
                        <textarea id="revisao-pecas" rows="2" placeholder="Liste as peças utilizadas..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label>Observações / Comentários</label>
                        <textarea id="revisao-obs" rows="3"></textarea>
                    </div>

                    <div class="form-section">
                        <h3><i class="fas fa-signature"></i> Assinaturas</h3>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Nome do Técnico</label>
                                <input type="text" id="revisao-nome-tecnico">
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label>Assinatura do Técnico</label>
                                <canvas id="assinatura-tecnico-revisao" width="280" height="80" style="border:1px solid #ccc; border-radius:6px; background:#fff;"></canvas>
                                <button type="button" class="btn-secondary" onclick="limparAssinatura('assinatura-tecnico-revisao')">Limpar</button>
                            </div>
                            <div class="form-group">
                                <label>Assinatura do Cliente</label>
                                <canvas id="assinatura-cliente-revisao" width="280" height="80" style="border:1px solid #ccc; border-radius:6px; background:#fff;"></canvas>
                                <button type="button" class="btn-secondary" onclick="limparAssinatura('assinatura-cliente-revisao')">Limpar</button>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-actions">
                        <button type="button" class="btn-cancel" id="cancelar-revisao">Cancelar</button>
                        <button type="submit" class="btn-save">Salvar Revisão</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Loading Overlay -->
    <div id="loading" class="loading-overlay">
        <div class="spinner"></div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="toast"></div>

    <!-- SCRIPTS -->
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <script>
        // ========== CONFIGURAÇÃO ==========
        var SUPABASE_URL = 'https://rhbozicoxsilhgjmuuui.supabase.co';
        var SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InJoYm96aWNveHNpbGhnam11dXVpIiwicm9sZSI6ImFub24iLCJpYXQiOjE3Njk0NDk5NTAsImV4cCI6MjA4NTAyNTk1MH0.9jQwKwalHPH0OEVkuP6sTNFaCWkadp_UOwlMKuBqFRo';
        
        // ========== LOGOS DAS EMPRESAS ==========
        var LOGO_CF_COMEX = 'data:image/png;base64,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';
        var LOGO_ENJOY_COMEX = 'data:image/png;base64,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';

        var supabase;
        var currentUser = null;
        var currentUserEmail = null;
        var currentUserFuncao = null;
        var currentUserNome = null;
        var clientes = [];
        var maquinas = [];
        var propostas = [];
        var catalogos = [];
        var filtroStatus = 'todas';

        // ========== UTILIDADES ==========
        function showScreen(id) {
            var screens = document.querySelectorAll('.screen');
            for (var i = 0; i < screens.length; i++) {
                screens[i].classList.remove('active');
            }
            document.getElementById(id).classList.add('active');
        }

        function showLoading() {
            document.getElementById('loading').classList.add('active');
        }

        function hideLoading() {
            document.getElementById('loading').classList.remove('active');
        }

        function showToast(msg, type) {
            var toast = document.getElementById('toast');
            toast.textContent = msg;
            toast.className = 'toast show ' + (type || '');
            setTimeout(function() { toast.classList.remove('show'); }, 3000);
        }

        function formatCurrency(val) {
            return new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' }).format(val || 0);
        }

        function formatDate(d) {
            if (!d) return '';
            return new Date(d).toLocaleDateString('pt-BR');
        }

        function parseCurrency(str) {
            if (!str) return 0;
            return parseFloat(str.toString().replace(/\./g, '').replace(',', '.')) || 0;
        }

        // ========== CONTROLE DE MENUS POR FUNÇÃO ==========
        function configurarMenusPorFuncao(funcao) {
            var menuPosvenda = document.getElementById('menu-posvenda');
            var menuPropostas = document.getElementById('menu-propostas');
            var menuRelatorios = document.getElementById('menu-relatorios');
            
            // Reset - mostrar todos
            menuPosvenda.style.display = 'flex';
            menuPropostas.style.display = 'flex';
            menuRelatorios.style.display = 'flex';
            
            if (funcao === 'tecnico') {
                // Técnico só vê Pós-Venda, Clientes, Máquinas, Catálogos
                menuPropostas.style.display = 'none';
                menuRelatorios.style.display = 'none';
            } else if (funcao === 'vendedor') {
                // Vendedor não vê Pós-Venda
                menuPosvenda.style.display = 'none';
            }
            // Diretoria e Gerente veem tudo
        }

        // ========== LOGIN REAL COM SUPABASE ==========
        document.getElementById('btn-entrar').onclick = async function() {
            var email = document.getElementById('login-email').value.trim().toLowerCase();
            var senha = document.getElementById('login-senha').value;
            var errorDiv = document.getElementById('login-error');

            if (!email) {
                errorDiv.textContent = 'Digite seu email!';
                errorDiv.style.display = 'block';
                return;
            }

            if (!senha) {
                errorDiv.textContent = 'Digite sua senha!';
                errorDiv.style.display = 'block';
                return;
            }

            showLoading();
            errorDiv.style.display = 'none';

            try {
                // Autenticar com Supabase
                var authResult = await supabase.auth.signInWithPassword({
                    email: email,
                    password: senha
                });

                if (authResult.error) {
                    hideLoading();
                    errorDiv.textContent = 'Email ou senha incorretos!';
                    errorDiv.style.display = 'block';
                    return;
                }

                // Buscar dados do usuário na tabela usuarios
                var userResult = await supabase
                    .from('usuarios')
                    .select('nome, funcao')
                    .eq('email', email)
                    .eq('ativo', true)
                    .single();

                if (userResult.error || !userResult.data) {
                    hideLoading();
                    await supabase.auth.signOut();
                    errorDiv.textContent = 'Usuário não autorizado!';
                    errorDiv.style.display = 'block';
                    return;
                }

                // Login bem sucedido
                currentUserEmail = email;
                currentUserNome = userResult.data.nome;
                currentUserFuncao = userResult.data.funcao;
                currentUser = currentUserNome;

                document.getElementById('usuario-logado').textContent = currentUserNome + ' (' + currentUserFuncao + ')';
                
                // Configurar menus baseado na função
                configurarMenusPorFuncao(currentUserFuncao);
                
                hideLoading();
                showScreen('menu-screen');
                showToast('Bem-vindo, ' + currentUserNome + '!', 'success');

            } catch (e) {
                hideLoading();
                console.error('Erro login:', e);
                errorDiv.textContent = 'Erro ao conectar. Tente novamente.';
                errorDiv.style.display = 'block';
            }
        };

        // Enter para fazer login
        document.getElementById('login-senha').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                document.getElementById('btn-entrar').click();
            }
        });

        // ========== ESQUECI MINHA SENHA ==========
        document.getElementById('btn-esqueci-senha').onclick = async function(e) {
            e.preventDefault();
            var email = document.getElementById('login-email').value.trim().toLowerCase();
            var errorDiv = document.getElementById('login-error');
            var successDiv = document.getElementById('login-success');
            
            errorDiv.style.display = 'none';
            successDiv.style.display = 'none';

            if (!email) {
                errorDiv.textContent = 'Digite seu email primeiro!';
                errorDiv.style.display = 'block';
                return;
            }

            showLoading();

            try {
                var result = await supabase.auth.resetPasswordForEmail(email, {
                    redirectTo: window.location.origin
                });

                hideLoading();

                if (result.error) {
                    errorDiv.textContent = 'Erro ao enviar email. Verifique o endereço.';
                    errorDiv.style.display = 'block';
                } else {
                    successDiv.textContent = 'Email enviado! Verifique sua caixa de entrada.';
                    successDiv.style.display = 'block';
                }
            } catch (e) {
                hideLoading();
                errorDiv.textContent = 'Erro ao conectar. Tente novamente.';
                errorDiv.style.display = 'block';
            }
        };

        // ========== LOGOUT ==========
        document.getElementById('btn-logout').onclick = async function() {
            showLoading();
            await supabase.auth.signOut();
            currentUser = null;
            currentUserEmail = null;
            currentUserFuncao = null;
            currentUserNome = null;
            document.getElementById('login-email').value = '';
            document.getElementById('login-senha').value = '';
            hideLoading();
            showScreen('login-screen');
            showToast('Logout realizado!', 'success');
        };

        // ========== VERIFICAR SESSÃO EXISTENTE ==========
        async function checkSession() {
            try {
                var session = await supabase.auth.getSession();
                if (session.data.session) {
                    var email = session.data.session.user.email;
                    
                    // Buscar dados do usuário
                    var userResult = await supabase
                        .from('usuarios')
                        .select('nome, funcao')
                        .eq('email', email)
                        .eq('ativo', true)
                        .single();

                    if (userResult.data) {
                        currentUserEmail = email;
                        currentUserNome = userResult.data.nome;
                        currentUserFuncao = userResult.data.funcao;
                        currentUser = currentUserNome;
                        
                        document.getElementById('usuario-logado').textContent = currentUserNome + ' (' + currentUserFuncao + ')';
                        configurarMenusPorFuncao(currentUserFuncao);
                        showScreen('menu-screen');
                    }
                }
            } catch (e) {
                console.error('Erro ao verificar sessão:', e);
            }
        }

        // ========== MENU ==========
        document.getElementById('menu-clientes').onclick = function() {
            showScreen('clientes-screen');
            loadClientes();
        };
        document.getElementById('menu-maquinas').onclick = function() {
            showScreen('maquinas-screen');
            loadMaquinas();
        };
        document.getElementById('menu-propostas').onclick = function() {
            showScreen('propostas-screen');
            loadPropostas();
            loadClientesSelect();
            loadMaquinasSelect();
        };
        document.getElementById('menu-catalogos').onclick = function() {
            showScreen('catalogos-screen');
            loadCatalogos();
        };
        document.getElementById('menu-relatorios').onclick = function() {
            showScreen('relatorios-screen');
        };
        document.getElementById('menu-posvenda').onclick = function() {
            showScreen('posvenda-screen');
        };

        // ========== VOLTAR ==========
        document.getElementById('voltar-clientes').onclick = function() { showScreen('menu-screen'); };
        document.getElementById('voltar-maquinas').onclick = function() { showScreen('menu-screen'); };
        document.getElementById('voltar-propostas').onclick = function() { showScreen('menu-screen'); };
        document.getElementById('voltar-catalogos').onclick = function() { showScreen('menu-screen'); };
        document.getElementById('voltar-relatorios').onclick = function() { showScreen('menu-screen'); };
        document.getElementById('voltar-posvenda').onclick = function() { showScreen('menu-screen'); };
        document.getElementById('voltar-inspecao').onclick = function() { showScreen('posvenda-screen'); };
        document.getElementById('voltar-entrega').onclick = function() { showScreen('posvenda-screen'); };
        document.getElementById('voltar-revisao').onclick = function() { showScreen('posvenda-screen'); };

        // ========== INICIALIZAR SUPABASE ==========
        try {
            supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_KEY);
            console.log('Supabase OK');
            // Verificar se já existe sessão
            checkSession();
        } catch (e) {
            console.error('Erro Supabase:', e);
        }

        // ========== CLIENTES ==========
        async function loadClientes() {
            showLoading();
            try {
                var result = await supabase.from('clientes').select('*').order('razao_social');
                clientes = result.data || [];
                renderClientes();
            } catch (e) {
                console.error(e);
                showToast('Erro ao carregar', 'error');
            }
            hideLoading();
        }

        function renderClientes(filtro) {
            filtro = filtro || '';
            var lista = document.getElementById('lista-clientes');
            var filtered = clientes.filter(function(c) {
                return (c.razao_social || '').toLowerCase().indexOf(filtro.toLowerCase()) >= 0 ||
                       (c.fantasia || '').toLowerCase().indexOf(filtro.toLowerCase()) >= 0;
            });

            if (filtered.length === 0) {
                lista.innerHTML = '<div class="empty-state"><i class="fas fa-users"></i><p>Nenhum cliente</p></div>';
                return;
            }

            lista.innerHTML = filtered.map(function(c) {
                return '<div class="card" onclick="editCliente(' + c.id + ')">' +
                    '<div class="card-header"><div><div class="card-title">' + (c.razao_social || '') + '</div>' +
                    '<div class="card-subtitle">' + (c.fantasia || '') + '</div></div></div>' +
                    '<div class="card-info">' + (c.cidade || '') + (c.estado ? '/' + c.estado : '') + '</div>' +
                    '<div class="card-actions">' +
                    '<button class="btn-card btn-edit" onclick="event.stopPropagation();editCliente(' + c.id + ')"><i class="fas fa-edit"></i> Editar</button>' +
                    '<button class="btn-card btn-delete" onclick="event.stopPropagation();deleteCliente(' + c.id + ')"><i class="fas fa-trash"></i></button>' +
                    '</div></div>';
            }).join('');
        }

        document.getElementById('busca-cliente').oninput = function(e) {
            renderClientes(e.target.value);
        };

        document.getElementById('btn-novo-cliente').onclick = function() {
            document.getElementById('modal-cliente-titulo').textContent = 'Novo Cliente';
            document.getElementById('form-cliente').reset();
            document.getElementById('cliente-id').value = '';
            document.getElementById('modal-cliente').classList.add('active');
        };

        document.getElementById('fechar-modal-cliente').onclick = function() {
            document.getElementById('modal-cliente').classList.remove('active');
        };
        document.getElementById('cancelar-cliente').onclick = function() {
            document.getElementById('modal-cliente').classList.remove('active');
        };

        window.editCliente = function(id) {
            var c = clientes.find(function(x) { return x.id === id; });
            if (!c) return;
            document.getElementById('modal-cliente-titulo').textContent = 'Editar Cliente';
            document.getElementById('cliente-id').value = c.id;
            document.getElementById('cliente-razao').value = c.razao_social || '';
            document.getElementById('cliente-fantasia').value = c.fantasia || '';
            document.getElementById('cliente-cnpj').value = c.cnpj || '';
            document.getElementById('cliente-telefone').value = c.telefone || '';
            document.getElementById('cliente-email').value = c.email || '';
            document.getElementById('cliente-cidade').value = c.cidade || '';
            document.getElementById('cliente-estado').value = c.estado || '';
            document.getElementById('cliente-contato').value = c.contato || '';
            document.getElementById('modal-cliente').classList.add('active');
        };

        window.deleteCliente = async function(id) {
            if (!confirm('Excluir cliente?')) return;
            showLoading();
            await supabase.from('clientes').delete().eq('id', id);
            hideLoading();
            showToast('Excluído!', 'success');
            loadClientes();
        };

        document.getElementById('form-cliente').onsubmit = async function(e) {
            e.preventDefault();
            var id = document.getElementById('cliente-id').value;
            var dados = {
                razao_social: document.getElementById('cliente-razao').value,
                fantasia: document.getElementById('cliente-fantasia').value,
                cnpj: document.getElementById('cliente-cnpj').value,
                telefone: document.getElementById('cliente-telefone').value,
                email: document.getElementById('cliente-email').value,
                cidade: document.getElementById('cliente-cidade').value,
                estado: document.getElementById('cliente-estado').value,
                contato: document.getElementById('cliente-contato').value
            };
            showLoading();
            if (id) {
                await supabase.from('clientes').update(dados).eq('id', id);
            } else {
                await supabase.from('clientes').insert(dados);
            }
            hideLoading();
            document.getElementById('modal-cliente').classList.remove('active');
            showToast('Salvo!', 'success');
            loadClientes();
        };

        // ========== MÁQUINAS ==========
        async function loadMaquinas() {
            showLoading();
            try {
                var result = await supabase.from('maquinas').select('*').order('modelo');
                maquinas = result.data || [];
                renderMaquinas();
            } catch (e) {
                console.error(e);
            }
            hideLoading();
        }

        // Sincronizar catálogos com máquinas
        document.getElementById('btn-sincronizar-catalogos').onclick = async function() {
            if (!confirm('Criar máquinas a partir dos catálogos existentes?\n\nIsso irá criar uma máquina para cada catálogo que ainda não possui máquina correspondente.')) {
                return;
            }

            showLoading();
            
            try {
                // Buscar todos os catálogos
                var catalogosResult = await supabase.from('catalogos').select('*');
                var cats = catalogosResult.data || [];
                
                // Buscar máquinas existentes
                var maquinasResult = await supabase.from('maquinas').select('modelo');
                var maquinasExistentes = (maquinasResult.data || []).map(function(m) { return m.modelo.toUpperCase(); });
                
                var criadas = 0;
                
                for (var i = 0; i < cats.length; i++) {
                    var cat = cats[i];
                    var titulo = cat.titulo || '';
                    
                    // Verificar se já existe
                    if (maquinasExistentes.indexOf(titulo.toUpperCase()) >= 0) {
                        continue;
                    }
                    
                    // Detectar categoria
                    var categoria = 'Outro';
                    var tituloUpper = titulo.toUpperCase();
                    
                    if (tituloUpper.indexOf('MINI CARREGADEIRA') >= 0 || tituloUpper.indexOf('SWL') >= 0 || tituloUpper.indexOf('SWTL') >= 0) {
                        categoria = 'Mini Carregadeira';
                    } else if (tituloUpper.indexOf('MINI ESCAVADEIRA') >= 0) {
                        categoria = 'Mini Escavadeira';
                    } else if (tituloUpper.indexOf('CARREGADEIRA') >= 0 || tituloUpper.indexOf(' FL9') >= 0) {
                        categoria = 'Carregadeira';
                    } else if (tituloUpper.indexOf('ESCAVADEIRA') >= 0 || tituloUpper.indexOf('SWE') >= 0 || tituloUpper.indexOf(' FR') >= 0) {
                        if (tituloUpper.indexOf('SWE 08') >= 0 || tituloUpper.indexOf('SWE 18') >= 0 || 
                            tituloUpper.indexOf('SWE08') >= 0 || tituloUpper.indexOf('SWE18') >= 0 ||
                            tituloUpper.indexOf('SWE 60') >= 0 || tituloUpper.indexOf('SWE60') >= 0 ||
                            tituloUpper.indexOf('SWE 80') >= 0 || tituloUpper.indexOf('SWE80') >= 0 ||
                            tituloUpper.indexOf('SWE 90') >= 0 || tituloUpper.indexOf('SWE90') >= 0 ||
                            tituloUpper.indexOf('FR18') >= 0 || tituloUpper.indexOf('FR26') >= 0 || 
                            tituloUpper.indexOf('FR36') >= 0 || tituloUpper.indexOf('FR80') >= 0) {
                            categoria = 'Mini Escavadeira';
                        } else {
                            categoria = 'Escavadeira';
                        }
                    }
                    
                    // Criar máquina
                    await supabase.from('maquinas').insert({
                        modelo: titulo,
                        fabricante: cat.fabricante || '',
                        categoria: categoria,
                        condicao: 'Nova',
                        descricao: 'Importado do catálogo'
                    });
                    
                    criadas++;
                }
                
                hideLoading();
                
                if (criadas > 0) {
                    showToast(criadas + ' máquinas criadas com sucesso!', 'success');
                    loadMaquinas();
                } else {
                    showToast('Todas as máquinas já existem!', 'info');
                }
                
            } catch (e) {
                console.error(e);
                hideLoading();
                showToast('Erro ao sincronizar', 'error');
            }
        };

        function renderMaquinas(filtro) {
            filtro = filtro || '';
            var lista = document.getElementById('lista-maquinas');
            var filtered = maquinas.filter(function(m) {
                return (m.modelo || '').toLowerCase().indexOf(filtro.toLowerCase()) >= 0 ||
                       (m.fabricante || '').toLowerCase().indexOf(filtro.toLowerCase()) >= 0;
            });

            if (filtered.length === 0) {
                lista.innerHTML = '<div class="empty-state"><i class="fas fa-cogs"></i><p>Nenhuma máquina</p></div>';
                return;
            }

            lista.innerHTML = filtered.map(function(m) {
                return '<div class="card" onclick="editMaquina(' + m.id + ')">' +
                    '<div class="card-header"><div><div class="card-title">' + (m.modelo || '') + '</div>' +
                    '<div class="card-subtitle">' + (m.fabricante || '') + '</div></div>' +
                    '<div class="card-value">' + formatCurrency(m.preco) + '</div></div>' +
                    '<div class="card-info">' + (m.categoria || '') + ' • ' + (m.condicao || '') + '</div>' +
                    '<div class="card-actions">' +
                    '<button class="btn-card btn-edit" onclick="event.stopPropagation();editMaquina(' + m.id + ')"><i class="fas fa-edit"></i> Editar</button>' +
                    '<button class="btn-card btn-delete" onclick="event.stopPropagation();deleteMaquina(' + m.id + ')"><i class="fas fa-trash"></i></button>' +
                    '</div></div>';
            }).join('');
        }

        document.getElementById('busca-maquina').oninput = function(e) {
            renderMaquinas(e.target.value);
        };

        document.getElementById('btn-nova-maquina').onclick = function() {
            document.getElementById('modal-maquina-titulo').textContent = 'Nova Máquina';
            document.getElementById('form-maquina').reset();
            document.getElementById('maquina-id').value = '';
            document.getElementById('modal-maquina').classList.add('active');
        };

        document.getElementById('fechar-modal-maquina').onclick = function() {
            document.getElementById('modal-maquina').classList.remove('active');
        };
        document.getElementById('cancelar-maquina').onclick = function() {
            document.getElementById('modal-maquina').classList.remove('active');
        };

        window.editMaquina = function(id) {
            var m = maquinas.find(function(x) { return x.id === id; });
            if (!m) return;
            document.getElementById('modal-maquina-titulo').textContent = 'Editar Máquina';
            document.getElementById('maquina-id').value = m.id;
            document.getElementById('maquina-modelo').value = m.modelo || '';
            document.getElementById('maquina-fabricante').value = m.fabricante || '';
            document.getElementById('maquina-categoria').value = m.categoria || '';
            document.getElementById('maquina-ano').value = m.ano || '';
            document.getElementById('maquina-preco').value = m.preco || '';
            document.getElementById('maquina-descricao').value = m.descricao || '';
            document.getElementById('maquina-condicao').value = m.condicao || 'Usada';
            document.getElementById('modal-maquina').classList.add('active');
        };

        window.deleteMaquina = async function(id) {
            if (!confirm('Excluir máquina?')) return;
            showLoading();
            await supabase.from('maquinas').delete().eq('id', id);
            hideLoading();
            showToast('Excluído!', 'success');
            loadMaquinas();
        };

        document.getElementById('form-maquina').onsubmit = async function(e) {
            e.preventDefault();
            var id = document.getElementById('maquina-id').value;
            var dados = {
                modelo: document.getElementById('maquina-modelo').value,
                fabricante: document.getElementById('maquina-fabricante').value,
                categoria: document.getElementById('maquina-categoria').value,
                ano: document.getElementById('maquina-ano').value ? parseInt(document.getElementById('maquina-ano').value) : null,
                preco: parseCurrency(document.getElementById('maquina-preco').value),
                descricao: document.getElementById('maquina-descricao').value,
                condicao: document.getElementById('maquina-condicao').value
            };
            showLoading();
            if (id) {
                await supabase.from('maquinas').update(dados).eq('id', id);
            } else {
                await supabase.from('maquinas').insert(dados);
            }
            hideLoading();
            document.getElementById('modal-maquina').classList.remove('active');
            showToast('Salvo!', 'success');
            loadMaquinas();
        };

        // ========== PROPOSTAS ==========
        async function loadPropostas() {
            showLoading();
            try {
                var result = await supabase.from('propostas').select('*, clientes(razao_social), maquinas(modelo)').order('created_at', { ascending: false });
                propostas = result.data || [];
                renderPropostas();
            } catch (e) {
                console.error(e);
            }
            hideLoading();
        }

        // Cache de clientes para autocomplete
        var clientesCache = [];

        async function loadClientesSelect() {
            var result = await supabase.from('clientes').select('id, razao_social').order('razao_social');
            clientesCache = result.data || [];
            initAutocompleteCliente('proposta-cliente');
        }

        // Controle para evitar duplicatas
        var autocompleteIniciado = {};

        function initAutocompleteCliente(prefix) {
            if (autocompleteIniciado[prefix]) return;
            
            var input = document.getElementById(prefix + '-busca');
            var hidden = document.getElementById(prefix);
            var lista = document.getElementById(prefix + '-lista');
            if (!input || !hidden || !lista) return;

            autocompleteIniciado[prefix] = true;
            var fechando = false;

            function mostrar(filtro) {
                var val = (filtro || '').trim().toLowerCase();
                var items = clientesCache.filter(function(c) {
                    if (!val) return true;
                    return (c.razao_social || '').toLowerCase().indexOf(val) >= 0;
                }).slice(0, 30);

                if (items.length === 0) {
                    lista.innerHTML = '<div style="padding:12px;color:#999;">Nenhum cliente encontrado</div>';
                } else {
                    var html = '';
                    items.forEach(function(c) {
                        html += '<div class="autocomplete-item" onclick="selecionarCliente(\'' + prefix + '\',' + c.id + ',\'' + (c.razao_social || '').replace(/'/g, "\\'") + '\')">' + c.razao_social + '</div>';
                    });
                    lista.innerHTML = html;
                }
                lista.style.display = 'block';
            }

            input.addEventListener('focus', function() {
                if (clientesCache.length > 0) mostrar(this.value);
            });

            input.addEventListener('input', function() {
                hidden.value = '';
                input.classList.remove('autocomplete-selected');
                mostrar(this.value);
            });

            input.addEventListener('blur', function() {
                setTimeout(function() { lista.style.display = 'none'; }, 250);
            });
        }

        // Função global para selecionar cliente (funciona com onclick no mobile)
        window.selecionarCliente = function(prefix, id, nome) {
            var input = document.getElementById(prefix + '-busca');
            var hidden = document.getElementById(prefix);
            var lista = document.getElementById(prefix + '-lista');
            hidden.value = id;
            input.value = nome;
            input.classList.add('autocomplete-selected');
            lista.style.display = 'none';
        };

        // Função para setar cliente programaticamente (ex: ao editar proposta)
        function setAutocompleteCliente(prefix, id) {
            var hidden = document.getElementById(prefix);
            var input = document.getElementById(prefix + '-busca');
            if (!hidden || !input) return;
            
            hidden.value = id || '';
            if (id) {
                var c = clientesCache.find(function(cl) { return cl.id == id; });
                if (c) {
                    input.value = c.razao_social;
                    input.classList.add('autocomplete-selected');
                } else {
                    input.value = '';
                    input.classList.remove('autocomplete-selected');
                }
            } else {
                input.value = '';
                input.classList.remove('autocomplete-selected');
            }
        }

        // Função helper para pegar texto do cliente selecionado
        function getClienteTexto(prefix) {
            var input = document.getElementById(prefix + '-busca');
            return input ? input.value : '';
        }

        async function loadMaquinasSelect() {
            var result = await supabase.from('maquinas').select('id, modelo').order('modelo');
            var sel = document.getElementById('proposta-maquina');
            sel.innerHTML = '<option value="">Selecione...</option>' + (result.data || []).map(function(m) {
                return '<option value="' + m.id + '">' + m.modelo + '</option>';
            }).join('');
        }

        function renderPropostas(filtro) {
            filtro = filtro || '';
            var lista = document.getElementById('lista-propostas');
            var filtered = propostas.filter(function(p) {
                var matchText = (p.clientes?.razao_social || '').toLowerCase().indexOf(filtro.toLowerCase()) >= 0;
                var matchStatus = filtroStatus === 'todas' || p.status === filtroStatus;
                return matchText && matchStatus;
            });

            if (filtered.length === 0) {
                lista.innerHTML = '<div class="empty-state"><i class="fas fa-file-invoice-dollar"></i><p>Nenhuma proposta</p></div>';
                return;
            }

            lista.innerHTML = filtered.map(function(p) {
                return '<div class="card" onclick="editProposta(' + p.id + ')">' +
                    '<div class="card-header"><div><div class="card-title">' + (p.clientes?.razao_social || '-') + '</div>' +
                    '<div class="card-subtitle">' + (p.maquinas?.modelo || '-') + '</div></div>' +
                    '<span class="card-badge badge-' + (p.status || '').toLowerCase() + '">' + (p.status || '') + '</span></div>' +
                    '<div class="card-info">' + formatDate(p.data_proposta) + ' • ' + (p.vendedor || '') + '</div>' +
                    '<div class="card-value">' + formatCurrency(p.valor) + '</div>' +
                    '<div class="card-actions">' +
                    '<button class="btn-card btn-edit" onclick="event.stopPropagation();editProposta(' + p.id + ')"><i class="fas fa-edit"></i> Editar</button>' +
                    '<button class="btn-card btn-delete" onclick="event.stopPropagation();deleteProposta(' + p.id + ')"><i class="fas fa-trash"></i></button>' +
                    '</div></div>';
            }).join('');
        }

        document.getElementById('busca-proposta').oninput = function(e) {
            renderPropostas(e.target.value);
        };

        var filterTabs = document.querySelectorAll('.filter-tab');
        for (var i = 0; i < filterTabs.length; i++) {
            filterTabs[i].onclick = function() {
                for (var j = 0; j < filterTabs.length; j++) {
                    filterTabs[j].classList.remove('active');
                }
                this.classList.add('active');
                filtroStatus = this.getAttribute('data-status');
                renderPropostas();
            };
        }

        document.getElementById('btn-nova-proposta').onclick = function() {
            document.getElementById('modal-proposta-titulo').textContent = 'Nova Proposta';
            document.getElementById('form-proposta').reset();
            document.getElementById('proposta-id').value = '';
            document.getElementById('proposta-data').value = new Date().toISOString().split('T')[0];
            setAutocompleteCliente('proposta-cliente', '');
            document.getElementById('modal-proposta').classList.add('active');
        };

        document.getElementById('fechar-modal-proposta').onclick = function() {
            document.getElementById('modal-proposta').classList.remove('active');
        };
        document.getElementById('cancelar-proposta').onclick = function() {
            document.getElementById('modal-proposta').classList.remove('active');
        };

        window.editProposta = function(id) {
            var p = propostas.find(function(x) { return x.id === id; });
            if (!p) return;
            document.getElementById('modal-proposta-titulo').textContent = 'Editar Proposta';
            document.getElementById('proposta-id').value = p.id;
            document.getElementById('proposta-empresa').value = p.empresa || '';
            setAutocompleteCliente('proposta-cliente', p.cliente_id);
            document.getElementById('proposta-maquina').value = p.maquina_id || '';
            document.getElementById('proposta-data').value = p.data_proposta || '';
            document.getElementById('proposta-valor').value = p.valor || '';
            document.getElementById('proposta-pagamento').value = p.condicao_pagamento || 'À Vista';
            document.getElementById('proposta-validade').value = p.validade || 15;
            document.getElementById('proposta-obs').value = p.observacoes || '';
            document.getElementById('proposta-status').value = p.status || 'Pendente';
            document.getElementById('modal-proposta').classList.add('active');
        };

        window.deleteProposta = async function(id) {
            if (!confirm('Excluir proposta?')) return;
            showLoading();
            await supabase.from('propostas').delete().eq('id', id);
            hideLoading();
            showToast('Excluído!', 'success');
            loadPropostas();
        };

        document.getElementById('form-proposta').onsubmit = async function(e) {
            e.preventDefault();
            
            // Validar cliente selecionado
            var clienteVal = document.getElementById('proposta-cliente').value;
            if (!clienteVal) {
                showToast('Selecione um cliente!', 'error');
                document.getElementById('proposta-cliente-busca').focus();
                return;
            }
            
            var id = document.getElementById('proposta-id').value;
            var dados = {
                empresa: document.getElementById('proposta-empresa').value,
                cliente_id: parseInt(clienteVal),
                maquina_id: parseInt(document.getElementById('proposta-maquina').value),
                data_proposta: document.getElementById('proposta-data').value,
                valor: parseCurrency(document.getElementById('proposta-valor').value),
                condicao_pagamento: document.getElementById('proposta-pagamento').value,
                validade: parseInt(document.getElementById('proposta-validade').value) || 15,
                observacoes: document.getElementById('proposta-obs').value,
                status: document.getElementById('proposta-status').value,
                vendedor: currentUser,
                email_vendedor: currentUserEmail
            };
            showLoading();
            if (id) {
                await supabase.from('propostas').update(dados).eq('id', id);
            } else {
                await supabase.from('propostas').insert(dados);
            }
            hideLoading();
            document.getElementById('modal-proposta').classList.remove('active');
            showToast('Salvo!', 'success');
            loadPropostas();
        };

        // Condições Gerais padrão
        var condicoesGerais = `
<h3>CONDIÇÕES GERAIS DE VENDA</h3>
<ol style="font-size:12px; line-height:1.6;">
<li><strong>EQUIPAMENTO:</strong> O equipamento será entregue conforme especificações descritas nesta proposta, em perfeito estado de funcionamento.</li>
<li><strong>GARANTIA:</strong> O equipamento possui garantia de 90 (noventa) dias contra defeitos de fabricação, a contar da data de entrega, exceto peças de desgaste natural.</li>
<li><strong>FRETE:</strong> O frete é por conta do comprador, salvo acordo em contrário. A entrega será realizada em até 15 dias úteis após confirmação do pagamento.</li>
<li><strong>INSTALAÇÃO:</strong> A instalação e treinamento operacional não estão inclusos nesta proposta, podendo ser contratados separadamente.</li>
<li><strong>PAGAMENTO:</strong> O não cumprimento das condições de pagamento acordadas acarretará em multa de 2% e juros de 1% ao mês sobre o valor em atraso.</li>
<li><strong>RESERVA DE DOMÍNIO:</strong> O equipamento permanecerá em nome do vendedor até a quitação total do valor acordado.</li>
<li><strong>CANCELAMENTO:</strong> Em caso de desistência pelo comprador após a confirmação do pedido, será cobrada multa de 20% sobre o valor total da proposta.</li>
<li><strong>DOCUMENTAÇÃO:</strong> O vendedor fornecerá nota fiscal e documentação técnica do equipamento.</li>
<li><strong>ASSISTÊNCIA TÉCNICA:</strong> Disponibilizamos assistência técnica mediante orçamento prévio após o período de garantia.</li>
<li><strong>VALIDADE:</strong> Esta proposta tem validade conforme indicado acima, podendo sofrer alterações após este prazo.</li>
</ol>
`;

        document.getElementById('btn-gerar-pdf').onclick = function() {
            var empresaSel = document.getElementById('proposta-empresa');
            var empresa = empresaSel.value;
            var empresaNome = empresa === 'CF Comex' ? 'CF Comex Equipamentos e Serviços Ltda' : 'Enjoy Comex Ltda';
            var maquinaSel = document.getElementById('proposta-maquina');
            var cliente = getClienteTexto('proposta-cliente');
            var maquina = maquinaSel.options[maquinaSel.selectedIndex]?.text || '';
            var valor = document.getElementById('proposta-valor').value;
            var pagamento = document.getElementById('proposta-pagamento').value;
            var validade = document.getElementById('proposta-validade').value;
            var obs = document.getElementById('proposta-obs').value;
            var data = document.getElementById('proposta-data').value;

            if (!empresa) {
                showToast('Selecione a empresa emissora!', 'error');
                return;
            }

            var logoBase64 = empresa === 'CF Comex' ? LOGO_CF_COMEX : LOGO_ENJOY_COMEX;

            var html = `<html><head><title>Proposta Comercial - ${empresaNome}</title>
            <style>
                body { font-family: Arial, sans-serif; padding: 40px; max-width: 800px; margin: 0 auto; }
                .logo-header { text-align: center; margin-bottom: 20px; }
                .logo-header img { max-height: 80px; }
                h1 { color: #2563eb; border-bottom: 3px solid #2563eb; padding-bottom: 10px; text-align: center; }
                h3 { color: #1e40af; margin-top: 30px; border-bottom: 1px solid #ccc; padding-bottom: 5px; }
                .header-info { background: #f3f4f6; padding: 15px; border-radius: 8px; margin: 20px 0; }
                .destaque { background: #dbeafe; padding: 20px; border-radius: 8px; margin: 20px 0; }
                .valor { font-size: 28px; color: #2563eb; font-weight: bold; }
                .footer { margin-top: 40px; padding-top: 20px; border-top: 2px solid #2563eb; }
                .assinatura { margin-top: 60px; display: flex; justify-content: space-between; }
                .assinatura div { width: 45%; text-align: center; border-top: 1px solid #000; padding-top: 10px; }
                @media print { body { padding: 20px; } }
            </style></head><body>
            
            <div class="logo-header">
                <img src="${logoBase64}" alt="${empresaNome}">
            </div>
            
            <h1>PROPOSTA COMERCIAL</h1>
            
            <div class="header-info">
                <p><strong>${empresaNome}</strong></p>
                <p>📅 Data: ${formatDate(data)}</p>
                <p>👤 Vendedor: ${currentUser}</p>
                <p>📄 Proposta válida por: ${validade} dias</p>
            </div>
            
            <h3>DADOS DO CLIENTE</h3>
            <p><strong>${cliente}</strong></p>
            
            <h3>EQUIPAMENTO</h3>
            <p><strong>${maquina}</strong></p>
            
            <div class="destaque">
                <p><strong>💰 VALOR:</strong></p>
                <p class="valor">R$ ${valor}</p>
                <p><strong>💳 Condição de Pagamento:</strong> ${pagamento}</p>
            </div>
            
            ${obs ? '<h3>OBSERVAÇÕES</h3><p>' + obs + '</p>' : ''}
            
            ${condicoesGerais}
            
            <div class="footer">
                <p>Estamos à disposição para quaisquer esclarecimentos.</p>
                <p>Atenciosamente,</p>
                <p><strong>${currentUser}</strong><br>${empresaNome}</p>
            </div>
            
            <div class="assinatura">
                <div>
                    <p><strong>VENDEDOR</strong></p>
                    <p>${currentUser}</p>
                </div>
                <div>
                    <p><strong>CLIENTE</strong></p>
                    <p>De acordo</p>
                </div>
            </div>
            
            </body></html>`;

            var win = window.open('', '_blank');
            win.document.write(html);
            win.document.close();
            setTimeout(function() { win.print(); }, 300);
        };

        // Função para obter dados da proposta formatados
        function getPropostaTexto() {
            var empresaSel = document.getElementById('proposta-empresa');
            var empresa = empresaSel.value;
            var empresaNome = empresa === 'CF Comex' ? 'CF Comex Equipamentos e Serviços Ltda' : 'Enjoy Comex Ltda';
            var maquinaSel = document.getElementById('proposta-maquina');
            var cliente = getClienteTexto('proposta-cliente');
            var maquina = maquinaSel.options[maquinaSel.selectedIndex]?.text || '';
            var valor = document.getElementById('proposta-valor').value;
            var pagamento = document.getElementById('proposta-pagamento').value;
            var validade = document.getElementById('proposta-validade').value;
            var data = document.getElementById('proposta-data').value;

            return `*PROPOSTA COMERCIAL*
*${empresaNome}*

📅 Data: ${formatDate(data)}
👤 Vendedor: ${currentUser}

*CLIENTE:* ${cliente}

*EQUIPAMENTO:* ${maquina}

💰 *VALOR:* R$ ${valor}
💳 *Pagamento:* ${pagamento}
📄 *Validade:* ${validade} dias

---
✅ Garantia de 90 dias
✅ Documentação completa
✅ Assistência técnica disponível

Entre em contato para mais informações!
*${empresaNome}*`;
        }

        // WhatsApp
        document.getElementById('btn-whatsapp').onclick = async function() {
            var clienteId = document.getElementById('proposta-cliente').value;
            if (!clienteId) {
                showToast('Selecione um cliente', 'error');
                return;
            }

            var empresaSel = document.getElementById('proposta-empresa');
            var empresa = empresaSel.value;
            if (!empresa) {
                showToast('Selecione a empresa emissora!', 'error');
                return;
            }

            // Buscar telefone do cliente
            var result = await supabase.from('clientes').select('telefone, razao_social').eq('id', clienteId).single();
            var telefone = result.data?.telefone || '';
            var clienteNome = result.data?.razao_social || '';
            
            if (!telefone) {
                telefone = prompt('Digite o telefone do cliente (com DDD, ex: 11999998888):');
                if (!telefone) return;
            }

            // Limpar telefone (só números)
            telefone = telefone.replace(/\D/g, '');
            
            // Adicionar código do Brasil se necessário
            if (telefone.length === 10 || telefone.length === 11) {
                telefone = '55' + telefone;
            }

            showToast('Gerando PDF da proposta...', 'success');

            // Gerar HTML da proposta
            var empresaNome = empresa === 'CF Comex' ? 'CF Comex Equipamentos e Serviços Ltda' : 'Enjoy Comex Ltda';
            var logoBase64 = empresa === 'CF Comex' ? LOGO_CF_COMEX : LOGO_ENJOY_COMEX;
            var maquinaSel = document.getElementById('proposta-maquina');
            var cliente = getClienteTexto('proposta-cliente');
            var maquina = maquinaSel.options[maquinaSel.selectedIndex]?.text || '';
            var valor = document.getElementById('proposta-valor').value;
            var pagamento = document.getElementById('proposta-pagamento').value;
            var validade = document.getElementById('proposta-validade').value;
            var obs = document.getElementById('proposta-obs').value;
            var data = document.getElementById('proposta-data').value;

            // Criar elemento temporário para o PDF
            var tempDiv = document.createElement('div');
            tempDiv.innerHTML = `
                <div style="font-family: Arial, sans-serif; padding: 40px; max-width: 800px; margin: 0 auto; background: white;">
                    <div style="text-align: center; margin-bottom: 20px;">
                        <img src="${logoBase64}" alt="${empresaNome}" style="max-height: 80px;">
                    </div>
                    
                    <h1 style="color: #2563eb; border-bottom: 3px solid #2563eb; padding-bottom: 10px; text-align: center;">PROPOSTA COMERCIAL</h1>
                    
                    <div style="background: #f3f4f6; padding: 15px; border-radius: 8px; margin: 20px 0;">
                        <p><strong>${empresaNome}</strong></p>
                        <p>📅 Data: ${formatDate(data)}</p>
                        <p>👤 Vendedor: ${currentUser}</p>
                        <p>📄 Proposta válida por: ${validade} dias</p>
                    </div>
                    
                    <h3 style="color: #1e40af; margin-top: 30px; border-bottom: 1px solid #ccc; padding-bottom: 5px;">DADOS DO CLIENTE</h3>
                    <p><strong>${cliente}</strong></p>
                    
                    <h3 style="color: #1e40af; margin-top: 30px; border-bottom: 1px solid #ccc; padding-bottom: 5px;">EQUIPAMENTO</h3>
                    <p><strong>${maquina}</strong></p>
                    
                    <div style="background: #dbeafe; padding: 20px; border-radius: 8px; margin: 20px 0;">
                        <p><strong>💰 VALOR:</strong></p>
                        <p style="font-size: 28px; color: #2563eb; font-weight: bold;">R$ ${valor}</p>
                        <p><strong>💳 Condição de Pagamento:</strong> ${pagamento}</p>
                    </div>
                    
                    ${obs ? '<h3 style="color: #1e40af; margin-top: 30px; border-bottom: 1px solid #ccc; padding-bottom: 5px;">OBSERVAÇÕES</h3><p>' + obs + '</p>' : ''}
                    
                    ${condicoesGerais}
                    
                    <div style="margin-top: 40px; padding-top: 20px; border-top: 2px solid #2563eb;">
                        <p>Estamos à disposição para quaisquer esclarecimentos.</p>
                        <p>Atenciosamente,</p>
                        <p><strong>${currentUser}</strong><br>${empresaNome}</p>
                    </div>
                </div>
            `;
            document.body.appendChild(tempDiv);

            try {
                // Gerar PDF
                var opt = {
                    margin: 10,
                    filename: 'proposta.pdf',
                    image: { type: 'jpeg', quality: 0.98 },
                    html2canvas: { scale: 2, useCORS: true },
                    jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
                };

                var pdfBlob = await html2pdf().from(tempDiv).set(opt).outputPdf('blob');
                
                // Remover elemento temporário
                document.body.removeChild(tempDiv);

                // Nome único para o arquivo
                var timestamp = Date.now();
                var nomeArquivo = 'proposta_' + timestamp + '.pdf';

                showToast('Enviando PDF para o servidor...', 'success');

                // Upload para Supabase Storage
                var uploadResult = await supabase.storage
                    .from('PROPOSTAS')
                    .upload(nomeArquivo, pdfBlob, {
                        contentType: 'application/pdf',
                        cacheControl: '3600'
                    });

                if (uploadResult.error) {
                    console.error('Erro upload:', uploadResult.error);
                    showToast('Erro ao enviar PDF: ' + uploadResult.error.message, 'error');
                    return;
                }

                // Pegar URL pública
                var urlResult = supabase.storage.from('PROPOSTAS').getPublicUrl(nomeArquivo);
                var pdfUrl = urlResult.data.publicUrl;

                // Montar mensagem para WhatsApp
                var mensagem = `📋 *PROPOSTA COMERCIAL*\n\n`;
                mensagem += `🏢 *${empresaNome}*\n`;
                mensagem += `👤 Cliente: ${cliente}\n`;
                mensagem += `🔧 Equipamento: ${maquina}\n`;
                mensagem += `💰 Valor: R$ ${valor}\n`;
                mensagem += `💳 Pagamento: ${pagamento}\n`;
                mensagem += `📅 Válido por: ${validade} dias\n\n`;
                mensagem += `📎 *Proposta completa em PDF:*\n${pdfUrl}\n\n`;
                mensagem += `Vendedor: ${currentUser}`;

                var texto = encodeURIComponent(mensagem);
                
                // Detectar se está no celular ou desktop
                var isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
                
                showToast('Abrindo WhatsApp...', 'success');
                
                if (isMobile) {
                    window.location.href = 'whatsapp://send?phone=' + telefone + '&text=' + texto;
                } else {
                    window.open('https://web.whatsapp.com/send?phone=' + telefone + '&text=' + texto, '_blank');
                }

            } catch (err) {
                console.error('Erro:', err);
                document.body.removeChild(tempDiv);
                showToast('Erro ao gerar PDF: ' + err.message, 'error');
            }
        };

        // Email
        document.getElementById('btn-email').onclick = async function() {
            var clienteId = document.getElementById('proposta-cliente').value;
            if (!clienteId) {
                showToast('Selecione um cliente', 'error');
                return;
            }

            // Buscar email do cliente
            var result = await supabase.from('clientes').select('email, razao_social').eq('id', clienteId).single();
            var emailCliente = result.data?.email || '';
            
            if (!emailCliente) {
                emailCliente = prompt('Digite o email do cliente:');
                if (!emailCliente) return;
            }

            var maquinaSel = document.getElementById('proposta-maquina');
            var empresaSel = document.getElementById('proposta-empresa');
            var empresa = empresaSel.value;
            var empresaNome = empresa === 'CF Comex' ? 'CF Comex Equipamentos e Serviços Ltda' : 'Enjoy Comex Ltda';
            var cliente = getClienteTexto('proposta-cliente');
            var maquina = maquinaSel.options[maquinaSel.selectedIndex]?.text || '';
            var valor = document.getElementById('proposta-valor').value;

            var assunto = 'Proposta Comercial - ' + maquina + ' - ' + empresaNome;
            var corpo = getPropostaTexto().replace(/\*/g, '');
            
            // Perguntar qual serviço de email usar
            var opcao = confirm('Clique OK para abrir no GMAIL\nClique CANCELAR para abrir no cliente de email padrão (Outlook, etc)');
            
            if (opcao) {
                // Abrir no Gmail Web
                var gmailUrl = 'https://mail.google.com/mail/?view=cm&fs=1' +
                    '&to=' + encodeURIComponent(emailCliente) +
                    '&su=' + encodeURIComponent(assunto) +
                    '&body=' + encodeURIComponent(corpo);
                window.open(gmailUrl, '_blank');
            } else {
                // Abrir cliente de email padrão (mailto)
                window.location.href = 'mailto:' + emailCliente + 
                    '?subject=' + encodeURIComponent(assunto) + 
                    '&body=' + encodeURIComponent(corpo);
            }
            
            showToast('Abrindo email...', 'success');
        };

        // ========== CATÁLOGOS ==========
        async function loadCatalogos() {
            showLoading();
            try {
                var result = await supabase.from('catalogos').select('*').order('titulo');
                catalogos = result.data || [];
                renderCatalogos();
            } catch (e) {
                console.error(e);
            }
            hideLoading();
        }

        function renderCatalogos(filtro) {
            filtro = filtro || '';
            var lista = document.getElementById('lista-catalogos');
            var filtered = catalogos.filter(function(c) {
                return (c.titulo || '').toLowerCase().indexOf(filtro.toLowerCase()) >= 0;
            });

            if (filtered.length === 0) {
                lista.innerHTML = '<div class="empty-state"><i class="fas fa-book-open"></i><p>Nenhum catálogo</p></div>';
                return;
            }

            lista.innerHTML = filtered.map(function(c) {
                return '<div class="catalogo-card">' +
                    '<i class="fas fa-file-pdf" onclick="window.open(\'' + c.url + '\',\'_blank\')"></i>' +
                    '<h4 onclick="window.open(\'' + c.url + '\',\'_blank\')">' + (c.titulo || '') + '</h4>' +
                    '<p>' + (c.fabricante || '') + '</p>' +
                    '<div style="margin-top:10px">' +
                    '<button class="btn-card btn-edit" onclick="editCatalogo(' + c.id + ')" style="font-size:11px;padding:5px 10px"><i class="fas fa-edit"></i></button> ' +
                    '<button class="btn-card btn-delete" onclick="deleteCatalogo(' + c.id + ')" style="font-size:11px;padding:5px 10px"><i class="fas fa-trash"></i></button>' +
                    '</div></div>';
            }).join('');
        }

        document.getElementById('busca-catalogo').oninput = function(e) {
            renderCatalogos(e.target.value);
        };

        document.getElementById('btn-novo-catalogo').onclick = function() {
            document.getElementById('modal-catalogo-titulo').textContent = 'Novo Catálogo';
            document.getElementById('form-catalogo').reset();
            document.getElementById('catalogo-id').value = '';
            document.getElementById('catalogo-url').value = '';
            document.getElementById('arquivo-info').innerHTML = '';
            document.getElementById('modal-catalogo').classList.add('active');
        };

        document.getElementById('fechar-modal-catalogo').onclick = function() {
            document.getElementById('modal-catalogo').classList.remove('active');
        };
        document.getElementById('cancelar-catalogo').onclick = function() {
            document.getElementById('modal-catalogo').classList.remove('active');
        };

        window.editCatalogo = function(id) {
            var c = catalogos.find(function(x) { return x.id === id; });
            if (!c) return;
            document.getElementById('modal-catalogo-titulo').textContent = 'Editar Catálogo';
            document.getElementById('catalogo-id').value = c.id;
            document.getElementById('catalogo-titulo').value = c.titulo || '';
            document.getElementById('catalogo-fabricante').value = c.fabricante || '';
            document.getElementById('catalogo-url').value = c.url || '';
            document.getElementById('catalogo-descricao').value = c.descricao || '';
            document.getElementById('arquivo-info').innerHTML = c.url ? '<i class="fas fa-check-circle" style="color:green"></i> Arquivo já cadastrado' : '';
            document.getElementById('modal-catalogo').classList.add('active');
        };

        window.deleteCatalogo = async function(id) {
            if (!confirm('Excluir catálogo?')) return;
            showLoading();
            await supabase.from('catalogos').delete().eq('id', id);
            hideLoading();
            showToast('Excluído!', 'success');
            loadCatalogos();
        };

        document.getElementById('form-catalogo').onsubmit = async function(e) {
            e.preventDefault();
            var id = document.getElementById('catalogo-id').value;
            var arquivo = document.getElementById('catalogo-arquivo').files[0];
            var urlAtual = document.getElementById('catalogo-url').value;
            var urlFinal = urlAtual;

            showLoading();

            // Se tem arquivo novo, faz upload
            if (arquivo) {
                var nomeArquivo = Date.now() + '_' + arquivo.name.replace(/[^a-zA-Z0-9.-]/g, '_');
                
                var uploadResult = await supabase.storage
                    .from('catalogos')
                    .upload(nomeArquivo, arquivo, { contentType: 'application/pdf' });

                if (uploadResult.error) {
                    hideLoading();
                    showToast('Erro no upload: ' + uploadResult.error.message, 'error');
                    return;
                }

                // Pegar URL pública
                var urlResult = supabase.storage.from('catalogos').getPublicUrl(nomeArquivo);
                urlFinal = urlResult.data.publicUrl;
            }

            if (!urlFinal && !id) {
                hideLoading();
                showToast('Selecione um arquivo PDF', 'error');
                return;
            }

            var dados = {
                titulo: document.getElementById('catalogo-titulo').value,
                fabricante: document.getElementById('catalogo-fabricante').value,
                url: urlFinal,
                descricao: document.getElementById('catalogo-descricao').value
            };

            if (id) {
                await supabase.from('catalogos').update(dados).eq('id', id);
            } else {
                await supabase.from('catalogos').insert(dados);
            }
            hideLoading();
            document.getElementById('modal-catalogo').classList.remove('active');
            showToast('Catálogo salvo!', 'success');
            loadCatalogos();
        };

        // ========== IMPORTAÇÃO EM LOTE ==========
        document.getElementById('btn-importar-catalogos').onclick = function() {
            document.getElementById('arquivos-importar').value = '';
            document.getElementById('lista-importar').innerHTML = '';
            document.getElementById('progresso-importar').style.display = 'none';
            document.getElementById('modal-importar').classList.add('active');
        };

        document.getElementById('fechar-modal-importar').onclick = function() {
            document.getElementById('modal-importar').classList.remove('active');
        };

        document.getElementById('arquivos-importar').onchange = function(e) {
            var files = e.target.files;
            var lista = document.getElementById('lista-importar');
            
            if (files.length === 0) {
                lista.innerHTML = '';
                return;
            }

            var html = '<table style="width:100%;font-size:13px;"><thead><tr style="background:#f3f4f6;"><th style="padding:8px;text-align:left;">Arquivo</th><th style="padding:8px;text-align:left;">Título</th><th style="padding:8px;text-align:left;">Fabricante</th></tr></thead><tbody>';
            
            for (var i = 0; i < files.length; i++) {
                var nome = files[i].name.replace('.pdf', '').replace(/_/g, ' ').replace(/-/g, ' ');
                var nomeUpper = nome.toUpperCase();
                
                // Detectar marca e tipo automaticamente
                var fabricante = 'LOVOL';
                var tipo = 'Equipamento';
                var modelo = nome.split(' ')[0] || nome;
                
                if (nomeUpper.indexOf('SWE') >= 0 || nomeUpper.indexOf('SWL') >= 0 || nomeUpper.indexOf('SWTL') >= 0) {
                    fabricante = 'SUNWARD';
                    // Extrair modelo SUNWARD (ex: SWE_08B -> SWE 08B)
                    var match = nome.match(/(SWE|SWL|SWTL)[\s_]?(\d+[A-Z0-9]*)/i);
                    if (match) modelo = match[1].toUpperCase() + ' ' + match[2];
                    
                    if (nomeUpper.indexOf('SWE') >= 0) tipo = 'Escavadeira SUNWARD';
                    else if (nomeUpper.indexOf('SWTL') >= 0) tipo = 'Mini Carregadeira SUNWARD';
                    else if (nomeUpper.indexOf('SWL') >= 0) tipo = 'Mini Carregadeira SUNWARD';
                } else if (nomeUpper.indexOf('FR') >= 0) {
                    fabricante = 'LOVOL';
                    tipo = 'Escavadeira LOVOL';
                    var match = nome.match(/(FR\d+[A-Z0-9-]*)/i);
                    if (match) modelo = match[1].toUpperCase();
                } else if (nomeUpper.indexOf('FL') >= 0) {
                    fabricante = 'LOVOL';
                    tipo = 'Carregadeira LOVOL';
                    var match = nome.match(/(FL\d+[A-Z0-9]*)/i);
                    if (match) modelo = match[1].toUpperCase();
                }
                
                var titulo = tipo + ' ' + modelo;
                
                html += '<tr><td style="padding:8px;font-size:11px;">' + files[i].name + '</td><td style="padding:8px;"><input type="text" class="titulo-import" value="' + titulo + '" style="width:100%;padding:5px;border:1px solid #ddd;border-radius:4px;"></td><td style="padding:8px;"><input type="text" class="fabricante-import" value="' + fabricante + '" style="width:100%;padding:5px;border:1px solid #ddd;border-radius:4px;"></td></tr>';
            }
            
            html += '</tbody></table>';
            lista.innerHTML = html;
        };

        document.getElementById('btn-iniciar-importacao').onclick = async function() {
            var files = document.getElementById('arquivos-importar').files;
            if (files.length === 0) {
                showToast('Selecione arquivos para importar', 'error');
                return;
            }

            var titulos = document.querySelectorAll('.titulo-import');
            var fabricantes = document.querySelectorAll('.fabricante-import');
            var criarMaquinas = document.getElementById('criar-maquinas').checked;
            
            document.getElementById('progresso-importar').style.display = 'block';
            var barra = document.getElementById('barra-progresso');
            var texto = document.getElementById('texto-progresso');
            
            var sucesso = 0;
            var erro = 0;
            var maquinasCriadas = 0;

            for (var i = 0; i < files.length; i++) {
                var file = files[i];
                var titulo = titulos[i].value || file.name.replace('.pdf', '');
                var fabricante = fabricantes[i].value || 'LOVOL';
                
                texto.textContent = 'Enviando ' + (i + 1) + ' de ' + files.length + ': ' + file.name;
                barra.style.width = ((i / files.length) * 100) + '%';

                try {
                    // Upload do arquivo
                    var nomeArquivo = Date.now() + '_' + i + '_' + file.name.replace(/[^a-zA-Z0-9.-]/g, '_');
                    
                    var uploadResult = await supabase.storage
                        .from('catalogos')
                        .upload(nomeArquivo, file, { contentType: 'application/pdf' });

                    if (uploadResult.error) {
                        console.error('Erro upload:', uploadResult.error);
                        erro++;
                        continue;
                    }

                    // Pegar URL pública
                    var urlResult = supabase.storage.from('catalogos').getPublicUrl(nomeArquivo);
                    var urlFinal = urlResult.data.publicUrl;

                    // Inserir catálogo no banco
                    await supabase.from('catalogos').insert({
                        titulo: titulo,
                        fabricante: fabricante,
                        url: urlFinal,
                        descricao: 'Catálogo técnico ' + titulo
                    });

                    // Criar máquina se checkbox marcado
                    if (criarMaquinas) {
                        // Detectar categoria baseado no título
                        var categoria = 'Outro';
                        var tituloUpper = titulo.toUpperCase();
                        
                        if (tituloUpper.indexOf('MINI CARREGADEIRA') >= 0 || tituloUpper.indexOf('SWL') >= 0 || tituloUpper.indexOf('SWTL') >= 0) {
                            categoria = 'Mini Carregadeira';
                        } else if (tituloUpper.indexOf('MINI ESCAVADEIRA') >= 0) {
                            categoria = 'Mini Escavadeira';
                        } else if (tituloUpper.indexOf('CARREGADEIRA') >= 0 || tituloUpper.indexOf('FL9') >= 0) {
                            categoria = 'Carregadeira';
                        } else if (tituloUpper.indexOf('ESCAVADEIRA') >= 0 || tituloUpper.indexOf('SWE') >= 0 || tituloUpper.indexOf('FR') >= 0) {
                            // Verificar se é mini (peso < 10t geralmente)
                            if (tituloUpper.indexOf('SWE 08') >= 0 || tituloUpper.indexOf('SWE 18') >= 0 || 
                                tituloUpper.indexOf('SWE08') >= 0 || tituloUpper.indexOf('SWE18') >= 0 ||
                                tituloUpper.indexOf('FR18') >= 0 || tituloUpper.indexOf('FR26') >= 0 || 
                                tituloUpper.indexOf('FR36') >= 0 || tituloUpper.indexOf('FR80') >= 0) {
                                categoria = 'Mini Escavadeira';
                            } else {
                                categoria = 'Escavadeira';
                            }
                        }

                        // Verificar se máquina já existe
                        var existente = await supabase.from('maquinas').select('id').eq('modelo', titulo).single();
                        
                        if (!existente.data) {
                            await supabase.from('maquinas').insert({
                                modelo: titulo,
                                fabricante: fabricante,
                                categoria: categoria,
                                condicao: 'Nova',
                                descricao: 'Importado do catálogo - ' + fabricante
                            });
                            maquinasCriadas++;
                        }
                    }

                    sucesso++;
                } catch (e) {
                    console.error('Erro:', e);
                    erro++;
                }
            }

            barra.style.width = '100%';
            var msgMaquinas = criarMaquinas ? ' | ' + maquinasCriadas + ' máquinas criadas' : '';
            texto.textContent = 'Concluído! ' + sucesso + ' catálogos importados' + msgMaquinas;
            
            var toastMsg = sucesso + ' catálogos importados!';
            if (criarMaquinas && maquinasCriadas > 0) {
                toastMsg += ' + ' + maquinasCriadas + ' máquinas criadas!';
            }
            showToast(toastMsg, 'success');
            loadCatalogos();
            
            setTimeout(function() {
                document.getElementById('modal-importar').classList.remove('active');
            }, 2000);
        };

        // ========== RELATÓRIOS ==========
        document.getElementById('rel-resumo').onclick = async function() {
            showLoading();
            var r1 = await supabase.from('clientes').select('id');
            var r2 = await supabase.from('maquinas').select('id');
            var r3 = await supabase.from('propostas').select('*');
            var props = r3.data || [];
            var pend = props.filter(function(p) { return p.status === 'Pendente'; }).length;
            var aprov = props.filter(function(p) { return p.status === 'Aprovada'; }).length;
            var total = props.filter(function(p) { return p.status === 'Aprovada'; }).reduce(function(a, p) { return a + (p.valor || 0); }, 0);
            hideLoading();

            document.getElementById('relatorio-resultado').innerHTML =
                '<div class="relatorio-box"><h3>Resumo Geral</h3><div class="stat-grid">' +
                '<div class="stat-item"><div class="stat-value">' + (r1.data?.length || 0) + '</div><div class="stat-label">Clientes</div></div>' +
                '<div class="stat-item"><div class="stat-value">' + (r2.data?.length || 0) + '</div><div class="stat-label">Máquinas</div></div>' +
                '<div class="stat-item"><div class="stat-value">' + props.length + '</div><div class="stat-label">Propostas</div></div>' +
                '<div class="stat-item"><div class="stat-value">' + pend + '</div><div class="stat-label">Pendentes</div></div>' +
                '<div class="stat-item"><div class="stat-value">' + aprov + '</div><div class="stat-label">Aprovadas</div></div>' +
                '<div class="stat-item"><div class="stat-value">' + formatCurrency(total) + '</div><div class="stat-label">Valor</div></div>' +
                '</div></div>';
        };

        document.getElementById('rel-status').onclick = async function() {
            showLoading();
            var r = await supabase.from('propostas').select('status, valor');
            var props = r.data || [];
            var pend = props.filter(function(p) { return p.status === 'Pendente'; });
            var aprov = props.filter(function(p) { return p.status === 'Aprovada'; });
            var repr = props.filter(function(p) { return p.status === 'Reprovada'; });
            hideLoading();

            document.getElementById('relatorio-resultado').innerHTML =
                '<div class="relatorio-box"><h3>Por Status</h3><div class="stat-grid">' +
                '<div class="stat-item"><div class="stat-value" style="color:#d97706">' + pend.length + '</div><div class="stat-label">Pendentes</div></div>' +
                '<div class="stat-item"><div class="stat-value" style="color:#059669">' + aprov.length + '</div><div class="stat-label">Aprovadas</div></div>' +
                '<div class="stat-item"><div class="stat-value" style="color:#dc2626">' + repr.length + '</div><div class="stat-label">Reprovadas</div></div>' +
                '</div></div>';
        };

        document.getElementById('rel-vendedor').onclick = async function() {
            showLoading();
            var r = await supabase.from('propostas').select('vendedor, status, valor');
            var props = r.data || [];
            var vendedores = ['Pietro', 'Fabio', 'Artur Junior', 'Regina', 'Daniel', 'Aronidis', 'Alexandre', 'Fernando', 'Paulo Carneiro', 'Paulo Lanes', 'Orlando'];
            hideLoading();

            var html = '<div class="relatorio-box"><h3>Por Vendedor</h3>';
            vendedores.forEach(function(v) {
                var vp = props.filter(function(p) { return p.vendedor === v; });
                if (vp.length > 0) {
                    var ap = vp.filter(function(p) { return p.status === 'Aprovada'; });
                    var tot = ap.reduce(function(a, p) { return a + (p.valor || 0); }, 0);
                    html += '<div style="padding:12px;background:#f3f4f6;border-radius:8px;margin-bottom:8px"><strong>' + v + '</strong><br>' +
                        '<small>' + vp.length + ' propostas • ' + ap.length + ' aprovadas • ' + formatCurrency(tot) + '</small></div>';
                }
            });
            html += '</div>';
            document.getElementById('relatorio-resultado').innerHTML = html;
        };

        document.getElementById('rel-propostas-periodo').onclick = function() {
            document.getElementById('relatorio-resultado').innerHTML =
                '<div class="relatorio-box"><h3>Por Período</h3>' +
                '<div class="form-row"><div class="form-group"><label>Início</label><input type="date" id="filtro-ini"></div>' +
                '<div class="form-group"><label>Fim</label><input type="date" id="filtro-fim"></div></div>' +
                '<button class="btn-save" onclick="filtrarPeriodo()">Filtrar</button>' +
                '<div id="resultado-periodo"></div></div>';
        };

        window.filtrarPeriodo = async function() {
            var ini = document.getElementById('filtro-ini').value;
            var fim = document.getElementById('filtro-fim').value;
            if (!ini || !fim) { showToast('Informe as datas', 'error'); return; }

            showLoading();
            var r = await supabase.from('propostas').select('*, clientes(razao_social)').gte('data_proposta', ini).lte('data_proposta', fim);
            hideLoading();

            var props = r.data || [];
            var total = props.reduce(function(a, p) { return a + (p.valor || 0); }, 0);

            document.getElementById('resultado-periodo').innerHTML =
                '<p><strong>' + props.length + '</strong> propostas • Total: ' + formatCurrency(total) + '</p>' +
                props.map(function(p) {
                    return '<div style="padding:8px;background:#f9f9f9;border-radius:6px;margin-top:8px;font-size:13px">' +
                        '<strong>' + (p.clientes?.razao_social || '-') + '</strong> • ' + formatDate(p.data_proposta) + ' • ' + formatCurrency(p.valor) + '</div>';
                }).join('');
        };

        // ========== PÓS-VENDA ==========
        
        // Navegação sub-ícones
        document.getElementById('posvenda-inspecao').onclick = function() {
            showScreen('inspecao-screen');
            loadInspecoes();
        };
        document.getElementById('posvenda-entrega').onclick = function() {
            showScreen('entrega-screen');
            loadEntregas();
        };
        document.getElementById('posvenda-revisao').onclick = function() {
            showScreen('revisao-screen');
            loadRevisoes();
        };

        // Arrays para armazenar dados
        var inspecoes = [];
        var entregas = [];
        var revisoes = [];
        var fotosInspecao = [];
        var fotosEntrega = [];
        var fotosRevisao = [];

        // Carregar selects de clientes e máquinas nos formulários
        async function loadSelectsPosvenda() {
            var rc = await supabase.from('clientes').select('id, razao_social').order('razao_social');
            var rm = await supabase.from('maquinas').select('id, modelo, fabricante').order('modelo');
            
            // Atualizar cache de clientes
            clientesCache = rc.data || [];
            
            var maquinasOpts = '<option value="">Selecione...</option>';
            (rm.data || []).forEach(function(m) {
                maquinasOpts += '<option value="' + m.id + '">' + m.fabricante + ' ' + m.modelo + '</option>';
            });
            
            // Inicializar autocomplete de clientes nos módulos pós-venda
            ['inspecao-cliente', 'entrega-cliente', 'revisao-cliente'].forEach(function(id) {
                initAutocompleteCliente(id);
            });
            ['inspecao-maquina', 'entrega-maquina', 'revisao-maquina'].forEach(function(id) {
                var el = document.getElementById(id);
                if (el) el.innerHTML = maquinasOpts;
            });
        }

        // ===== INSPEÇÃO DE RECEBIMENTO =====
        async function loadInspecoes() {
            showLoading();
            await loadSelectsPosvenda();
            // Por enquanto lista vazia - será implementado com banco
            hideLoading();
            renderInspecoes();
        }

        function renderInspecoes() {
            var lista = document.getElementById('lista-inspecoes');
            if (inspecoes.length === 0) {
                lista.innerHTML = '<div class="empty-state"><i class="fas fa-clipboard-check"></i><p>Nenhuma inspeção registrada</p></div>';
                return;
            }
        }

        document.getElementById('btn-nova-inspecao').onclick = function() {
            document.getElementById('modal-inspecao-titulo').textContent = 'Nova Inspeção de Recebimento';
            document.getElementById('form-inspecao').reset();
            document.getElementById('inspecao-id').value = '';
            document.getElementById('inspecao-data').value = new Date().toISOString().split('T')[0];
            document.getElementById('preview-fotos-inspecao').innerHTML = '';
            document.getElementById('preview-video-inspecao').innerHTML = '';
            fotosInspecao = [];
            document.getElementById('modal-inspecao').classList.add('active');
        };

        document.getElementById('fechar-modal-inspecao').onclick = function() {
            document.getElementById('modal-inspecao').classList.remove('active');
        };
        document.getElementById('cancelar-inspecao').onclick = function() {
            document.getElementById('modal-inspecao').classList.remove('active');
        };

        // Preview fotos inspeção
        document.getElementById('inspecao-fotos').onchange = function(e) {
            var files = Array.from(e.target.files).slice(0, 10);
            fotosInspecao = files;
            var preview = document.getElementById('preview-fotos-inspecao');
            preview.innerHTML = '';
            files.forEach(function(file, i) {
                var reader = new FileReader();
                reader.onload = function(ev) {
                    preview.innerHTML += '<div class="foto-thumb-container"><img src="' + ev.target.result + '" class="foto-thumb"><button type="button" class="remove-foto" onclick="removeFotoInspecao(' + i + ')">&times;</button></div>';
                };
                reader.readAsDataURL(file);
            });
        };

        window.removeFotoInspecao = function(index) {
            fotosInspecao.splice(index, 1);
            document.getElementById('inspecao-fotos').onchange({target: {files: fotosInspecao}});
        };

        // Preview vídeo inspeção
        document.getElementById('inspecao-video').onchange = function(e) {
            var file = e.target.files[0];
            if (file) {
                var video = document.createElement('video');
                video.src = URL.createObjectURL(file);
                video.controls = true;
                video.style.maxWidth = '100%';
                document.getElementById('preview-video-inspecao').innerHTML = '';
                document.getElementById('preview-video-inspecao').appendChild(video);
            }
        };

        document.getElementById('form-inspecao').onsubmit = function(e) {
            e.preventDefault();
            showToast('Inspeção salva com sucesso!', 'success');
            document.getElementById('modal-inspecao').classList.remove('active');
        };

        // ===== ENTREGA TÉCNICA =====
        async function loadEntregas() {
            showLoading();
            await loadSelectsPosvenda();
            hideLoading();
            renderEntregas();
        }

        function renderEntregas() {
            var lista = document.getElementById('lista-entregas');
            if (entregas.length === 0) {
                lista.innerHTML = '<div class="empty-state"><i class="fas fa-truck-loading"></i><p>Nenhuma entrega registrada</p></div>';
                return;
            }
        }

        document.getElementById('btn-nova-entrega').onclick = function() {
            document.getElementById('modal-entrega-titulo').textContent = 'Nova Entrega Técnica';
            document.getElementById('form-entrega').reset();
            document.getElementById('entrega-id').value = '';
            document.getElementById('entrega-data').value = new Date().toISOString().split('T')[0];
            document.getElementById('preview-fotos-entrega').innerHTML = '';
            document.getElementById('preview-video-entrega').innerHTML = '';
            fotosEntrega = [];
            initAssinatura();
            document.getElementById('modal-entrega').classList.add('active');
        };

        document.getElementById('fechar-modal-entrega').onclick = function() {
            document.getElementById('modal-entrega').classList.remove('active');
        };
        document.getElementById('cancelar-entrega').onclick = function() {
            document.getElementById('modal-entrega').classList.remove('active');
        };

        // Preview fotos entrega
        document.getElementById('entrega-fotos').onchange = function(e) {
            var files = Array.from(e.target.files).slice(0, 10);
            fotosEntrega = files;
            var preview = document.getElementById('preview-fotos-entrega');
            preview.innerHTML = '';
            files.forEach(function(file) {
                var reader = new FileReader();
                reader.onload = function(ev) {
                    preview.innerHTML += '<div class="foto-thumb-container"><img src="' + ev.target.result + '" class="foto-thumb"></div>';
                };
                reader.readAsDataURL(file);
            });
        };

        // Preview vídeo entrega
        document.getElementById('entrega-video').onchange = function(e) {
            var file = e.target.files[0];
            if (file) {
                var video = document.createElement('video');
                video.src = URL.createObjectURL(file);
                video.controls = true;
                video.style.maxWidth = '100%';
                document.getElementById('preview-video-entrega').innerHTML = '';
                document.getElementById('preview-video-entrega').appendChild(video);
            }
        };

        // Assinatura canvas
        var assinaturaCanvas, assinaturaCtx, desenhando = false;
        
        function initAssinatura() {
            ['assinatura-cliente', 'assinatura-tecnico-entrega'].forEach(function(canvasId) {
                var canvas = document.getElementById(canvasId);
                if (!canvas) return;
                var ctx = canvas.getContext('2d');
                ctx.strokeStyle = '#000';
                ctx.lineWidth = 2;
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                
                var drawing = false;
                canvas.onmousedown = function(e) {
                    drawing = true;
                    ctx.beginPath();
                    ctx.moveTo(e.offsetX, e.offsetY);
                };
                canvas.onmousemove = function(e) {
                    if (drawing) {
                        ctx.lineTo(e.offsetX, e.offsetY);
                        ctx.stroke();
                    }
                };
                canvas.onmouseup = function() { drawing = false; };
                canvas.onmouseleave = function() { drawing = false; };
                
                canvas.ontouchstart = function(e) {
                    e.preventDefault();
                    var rect = canvas.getBoundingClientRect();
                    drawing = true;
                    ctx.beginPath();
                    ctx.moveTo(e.touches[0].clientX - rect.left, e.touches[0].clientY - rect.top);
                };
                canvas.ontouchmove = function(e) {
                    e.preventDefault();
                    if (drawing) {
                        var rect = canvas.getBoundingClientRect();
                        ctx.lineTo(e.touches[0].clientX - rect.left, e.touches[0].clientY - rect.top);
                        ctx.stroke();
                    }
                };
                canvas.ontouchend = function() { drawing = false; };
            });
        }

        window.limparAssinatura = function(canvasId) {
            var canvas = document.getElementById(canvasId);
            var ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        };

        document.getElementById('form-entrega').onsubmit = function(e) {
            e.preventDefault();
            showToast('Entrega técnica salva com sucesso!', 'success');
            document.getElementById('modal-entrega').classList.remove('active');
        };

        // ===== REVISÃO / MANUTENÇÃO =====
        async function loadRevisoes() {
            showLoading();
            await loadSelectsPosvenda();
            hideLoading();
            renderRevisoes();
        }

        function renderRevisoes() {
            var lista = document.getElementById('lista-revisoes');
            if (revisoes.length === 0) {
                lista.innerHTML = '<div class="empty-state"><i class="fas fa-wrench"></i><p>Nenhuma revisão registrada</p></div>';
                return;
            }
        }

        document.getElementById('btn-nova-revisao').onclick = function() {
            document.getElementById('modal-revisao-titulo').textContent = 'Nova Revisão / Manutenção';
            document.getElementById('form-revisao').reset();
            document.getElementById('revisao-id').value = '';
            document.getElementById('revisao-data').value = new Date().toISOString().split('T')[0];
            document.getElementById('preview-fotos-revisao').innerHTML = '';
            document.getElementById('preview-video-revisao').innerHTML = '';
            document.getElementById('atendimentos-container').innerHTML = getAtendimentoHTML();
            fotosRevisao = [];
            initAssinaturasRevisao();
            document.getElementById('modal-revisao').classList.add('active');
        };

        function getAtendimentoHTML() {
            return '<div class="atendimento-item" style="background:#f9fafb;padding:15px;border-radius:8px;margin-bottom:10px;">' +
                '<div class="form-row">' +
                '<div class="form-group"><label>Data</label><input type="date" class="atend-data"></div>' +
                '<div class="form-group"><label>Horário Início</label><input type="time" class="atend-inicio"></div>' +
                '<div class="form-group"><label>Horário Fim</label><input type="time" class="atend-fim"></div>' +
                '</div>' +
                '<div class="form-row">' +
                '<div class="form-group"><label>Tipo</label><select class="atend-tipo"><option value="Serv.">Serviço</option><option value="Desl.">Deslocamento</option></select></div>' +
                '<div class="form-group"><label>KM Rodados</label><input type="number" class="atend-km" placeholder="0"></div>' +
                '</div></div>';
        }

        window.adicionarAtendimento = function() {
            var container = document.getElementById('atendimentos-container');
            container.innerHTML += getAtendimentoHTML();
        };

        function initAssinaturasRevisao() {
            ['assinatura-tecnico-revisao', 'assinatura-cliente-revisao'].forEach(function(canvasId) {
                var canvas = document.getElementById(canvasId);
                if (!canvas) return;
                var ctx = canvas.getContext('2d');
                ctx.strokeStyle = '#000';
                ctx.lineWidth = 2;
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                
                var drawing = false;
                canvas.onmousedown = function(e) {
                    drawing = true;
                    ctx.beginPath();
                    ctx.moveTo(e.offsetX, e.offsetY);
                };
                canvas.onmousemove = function(e) {
                    if (drawing) {
                        ctx.lineTo(e.offsetX, e.offsetY);
                        ctx.stroke();
                    }
                };
                canvas.onmouseup = function() { drawing = false; };
                canvas.onmouseleave = function() { drawing = false; };
                
                canvas.ontouchstart = function(e) {
                    e.preventDefault();
                    var rect = canvas.getBoundingClientRect();
                    drawing = true;
                    ctx.beginPath();
                    ctx.moveTo(e.touches[0].clientX - rect.left, e.touches[0].clientY - rect.top);
                };
                canvas.ontouchmove = function(e) {
                    e.preventDefault();
                    if (drawing) {
                        var rect = canvas.getBoundingClientRect();
                        ctx.lineTo(e.touches[0].clientX - rect.left, e.touches[0].clientY - rect.top);
                        ctx.stroke();
                    }
                };
                canvas.ontouchend = function() { drawing = false; };
            });
        }

        document.getElementById('fechar-modal-revisao').onclick = function() {
            document.getElementById('modal-revisao').classList.remove('active');
        };
        document.getElementById('cancelar-revisao').onclick = function() {
            document.getElementById('modal-revisao').classList.remove('active');
        };

        // Preview fotos revisão
        document.getElementById('revisao-fotos').onchange = function(e) {
            var files = Array.from(e.target.files).slice(0, 10);
            fotosRevisao = files;
            var preview = document.getElementById('preview-fotos-revisao');
            preview.innerHTML = '';
            files.forEach(function(file) {
                var reader = new FileReader();
                reader.onload = function(ev) {
                    preview.innerHTML += '<div class="foto-thumb-container"><img src="' + ev.target.result + '" class="foto-thumb"></div>';
                };
                reader.readAsDataURL(file);
            });
        };

        // Preview vídeo revisão
        document.getElementById('revisao-video').onchange = function(e) {
            var file = e.target.files[0];
            if (file) {
                var video = document.createElement('video');
                video.src = URL.createObjectURL(file);
                video.controls = true;
                video.style.maxWidth = '100%';
                document.getElementById('preview-video-revisao').innerHTML = '';
                document.getElementById('preview-video-revisao').appendChild(video);
            }
        };

        document.getElementById('form-revisao').onsubmit = function(e) {
            e.preventDefault();
            showToast('Revisão salva com sucesso!', 'success');
            document.getElementById('modal-revisao').classList.remove('active');
        };

        // Busca
        document.getElementById('busca-inspecao').oninput = function(e) {
            // Implementar filtro
        };
        document.getElementById('busca-entrega').oninput = function(e) {
            // Implementar filtro
        };
        document.getElementById('busca-revisao').oninput = function(e) {
            // Implementar filtro
        };

        console.log('MaqVendas carregado!');

        // Registrar Service Worker para PWA
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('sw.js').then(function(reg) {
                console.log('Service Worker registrado');
            }).catch(function(err) {
                console.log('Erro SW:', err);
            });
        }
    </script>
</body>
</html>
