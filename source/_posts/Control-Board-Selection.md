---
title: Control Board Selection
date: 2021-11-18 09:29:24
tags:
- Controller
- Research
---
# Control Board Selection
To control motors and read sensors, we needed a microcontroller or single-board computer in the AutoBoard. Our initial requirements were that the board had to have some amount of input/output pins, and it had to have WiFi. We had many options available, so we decided to stick with something we've already worked with before. We immediately narrowed down our search to three options: an Arduino, a Raspberry Pi, or a TI Connected Launchpad.

## Arduino
There are many Arduino boards available, and many with networking. The [Arduino Nano IOT 33](https://store-usa.arduino.cc/products/arduino-nano-33-iot) quickly got our attention, as a board that was pretty small, has just enough analog input for if we used hall effect sensors, and has some digital output for driving motors. The Nano IOT 33 also has WiFi, which we needed. The process on the Arduino is slow compared to the Raspberry Pi, but we decided to have a very low-level onboard chess engine, and use Lichess's bot for more challenging AI matches.

## Raspberry Pi
There are a few Raspberry Pi boards, but we decided to consider the [Raspberry Pi Zero W](https://www.raspberrypi.com/products/raspberry-pi-zero-w/), because it is the smallest of the boards and still has WiFi and the same GPIO pins. However, we had mixed feelings about the full onboard operating system. We really didn't need a full OS, but it would allow for more rapid prototyping by being able to run commands directly over an SSH connection. The larger process on the Pi also would allow for a better onboard chess engine, as we could likely run Stockfish, something that would be impossible on a microcontroller as opposed to the single-board computer. However, because of the use of a full OS, we would have to figure out how to protect the SD card from corruption if the board was unplugged without going through the shutdown process. This was a massive drawback. We also didn't need the bulk of a full OS, and managing this could waste time.

## TI Connected Launchpad 
We also had a Connected Launchpad board, a lesser-known microcontroller made by Texas Instruments. The version we had featured plenty of GPIO, an ethernet port, and optional WiFi add-on modules. We didn't have nearly as much experience with the Launchpad and decided that the board we already had was far too big, but didn't want to have to learn how to use a smaller board.

## Selection: Arduino Nano IOT 33
Our final decision was to use the Arduino Nano IOT 33. We liked this board's small footprint and the fact that it had the exact amount of analog inputs we needed. We had quickly eliminated the Connected Launchpad, due to a lack of experience with the boards. The Raspberry Pi was a much stronger contender, but we decided that the drawbacks of having a full operating system available outweighed the benefits. The AutoBoard is meant to be relatively volatile, meaning users should be able to plug in and out the AutoBoard often. We didn't want a shutdown process to hinder this, and although there are options to make the onboard SD card read-only, this was something we didn't want to deal with and risk losing work due to mistakes or corruption. The main drawback to the Arduino was its slow processor, but Lichess' API should be able to let us play games against bots, and not have to worry so much about a strong onboard AI opponent.
