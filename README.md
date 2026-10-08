# Multithreaded Card Game

A concurrent card-game simulation in Java. Each player runs on its own thread. Players
draw from the deck on their left and discard to the deck on their right until one of
them holds four cards of the same value.

> Built for the **ECM2414** software development module at the University of Exeter
> (pair coursework, 2024).

## How it works

- `n` players and `n` decks sit in a ring. The pack holds `8n` cards.
- Each `Player` is a `Thread`. Each turn it draws a card, discards one it doesn't want,
  and checks whether it has won.
- `CardDeck` methods are `synchronized`, so two threads never change a deck at once.
  A `volatile` flag tells every player thread to stop as soon as someone wins.
- Every move is logged to `PlayerN_output.txt`. Each deck's final contents go to
  `DeckN_output.txt`.
- JUnit 5 tests cover every class (`src/test/java/cards`).

## Running

Compile and run with any JDK 17+:

```bash
javac -d out src/main/java/cards/*.java
java -cp out cards.CardGame
```

When prompted, enter the number of players and a pack file, for example `4` and
`src/main/resources/4players.txt`. The winner prints to the console and the log files are
written to the working directory.

You can also build a runnable jar with Maven: `mvn package`, then `java -jar target/cards-1.0.jar`.

## Tests

```bash
mvn test
```

## Team

Pair project by [Edward Pratt](https://github.com/Edward-Pratt) and
[CliffHanger201](https://github.com/CliffHanger201).
Edward wrote most of the game loop (`CardGame`) and the threaded `Player`.
CliffHanger201 wrote most of `CardDeck`, `FileEditor` and the test suite.
The design report is in [`res/`](res/).
