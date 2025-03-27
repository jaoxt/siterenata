<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Estante de Livros</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(120deg, #ff7f7f, #ff4f4f);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .container {
            max-width: 600px;
            width: 90%;
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            text-align: center;
        }
        h2 {
            color: #333;
            font-size: 24px;
        }
        input {
            width: 100%;
            padding: 12px;
            margin: 15px 0;
            border: 2px solid #ff4f4f;
            border-radius: 8px;
            font-size: 16px;
            outline: none;
        }
        input:focus {
            border-color: #ff7f7f;
        }
        .book-list {
            list-style: none;
            padding: 0;
        }
        .book-list li {
            padding: 12px;
            border-bottom: 1px solid #ddd;
            font-size: 16px;
            background: #f9f9f9;
            transition: all 0.3s;
            border-radius: 6px;
            margin: 5px 0;
            cursor: pointer;
        }
        .book-list li:hover {
            background: #ff4f4f;
            color: white;
        }
        .book-details {
            display: none;
            color: black;
            background: #f1f1f1;
            padding: 10px;
            border-radius: 6px;
            margin-top: 10px;
            text-align: left;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>📚 Estante de Livros 📖</h2>
        <input type="text" id="search" placeholder="🔍 Pesquisar livros...">
        <ul id="books" class="book-list"></ul>
    </div>

    <script>
        const books = [
            { title: "Cartas Sertanejas Professarias", author: "Júlio Ribeiro", nationality: "br", details: "Este livro narra as experiências e cartas de um professor no sertão." },
            { title: "Triste Fim de Policarpo Quaresma", author: "Lima Barreto", nationality: "br", details: "Uma crítica social sobre o Brasil pós-abolição e seus desafios." }
        ];

        function displayBooks(filter = "") {
            const bookList = document.getElementById("books");
            bookList.innerHTML = "";
            books.filter(book => 
                book.title.toLowerCase().includes(filter.toLowerCase()) ||
                book.author.toLowerCase().includes(filter.toLowerCase())
            ).forEach((book, index) => {
                const li = document.createElement("li");
                li.textContent = `${book.title} – ${book.author}`;
                li.addEventListener("click", () => toggleDetails(index));
                const detailsDiv = document.createElement("div");
                detailsDiv.classList.add("book-details");
                detailsDiv.innerHTML = `<strong>Detalhes:</strong><p>${book.details}</p>`;
                li.appendChild(detailsDiv);
                bookList.appendChild(li);
            });
        }

        function toggleDetails(index) {
            const bookList = document.getElementById("books");
            const bookItems = bookList.getElementsByTagName("li");
            const detailsDiv = bookItems[index].querySelector(".book-details");
            detailsDiv.style.display = detailsDiv.style.display === "block" ? "none" : "block";
        }

        document.getElementById("search").addEventListener("input", function() {
            displayBooks(this.value);
        });

        displayBooks();
    </script>
</body>
</html>
