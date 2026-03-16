---
layout: default
title: Movie Guessing Game
parent: Systems & Backend
grand_parent: Main Projects
---

# Movie Guessing Game

## The problem

A turn-based multiplayer movie guessing game with a specific constraint:
three gameplay commands (skip, escape, block) all needed to modify game
state, but the core engine couldn't know what each command did internally.
The design had to be extensible without touching the engine every time
a new action was added.

## What I built

A Java game where 2 players compete to identify movies from progressive
hints, built on MVC architecture with the Command pattern handling all
gameplay actions.

- Model manages game data and state, View handles the game UI popup,
  Controller owns core game logic and mediates between them
- Encapsulated each gameplay action (skip, escape, block) as a Command
  object that modifies game state independently from the engine
- Built progressive hint system fetching year, genre, and actor from
  an integrated movie database, revealed in order of specificity
- Implemented win condition detection across multiple game modes
  including a 5/5 Comedy Films challenge
- 95%+ JUnit test coverage, Maven build pipeline, Git collaboration

## How it works

The Command pattern was the right call because all three actions needed
to change game state in different ways — block affects the opponent,
skip costs a turn, escape ends the round. Without encapsulation, the
engine becomes a mess of conditionals. With it, adding power-ups later
meant writing one new class, not touching anything that already worked.

MVC separation meant the game UI popup (our first time building anything
with a popup window) could be developed and debugged independently from
the game logic. That separation saved us when getting the popup to render
correctly turned into the hardest part of the project.

The trickiest challenge: loading movie data from CSV using a library
that parsed strings differently than expected, and writing split
functions to extract tokens reliably across inconsistent formats.

## What I learned

Two design patterns in one project sounds like over-engineering until
you actually need both. MVC kept the UI work from bleeding into game
logic. Command kept the engine clean as actions multiplied.

The popup was our first time doing anything UI-related in Java — getting that working taught more about Java I/O and rendering than
any of the game logic did.

## Screenshots

> 📸 Screenshot: 
![alt text](<Screenshot 2026-03-15 at 9.48.16 PM.png>) 
![alt text](<Screenshot 2026-03-15 at 9.48.41 PM.png>)
![alt text](<Screenshot 2026-03-15 at 10.01.26 PM.png>)
---

**Tech:** Java · OOP · Command Pattern · JUnit · Maven · Git
