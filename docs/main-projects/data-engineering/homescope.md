---
layout: default
title: HomeScope
parent: Data Engineering
grand_parent: Main Projects
---

# HomeScope

## the problem

Buying a home means evaluating schools, demographics, healthcare access, and neighborhood amenities — but that data lives in six different places. Nobody has time to cross-reference Zillow, GreatSchools, the Census Bureau, and Yelp before making a $400K decision.

HomeScope pulls it all into one database and lets you ask real questions: Which ZIP codes have strong schools and below-average home prices? Where does hospital bed capacity not keep up with population?

## what I built

A full-stack web application integrating 2.2M+ real estate listings across six datasets — schools, demographics, restaurants, hospitals, and retail locations — into a unified PostgreSQL schema on AWS RDS.

I owned the Demographics page end-to-end: designed the API endpoints, wrote the SQL queries, and built the React frontend for ZIP-code level population, density, and community indicator exploration.

Beyond my primary page, I contributed equally across the full project lifecycle:

- **Data pipeline:** wrote Python/pandas scripts for ZIP normalization, entity resolution across six datasets, deduplication, and type standardization
- **Database design:** co-designed the relational schema including the ISA supertype/subtype pattern for facilities and 3NF normalization proof
- **Backend:** built RESTful API endpoints with Express, wrote and optimized complex multi-table SQL queries using CTEs and indexes
- **Frontend:** built React components with dynamic filtering, paginated tables, and Leaflet map integration

The platform went through four structured milestones — schema design, data ingestion, query optimization, and full deployment — and I was hands-on at every stage.

## how it works

The data problem nobody talks about: six Kaggle datasets with inconsistent ZIP formats, duplicate facilities identified only by name+coordinates, and 2.2M rows that needed to join cleanly across all tables. Before writing a single API, we built a standardization pipeline that:

- Normalized all ZIPs to 5-digit strings (the join key for everything)
- Deduplicated facilities using composite (lat, long) primary keys
- Removed zero-price listings and invalid house sizes that would skew averages
- Merged public and private school datasets into one table with a type enum

Schema design decision: facilities use a supertype/subtype ISA pattern — a shared facilities table with (latitude, longitude) as composite PK, and subtype tables inheriting via foreign key.

The query that took the most work: the neighborhood scoring query initially ran in 850 seconds. Problem: multiple LEFT JOINs on raw tables producing 100M+ intermediate rows. Fix: pre-aggregate each dataset into CTEs by ZIP before joining. Final runtime: 14.6 seconds — a 98% reduction. Indexes on ZIP columns across all six tables brought most single-table queries from 40+ seconds to under 5 seconds.

## what I learned

Data engineering is 80% making things joinable. The interesting queries were easy once the pipeline was solid. Getting six datasets to agree on what a ZIP code looks like took longer than building the entire frontend.

Query optimization is not guesswork. The 850s → 14s improvement came from understanding why the query was slow — intermediate result size — not from random index-adding. Running EXPLAIN ANALYZE before touching anything made the fix obvious.

Schema decisions have long tails. The ISA facility pattern made cross-facility queries clean, but added complexity when loading data. Worth it, but the tradeoff wasn't obvious upfront.

## screenshots

> 📸 Screenshot: Demographics page — ZIP code search with population, density, state-level comparison table

> 📸 Screenshot: Housing Explorer — multi-filter property search with ZIP-level median comparisons

> 📸 Screenshot: Neighborhood ranking — composite livability score sorted by amenity density vs. home price

> 📸 Screenshot: Facilities map — Leaflet interactive map with color-coded markers

---

Live demo: [cis-5500-final-project-team-23-fall.vercel.app](https://cis-5500-final-project-team-23-fall.vercel.app) *(note: AWS RDS instance is offline post-course)*

**Tech:** PostgreSQL · AWS RDS · Node.js · Express · React · Python/pandas · Vercel · Render
