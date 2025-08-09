# Atzz.com
Loja de livros online 
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Loja de Livros - Arthur Martin</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background: #f4f4f4;
      color: #333;
    }
    header {
      background: #2d6cdf;
      color: white;
      padding: 1em 2em;
      text-align: center;
    }
    header h1 {
      margin: 0;
    }
    main {
      max-width: 900px;
      margin: 2em auto;
      background: white;
      padding: 2em;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .book-list {
      display: flex;
      flex-wrap: wrap;
      gap: 1.5em;
      justify-content: center;
    }
    .book {
      border: 1px solid #ccc;
      border-radius: 6px;
      padding: 1em;
      width: 250px;
      background: #fafafa;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
    .book img {
      max-width: 100%;
      border-radius: 4px;
      margin-bottom: 0.8em;
    }
    .book h3 {
      margin: 0 0 0.5em;
      font-size: 1.2em;
      color: #2d6cdf;
    }
    .book p {
      flex-grow: 1;
      font-size: 0.9em;
      margin-bottom: 1em;
    }
    .price {
      font-weight: bold;
      margin-bottom: 1em;
      color: #009900;
    }
    button.buy-btn {
      background: #2d6cdf;
      color: white;
      border: none;
      padding: 0.6em;
      font-size: 1em;
      border-radius: 4px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    button.buy-btn:hover {
      background: #1a47a3;
    }
    section.contact {
      margin-top: 3em;
      padding-top: 1em;
      border-top: 2px solid #ccc;
      text-align: center;
    }
    section.contact a {
      color: #2d6cdf;
      text-decoration: none;
      font-weight: bold;
    }
    section.contact a:hover {
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

<header>
  <h1>Loja de Livros - Arthur Martin</h1>
</header>

<main>
  <div class="book-list" id="book-list">
    <!-- Livros serão inseridos aqui -->
  </div>

  <section class="contact">
    <h2>Contato</h2>
    <p>Se ocorrer algum problema ou dúvida, entre em contato:</p>
    <p>E-mail: <a href="mailto:arthur.martin@escola.pr.gov.br">arthur.martin@escola.pr.gov.br</a></p>
    <p>Instagram: <a href="https://www.instagram.com/arthur_santos_martin?igsh=bzBsNXQzdnpwMTJr" target="_blank">@arthur_santos_martin</a></p>
  </section>
</main>

<!-- Modal de compra -->
<div id="modal">
  <div class="modal-content">
    <h3>Compra do Livro</h3>
    <p id="modal-book-title"></p>
    <p id="modal-book-price"></p>
    <p>Este é um exemplo de compra. Para finalizar, você deve integrar um sistema de pagamento real.</p>
    <button onclick="closeModal()">Fechar</button>
  </div>
</div>

<script>
  // Aqui você pode personalizar seus livros
  const books = [
    {
      id: 1,
      title: "Meu Primeiro Livro",
      description: "Um livro incrível escrito por Arthur Martin. Conteúdo original e emocionante.",
      price: 29.90,
      image: "https://images.unsplash.com/photo-1524995997946-a1c2e315a42f?auto=format&fit=crop&w=400&q=80"
    },
    {
      id: 2,
      title: "Segredos da Escrita",
      description: "Dicas e técnicas para escrever livros que encantam leitores.",
      price: 39.90,
      image: "https://images.unsplash.com/photo-1512820790803-83ca734da794?auto=format&fit=crop&w=400&q=80"
    },
    {
      id: 3,
      title: "A Jornada do Autor",
      description: "Descubra o caminho para publicar e vender seus livros com sucesso.",
      price: 24.90,
      image: "https://images.unsplash.com/photo-1526947425960-945c6e7287f0?auto=format&fit=crop&w=400&q=80"
    }
  ];

  const bookListEl = document.getElementById("book-list");
  const modal = document.getElementById("modal");
  const modalBookTitle = document.getElementById("modal-book-title");
  const modalBookPrice = document.getElementById("modal-book-price");

  function renderBooks() {
    bookListEl.innerHTML = "";
    books.forEach(book => {
      const bookEl = document.createElement("div");
      bookEl.className = "book";
      bookEl.innerHTML = `
        <img src="${book.image}" alt="${book.title}" />
        <h3>${book.title}</h3>
        <p>${book.description}</p>
        <div class="price">R$ ${book.price.toFixed(2)}</div>
        <button class="buy-btn" onclick="buyBook(${book.id})">Comprar</button>
      `;
      bookListEl.appendChild(bookEl);
    });
  }

  function buyBook(bookId) {
    const book = books.find(b => b.id === bookId);
    if (!book) return;
    modalBookTitle.textContent = book.title;
    modalBookPrice.textContent = `Preço: R$ ${book.price.toFixed(2)}`;
    modal.style.display = "flex";
  }

  function closeModal() {
    modal.style.display = "none";
  }

  // Fechar modal clicando fora do conteúdo
  modal.addEventListener("click", (e) => {
    if (e.target === modal) closeModal();
  });

  renderBooks();
</script>

</body>
</html>
