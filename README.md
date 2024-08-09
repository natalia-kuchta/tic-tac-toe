

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

 ## Tic-Tac-Toe with React and Tailwind CSS

This project is a simple implementation of the classic Tic-Tac-Toe game built using React for the frontend and styled with Tailwind CSS. The game allows two players to take turns marking spaces in a 3x3 grid with "X" or "O". The first player to align three of their marks horizontally, vertically, or diagonally wins the game.

## Features

```
Interactive Gameplay: Players can click on the squares to place their "X" or "O" marks.

Winner Detection: The game detects and announces the winner when three marks are aligned.

Dynamic Status Updates: The UI updates to show the next player or the winner of the game.

Responsive Design: Styled with Tailwind CSS to ensure the game looks great on various devices.
```


## Square Component

The Square component represents an individual square on the Tic-Tac-Toe board. It accepts value and onSquareClick as props and renders a button that displays the current value ("X", "O", or null) and triggers the onSquareClick function when clicked.

```javascript
function Square({value, onSquareClick}) {
    return (
        <button className="square" onClick={onSquareClick}>
         {value}
        </button>
    );
}
```
## Board Component
The Board component manages the state of the game, including which player's turn it is and the state of each square. It passes down the necessary props to the Square components and handles the logic for determining the winner.

```javascript
export default function Board() {
    const [xIsNext, setXIsNext] = useState(true);
    const [squares, setSquares] = useState(Array(9).fill(null));

    function handleClick(i) {
        if (calculateWinner(squares) || squares[i]) {
            return;
        }
        const nextSquares = squares.slice();

        if (xIsNext) {
            nextSquares[i] = "X";
        } else {
            nextSquares[i] = "O";
        }

        setSquares(nextSquares);
        setXIsNext(!xIsNext);
    }

    const winner = calculateWinner(squares);
    let status;
    if (winner) {
        status = 'Winner: ' + winner;
    } else {
        status = 'Next player: ' + (xIsNext ? 'X' : 'O');
    }

    return (
        <>
            <div className="status h-24 bg-gradient-to-r from-pink-400 via-violet-500 to-yellow-500 pt-8">

                <RainbowText value={status}/>

            </div>
            <main className="flex items-center flex-col bg-clip-border p-4 border-4 border-dashed border-purple-800 bg-purple-500">
            <div className="board-row ">
                <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
                <Square value={squares[1]} onSquareClick={() => handleClick(1)}/>
                <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
            </div>
            <div className="board-row">
                <Square value={squares[3]} onSquareClick={() => handleClick(3)}/>
                <Square value={squares[4]} onSquareClick={() => handleClick(4)}/>
                <Square value={squares[5]} onSquareClick={() => handleClick(5)}/>
            </div>
            <div className="board-row">
                <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
                <Square value={squares[7]} onSquareClick={() => handleClick(7)}/>
                <Square value={squares[8]} onSquareClick={() => handleClick(8)}/>
            </div>
            </main>
        </>
    );
}
```

 ## Winner Calculation

The calculateWinner function checks the board's current state to determine if there is a winner. It returns 'X', 'O', or null based on the current configuration of the board.

```javascript
function calculateWinner(squares) {
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
    ];
    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
            return squares[a];
        }
    }
    return null;
}
```

 ## Screenshot

![screenshot.png](public%2Fscreenshot.png)