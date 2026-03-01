---
name: solvebeam-wordpress-plugin-governance
description: A strict governance skill for auditing, upgrading, refactoring, and scaffolding WordPress plugins according to the official SolveBeam Plugin Development Guidelines.
license: GPL-2.0-or-later
metadata:
  author: solvebeam
  version: "1.0"
---

# 🧠 Skill: solvebeam-wordpress-plugin-governance

## Description

A strict governance AI agent for auditing, upgrading, refactoring, and scaffolding WordPress plugins according to the official SolveBeam Plugin Development Guidelines.

This skill enforces:

* PHP 8.2+
* Modern PHP architecture
* Strict typing
* Minimal visibility surface
* Deterministic plugin structure
* Clean build artifacts
* Tooling-first workflow
* WordPress best practices
* Clean distribution archives

It is intentionally opinionated and strict.

---

# 🔐 Global Enforcement Rules (Always Applied)


## 1️⃣ PHP Version

* Minimum PHP: **8.2**
* Always support the latest major PHP release
* Use modern language features

---

## Composer.json

Required structure:

```json
{
  "config": {
    "platform": {
      "php": "8.2"
    },
    "platform-check": false,
    "sort-packages": true,
    "wp-slug": "plugin-slug"
  },
  "require": {
    "php": "^8.2"
  },
  "require-dev": {
    "phpstan/phpstan": "*",
    "rector/rector": "*",
    "szepeviktor/phpstan-wordpress": "*",
    "vimeo/psalm": "*",
    "wp-cli/wp-cli": "*",
    "wp-coding-standards/wpcs": "*"
  },
  "autoload": {
    "psr-4": {
      "SolveBeam\\PluginNamespace\\": "psr-4/"
    }
  },
  "scripts": {
    "build": ["@phpcs", "@phpstan"],
    "lint": "@phpcs",
    "analyse": "@phpstan",
    "psalm": "psalm"
  }
}
```

---

## 2️⃣ PHP File Requirements

Every PHP file:

```php
<?php
declare(strict_types=1);
```

No exceptions.

---

## 3️⃣ Namespace Architecture

Always:

```php
namespace SolveBeam\SpecificPluginNamespace;
```

Rules:

* No sub-namespaces
* No deep structure
* Flat architecture
* PSR-4 → `psr-4/`

---

## 4️⃣ Autoload

PSR-4 → `psr-4/` (see composer.json example above)

# 🧱 Architecture Rules

---

## 5️⃣ Plugin.php Requirements

`psr-4/Plugin.php` must:

* Be `final`
* Implement Singleton pattern
* Have private constructor
* Have `public static function instance(): self`
* Register hooks internally
* Use first-class callable syntax

Example structure:

```php
final class Plugin {

    private static ?self $instance = null;

    private function __construct() {
        $this->register_hooks();
    }

    public static function instance(): self {
        return self::$instance ??= new self();
    }

    private function register_hooks(): void {
        add_action( 'init', $this->init(...) );
    }

    private function init(): void {
    }
}
```

---

## 6️⃣ Visibility Rules

* Classes → `final` wherever possible
* Properties → `private readonly` wherever possible
* Methods → `private` wherever possible
* Only expose what must be public

---

## 7️⃣ Hooks

Always use first-class callable syntax:

```php
add_action( 'init', $this->init( ... ) );
```

Never:

```php
[ $this, 'init' ]
```

---

## 8️⃣ Comments

* No redundant comments
* No obvious comments
* Only meaningful documentation

---

# 📦 Distribution Cleanliness (Mandatory)

---

## 9️⃣ .distignore

Must always include a `.distignore` file to exclude development artifacts from WordPress plugin builds.

Typical contents:

```
.git
.gitignore
.github
node_modules
vendor/bin
tests
phpstan.neon
phpcs.xml.dist
psalm.xml.dist
rector.php
.editorconfig
package.json
package-lock.json
composer.lock
```

---

## 🔟 .gitattributes

Must include `.gitattributes` to ensure clean GitHub ZIP exports.

Must use `export-ignore` for dev-only files.

Example:

```
/.github export-ignore
/tests export-ignore
/node_modules export-ignore
/phpstan.neon export-ignore
/phpcs.xml.dist export-ignore
/psalm.xml.dist export-ignore
/rector.php export-ignore
/.editorconfig export-ignore
/.wp-env.json export-ignore
/package.json export-ignore
/package-lock.json export-ignore
/composer.lock export-ignore
```

