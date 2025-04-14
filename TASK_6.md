---
title: "[]{#_ifj4vw4fthim .anchor}**[PROJECT 4:MECHANICAL
  TURK]{.underline}**"
---

# **[TASK A]{.underline}**

Proposed Mechanism : Use of Pressure Sensitive Conductive Switches

Working : Each square contains a conductive foam that completes the
circuit only after a piece is pressed against it. When a piece is
lifted, it breaks the circuit sending a signal to the Arduino circuit
board. This avoids the use of any electronic components inside the chess
pieces.

Alternative : The use of capacitive touch sensors can increase
sensitivity. It works on the principle of varying capacitance of the
circuit based on the position of a chess piece.

Diagram :

+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+

\| Chess Piece \|

+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+

\| Square Tile \|

+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+

\| Conductive Foam \|

+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+

\| Bottom Contact \|

+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+

\| Base Circuitry \|

# **[TASK B]{.underline}**

To solve the given problem, the most efficient way is to consider an 8x8
grid, and to use an Arduino pin for each row and column individually. In
this way, we have used a total of 16 I/O pins. As each square is located
at the intersection of a row and a column, and a piece is located at a
square if it is located in that particular row and column both. If we
decide to use a multiplexer, we realise that we only need 10 pins. This
is because we are using 2 multiplexers, one for rows and one for
columns. As each multiplexer has 4 pins and one signal pin, we get a
total of 5 pins for each multiplexer. The C# code has been written for
reference.

const int ROWS = 8;

const int COLS = 8;

const int rowPins\[ROWS\] = {2, 3, 4, 5, 6, 7, 8, 9};

const int colPins\[COLS\] = {10, 11, 12, 13, A0, A1, A2, A3};

void setup()

{

Serial.begin(9600);

for (int i = 0; i \< ROWS; i++)

{

pinMode(rowPins\[i\], OUTPUT);

digitalWrite(rowPins\[i\], HIGH);

}

for (int i = 0; i \< COLS; i++)

{

pinMode(colPins\[i\], INPUT_PULLUP);

}

}

void loop()

{

for (int row = 0; row \< ROWS; row++)

{

digitalWrite(rowPins\[row\], LOW);

for (int col = 0; col \< COLS; col++)

> {

int state = digitalRead(colPins\[col\]);

if (state == LOW)

> {

Serial.print(\"Square activated at: \");

Serial.print(\"Row \");

Serial.print(row);

Serial.print(\", Col \");

Serial.println(col);

delay(100);

> }

}

digitalWrite(rowPins\[row\], HIGH);

}

}
