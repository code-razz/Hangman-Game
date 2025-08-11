# Hangman (C)

A simple terminal Hangman game written in C with ASCII art and a very lightweight username/password system stored in a text file.

## Quick Start

### Windows
- Run the included executable:
  - Double‑click `hangman.exe`, or
  - From PowerShell in this folder: `./hangman.exe`

### Build From Source (all platforms)
You need a C compiler (GCC or Clang).

- Windows (MinGW‑w64):
  ```powershell
  gcc hangman.c -o hangman
  ./hangman.exe
  ```
- Linux/macOS:
  ```bash
  gcc hangman.c -o hangman
  ./hangman
  ```

> Note: The program expects to run from the same directory as its data files. Ensure `database.txt` and `hangman_words.txt` are next to the executable when you run it.

## How To Play
1. On launch, choose:
   - Sign In (enter an existing username and password), or
   - Create Account (register a new username and password). Credentials are stored in `database.txt` as plain text.
2. Guess letters to reveal the hidden word. Repeated guesses are detected as duplicates.
3. You have up to 7 incorrect guesses before the hangman is complete and you lose.
4. After a round, you can choose to play again.

Example gallows stage shown during play:
```
  +---+
  |   |
  O   |
 /|\  |
 / \  |
      |
=========
```

## Files
- `hangman.c`: Source code for the game.
- `hangman.exe`: Prebuilt Windows executable.
- `database.txt`: Stores username and password pairs (space‑separated, one pair per line). Example:
  ```
  alice mypassword
  bob hunter2
  ```
- `hangman_words.txt`: Word list for the game (one word per line).

## Configuration and Notes
- Word selection: The code currently uses a random line number with `rand()%2400+1`. Ensure `hangman_words.txt` has at least 2400 lines. If you change the word list length, update the modulus accordingly in `hangman.c`.
- Clear screen: The program uses ANSI escape sequences (`\e[1;1H\e[2J`) to clear the screen. These work in most modern terminals, including Windows 10+ PowerShell/Windows Terminal. If your terminal doesn't clear, it's cosmetic only.
- Case handling: Letter guesses are converted to uppercase internally; word list should be uppercase or mixed case is fine.
- Credentials: Stored in plain text for demonstration only. Do not use real passwords.

## Portability
- `strlwr` is non‑standard and may not be available on some non‑Windows toolchains. If your compiler complains, replace the username‑lowercasing with a simple loop using `tolower`.
- Compilers: Tested with GCC. Clang should also work.

## Building with Warnings Enabled (recommended)
```bash
gcc -Wall -Wextra -Wpedantic hangman.c -o hangman
```

## Troubleshooting
- Program can’t find files: Run the executable from the folder containing `database.txt` and `hangman_words.txt` (or provide absolute paths in the code).
- Empty/short word list: If `hangman_words.txt` has fewer lines than the random range, selection can fail. Ensure enough lines or reduce the modulus in code.
- Screen doesn’t clear: Use a terminal that supports ANSI (Windows Terminal/PowerShell on Windows 10+). Otherwise ignore the cosmetic clearing.
- Unicode/locale issues: Keep the word list to basic ASCII if your terminal has trouble rendering.

