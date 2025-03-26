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
            background: linear-gradient(120deg, #84fab0, #8fd3f4);
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
            { title: "A Muralha", author: "Diná Silveira de Queiroz", nationality: "br", details: "Um romance que trata de relações humanas, conflitos e identidade." },
            { title: "O Seminarista", author: "Bernardo Guimarães", nationality: "br", details: "A história de um seminarista que se perde em dilemas de fé e amor." },
            { title: "Divã", author: "Martha Medeiros", nationality: "br", details: "Uma obra que mistura ficção e reflexão sobre a vida moderna e as relações." },
            { title: "Cantar Histórias", author: "José Alércio Zamoner", nationality: "br", details: "Uma obra que resgata a tradição oral e as histórias contadas ao longo do tempo." },
            { title: "Madrugada sem Deus", author: "Mário Donato", nationality: "br", details: "Relatos de uma vida marcada pela solidão e pela busca por sentido." },
            { title: "Cabo de Guerra", author: "Ivone Benedetti", nationality: "br", details: "Uma análise das relações humanas em tempos de tensão e conflito." },
            { title: "Um Olhar que Transforma", author: "Januário Cristina Alves", nationality: "br", details: "O livro propõe reflexões sobre o mundo do trabalho e suas diversas faces." },
            { title: "Memórias Inventadas", author: "Manoel de Barros", nationality: "br", details: "Uma narrativa sobre infância e a memória inventada do autor." },
            { title: "Fogo Morto", author: "José Lins do Rego", nationality: "br", details: "Romance que descreve o interior nordestino e seus conflitos." },
            { title: "A Droga da Obediência", author: "Pedro Bandeira", nationality: "br", details: "Uma obra infantojuvenil que mistura ação e reflexão sobre a obediência." },
            { title: "Monteiro Lobato: O Editor do Brasil", author: "Cassiano Nunes", nationality: "br", details: "Uma biografia de Monteiro Lobato e seu impacto no Brasil." },
            { title: "O Cabeleira", author: "Franklin Távora", nationality: "br", details: "Um romance que aborda a vida no sertão e a luta contra as injustiças." },
            { title: "O Outro Apaixonado por Marília de Dirceu", author: "Jair Vitória", nationality: "br", details: "A obra descreve um amor impossível entre os personagens." },
            { title: "Armadilha", author: "João Targino", nationality: "br", details: "Uma narrativa que mistura mistério e drama." },
            { title: "O Zahir", author: "Paulo Coelho", nationality: "br", details: "Explora o conceito do 'Zahir', algo que não pode ser ignorado na vida." },
            { title: "Espumas Flutuantes", author: "Castro Alves", nationality: "br", details: "Poemas que exploram a liberdade e os direitos humanos." },
            { title: "A Perfeição", author: "Eça de Queiroz", nationality: "pt", details: "Uma crítica social que aborda a busca pela perfeição na sociedade." },
            { title: "Gaivota / Tio Vânia", author: "Anton Tchekhov", nationality: "ru", details: "Duas peças que tratam do dilema existencial e da busca por significado." },
            { title: "Viagens na Minha Terra", author: "Almeida Garrett", nationality: "pt", details: "Uma mistura de romance e crônica sobre as viagens e a cultura portuguesa." },
            { title: "O Velho da Horta / Auto da Barca do Inferno / A Farsa de Inês Pereira", author: "Gil Vicente", nationality: "pt", details: "Três peças que representam a crítica social e o teatro português." }
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
