## Adding new languages to Helix

In order to add a new language to Helix, you will need to follow the steps
below.

## Language configuration

1. Add a new `[[language]]` entry in the `languages.toml` file and provide the
   necessary configuration for the new language. For more information on
   language configuration, refer to the
   [language configuration section](../languages.md) of the documentation.
   A new language server can be added by extending the `[language-server]` table in the same file.
2. If you are adding a new language or updating an existing language server
   configuration, run the command `cargo xtask docgen` to update the
   [Language Support](../lang-support.md) documentation.

> 💡 If you are adding a new Language Server configuration, make sure to update
> the
> [Language Server Wiki](https://github.com/helix-editor/helix/wiki/Language-Server-Configurations)
> with the installation instructions.

## Grammar configuration

1. If a tree-sitter grammar is available for the new language, add a new
   `[[grammar]]` entry to the `languages.toml` file.
2. If you are testing the grammar locally, you can use the `source.path` key
   with an absolute path to the grammar. However, before submitting a pull
   request, make sure to switch to using `source.git`.

## Queries

1. In order to provide syntax highlighting and indentation for the new language,
   you will need to add queries.
2. Create a new directory for the language with the path
   `runtime/queries/<name>/`.
3. Refer to the
   [tree-sitter website](https://tree-sitter.github.io/tree-sitter/3-syntax-highlighting.html#highlights)
   for more information on writing queries.
4. A list of highlight captures can be found [on the themes page](https://docs.helix-editor.com/themes.html#scopes).

## Common issues

- If you encounter errors when running Helix after switching branches, you may
  need to update the tree-sitter grammars. Run the command `hx --grammar fetch`
  to fetch the grammars and `hx --grammar build` to build any out-of-date
  grammars.
- If a parser is causing a segfault, or you want to remove it, make sure to
  remove the compiled parser located at `runtime/grammars/<name>.so`.
- If you are attempting to add queries and Helix is unable to locate them, ensure that the environment variable `HELIX_RUNTIME` is set to the location of the `runtime` folder you're developing in.
