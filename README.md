<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestão de Entregas - Lanchonete</title>
    <style>
        :root {
            --primary: #ff5722;
            --primary-dark: #e64a19;
            --bg: #121212;
            --surface: #1e1e1e;
            --surface-card: #252525;
            --text: #e0e0e0;
            --text-muted: #9e9e9e;
            --border: #333333;
            --accent: #4caf50;
            --danger: #d32f2f;
            --whatsapp: #25d366;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            display: flex;
            height: 100vh;
            overflow: hidden;
        }

        /* Sidebar */
        sidebar {
            width: 260px;
            background-color: var(--surface);
            border-right: 1px solid var(--border);
            display: flex;
            flex-direction: column;
        }

        .logo-area {
            padding: 20px;
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--primary);
            border-bottom: 1px solid var(--border);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .nav-menu {
            list-style: none;
            padding: 20px 0;
        }

        .nav-item {
            padding: 12px 20px;
            cursor: pointer;
            transition: 0.2s;
            color: var(--text-muted);
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .nav-item:hover, .nav-item.active {
            background-color: rgba(255, 87, 34, 0.1);
            color: var(--primary);
            border-left: 4px solid var(--primary);
        }

        /* Main Content */
        main {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
        }

        header {
            padding: 20px 30px;
            background-color: var(--surface);
            border-bottom: 1px solid var(--border);
            font-size: 1.4rem;
            font-weight: 600;
        }

        .content-body {
            padding: 30px;
            flex: 1;
        }

        .view {
            display: none;
        }

        .view.active {
            display: block;
        }

        /* Forms & Cards */
        .card {
            background-color: var(--surface-card);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 25px;
            max-width: 650px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
        }

        .form-row {
            display: flex;
            gap: 15px;
        }

        .form-row .form-group {
            flex: 1;
        }

        .form-group {
            margin-bottom: 18px;
        }

        label {
            display: block;
            margin-bottom: 6px;
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        input, select, textarea {
            width: 100%;
            padding: 10px 12px;
            background-color: var(--bg);
            border: 1px solid var(--border);
            border-radius: 6px;
            color: var(--text);
            font-size: 1rem;
        }

        input:focus, select:focus, textarea:focus {
            border-color: var(--primary);
            outline: none;
        }

        .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: 0.2s;
            width: 100%;
        }

        .btn:hover {
            background-color: var(--primary-dark);
        }

        .btn-success {
            background-color: var(--accent);
            width: auto;
        }
        .btn-success:hover {
            background-color: #388e3c;
        }

        .btn-whatsapp {
            background-color: var(--whatsapp);
            width: auto;
            color: white;
        }
        .btn-whatsapp:hover {
            background-color: #1ebe5d;
        }

        .btn-danger {
            background-color: var(--danger);
            width: auto;
        }
        .btn-danger:hover {
            background-color: #b71c1c;
        }

        .btn-print {
            background-color: #2196f3;
            width: auto;
            color: white;
        }
        .btn-print:hover {
            background-color: #1976d2;
        }

        .btn-sm {
            padding: 6px 12px;
            font-size: 0.85rem;
            width: auto;
        }

        /* Dashboard de Fechamento */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .stat-card {
            background-color: var(--surface-card);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
        }

        .stat-card h4 {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-bottom: 8px;
            text-transform: uppercase;
        }

        .stat-card .value {
            font-size: 1.6rem;
            font-weight: bold;
            color: var(--primary);
        }

        .stat-card.green .value {
            color: var(--accent);
        }

        /* Tables & Lists */
        table {
            width: 100%;
            border-collapse: collapse;
            background-color: var(--surface-card);
            border-radius: 8px;
            overflow: hidden;
            border: 1px solid var(--border);
        }

        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid var(--border);
            font-size: 0.9rem;
        }

        th {
            background-color: rgba(255,255,255,0.03);
            color: var(--text-muted);
            font-weight: 600;
        }

        tr:hover {
            background-color: rgba(255,255,255,0.01);
        }

        .toolbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        /* ESTILOS EXCLUSIVOS PARA IMPRESSÃO / PDF */
        @media print {
            sidebar, .toolbar, header, .nav-menu {
                display: none !important;
            }
            body {
                background-color: white !important;
                color: black !important;
                display: block !important;
                height: auto !important;
                overflow: visible !important;
            }
            main {
                overflow: visible !important;
            }
            .content-body {
                padding: 0 !important;
            }
            .stat-card {
                background-color: #f5f5f5 !important;
                border: 1px solid #ccc !important;
                color: black !important;
            }
            .stat-card h4 {
                color: #555 !important;
            }
            .stat-card .value {
                color: #000 !important;
            }
            table {
                background-color: white !important;
                border: 1px solid #ccc !important;
            }
            th, td {
                color: black !important;
                border-bottom: 1px solid #ccc !important;
            }
            th {
                background-color: #eee !important;
            }
        }
    </style>
