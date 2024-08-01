{
  "extends": [
    "eslint:recommended",
    "plugin:prettier/recommended"
  ],
  "plugins": [
    "simple-import-sort"
  ],
  "rules": {
    "prettier/prettier": ["error", { "endOfLine": "auto" }],
    "simple-import-sort/imports": "error",
    "padding-line-between-statements": [
      "error",
      { "blankLine": "always", "prev": "import", "next": "*" },
      { "blankLine": "any", "prev": "import", "next": "import" },
      { "blankLine": "always", "prev": "function", "next": "*" },
      { "blankLine": "always", "prev": "*", "next": "return" }
    ]
  }
}

prettier.config.js
module.exports = {
  semi: true,
  trailingComma: "es5",
  singleQuote: true,
  printWidth: 80,
  tabWidth: 2
};
