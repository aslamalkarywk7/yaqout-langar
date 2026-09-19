# Contributors

Thanks to everyone helping build Yaqout — the Arabic programming language based on Lua.

## Lead Developer

- **Islam Al-Nashar** — Language design, Arabic lexer (`llex.c`), Arabic character support (`lctype.c`), localized standard libraries, VS Code extension, documentation.
  - GitHub: [@aslamalkarywk7](https://github.com/aslamalkarywk7)
  - Organization: Al-Nashar Studio

## How to become a contributor

1. Fork the repo and create a branch: `feature/short-name` or `fix/short-name`.
2. Follow the code style in CONTRIBUTING.md (C99, `snake_case` for C, Arabic names with underscores for Yaqout APIs).
3. Add or update tests under `testes/` when you change behavior.
4. Update docs (`README.md`, `build.md`, `YAQOUT_BOOK.md`) in the same PR when the change is user-facing.
5. Open a Pull Request against `main` with a clear description and test steps.

Areas needing help right now:

- Localizing `lcorolib.c` and `ldblib.c` (keep English aliases for compatibility)
- Docs and learning examples in English
- Tests for Arabic keywords and `.yq` files
- Bug reports with minimal reproduction (version, command, output)

## Recognition

All contributors are listed here after their first merged PR (name + area). Small doc fixes count too.

<!-- Add new contributors below, alphabetical by GitHub handle. Example:
- **@username** — what they did (docs, tests, fix in `lbaselib.c`)
-->

## License

By contributing you agree your work is released under the MIT License of this repo.
