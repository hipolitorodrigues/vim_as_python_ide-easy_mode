# Set Up Vim as a Python IDE (with Virtual Environment)
## (To view the Set Up without a virtual environment: CLICK HERE)

### 1. **Install System Dependencies**

Update your system and install the required tools for Vim and the virtual environment:

```bash
sudo apt update && sudo apt install vim python3 python3-venv python3-pip git curl build-essential -y
```

### 2. **Create and Activate a Virtual Environment**

Create and activate a virtual environment:

```bash
python3 -m venv ~/env01
source ~/env01/bin/activate
```

Or, in the current directory:

```bash
python3 -m venv env01
source env01/bin/activate
```

To confirm the correct Python path:

```bash
which python3
```

#### Notes

* **Virtual Environment**: Always activate the virtual environment (`source env01/bin/activate`) before using Vim to ensure plugins can find the necessary Python dependencies.
* **Deactivate**: Use `deactivate` when you no longer need the virtual environment.

### 3. **Install Python Dependencies Inside the Virtual Environment**

With the virtual environment activated, install the necessary Python packages for Vim plugins:

```bash
pip install jedi flake8 pylint black isort
```

### 4. **Install Vim-Plug**

Add the Vim-Plug plugin manager:

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### 5. **Configure Vim**

Create or edit the Vim configuration file:

```bash
vim ~/.vimrc
```

Add the following content with explanatory comments:

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
Plug 'jiangmiao/auto-pairs'            " Auto-close brackets and quotes

" End Vim-Plug block
call plug#end()

" General Vim Settings (To find the correct Python path, activate the virtual environment and run: $ which python3)
let g:python3_host_prog = '/PATH/OF/YOUR/PROJECT/env01/bin/python3'
set number                            " Show line numbers
" set relativenumber                  " Relative line numbers
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
let g:ale_fix_on_save = 1
let g:ale_python_pylint_options = '--disable=C0114,C0115,C0116' " Ignore missing docstrings in headers, functions, and classes

" jedi-vim Settings
let g:jedi#completions_enabled = 1
let g:jedi#use_splits_not_buffers = "right"
let g:jedi#popup_on_dot = 1
nnoremap <leader>g :JediGoToDefinition<CR>

" Useful Shortcuts
nnoremap <C-t> :NERDTreeToggle<CR>
nnoremap <C-s> :w<CR>
inoremap <C-s> <Esc>:w<CR>a

" Airline Settings
let g:airline_powerline_fonts = 1
```

Save the file with `:wq`.

### 6. **Install the Plugins**

Inside Vim, install the plugins listed in `.vimrc`:

```vim
:PlugInstall
```

#### ✅ How to Install Plugins Using Vim-Plug:

1. **Open Vim normally** (you don’t need to open a specific file):

   ```bash
   vim
   ```
2. **Inside Vim**, type this command in normal mode (press `Esc` to ensure you’re not in insert mode):

   ```vim
   :PlugInstall
   ```

   * Vim will open a window showing the list of plugins being downloaded and installed.
3. **Wait for all plugins to finish installing.**

   * Press `Enter` if prompted.
   * Then, exit Vim with:

   ```vim
   :q
   ```

### 7. **Test the Configuration**

Make sure the virtual environment is activated:

```bash
source env01/bin/activate
```

Create a Python test file:

```bash
vim test.py
```

Add this code:

```python
def soma(a, b):
    return a + b
print(soma(2, 3))
```

Test the features:

* **Autocomplete**: Type `so` or `soma.` in insert mode; suggestions should appear (use `Ctrl+N`/`Ctrl+P` to navigate).
* **Navigation**: Press `\g` to jump to the definition of a function or variable.
* **Linting/Formatting**: Save with `:w`; ALE will auto-format (via Black/isort) or show errors (via Flake8/Pylint).
* **File Explorer**: Press `Ctrl+T` to toggle NERDTree.
* **Save**: Use `Ctrl+S` to save in both normal and insert modes.

---

### Configured Features

* **Autocomplete & Navigation**: `jedi-vim` for suggestions and “Go to Definition”.
* **Linting & Formatting**: `ALE` using Flake8, Pylint, Black, and isort (installed in the virtual environment).
* **File Explorer**: `NERDTree` for navigation.
* **Status Bar**: `Airline` with themes.

### Notes

* **Virtual Environment**: Always activate the virtual environment (`source env01/bin/activate`) before using Vim to ensure Python dependencies are available to plugins.
* **.vimrc**: This config file stays at `~/.vimrc`, even when using a virtual environment.
* **Deactivate**: Use `deactivate` when you don’t need the virtual environment.
