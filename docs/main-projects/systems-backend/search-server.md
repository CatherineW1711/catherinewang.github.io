---
layout: default
title: Multithreaded Search Server
parent: Systems & Backend
grand_parent: Main Projects
---

# Multithreaded Search Server

## the problem

Most search implementations are either trivially simple (linear scan) or require heavy infrastructure (Elasticsearch). This project sits in the middle: a from-scratch search server that handles concurrent requests, ranks results by relevance, and actually performs — no external dependencies.

## what I built

A multithreaded HTTP search server in C++ with a full inverted index and TF-IDF ranking, built from scratch using POSIX primitives.

- Implemented a WordIndex that crawls a directory tree, tokenizes files, and builds an inverted index with term frequencies — reducing index-build time from minutes to under 30 seconds on a 10,000-document corpus
- Developed a pthreads-based ThreadPool and ServerSocket/HttpSocket classes to accept HTTP connections, dispatch each request to a worker thread, and safely handle concurrent client queries
- Parsed HTTP requests and served search queries using TF-IDF ranking over the inverted index, with proper header formatting and error handling
- Automated builds with CMake, achieved 85%+ unit-test coverage with Catch2, and validated memory safety with Valgrind — zero leaks

## how it works

Index build: directory crawler → tokenizer → inverted index (term → doc list with frequencies). Query time: parse HTTP request → look up terms → TF-IDF score each doc → return ranked results as HTTP response.

The ThreadPool design uses a task queue with mutex + condition variable. Worker threads block on an empty queue and wake when a new connection arrives. This avoids thread-per-request overhead and keeps latency stable under load.

Critical section: the inverted index is read-only after build, so no locking needed during query serving — a deliberate design choice that simplified concurrency significantly.

## what I learned

Concurrency bugs are deterministic — they just require the right conditions to trigger. Valgrind and thread sanitizers found issues that testing alone never would have.

Read-only data structures are a superpower in concurrent systems. Designing the index to be immutable after build eliminated an entire class of problems.

## screenshots

> 📸 Screenshot: [add when available]

---

**Tech:** C++ · pthreads · HTTP · TF-IDF · CMake · Catch2 · Valgrind
