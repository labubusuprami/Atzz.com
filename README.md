<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Teste Simples - Livros</title>
</head>
<body>
  <h1>Cadastro de Livros</h1>
  <form id="formLivro">
    <input type="text" id="titulo" placeholder="Título" required /><br/><br/>
    <textarea id="descricao" placeholder="Descrição" required></textarea><br/><br/>
    <input type="number" id="preco" placeholder="Preço" step="0.01" min="0" required /><br/><br/>
    <input type="url" id="imagem" placeholder="URL da capa" required /><br/><br/>
    <button type="submit">Salvar</button>
  </form>

  <h2>Livros cadastrados:</h2>
  <div id="listaLivros"></div>

<script>
  const form = document.getElementById('formLivro');
  const lista = document.getElementById('listaLivros');
  let livros = JSON.parse(localStorage.getItem('livros') || '[]');

  function salvarLivros() {
    localStorage.setItem('livros', JSON.stringify(livros));
  }

  function mostrarLivros() {
    lista.innerHTML = '';
    livros.forEach((livro, i) => {
      lista.innerHTML += `
        <div style="border:1px solid #ccc; margin-bottom:10px; padding:10px;">
          <h3>${livro.titulo}</h3>
          <p>${livro.descricao}</p>
          <p><b>Preço:</b> R$ ${parseFloat(livro.preco).toFixed(2)}</p>
          <img src="${livro.imagem}" alt="${livro.titulo}" style="max-width:100px;" />
        </div>
      `;
    });
  }

  form.addEventListener('submit', e => {
    e.preventDefault();
    const titulo = document.getElementById('titulo').value.trim();
    const descricao = document.getElementById('descricao').value.trim();
    const preco = document.getElementById('preco').value;
    const imagem = document.getElementById('imagem').value.trim();

    if (!titulo || !descricao || !preco || !imagem) {
      alert('Preencha todos os campos.');
      return;
    }

    livros.push({ titulo, descricao, preco, imagem });
    salvarLivros();
    mostrarLivros();
    form.reset();
  });

  mostrarLivros();
</script>
</body>
</html>
