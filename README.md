# LintKit: Mago Config

Liquid Light base configuration for [Mago](https://mago.carthage.software) - the PHP formatter, linter and analyzer

## Usage

Install the dependency:

```bash
composer require --dev lintkit/mago-config
```

Add the scripts:

```json
"scripts": {
    "mago": "mago --config vendor/lintkit/mago-config/.mago.toml",
    "mago:analyze": "@mago analyze",
    "mago:dry-run": "@mago:fix --check",
    "mago:fix": "@mago fmt",
    "mago:lint": "@mago lint"
},
```

### PHP version

Mago targets PHP 8.4 by default. If the project sets `config.platform.php`, pass that version to Mago instead:

```json
"mago": "MAGO_PHP_VERSION=$(composer config platform.php) mago --config vendor/lintkit/mago-config/.mago.toml",
```

### TYPO3

If using LintKit with TYPO3, you can require `.typo3.mago.toml` instead of `.mago.toml`. This excludes TYPO3-related directories and allows TYPO3 patterns, such as `$GLOBALS['TCA']` and Extbase models with many properties

### Baselines

The linter and analyzer read their baselines from a `.mago/` directory in the project root. If these don't exist, Mago warns and reports every issue.

Generate them with:

```bash
mkdir -p .mago
composer mago:lint -- --generate-baseline
composer mago:analyze -- --generate-baseline
```

Commit the `.mago/` directory.
