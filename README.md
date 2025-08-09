<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Mini KDP - Plataforma de Publicação</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f7fa;
      margin: 0; padding: 0;
      color: #333;
    }
    header {
      background-color: #2d6cdf;
      color: white;
      padding: 1.2em;
      text-align: center;
      font-size: 1.5em;
      font-weight: bold;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    main {
      max-width: 900px;
      margin: 2em auto;
      background: white;
      padding: 1.5em;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h2 {
      color: #2d6cdf;
      margin-top: 0;
    }
    form {
      background: #e9f0fe;
      padding: 1em;
      border-radius: 6px;
      margin-bottom: 2em;
    }
    form label {
      display: block;
      font-weight: bold;
      margin-top: 0.8em;
    }
    form input[type="text"],
    form input[type="url"],
    form input[type="number"],
    form textarea {
      width: 100%;
      padding: 0.5em;
      margin-top: 0.3em;
      border-radius: 4px;
      border: 1px solid #ccc;
      box-sizing: border-box;
      font-size: 1em;
    }
    form button {
      margin-top: 1em;
      background-color: #2d6cdf;
      color: white;
      border: none;
      padding: 0.7em 1.5em;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1em;
    }
    form button:hover {
      background-color: #1a47a3;
    }
    .books-list {
      display: flex;
      flex-wrap: wrap;
      gap: 1em;
      justify-content: center;
    }
    .book-card {
      background: #fafafa;
      border: 1px solid #ddd;
      border-radius: 6px;
      width: 260px;
      box-sizing: border-box;
      display: flex;
      flex-direction: column;
      padding: 1em;
      justify-content: space-between;
      box-shadow: 0 2px 5px rgba(0,0,0,0.05);
    }
    .book-card img {
      width: 100%;
      height: 140px;
      object-fit: cover;
      border-radius: 4px;
      margin-bottom: 0.8em;
      background: #ddd;
    }
    .book-title {
      font-size: 1.2em;
      color: #2d6cdf;
      margin: 0 0 0.5em 0;
      font-weight: bold;
    }
    .book-description {
      font-size: 0.9em;
      margin-bottom: 0.8em;
      flex-grow: 1;
      color: #555;
    }
    .book-price {
      font-weight: bold;
      color: #009900;
      margin-bottom: 1em;
    }
    .book-actions {
      display: flex;
      gap: 0.5em;
    }
    .book-actions button {
      flex: 1;
      padding: 0.5em;
      border: none;
      border-radius: 5px;
      font-size: 0.9em;
      cursor: pointer;
      color: white;
    }
    .edit-btn {
      background-color: #f0ad4e;
    }
    .edit-btn:hover {
      background-color: #d99932;
    }
    .delete-btn {
      background-color: #d9534f;
    }
    .delete-btn:hover {
      background-color: #b7332b;
    }
    .buy-btn {
      background-color: #5cb85c;
    }
    .buy-btn:hover {
      background-color: #3d823d;
    }
    footer {
      margin-top: 3em;
      text-align: center;
      padding: 1em;
      background: #2d6cdf;
      color: white;
      font-size: 0.9em;
    }
    footer a {
      color: #ffe;
      text-decoration: underline;
    }

    /* Modal */
    #modal {
      display: none;
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.5);
      justify-content: center;
      align-items: center;
      z-index: 10;
    }
    #modal .modal-content {
      background: white;
      padding: 2em;
      border-radius: 8px;
      max-width: 400px;
      width: 90%;
      text-align: center;
      box-shadow: 0 0 10px rgba(0,0,0,0.25);
    }
    #modal .modal-content h3 {
      margin-top: 0;
      color: #2d6cdf;
    }
    #modal .modal-content button {
      margin-top: 1.5em;
      padding: 0.5em 1.5em;
      background: #2d6cdf;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    #modal .modal-content button:hover {
      background: #1a47a3;
    }
  </style>
</head>
<body>

<header>Mini KDP - Plataforma de Publicação</header>

<main>
  <h2>Cadastre seu livro</h2>
  <form id="bookForm">
    <input type="hidden" id="bookId" />
    <label for="title">Título do livro:</label>
    <input type="text" id="title" required placeholder="Digite o título" />
    <label for="description">Descrição:</label>
    <textarea id="description" rows="3" required placeholder="Descrição do livro"></textarea>
    <label for="price">Preço (R$):</label>
    <input type="number" id="price" min="0" step="0.01" required placeholder="Ex: 29.90" />
    <label for="image">URL da capa (imagem):</label>
    <input type="url" id="image" required placeholder="Link da imagem da capa" />
    <button type="submit">Salvar Livro</button>
  </form>

  <h2>Livros publicados</h2>
  <div class="books-list" id="booksList">
    <!-- Livros aparecerão aqui -->
  </div>
