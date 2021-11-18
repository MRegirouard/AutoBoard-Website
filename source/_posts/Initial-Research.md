---
title: Initial Research
date: 2021-11-15 10:17:10
tags:
- Documentation
- Research
---
# Initial Research
We started the AutoBoard project off by outlining goals and basic design ideas and then began research to see if similar projects had been done before. We found that this was the case, and that several automated chess boards had already been developed.

## Square Off
<img src="https://www.chess-site.com/wp-content/uploads/SquareOff2.jpg">

### Overview
[Square Off](https://squareoffnow.com/) is a chess board very similar to the one we are designing. It was made by a company, and its product is available for $499. The board uses a Bluetooth connection to a smartphone to control the board and start games. You can play against an onboard AI or other players around the world using Square Off Boards.

### Technical Details
The board is operated by pressing down pieces hard to register a start and end position. We are unsure exactly how this works. Pieces are moved using a CoreXY system, as we plan to do.

## Phantom Chess
<img src="https://images.squarespace-cdn.com/content/v1/60ae7dcca134e70b479ddf12/1622313783664-ZBZHSWI3L5K51Q3WMSG0/centered%2Bcover%2Bimage.jpg">

### Overview
The [Phantom Chess Board](https://www.phantomchessboard.com/0) is a Kickstarter project, which gives a much more detailed explanation of its production [in these build logs](https://hackaday.io/project/179268-automatic-chessboard). The Phantom board is even closer to our end goal than Square Off, and can be obtained by pledging $399 or more towards the Kickstarter. The project has raised over 1.9 million dollars, with over 3,000 backers. This truly inspired us to push to finish our own project. The board also connects to a smartphone.

### Technical Details
The Phantom board uses an array of five hundred hall effect sensors, to detect the movement of pieces. It uses a Scara mechanism for moving the pieces, consisting of a "double pendulum" rotating arm. The movement mechanism consists of a magnet on a servo motor, as opposed to our approach of an electromagnet.

## Autopatzer
<img src="https://i.ytimg.com/vi/8ScFtkWvHW8/mqdefault.jpg">

### Overview
Another chess project we have come across is the [Autopatzer](https://incoherency.co.uk/blog/stories/autopatzer.html). This project seems to be in earlier stages of development compared to Square Off and the Phantom Board. A notable difference is the use of a touchscreen as opposed to a smartphone.

### Technical Details
The board uses hall effect sensors, and features a CoreXY motion system with an electromagnet. The Autopatzer uses a Raspberry Pi and Arduino Teensy for motion control and Lichess connectivity, and a touchscreen for user input.

## Overall Findings
Our research shows that constructing a working automatic chess board is an entirely attainable goal. We noted the use of hall effect sensors, magnets, and the CoreXY motion system, which we are planning to use. We also noticed that projects with pieces containing magnets used a metal ring to protect against magnetic fields interfering with neighboring pieces. It was encouraging to see our design ideas reflected in already-made, working chess boards.
