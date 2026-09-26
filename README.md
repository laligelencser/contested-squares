# Contested Squares

Chess with the pressure made visible. Every square on the board is tinted by how many pieces attack it: blue for yours, red for the bot's. The deeper the tint, the more attackers. You play against a built-in chess bot with eight difficulty levels.

It is a single HTML file with no build step and no dependencies beyond Google Fonts. Open `index.html` in a browser to play.

## The overlay

- **Both** (default): a square reached by only one side is tinted in that side's colour. A square both sides attack is split corner to corner, with your half in the bottom-left and the bot's in the top-right.
- **Yours / Bot's**: show one side only.
- **Balance**: your attackers minus the bot's. Evenly contested squares are striped.
- **Off**: a plain board.

Small badges in the corners show the exact counts. A square holding a piece counts attackers of that square, so the same number tells you how well a piece is defended or how hard it is being hit. Point at or tap any square to see which pieces attack it. An optional setting also counts batteries, such as a rook lined up behind another rook, or a queen behind a bishop.

## The bot

| Level | Name | How it plays |
|---|---|---|
| 1 | Patzer | 1 ply, no capture search, large random error |
| 2 | Novice | 1 ply plus captures, large random error |
| 3 | Casual | 2 plies, moderate random error |
| 4 | Club player | 3 plies, light random error, opening book |
| 5 | Strong club | 4 plies, slight random error, opening book |
| 6 | Expert | about 1 s per move |
| 7 | Tactician | up to 2.5 s per move |
| 8 | Full strength | up to 5 s per move |

The engine is written from scratch in JavaScript and runs in a Web Worker, so the page stays responsive while it thinks. It uses a 0x88 board, alpha-beta search with principal variation search, a transposition table, null-move pruning, late move reductions, killer and history move ordering, and quiescence search. Its evaluation combines material, piece-square tables tapered between middlegame and endgame, pawn structure (passed, doubled and isolated pawns), the bishop pair, rooks on open files, and a mop-up term for converting won endgames. Move generation is verified against the standard perft counts.

## Other features

- Play as white, black or a random colour
- Drag and drop or click to move, with legal-move hints and a promotion picker
- Keyboard play: arrow keys move between squares, Enter picks up or places a piece
- Take back, flip board, and a scoresheet in standard algebraic notation
- Detects checkmate, stalemate, threefold repetition, the 50-move rule and insufficient material
- Remembers your game and settings in the browser between visits
- Light and dark themes that follow your system setting
