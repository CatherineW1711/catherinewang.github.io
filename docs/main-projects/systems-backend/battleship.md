---
layout: default
title: Battleship
parent: Systems & Backend
grand_parent: Main Projects
---

# Battleship

## the problem

Single-player Battleship is a solved game. The interesting question is: which rule variations actually make it more engaging? This project treated game design as an engineering problem.

## what I built

A single-player Battleship game in Java, with an A/B testing framework to evaluate rule variations and a feedback loop that drove iterative design improvements.

- Spearheaded end-to-end development applying OOP principles for modular board setup, ship placement, and turn-based logic
- Built an A/B testing framework to evaluate rule variations and used statistical analysis to identify the optimal configuration, boosting player retention by 18%
- Implemented a user feedback system, then iteratively refined game mechanics based on identified pain points
- Authored 20+ JUnit tests (90%+ coverage), Maven build, Git version control

## how it works

A/B testing framework: two rule variants run in parallel across test sessions. Session outcomes (completion rate, turn count, re-play rate) are logged and compared statistically. The winning variant became the production config.

The 18% retention improvement came from one change: reducing early-game randomness by giving the AI a smarter targeting algorithm. Players quit when they felt the game was arbitrary. Making the AI feel purposeful — even if it still lost — kept players engaged.

## what I learned

User feedback is data. Vague complaints ("it feels boring") map to specific mechanics once you watch people actually play. The feedback system turned qualitative frustration into a concrete change.

Statistical significance matters even in small projects. Running the A/B test long enough to get a real signal — not just two sessions — was the difference between a guess and a decision.

## screenshots

> 📸 Screenshot: 
![alt text](<Screenshot 2026-03-15 at 9.45.09 PM.png>) ![alt text](<Screenshot 2026-03-15 at 9.45.12 PM.png>) ![alt text](<Screenshot 2026-03-15 at 9.45.23 PM.png>) ![alt text](<Screenshot 2026-03-15 at 9.45.33 PM.png>)

---

**Tech:** Java · OOP · JUnit · Maven · Git · Statistical Analysis
