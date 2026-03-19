---
name: solvebeam-wordpress-plugin-governance
description: >-
  A strict governance skill for auditing, upgrading, refactoring, and
  scaffolding WordPress plugins according to the official SolveBeam Plugin
  Development Guidelines.
license: GPL-2.0-or-later
metadata:
  author: solvebeam
  version: "1.1"
---

# Skill: solvebeam-wordpress-plugin-governance

A strict, opinionated governance skill for WordPress plugins following SolveBeam standards.

## Canonical Boilerplate

The `assets/solvebeam-boilerplate/` directory is the **canonical reference implementation**. It contains a fully compliant plugin that demonstrates all required conventions, file structure, tooling configuration, and code patterns. Always use it as the authoritative source when auditing, scaffolding, or refactoring plugins.

## Core Principles

* **PHP 8.2+** — every PHP file starts with `declare(strict_types=1);`
* **Flat PSR-4** — autoload into `psr-4/`, no sub-namespaces (see rationale below)
* **Minimal visibility** — classes `final`, properties `private readonly`, methods `private` unless they must be public
* **First-class callable hooks** — always `$this->method(...)`, never `[ $this, 'method' ]`
* **Singleton Plugin.php** — `final` class, private constructor, `public static function instance()`
* **Clean distribution** — `.distignore` excludes dev artifacts from builds
* **Tooling-first** — `phpcs.xml.dist`, `rector.php`, and Composer scripts for linting, analysis, and building
* **WordPress dev environment** — `.wp-env.json` + `@wordpress/env` and `@wordpress/scripts`
* **Documentation** — `README.md`, `CHANGELOG.md` (Keep a Changelog format), `readme.txt`
* **No noise** — no redundant comments, no obvious documentation

## Why `psr-4/` Instead of `src/`?

WordPress plugins contain PHP, JavaScript, CSS, and other assets. Using `src/` for only PHP creates ambiguity. The `psr-4/` directory makes the PSR-4 autoload root explicit and prevents mixing PHP and non-PHP sources.

## Modes

### audit

Outputs a structured compliance report comparing the target plugin against the boilerplate. Reports blocking issues, modernization opportunities, tooling gaps, distribution hygiene gaps, architecture violations, visibility violations, and hook syntax violations. No code changes.

### config

Safe, non-breaking modernization: adds missing tooling config, `declare(strict_types=1)`, dist hygiene files, documentation files, normalizes visibility, and converts hooks to first-class callable syntax. No major file moves.

### refactor

Includes everything in **config**, plus: flattens namespaces, moves code into `psr-4/`, extracts procedural code, enforces singleton pattern, reduces public surface, adds `readonly` properties, finalizes classes, and rewrites hook architecture. May introduce breaking changes.

### scaffold

Generates a new, fully compliant plugin by copying and adapting the boilerplate from `assets/solvebeam-boilerplate/`. Replaces names, namespaces, slugs, and text domains to match the new plugin.
