---
layout: default
title: Movie Guessing Game
parent: Work
nav_order: 5
---

# Movie Guessing Game

## the problem

A command-line game project with a real engineering constraint: gameplay actions (guess, skip, block, escape) needed to be extensible without rewriting the core engine. Classic OOP design problem.

## what I built

A turn-based movie guessing game in Java with a clean architecture that separates concerns between game engine, actions, and I/O.

- Applied the Command pattern to encapsulate each gameplay action as an object — adding a new action means writing one class, not touching the engine
- Implemented a central game engine managing state transitions, win/loss rules, power-up effects, and progressive hint fetching (year → genre → actor) from an integrated movie database
- Built a console interface using Java I/O streams with sub-200ms response time and robust error recovery
- Established full test coverage with JUnit (95%+) and Maven build pipeline

## how it works

The Command pattern: each action implements a common interface with an `execute()` method. The game engine holds a queue of commands and processes them without knowing what they do internally. This made testing trivial — each command is independently testable, and the engine can be tested with mock commands.

Progressive hint system: hints reveal in order of specificity (year first, then genre, then actor). Each hint is fetched lazily from the movie database only when requested, keeping early-game tension intact.

## what I learned

Design patterns solve real problems, not hypothetical ones. The Command pattern felt like overhead until we needed to add power-ups — at that point, the architecture paid for itself in under an hour.

95% test coverage isn't about the number. It's about the confidence to refactor without fear.

## screenshots

> 📸 Screenshot: [add when available]

---

**Tech:** Java · OOP · Command Pattern · JUnit · Maven · Git
