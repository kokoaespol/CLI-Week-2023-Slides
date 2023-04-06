---
title: Bienvenidos a la CLI Week
author: Alexander Goussas
patat:
  incrementalLists: true
  margins:
    left: 20
    right: 20
  pandocExtensions:
    - patat_extensions
    - emoji
  images:
    backend: auto
...

# ¿Qué es una herramienta de CLI?

Una herramienta diseñada para ser utilizada a través de una interfaz de texto.

Estas pueden categorizarse como:

- Intérpretes de línea de comando
    - grep
    - xclip
    - fd
    - jq
- TUIs
    - htop
    - ranger
    - fzf
    - spotify-tui

# Ejemplos de aplicaciones

Vamos a ver algunas aplicaciones para inspirarnos.

- youtube-dl
    - Descarga video de YouTube u otros sitios. 
    - Escrito en Python.
    - Ejemplo: `yt-dlp https://www.youtube.com/watch?v=Lngmx0v3aOs`
- httpie
    - Un cliente http para la terminal.
    - Escrito en Python.
    - Ejemplo: `http httpbin.org/status/418`
- ranger
    - Un file manager para la terminal.
    - Escrito en Python.
- fzf
    - Un fuzzy finder.
    - Escrito en Go.
    - Muy útil combinado con otras herramientas en scripts.
- patat
    - Presentaciones en la terminal.
    - Escrito en Haskell.
    - Usado para hacer esta presentación :).
- figlet
    - Arte ascii.
    - Escrito en C.
    - Ejemplo: `figlet "CLI Week <3"`
    - Ver también:
        - `toilet "CLI Week <3" --gay`
        - `toilet "CLI Week <3" | lolcat`

# Editores de texto

- vim
    - Editor de texto modal.
    - Escrito en C.
    - Configurado en VimL.
- nvim
    - Sucesor de vim.
    - Configurado en VimL o Lua.
- helix
    - Editor de texto modal.
    - Escrito en Rust.
    - Configurado en archivos toml.
- emacs
    - Configurado en un EmacsLisp.
    - Mucho más que un editor.
- micro
    - Sencillo.
    - Se tiene planeado implementar keybindings de Vim.
    - Escrito en Go.
    - Cuenta con un plugin manager builtin.

# Y muchas más

- https://github.com/agarrharr/awesome-cli-apps.
- https://github.com/rothgar/awesome-tuis

# Librerías

Ahora vamos a ver cómo podríamos hacer nuestra propia herramienta de CLI.

# Sin librería

- Secuencias de escape ANSI.
- Se pueden utilizar para controlar los atributos de la terminal.
- Ejemplo: `printf "CLI Week \033[31m<3\033[m\n"`
- El file manager fff está escrito en Bash únicamente utilizando estas
  secuencias de escape: https://github.com/dylanaraps/fff.
- Algunas librerías son simple wrappers para estas secuencias de escape, como 
  `ansi-terminal` en el ecosistema de Haskell.
- Referencia: https://www2.ccs.neu.edu/research/gpc/VonaUtils/vona/terminal/vtansi.htm

# ncurses

- Librería para crear TUIs ampliamente utilizada.
- Es de más bajo nivel que otras librerías o frameworks.
- Originalmente escrita en C, pero tiene bindings para muchos lenguajes:
    - JavaScript: https://github.com/chjj/blessed
    - Python: https://docs.python.org/3/howto/curses.html
    - Ruby: https://github.com/ruby/curses
    - Perl: https://metacpan.org/pod/Curses
    - Php: http://php.adamharvey.name/manual/en/book.ncurses.php
- Referencia: https://tldp.org/HOWTO/NCURSES-Programming-HOWTO/

# Bubble Tea

- Un toolkit para crear aplicaciones de consola interactivas.
- Lenguaje: Go.
- Github: https://github.com/charmbracelet/bubbletea.

#

![](./assets/bubbletea.png)

# ink

- React para hacer TUIs.
- Github: https://github.com/vadimdemedes/ink
- Ejemplo:
```js
import React, {useState, useEffect} from 'react';
import {render, Text} from 'ink';

const Counter = () => {
  const [counter, setCounter] = useState(0);
  useEffect(() => {
    const timer = setInterval(() => {
      setCounter(previousCounter => previousCounter + 1);
    }, 100);
    return () => {
      clearInterval(timer);
    };
  }, []);
  return <Text color="green">{counter} tests passed</Text>;
};

render(<Counter />);
```

# nimwave

- Lenguaje: Nim.
- Github: https://github.com/ansiwave/nimwave.
- Ejemplo:
```nim
render(
  nw.Box(
    direction: nw.Direction.Vertical,
    border: nw.Border.Single,
    children: nw.seq(
      "Hello, world!",
      "Nim rocks",
    ),
  ),
  ctx
)
```

# textual

- Lenguaje: Python
- Github: https://github.com/Textualize/textual
- Ejemplo:
```python
from textual.app import App, ComposeResult
from textual.widgets import Header, Footer


class StopwatchApp(App):
    """A Textual app to manage stopwatches."""

    BINDINGS = [("d", "toggle_dark", "Toggle dark mode")]

    def compose(self) -> ComposeResult:
        """Create child widgets for the app."""
        yield Header()
        yield Footer()

    def action_toggle_dark(self) -> None:
        """An action to toggle dark mode."""
        self.dark = not self.dark


if __name__ == "__main__":
    app = StopwatchApp()
    app.run()
```

# Thermage

- Lenguaje: PHP
- Github: https://github.com/thermage/thermage
- Ejemplo:
```php
use function Thermage\paragraph;
use function Thermage\render;

render (
  paragraph('Stay RAD!')
    ->pl5()
    ->colorGreen()
    ->bgPurple()
    ->bold()
);
```

# tcell

- Lenguaje: Go
- Github: https://github.com/gdamore/tcell
- Ejemplos:
    - micro
    - fzf
    - lf


# Procesamiento de argumentos

Ejemplo:
```bash
ls --color=auto --hyperlink=auto -lh some-dir
#   ^------- flags ----^  switch -^   ^- argumento
```

- Sin librería (`argc` + `argv`)
- Con librería:
    - argparse: Python
    - clap: Rust
    - optparse-applicative: Haskell
    - flag/cobra: Go
    - optparse: Ruby
    - yargs: JavaScript (Node)
    - GetOpt: Php

# ¡Ahora te toca a ti!

Diviértete creando tu propia herramienta de CLI esta semana.

¡Estamos ansiosos por ver los resultados!

Links:
- 12 Factor CLI Apps: https://medium.com/@jdxcode/12-factor-cli-apps-dd3c227a0e46
