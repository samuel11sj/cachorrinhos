<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>Cadastro de Cachorro</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Escolha seu Cachorro</h1>

  <label for="raca">Raça:</label>
  <select id="raca" onchange="atualizarCores()"></select>

  <label for="cor">Cor:</label>
  <select id="cor"></select>

  <button onclick="gerarCachorro()">Gerar Cachorro</button>

  <div id="resultado"></div>

  <script>
    // Superclasse
    class Animal {
      constructor(patas, olhos) {
        this.patas = patas;
        this.olhos = olhos;
      }
    }

    // Classe Cachorro herdando de Animal
    class Cachorro extends Animal {
      constructor(raca, cor, patas, olhos) {
        super(patas, olhos);
        this.raca = raca;
        this.cor = cor;
      }
    }

    // Objeto com raças
    const racas = {
      "Labrador": {
        descricao: "Cão amigável, leal e cheio de energia.",
        cores: ["Amarelo", "Chocolate", "Preto"],
        patas: 4,
        olhos: 2,
        imagem: "imagens/labrador.jpg"
      },
      "Poodle": {
        descricao: "Cão inteligente, elegante e brincalhão.",
        cores: ["Branco", "Preto", "Marrom"],
        patas: 4,
        olhos: 2,
        imagem: "imagens/poodle.jpg"
      },
      "Bulldog": {
        descricao: "Cão calmo, forte e afetuoso.",
        cores: ["Branco", "Rajado", "Caramelo"],
        patas: 4,
        olhos: 2,
        imagem: "imagens/bulldog.jpg"
      },
      "Golden Retriever": {
        descricao: "Cão dócil, paciente e muito inteligente.",
        cores: ["Dourado", "Caramelo", "Areia"],
        patas: 4,
        olhos: 2,
        imagem: "imagens/golden.jpg"
      }
    };

    // DOM
    const selectRaca = document.getElementById("raca");
    const selectCor = document.getElementById("cor");
    const resultadoDiv = document.getElementById("resultado");

    for (let raca in racas) {
      const option = document.createElement("option");
      option.value = raca;
      option.textContent = raca;
      selectRaca.appendChild(option);
    }

    function atualizarCores() {
      selectCor.innerHTML = "";
      const racaSelecionada = selectRaca.value;
      const cores = racas[racaSelecionada].cores;
      cores.forEach(cor => {
        const option = document.createElement("option");
        option.value = cor;
        option.textContent = cor;
        selectCor.appendChild(option);
      });
    }

    window.onload = atualizarCores;

    function gerarCachorro() {
      const raca = selectRaca.value;
      const cor = selectCor.value;
      const dados = racas[raca];

      const cachorro = new Cachorro(raca, cor, dados.patas, dados.olhos);

      resultadoDiv.innerHTML = `
        <div class="card">
          <h2>${cachorro.raca} (${cachorro.cor})</h2>
          <img src="${dados.imagem}" alt="${raca}" width="300">
          <p><strong>Descrição:</strong> ${dados.descricao}</p>
          <p><strong>Patas:</strong> ${cachorro.patas} | <strong>Olhos:</strong> ${cachorro.olhos}</p>
        </div>
      `;
    }
  </script>
</body>
</html>
