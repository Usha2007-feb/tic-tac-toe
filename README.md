# tic-tac-toe

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
            flex-direction: column;
        }
        h1 {
            margin-bottom: 20px;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
        }
        .cell {
            width: 100px;
            height: 100px;
            background: white;
            border: 2px solid black;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2em;
            cursor: pointer;
        }
        .cell.taken {
            pointer-events: none;
        }
        #status {
            margin-top: 20px;
            font-size: 1.2em;
        }
    </style>
</head>
<body>
    <h1>Tic-Tac-Toe</h1>
    <div class="board" id="board"></div>
    <div id="status">Player X's turn</div>
    <script>
        const board = document.getElementById("board");
        const status = document.getElementById("status");
        let currentPlayer = "X";
        let cells = Array(9).fill(null);
        
        function checkWinner() {
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8],
                [0, 3, 6], [1, 4, 7], [2, 5, 8],
                [0, 4, 8], [2, 4, 6]
            ];
            for (const pattern of winPatterns) {
                const [a, b, c] = pattern;
                if (cells[a] && cells[a] === cells[b] && cells[a] === cells[c]) {
                    status.innerText = `Player ${cells[a]} wins!`;
                    document.querySelectorAll(".cell").forEach(cell => cell.classList.add("taken"));
                    return true;
                }
            }
            if (!cells.includes(null)) {
                status.innerText = "It's a draw!";
                return true;
            }
            return false;
        }
        
        function handleClick(index) {
            if (!cells[index]) {
                cells[index] = currentPlayer;
                document.getElementById(`cell-${index}`).innerText = currentPlayer;
                document.getElementById(`cell-${index}`).classList.add("taken");
                if (!checkWinner()) {
                    currentPlayer = currentPlayer === "X" ? "O" : "X";
                    status.innerText = `Player ${currentPlayer}'s turn`;
                }
            }
        }
        
        function createBoard() {
            for (let i = 0; i < 9; i++) {
                const cell = document.createElement("div");
                cell.classList.add("cell");
                cell.id = `cell-${i}`;
                cell.addEventListener("click", () => handleClick(i));
                board.appendChild(cell);
            }
        }
        
        createBoard();
    </script>
</body>
</html>

