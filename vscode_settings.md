{
    "files.autoSave": "onFocusChange",
    "files.watcherExclude": {
        "**/.git/objects/**": true,
        "**/.git/subtree-cache/**": true,
        "**/node_modules/**": true,
        "**/vendor/**": true,
        "**/.cache/**": true,
        "**/.vscode/**": true
    },
    "telemetry.enableTelemetry": false,
    "explorer.confirmDelete": false,
    "files.autoSaveDelay": 5000,
    "eslint.autoFixOnSave": true,
    "explorer.confirmDragAndDrop": false,
    "javascript.updateImportsOnFileMove.enabled": "never",
    "javascript.implicitProjectConfig.experimentalDecorators": true,
    "files.exclude": {
        "**/.cache": true,
        "**/.DS_Store": true,
        "**/.git": true,
        "**/.hg": true,
        "**/node_modules": true,
        "**/.svn": true
    },
    "search.exclude": {
        "**/.cache": true,
        "**/bower_components": true,
        "**/node_modules": true,
        "**/vendor": true
    },
    "shellcheck.disableVersionCheck": true,
    "editor.formatOnSave": true,
    "files.eol": "\n",
    "git.confirmSync": false,
    "workbench.iconTheme": "material-icon-theme",
    "php-cs-fixer.rules": {
        "@PSR1": true,
        "@PSR2": true,
        "@PhpCsFixer": true,
        "array_syntax": {
            "syntax": "short"
        },
        "yoda_style": false,
        "single_quote": true,
        "binary_operator_spaces": {
            "operators": {
                "=>": "align_single_space_minimal",
                "=": "align_single_space_minimal"
            }
        },
        "concat_space": {
            "spacing": "one"
        },
        "phpdoc_inline_tag": false
    },
    "php-cs-fixer.executablePath": "${extensionPath}/php-cs-fixer.phar"
}
