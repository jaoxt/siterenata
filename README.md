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
            background: linear-gradient(120deg, #690202, #3f1719);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .container {
            max-width: 600px;
            width: 90%;
            background-color: #e6ddbc;
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
            border: 2px solid #8fd3f4;
            border-radius: 8px;
            font-size: 16px;
            outline: none;
        }
        input:focus {
            border-color: #84fab0;
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
            background: #8fd3f4;
            color: white;
        }
        .book-details {
            display: none;
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
            { title: "Triste Fim de Policarpo Quaresma", author: "Lima Barreto", nationality: "br", details: "Uma crítica social sobre o Brasil pós-abolição e seus desafios." },
            { title: "O Cortiço em Cordel", author: "Aluísio de Azevedo", nationality: "br", details: "A obra descreve a vida nos cortiços, com foco em problemas sociais e humanos." },
            { title: "Inovação", author: "Renato Cruz", nationality: "br", details: "Focado em temas contemporâneos, o livro explora o conceito de inovação no Brasil." },
            { title: "A Muralha", author: "Diná Silveira de Queiroz", nationality: "br", details: "Um romance que trata de relações humanas, conflitos e identidade." }
        ];

        function displayBooks(filter = "") {
            const bookList = document.getElementById("books");
            bookList.innerHTML = "";

            books.filter(book => 
                book.title.toLowerCase().includes(filter.toLowerCase()) ||
                book.author.toLowerCase().includes(filter.toLowerCase())
            ).forEach((book) => {
                const li = document.createElement("li");
                li.textContent = `${book.title} – ${book.author}`;
                
                const detailsDiv = document.createElement("div");
                detailsDiv.classList.add("book-details");
                detailsDiv.innerHTML = `<strong>Detalhes:</strong><p>${book.details}</p>`;
                
                li.appendChild(detailsDiv);
                
                // Evento de clique corrigido
                li.addEventListener("click", function () {
                    detailsDiv.style.display = detailsDiv.style.display === "block" ? "none" : "block";
                });

                bookList.appendChild(li);
            });
        }

        document.getElementById("search").addEventListener("input", function() {
            displayBooks(this.value);
        });

        displayBooks();
    </script>
</body>
</html>
