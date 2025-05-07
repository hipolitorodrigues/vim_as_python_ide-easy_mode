# Set Up Vim as a Python IDE

### 1. **Install Dependencies**

Update your system and install the necessary tools for Vim and its plugins:

```bash
sudo apt update && sudo apt install vim python3 python3-pip git curl build-essential -y
pip3 install flake8 pylint black isort jedi --user
```

### 2. **Install Vim-Plug**

Add the Vim-Plug plugin manager:

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### 3. **Configure Vim**

Create or edit your Vim configuration file:

```bash
vim ~/.vimrc
```

Add the following content, which includes explanatory comments:

```vim
" Start Vim-Plug
call plug#begin('~/.vim/plugged')

" Python Plugins
Plug 'vim-python/python-syntax'        " Enhanced Python syntax
Plug 'dense-analysis/ale'              " Linting and error checking
Plug 'davidhalter/jedi-vim'            " Autocompletion and navigation for Python
Plug 'preservim/nerdtree'              " File explorer
Plug 'vim-airline/vim-airline'         " Enhanced status bar
Plug 'vim-airline/vim-airline-themes'

" End Vim-Plug block
call plug#end()

" General Vim Settings
set number                            " Show line numbers
set relativenumber                    " Show relative line numbers
set tabstop=4                         " 4 spaces per tab
set shiftwidth=4                      " 4 spaces per indent
set expandtab                         " Convert tabs to spaces
set autoindent                        " Enable auto-indentation
set encoding=utf-8                    " Use UTF-8 encoding
set cursorline                        " Highlight current line
syntax on                             " Enable syntax highlighting

" ALE Settings (linting and formatting)
let g:ale_linters = {'python': ['flake8', 'pylint']}
let g:ale_fixers = {'python': ['black', 'isort']}
let g:ale_fix_on_save = 1             " Auto-fix on save

" jedi-vim Settings
let g:jedi#completions_enabled = 1    " Enable autocompletion
let g:jedi#use_splits_not_buffers = "right"  " Open definitions in split windows
let g:jedi#popup_on_dot = 1           " Show suggestions when typing a dot
nnoremap <leader>g :JediGoToDefinition<CR>  " Go to definition with \g

" Useful Shortcuts
nnoremap <C-t> :NERDTreeToggle<CR>    " Toggle NERDTree with Ctrl+T
nnoremap <C-s> :w<CR>                 " Save with Ctrl+S in normal mode
inoremap <C-s> <Esc>:w<CR>a           " Save with Ctrl+S in insert mode

" Airline Settings
let g:airline_powerline_fonts = 1
```

Save the file with `:wq`.

### 4. **Install the Plugins**

In Vim, install the plugins listed in `.vimrc`:

```bash
vim
:PlugInstall
```

Exit Vim with `:q` after installation is complete.

### 5. **Test the Configuration**

Create a Python file to test:

```bash
vim test.py
```

Add the following code:

```python
def soma(a, b):
    return a + b
print(soma(2, 3))
```

Test the features:

* **Autocomplete**: Type `so` or `soma.` in insert mode; suggestions should appear automatically (use `Ctrl+N`/`Ctrl+P` to navigate).
* **Navigation**: Press `\g` to go to the definition of a function or variable.
* **Linting/Formatting**: Save with `:w`; ALE will auto-format (using Black/isort) or show errors (via Flake8/Pylint).
* **File Explorer**: Press `Ctrl+T` to toggle NERDTree.
* **Saving**: Use `Ctrl+S` to save in both normal and insert modes.

---

### Configured Features

* **Autocomplete & Navigation**: `jedi-vim` provides suggestions and “Go to Definition”.
* **Linting & Formatting**: `ALE` using Flake8, Pylint, Black, and isort.
* **File Explorer**: `NERDTree` for easy file navigation.
* **Status Bar**: `Airline` with themes.