Goal:

Clean GitHub-generated zip archives.

---

# 🛠 Tooling Requirements

---

## 1️⃣1️⃣ Required Tool Config Files

Must generate:

* `phpcs.xml.dist`
* `phpstan.neon`
* `psalm.xml.dist`
* `rector.php`

All configured for WordPress plugin context.

---

# 🖥 Local Development (Mandatory)

---

## 1️⃣4️⃣ wp-env

Must include:

* `.wp-env.json`
* `package.json`
* Scripts:

  * `env:start`
  * `env:stop`
  * `env:clean`

---

## 1️⃣5️⃣ wp-scripts

Must use:

* `@wordpress/scripts`

package.json must include:

```json
"scripts": {
  "build": "wp-scripts build",
  "start": "wp-scripts start"
}
```

No custom webpack unless necessary.

---

# 📄 Documentation Requirements

---

## 1️⃣6️⃣ README.md (Mandatory)

Must include:

* Plugin description
* Installation instructions
* Development instructions
* wp-env usage
* Build instructions
* PHP version requirement
* License section

---

## 1️⃣7️⃣ CHANGELOG.md (Mandatory)

Must follow:

Keep a Changelog format

Structure:

```
# Changelog

All notable changes to this project will be documented in this file.

The format is based on Keep a Changelog.
```

Sections:

* Added
* Changed
* Deprecated
* Removed
* Fixed
* Security

---

# 🧑‍💻 .editorconfig (WordPress Oriented)

Must include a WordPress-aligned `.editorconfig`.

Example:

```
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
indent_style = tab
indent_size = 4
trim_trailing_whitespace = true

[*.md]
trim_trailing_whitespace = false
```

Tabs, not spaces (WordPress standard).

---

# 🎯 Modes

---

## 🧪 audit

Outputs structured compliance report:

* Blocking issues
* Modernization opportunities
* Tooling gaps
* Distribution hygiene gaps
* Architecture violations
* Visibility violations
* Hook syntax violations

No code changes.

---

## ⚙️ config

Safe modernization only:

* Add missing tooling
* Add PHP 8.2 requirement
* Add strict types
* Add Psalm
* Add Rector
* Add dist hygiene files
* Add README
* Add CHANGELOG
* Add wp-env
* Add wp-scripts
* Normalize visibility
* Convert hooks to first-class callable syntax

No major file moves.

---

## 🔨 refactor

Includes config plus:

* Flatten namespaces
* Move code into psr-4/  
  _Note for AI-agents: Use the `psr-4/` directory for all PSR-4 autoloaded PHP files instead of `src/`. This avoids confusion with non-PHP sources and aligns with the rationale described in the section "Why `psr-4/` Instead of `src/`?"._
* Extract procedural code
* Enforce singleton pattern
* Reduce public surface
* Add readonly properties
* Finalize classes
* Rewrite hook architecture

May introduce breaking changes.

---

## 🏗 scaffold

Generates fully compliant plugin:

* PHP 8.2+
* Singleton Plugin.php
* Strict typing
* Minimal visibility
* Tooling stack
* Clean distribution files
* Documentation
* wp-env
* wp-scripts
* Deterministic structure

---


# 📁 Why `psr-4/` Instead of `src/`?

**Rationale:**

In WordPress plugins, the `src/` directory is often misleading because plugins typically contain not only PHP source files, but also JavaScript, CSS, and other assets. Using `src/` for only PHP code can create confusion about where non-PHP source files belong. To avoid this ambiguity and to make the PSR-4 autoloaded directory explicit, this standard uses `psr-4/` for all PSR-4 loaded PHP files. This makes the plugin structure clearer and prevents accidental mixing of PHP and non-PHP sources.

# 📁 Canonical Directory Structure

```
plugin-slug/
│
├── plugin-slug.php
├── composer.json
├── package.json
├── .wp-env.json
├── .editorconfig
├── .distignore
├── .gitattributes
├── README.md
├── CHANGELOG.md
├── phpcs.xml.dist
├── phpstan.neon
├── psalm.xml.dist
├── rector.php
├── psr-4/
│   └── Plugin.php
├── assets/
│   ├── js/
│   └── css/
└── vendor/
```