</head>
<body>

    <sidebar>
        <div class="logo-area">🍔 Delivery System</div>
        <ul class="nav-menu">
            <li class="nav-item active" onclick="switchView('novo-pedido', this)">➕ Novo Pedido</li>
            <li class="nav-item" onclick="switchView('pedidos-abertos', this)" id="menu-abertos">📦 Pedidos Abertos</li>
            <li class="nav-item" onclick="switchView('historico', this)" id="menu-historico">📊 Histórico & Fechamento</li>
        </ul>
    </sidebar>

    <main>
        <header id="header-title">Lançar Novo Pedido</header>
        
        <div class="content-body">
            
            <!-- VIEW: NOVO PEDIDO -->
            <div id="novo-pedido" class="view active">
                <div class="card">
                    <form id="orderForm" onsubmit="salvarPedido(event)">
                        <div class="form-row">
                            <div class="form-group">
                                <label>Nome do Cliente</label>
                                <input type="text" id="cliente" required placeholder="Ex: João da Silva">
                            </div>
                            <div class="form-group">
                                <label>Telefone para Contato</label>
                                <input type="text" id="telefone" required placeholder="Ex: (84) 99999-9999">
                            </div>
                        </div>

                        <div class="form-group">
                            <label>Endereço Completo (Digite a rua ou bairro para autodetectar)</label>
                            <textarea id="endereco" rows="2" required placeholder="Ex: Rua Henrique Dias, 120" oninput="detectarBairroAutomatico()"></textarea>
                        </div>

                        <div class="form-group">
                            <label>Ponto de Referência</label>
                            <input type="text" id="referencia" placeholder="Ex: Próximo à praça, casa amarela">
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label>Bairro (Zona Norte e Região)</label>
                                <select id="bairro" required onchange="atualizarOpcoesTaxa()">
                                    <option value="" disabled selected>Aguardando endereço ou selecione...</option>
                                    <option value="Lagoa Azul" data-min="4.00" data-max="4.00">Lagoa Azul - R$ 4,00 (Fixo)</option>
                                    <option value="Pajuçara" data-min="6.00" data-max="8.00">Pajuçara - R$ 6,00 a R$ 8,00</option>
                                    <option value="Nossa Senhora da Apresentação" data-min="6.00" data-max="8.00">Nossa Senhora da Apresentação - R$ 6,00 a R$ 8,00</option>
                                    <option value="Potengi" data-min="5.00" data-max="8.00">Potengi - R$ 5,00 a R$ 8,00</option>
                                    <option value="Igapó" data-min="6.00" data-max="8.00">Igapó - R$ 6,00 a R$ 8,00</option>
                                    <option value="Redinha" data-min="9.00" data-max="12.00">Redinha - R$ 9,00 a R$ 12,00</option>
                                    <option value="Salinas" data-min="10.00" data-max="12.00">Salinas - R$ 10,00 a R$ 12,00</option>
                                    <option value="Extremoz" data-min="10.00" data-max="15.00">Extremoz - R$ 10,00 a R$ 15,00</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Taxa de Entrega (Ajustável por Km)</label>
                                <select id="taxaSelecionada" required onchange="calcularTotalGeral()">
                                    <option value="" disabled selected>Selecione o valor...</option>
                                </select>
                            </div>
                        </div>

                        <div class="form-group">
                            <label>Produtos / Itens do Pedido</label>
                            <textarea id="produtos" rows="2" required placeholder="Ex: 2x X-Tudo, 1x Coca-Cola 2L"></textarea>
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label>Valor dos Produtos (R$)</label>
                                <input type="number" step="0.01" id="valorProdutos" required placeholder="0.00" oninput="calcularTotalGeral()">
                            </div>
                            <div class="form-group">
                                <label>Valor Total (Produtos + Taxa)</label>
                                <input type="text" id="valorTotal" readonly value="R$ 0,00" style="color: var(--accent); font-weight: bold;">
                            </div>
                        </div>

                        <div class="form-group">
                            <label>Forma de Pagamento</label>
                            <select id="pagamento" required>
                                <option value="" disabled selected>Selecione a forma de pagamento...</option>
                                <option value="Débito">Débito</option>
                                <option value="Crédito">Crédito</option>
                                <option value="Pix">Pix</option>
                                <option value="Voucher">Voucher</option>
                                <option value="Link">Link</option>
                                <option value="Link Pago">Link Pago</option>
                                <option value="Pix Pago">Pix Pago</option>
                            </select>
                        </div>

                        <button type="submit" class="btn">Lançar Pedido</button>
                    </form>
                </div>
            </div>

            <!-- VIEW: PEDIDOS ABERTOS -->
            <div id="pedidos-abertos" class="view">
                <div class="toolbar">
                    <span style="color: var(--text-muted);">Selecione os pedidos para gerar a rota de entrega</span>
                    <button class="btn btn-success" onclick="gerarRotaMaps()">🗺️ Montar Rota no Google Maps</button>
                </div>

                <table>
                    <thead>
                        <tr>
                            <th width="30"><input type="checkbox" id="selectAll" onclick="toggleSelectAll(this)"></th>
                            <th>ID</th>
                            <th>Cliente</th>
                            <th>Endereço / Referência</th>
                            <th>Produtos / Pagamento</th>
                            <th>Total</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody id="tabelaPedidos">
                        <!-- Preenchido via JavaScript -->
                    </tbody>
                </table>
            </div>

            <!-- VIEW: HISTÓRICO & FECHAMENTO -->
            <div id="historico" class="view">
                <div class="toolbar">
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <label for="filtroData" style="margin: 0; color: var(--text);">Filtrar por Data:</label>
                        <input type="date" id="filtroData" onchange="renderizarHistorico()" style="width: auto; padding: 6px 10px;">
                        <button class="btn btn-sm" onclick="limparFiltroData()" style="width: auto; background: var(--border);">Ver Todos</button>
                    </div>
                    <div style="display: flex; gap: 10px;">
                        <button class="btn btn-print btn-sm" onclick="window.print()">🖨️ Imprimir Resumo</button>
                        <button class="btn btn-danger btn-sm" onclick="limparHistoricoConcluidos()">🗑️ Fechar o Dia</button>
                    </div>
                </div>

                <div class="stats-grid">
                    <div class="stat-card">
                        <h4>Total de Produtos</h4>
                        <div class="value" id="faturamentoProdutos">R$ 0,00</div>
                    </div>
                    <div class="stat-card">
                        <h4>Total em Taxas</h4>
                        <div class="value" id="faturamentoTaxas">R$ 0,00</div>
                    </div>
                    <div class="stat-card green">
                        <h4>Faturamento Geral</h4>
                        <div class="value" id="faturamentoGeral">R$ 0,00</div>
                    </div>
                    <div class="stat-card">
                        <h4>Entregas Realizadas</h4>
                        <div class="value" id="qtdEntregas" style="color: var(--text);">0</div>
                    </div>
                </div>

                <table>
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Data/Hora</th>
                            <th>Cliente</th>
                            <th>Endereço / Bairro</th>
                            <th>Produtos</th>
                            <th>Pagamento</th>
                            <th>Produtos (R$)</th>
                            <th>Taxa</th>
                            <th>Total</th>
                        </tr>
                    </thead>
                    <tbody id="tabelaHistorico">
                        <!-- Preenchido via JavaScript -->
                    </tbody>
                </table>
            </div>

        </div>
    </main>

    <script>
        let pedidos = JSON.parse(localStorage.getItem('pedidos_lanchonete')) || [];

        function switchView(viewId, element) {
            document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            
            document.getElementById(viewId).classList.add('active');
            element.classList.add('active');

            if(viewId === 'pedidos-abertos') {
                document.getElementById('header-title').innerText = 'Painel de Pedidos Abertos';
                renderizarTabelaAbertos();
            } else if(viewId === 'historico') {
                document.getElementById('header-title').innerText = 'Histórico & Fechamento da Noite';
                if(!document.getElementById('filtroData').value) {
                    const hoje = new Date().toISOString().split('T')[0];
                    document.getElementById('filtroData').value = hoje;
                }
                renderizarHistorico();
            } else {
                document.getElementById('header-title').innerText = 'Lançar Novo Pedido';
            }
        }

        function detectarBairroAutomatico() {
            const texto = document.getElementById('endereco').value.toLowerCase();
            const selectBairro = document.getElementById('bairro');
            let bairroEncontrado = "";

            if (texto.includes('henrique dias') || texto.includes('igapó') || texto.includes('joão medeiros')) {
                bairroEncontrado = 'Igapó';
            } else if (texto.includes('itapetinga') || texto.includes('santa catarina') || texto.includes('potengi')) {
                bairroEncontrado = 'Potengi';
            } else if (texto.includes('pajuçara') || texto.includes('maranguape')) {
                bairroEncontrado = 'Pajuçara';
            } else if (texto.includes('redinha') || texto.includes('largo da redinha')) {
                bairroEncontrado = 'Redinha';
            } else if (texto.includes('salinas')) {
                bairroEncontrado = 'Salinas';
            } else if (texto.includes('extremoz')) {
                bairroEncontrado = 'Extremoz';
            } else if (texto.includes('lagoa azul') || texto.includes('dos avelases')) {
                bairroEncontrado = 'Lagoa Azul';
            } else if (texto.includes('apresentação') || texto.includes('projeto moradia')) {
                bairroEncontrado = 'Nossa Senhora da Apresentação';
            }

            if (bairroEncontrado) {
                for (let i = 0; i < selectBairro.options.length; i++) {
                    if (selectBairro.options[i].value === bairroEncontrado) {
                        selectBairro.selectedIndex = i;
                        atualizarOpcoesTaxa();
                        break;
                    }
                }
            }
        }

        function atualizarOpcoesTaxa() {
            const selectBairro = document.getElementById('bairro');
            const selectTaxa = document.getElementById('taxaSelecionada');
            selectTaxa.innerHTML = '<option value="" disabled selected>Selecione o valor...</option>';

            if (selectBairro.selectedIndex <= 0) return;

            const selectedOption = selectBairro.options[selectBairro.selectedIndex];
            const min = parseFloat(selectedOption.getAttribute('data-min'));
            const max = parseFloat(selectedOption.getAttribute('data-max'));

            // Gera as opções de taxa de R$ em R$ (ex: de 6 a 8 gera 6, 7 e 8)
            for (let v = min; v <= max; v += 1.0) {
                const opt = document.createElement('option');
                opt.value = v.toFixed(2);
                opt.textContent = `R$ ${v.toFixed(2).replace('.', ',')}`;
                // Se for valor único ou o menor valor, deixa selecionado por padrão
                if (v === min) opt.selected = true;
                selectTaxa.appendChild(opt);
            }

            calcularTotalGeral();
        }

        function calcularTotalGeral() {
            const selectTaxa = document.getElementById('taxaSelecionada');
            const taxa = selectTaxa.selectedIndex > 0 ? parseFloat(selectTaxa.value) : 0;
            const valProdutos = parseFloat(document.getElementById('valorProdutos').value) || 0;

            const total = valProdutos + taxa;
            document.getElementById('valorTotal').value = `R$ ${total.toFixed(2).replace('.', ',')}`;
        }

        function salvarPedido(event) {
            event.preventDefault();
            
            const selectBairro = document.getElementById('bairro');
            const selectTaxa = document.getElementById('taxaSelecionada');

            if (!selectBairro.value || !selectTaxa.value) {
                alert('Por favor, informe o bairro e selecione a taxa de entrega.');
                return;
            }

            const agora = new Date();
            const dataIso = agora.toISOString().split('T')[0];
            const horaFormatada = agora.toLocaleTimeString('pt-BR', {hour: '2-digit', minute:'2-digit'});

            const bairroNome = selectBairro.value;
            const taxaValor = parseFloat(selectTaxa.value);
            const valProdutos = parseFloat(document.getElementById('valorProdutos').value) || 0;

            const novoPedido = {
                id: Date.now().toString().slice(-4),
                data: dataIso,
                hora: horaFormatada,
                cliente: document.getElementById('cliente').value,
                telefone: document.getElementById('telefone').value,
                bairro: bairroNome,
                endereco: document.getElementById('endereco').value,
                referencia: document.getElementById('referencia').value,
                produtos: document.getElementById('produtos').value,
                pagamento: document.getElementById('pagamento').value,
                taxa: taxaValor,
                valorProdutos: valProdutos,
                valorTotal: valProdutos + taxaValor,
                status: 'Aberto'
            };

            pedidos.push(novoPedido);
            localStorage.setItem('pedidos_lanchonete', JSON.stringify(pedidos));

            alert('Pedido lançado com sucesso!');
            document.getElementById('orderForm').reset();
            document.getElementById('taxaSelecionada').innerHTML = '<option value="" disabled selected>Selecione o valor...</option>';
            document.getElementById('valorTotal').value = 'R$ 0,00';
            
            switchView('pedidos-abertos', document.getElementById('menu-abertos'));
        }

        function renderizarTabelaAbertos() {
            const tbody = document.getElementById('tabelaPedidos');
            tbody.innerHTML = '';

            const pedidosAbertos = pedidos.filter(p => p.status === 'Aberto');

            if (pedidosAbertos.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" style="text-align: center; color: var(--text-muted);">Nenhum pedido aberto no momento.</td></tr>`;
                return;
            }

            pedidosAbertos.forEach(p => {
                const refHtml = p.referencia ? `<br><small style="color: var(--text-muted);">Ref: ${p.referencia}</small>` : '';
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td><input type="checkbox" class="pedido-check" value="${p.id}" data-endereco="${p.endereco}, ${p.bairro}, Natal - RN"></td>
                    <td>#${p.id}</td>
                    <td><strong>${p.cliente}</strong><br><small>${p.telefone}</small></td>
                    <td>${p.endereco} - <strong>${p.bairro}</strong>${refHtml}</td>
                    <td><span style="white-space: pre-line;">${p.produtos}</span><br><small style="color: var(--primary); font-weight: bold;">Pagamento: ${p.pagamento}</small></td>
                    <td><strong>R$ ${p.valorTotal.toFixed(2).replace('.', ',')}</strong><br><small style="color: var(--text-muted);">Taxa: R$ ${p.taxa.toFixed(2).replace('.', ',')}</small></td>
                    <td>
                        <div style="display: flex; gap: 5px; flex-direction: column;">
                            <button class="btn btn-whatsapp btn-sm" onclick="enviarWhatsApp('${p.id}')">💬 WhatsApp</button>
                            <button class="btn btn-success btn-sm" onclick="concluirPedido('${p.id}')">✅ Concluir</button>
                        </div>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function enviarWhatsApp(id) {
            const p = pedidos.find(item => item.id === id);
            if (!p) return;

            let textoMensagem = `📦 *DETALHES DO PEDIDO #${p.id}* 📦\n\n` +
                                `👤 *Cliente:* ${p.cliente}\n` +
                                `📞 *Contato:* ${p.telefone}\n` +
                                `📍 *Endereço:* ${p.endereco} - ${p.bairro}\n` +
                                (p.referencia ? `🔍 *Referência:* ${p.referencia}\n` : '') +
                                `\n🍔 *Produtos:* \n${p.produtos}\n\n` +
                                `💰 *Valor Total:* R$ ${p.valorTotal.toFixed(2).replace('.', ',')} (Taxa: R$ ${p.taxa.toFixed(2).replace('.', ',')})\n` +
                                `💳 *Forma de Pagamento:* ${p.pagamento}`;

            const urlWpp = `https://api.whatsapp.com/send?text=${encodeURIComponent(textoMensagem)}`;
            window.open(urlWpp, '_blank');
        }

        function renderizarHistorico() {
            const tbody = document.getElementById('tabelaHistorico');
            tbody.innerHTML = '';

            const dataFiltro = document.getElementById('filtroData').value;

            let pedidosConcluidos = pedidos.filter(p => p.status === 'Concluído');
            if (dataFiltro) {
                pedidosConcluidos = pedidosConcluidos.filter(p => p.data === dataFiltro);
            }

            let totalProd = 0;
            let totalTaxas = 0;

            if (pedidosConcluidos.length === 0) {
                tbody.innerHTML = `<tr><td colspan="9" style="text-align: center; color: var(--text-muted);">Nenhum pedido concluído encontrado para esta data.</td></tr>`;
            } else {
                pedidosConcluidos.forEach(p => {
                    totalProd += p.valorProdutos;
                    totalTaxas += p.taxa;

                    const tr = document.createElement('tr');
                    tr.innerHTML = `
                        <td>#${p.id}</td>
                        <td>${p.data ? p.data.split('-').reverse().join('/') : '-'} às ${p.hora || ''}</td>
                        <td>${p.cliente}</td>
                        <td>${p.endereco} - <strong>${p.bairro}</strong></td>
                        <td><span style="white-space: pre-line;">${p.produtos}</span></td>
                        <td><span style="color: var(--primary); font-weight: bold;">${p.pagamento}</span></td>
                        <td>R$ ${p.valorProdutos.toFixed(2).replace('.', ',')}</td>
                        <td>R$ ${p.taxa.toFixed(2).replace('.', ',')}</td>
                        <td><strong>R$ ${p.valorTotal.toFixed(2).replace('.', ',')}</strong></td>
                    `;
                    tbody.appendChild(tr);
                });
            }

            document.getElementById('faturamentoProdutos').innerText = `R$ ${totalProd.toFixed(2).replace('.', ',')}`;
            document.getElementById('faturamentoTaxas').innerText = `R$ ${totalTaxas.toFixed(2).replace('.', ',')}`;
            document.getElementById('faturamentoGeral').innerText = `R$ ${(totalProd + totalTaxas).toFixed(2).replace('.', ',')}`;
            document.getElementById('qtdEntregas').innerText = pedidosConcluidos.length;
        }

        function limparFiltroData() {
            document.getElementById('filtroData').value = '';
            renderizarHistorico();
        }

        function limparHistoricoConcluidos() {
            if(confirm('Tem certeza que deseja apagar o histórico dos pedidos concluídos e zerar o caixa do dia?')) {
                pedidos = pedidos.filter(p => p.status === 'Aberto');
                localStorage.setItem('pedidos_lanchonete', JSON.stringify(pedidos));
                renderizarHistorico();
                alert('Histórico limpo e caixa zerado com sucesso!');
            }
        }

        function concluirPedido(id) {
            const index = pedidos.findIndex(p => p.id === id);
            if (index !== -1) {
                pedidos[index].status = 'Concluído';
                localStorage.setItem('pedidos_lanchonete', JSON.stringify(pedidos));
                renderizarTabelaAbertos();
            }
        }

        function toggleSelectAll(master) {
            const checkboxes = document.querySelectorAll('.pedido-check');
            checkboxes.forEach(cb => cb.checked = master.checked);
        }

        function gerarRotaMaps() {
            const checkboxes = document.querySelectorAll('.pedido-check:checked');
            
            if (checkboxes.length === 0) {
                alert('Selecione pelo menos um pedido para montar a rota.');
                return;
            }

            let destinos = [];
            checkboxes.forEach(cb => {
                destinos.push(encodeURIComponent(cb.getAttribute('data-endereco')));
            });

            // Ponto base fixo da lanchonete na Rua da Toada, 990, Lagoa Azul, Natal/RN
            let origemBase = encodeURIComponent("Rua da Toada, 990, Lagoa Azul, Natal - RN");

            let baseURL = `https://www.google.com/maps/dir/${origemBase}/`;
            let urlRota = baseURL + destinos.join('/');

            window.open(urlRota, '_blank');
        }
    </script>
</body>
</html>