</main>

<footer>
  Contato: <a href="mailto:arthur.martin@escola.pr.gov.br">arthur.martin@escola.pr.gov.br</a> | Instagram: <a href="https://www.instagram.com/arthur_santos_martin?igsh=bzBsNXQzdnpwMTJr" target="_blank">@arthur_santos_martin</a>
</footer>

<!-- Modal para compra -->
<div id="modal">
  <div class="modal-content">
    <h3>Compra do livro</h3>
    <p id="modalBookTitle"></p>
    <p id="modalBookPrice"></p>
    <p>Compra simulada. Para pagamento real, integração necessária.</p>
    <button onclick="closeModal()">Fechar</button>
  </div>
</div>

<script>
  let books = JSON.parse(localStorage.getItem('books') || '[]');

  const form = document.getElementById('bookForm');
  const booksList = document.getElementById('booksList');
  const modal = document.getElementById('modal');
  const modalBookTitle = document.getElementById('modalBookTitle');
  const modalBookPrice = document.getElementById('modalBookPrice');
  const bookIdInput = document.getElementById('bookId');
  const titleInput = document.getElementById('title');
  const descriptionInput = document.getElementById('description');
  const priceInput = document.getElementById('price');
  const imageInput = document.getElementById('image');

  function saveBooks() {
    localStorage.setItem('books', JSON.stringify(books));
  }

  function renderBooks() {
    booksList.innerHTML = '';
    if (books.length === 0) {
      booksList.innerHTML = '<p>Nenhum livro publicado.</p>';
      return;
    }
    books.forEach(book => {
      const card = document.createElement('div');
      card.className = 'book-card';
      card.innerHTML = `
        <img src="${book.image}" alt="${book.title}" />
        <div class="book-title">${book.title}</div>
        <div class="book-description">${book.description}</div>
        <div class="book-price">R$ ${parseFloat(book.price).toFixed(2)}</div>
        <div class="book-actions">
          <button class="edit-btn" onclick="editBook('${book.id}')">Editar</button>
          <button class="delete-btn" onclick="deleteBook('${book.id}')">Excluir</button>
          <button class="buy-btn" onclick="buyBook('${book.id}')">Comprar</button>
        </div>
      `;
      booksList.appendChild(card);
    });
  }

  function generateId() {
    return '_' + Math.random().toString(36).substr(2, 9);
  }

  form.addEventListener('submit', e => {
    e.preventDefault();
    const id = bookIdInput.value;
    const title = titleInput.value.trim();
    const description = descriptionInput.value.trim();
    const price = priceInput.value;
    const image = imageInput.value.trim();

    if (!title || !description || !price || !image) {
      alert('Por favor, preencha todos os campos.');
      return;
    }

    if (id) {
      // Editar livro existente
      const index = books.findIndex(b => b.id === id);
      if (index !== -1) {
        books[index] = { id, title, description, price, image };
      }
    } else {
      // Adicionar novo livro
      books.push({ id: generateId(), title, description, price, image });
    }

    saveBooks();
    renderBooks();
    form.reset();
    bookIdInput.value = '';
  });

  window.editBook = function(id) {
    const book = books.find(b => b.id === id);
    if (!book) return;
    bookIdInput.value = book.id;
    titleInput.value = book.title;
    descriptionInput.value = book.description;
    priceInput.value = book.price;
    imageInput.value = book.image;
    window.scrollTo({ top: 0, behavior: 'smooth' });
  };

  window.deleteBook = function(id) {
    if (!confirm('Deseja realmente excluir este livro?')) return;
    books = books.filter(b => b.id !== id);
    saveBooks();
    renderBooks();
  };

  window.buyBook = function(id) {
    const book = books.find(b => b.id === id);
    if (!book) return;
    modalBookTitle.textContent = book.title;
    modalBookPrice.textContent = `Preço: R$ ${parseFloat(book.price).toFixed(2)}`;
    modal.style.display = 'flex';
  };

  function closeModal() {
    modal.style.display = 'none';
  }

  modal.addEventListener('click', e => {
    if (e.target === modal) closeModal();
  });

  renderBooks();
</script>

</body>
</html>
