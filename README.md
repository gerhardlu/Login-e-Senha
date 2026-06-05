<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Astrolin</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet"/>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css" rel="stylesheet"/>
    <style>
        body { background-color: #0d1117; min-height: 100vh; }
    </style>
</head>
<body>


<!--login-->
<div id="paginalogin" class="container mt-5">
    <div class="row justify-content-center">
        <div class="cold-md-4">
            <div class="cas p-4 shadow-sm">
                <h4 class="text-center mb-4">🚀Astrolin</h4>

                <div id="erroLogin" class="alert alert-danger d-none">usuário ou senha inválidos</div>
                
                <div class="mb-3">
                    <label for="email" class="form-label">Email</label>
                    <input type="email" id="email" class="form-control" placeholder="digite seu email">
                </div>
                <div class="mb-3">
                    <label for="senha" class="form-label">Senha</label>
                    <input type="password" id="email" class="form-control" placeholder="digite sua senha">
                
                </div>

                <button id="btnLogin" class="btn btn-primary w-100" onclick="fazerLogin()">Entrar</button>

                <p class="text=muted text-center mt-3 small">
                    Demo: operador@primeiroteste.space / 123456
                </p>
            </div>
        </div>
    </div>
</div>

<!--dashboard-->
<div id="paginaDashboard" class="container mt-5" style="display:none;">
    
    <div class="d-flex justify-content-between align-items-center mb-4">
        <h4>🚀 Astrolin - Nave Orion-01</h4>
        <button class="btn btn-outline-secondary btn-sm" onclick="sair()">Sair</button>
    </div>

<!--métricas-->
<div class="row g-3 mb-4">
    <div class="col-6 col-md-3">
        <div class="card p-3 text-white shadow-sm">
            <p class="text-muted mb-1 small">oxigênio</p>
            <h4 id="oxigenio">-</h4>
        </div>
    </div>
    <div class="row g-3 mb-4">
    <div class="col-6 col-md-3">
        <div class="card p-3 text-white shadow-sm">
            <p class="text-muted mb-1 small">temperatura</p>
            <h4 id="temperatura">-</h4>
        </div>
    </div>
    <div class="row g-3 mb-4">
    <div class="col-6 col-md-3">
        <div class="card p-3 text-white shadow-sm">
            <p class="text-muted mb-1 small">pressão</p>
            <h4 id="pressao">-</h4>
        </div>
    </div>
    <div class="row g-3 mb-4">
    <div class="col-6 col-md-3">
        <div class="card p-3 text-white shadow-sm">
            <p class="text-muted mb-1 small">velocidade</p>
            <h4 id="velocidade">-</h4>
        </div>
    </div>
    <!--alertas-->
<div class="cas p-3 shadow-sm">
        <h6 class="mb-3">Alertas</h6>
        <ul id="listaAlertas" class="list-group list-group-flush">
          <li class="list-group-item text-muted small">Nenhum alerta ativo</li>
        </ul>
</div>
<scrip>
    //login
    function fazerLogin() {
        const email = document.getElementById('email').value;
        const senha = document.getElementById('senha').value;

        if (email === 'operador@primeiroteste.space' && senha === '123456') {
            document.getElementById('paginalogin').style.display = 'none';
            document.getElementById('paginaDashboard').style.display = 'block';
            iniciarDashboard();
        } else {
            document.getElementById('erroLogin').classList.remove('d-none');
        }

        //Sair
        function sair() {
            document.getElementById('paginaDashboard').style.display = 'none';
            document.getElementById('paginalogin').style.display = 'block';
        }

        //Atualizar os dados a cada 3 segundos
        function iniciarDashboard() {
            atualizarDados();
            setInterval(atualizarDados, 3000);
        }

        function atualizarDados() {
            //Simular dados aleatórios
            var oxigenio = (Math.random() * (23 - 100)).toFixed(1);
            var temperatura = (Math.random() * (100 - (-50))).toFixed(1);
            var pressao = (Math.random() * (2 - 0.5)).toFixed(1);
            var velocidade = (Math.random() * (100 - 0)).toFixed(1);

            //mostrar os dados no dashboard

            document.getElementById('oxigenio').textContent = oxigenio + '%';
            document.getElementById('temperatura').textContent = temperatura + '°C';
            document.getElementById('pressao').textContent = pressao + ' kPa';
            document.getElementById('velocidade').textContent = velocidade + ' km/h';

            //alerta se oxigênio baixo
            if (oxigenio < 19.65) {
                adicionarAlerta('Nível de oxigênio crítico!: ' + oxigenio + '%', 'danger');
            }

            //alerta se temperatura alta
            if (temperatura > 50) {
                adicionarAlerta('Temperatura crítica!: ' + temperatura + '°C', 'warning');
            }
        }

        function adicionarAlerta(mensagem, tipo) {
            var lista = document.getElementById('listaAlertas');

            // Remove o texto padrão se for o primeiro alerta
            if (lista.children[0].classList.contains('text-muted')) {
                lista.innerHTML = '';
            }

            var item = document.createElement('li');
            item.className = 'list-group-item alert alert-' + tipo + ' small';
            item.textContent = new Date().toLocaleTimeString('pt-BR') + ' - ' + mensagem;
            lista.appendChild(item);
        }
</script>

</body>   
</html>
