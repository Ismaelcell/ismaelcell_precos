<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Preços</title>
    <style>
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
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        
        h2 {
            color: #333;
            margin-bottom: 20px;
        }
        
        h3 {
            color: #555;
            margin-top: 30px;
            margin-bottom: 15px;
        }
        
        input {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 1em;
        }
        
        input:focus {
            outline: none;
            border-color: #667eea;
        }
        
        button {
            width: 100%;
            padding: 12px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #764ba2;
        }
        
        #lista {
            margin-top: 20px;
        }
        
        .item {
            background: #f5f5f5;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .item-info {
            flex: 1;
        }
        
        .item button {
            width: auto;
            padding: 8px 15px;
            margin-left: 10px;
            font-size: 0.9em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>📱 Sistema de Preços</h2>
        
        <input id="modelo" placeholder="Modelo"><br>
        <input id="servico" placeholder="Serviço"><br>
        <input id="valor" placeholder="Valor"><br>
        
        <button onclick="add()">Adicionar</button>
        
        <h3>Lista</h3>
        <div id="lista"></div>
    </div>

    <script>
        let dados = [];

        function add(){
            let m = document.getElementById("modelo").value;
            let s = document.getElementById("servico").value;
            let v = document.getElementById("valor").value;

            if(!m || !s || !v){
                alert("Preencha tudo");
                return;
            }

            dados.push({m, s, v});
            document.getElementById("modelo").value = "";
            document.getElementById("servico").value = "";
            document.getElementById("valor").value = "";
            mostrar();
        }

        function mostrar(){
            let lista = document.getElementById("lista");
            lista.innerHTML = "";

            dados.forEach((d, i) => {
                lista.innerHTML += `
                    <div class="item">
                        <div class="item-info">
                            <strong>${d.m}</strong> - ${d.s} - R$ ${d.v}
                        </div>
                        <button onclick="compartilhar(${i})">Compartilhar</button>
                        <button onclick="deletar(${i})" style="background: #e74c3c;">Deletar</button>
                    </div>
                `;
            });
        }

        function compartilhar(i){
            let d = dados[i];
            let texto = `Modelo: ${d.m}\nServiço: ${d.s}\nValor: R$ ${d.v}`;

            if(navigator.share){
                navigator.share({text: texto});
            } else {
                alert(texto);
            }
        }

        function deletar(i){
            dados.splice(i, 1);
            mostrar();
        }
    </script>
</body>
</html>
