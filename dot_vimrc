" $VIMRUNTIME refers to the versioned system directory where Vim stores its
" system runtime files -- /usr/share/vim/vim<version>.
"
" Vim will load $VIMRUNTIME/defaults.vim if the user does not have a vimrc.
" This happens after /etc/vim/vimrc(.local) are loaded, so it will override
" any settings in these files.
"
" If you don't want that to happen, uncomment the below line to prevent
" defaults.vim from being loaded.
" let g:skip_defaults_vim = 1
"
" If you would rather _use_ default.vim's settings, but have the system or
" user vimrc override its settings, then uncomment the line below.
" source $VIMRUNTIME/defaults.vim

" All Debian-specific settings are defined in $VIMRUNTIME/debian.vim and
" sourced by the call to :runtime you can find below.  If you wish to change
" any of those settings, you should do it in this file or
" /etc/vim/vimrc.local, since debian.vim will be overwritten everytime an
" upgrade of the vim packages is performed. It is recommended to make changes
" after sourcing debian.vim so your settings take precedence.



" ====================================================================
" OS DETECTION (/etc/os-release)
" ====================================================================
let g:os_name = ""
if filereadable("/etc/os-release")
	let g:os_lines = readfile("/etc/os-release")
	for g:line in g:os_lines
		if g:line =~ '^ID='
			let g:os_name = substitute(g:line, '^ID=\([''"]\?\)\(.*\)\1', '\2', '')
			break
		endif
	endfor
endif

if g:os_name ==# "arch"
    runtime! archlinux.vim

elseif g:os_name ==# "ubuntu"
    runtime! debian.vim

endif


" Uncomment the next line to make Vim more Vi-compatible
" NOTE: debian.vim sets 'nocompatible'.  Setting 'compatible' changes
" numerous options, so any other options should be set AFTER changing
" 'compatible'.
"set compatible

" Vim5 and later versions support syntax highlighting. Uncommenting the next
" line enables syntax highlighting by default.
if has("syntax")
  syntax on
endif

" If using a dark background within the editing area and syntax highlighting
" turn on this option as well
set background=dark

" Uncomment the following to have Vim jump to the last position when
" reopening a file
au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif

" Uncomment the following to have Vim load indentation rules and plugins
" according to the detected filetype.
filetype plugin indent on
filetype indent on

" The following are commented out as they cause vim to behave a lot
" differently from regular Vi. They are highly recommended though.
"set showcmd		    " Show (partial) command in status line.
set showmatch		  " Show matching brackets.
set ignorecase		" Do case insensitive matching
set smartcase		  " Do smart case matching
set hlsearch	    " Highlight search matches
set incsearch		  " Incremental search
"set autowrite		 " Automatically save before commands like :next and :make
"set hidden		     " Hide buffers when they are abandoned
set mouse=a		    " Enable mouse usage (all modes)
set autoindent    " Auto-indentation
"set number        " Show linenumbers

" Set the default indentation to 2 for all files
set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab

" Highlight trailing whitespace in all files
autocmd BufRead,BufNewFile * match Error /\s\+$/

" Set backspace so it acts more intuitively
set backspace=indent,eol,start


" Source a global configuration file if available
if filereadable("/etc/vim/vimrc.local")
  source /etc/vim/vimrc.local
endif


" =====================================================================
" THÈME TOKYO NIGHT MINIMALISTE (SANS PLUGIN)
" =====================================================================

" Activer les couleurs 24-bit (True Color) dans le terminal
set termguicolors

" Activer la coloration syntaxique de base
syntax on

" ── PALETTE DE COULEURS TOKYO NIGHT ──────────────────────────────────
" Configuration manuelle des groupes de syntaxe principaux
highlight Normal       guifg=#c0caf5 guibg=NONE    " Texte principal / Fond transparent
highlight Comment      guifg=#565f89 gui=italic    " Commentaires en gris bleuté
highlight Constant     guifg=#ff9e64               " Chaînes de caractères / Chiffres
highlight Identifier   guifg=#7dcfff               " Noms de variables
highlight Statement    guifg=#bb9af7 gui=bold      " Mots-clés (if, for, return)
highlight PreProc      guifg=#7aa2f7               " Préprocesseur (#include, import)
highlight Type         guifg=#2ac3de               " Types (int, string, struct)
highlight Special      guifg=#b4f9f8               " Caractères spéciaux
highlight Underlined   gui=underline
highlight Error        guifg=#f7768e guibg=NONE gui=bold

" ── INTERFACE VIM ────────────────────────────────────────────────────
highlight LineNr       guifg=#3b4261               " Numéros de ligne inactifs
highlight CursorLineNr guifg=#7aa2f7 gui=bold      " Numéro de ligne actif (Bleu)
highlight Visual       guibg=#283457               " Couleur de la sélection de texte
highlight Search       guifg=#1f2335 guibg=#e0af68 " Couleur de recherche (Jaune)
highlight MatchParen   guifg=#ff9e64 guibg=NONE gui=bold " Parenthèses correspondantes


" ── BARRE D'ÉTAT DU BAS (STATUS LINE) ────────────────────────────────
" Configuration d'une barre de statut Vim ultra-minimaliste
set laststatus=2   " Affiche la barre d'état en permanence
set noshowmode     " Désactive les modes dans la dernière ligne
set noshowcmd      " Désactive l'affichage des commandes incomplètes en bas à droite
set cmdheight=1    " Force la ligne de commande à ne faire qu'une seule ligne de hauteur

"STATUSLINE MODE
 let g:currentmode={
 \ 'n' : 'NORMAL ',
 \ 'v' : 'VISUAL ',
 \ 'V' : 'V-LINE ',
 \ "\<C-V>" : 'V-BLOCK' ,
 \ 'i' : 'INSERT ',
 \ 'R' : 'R ',
 \ 'Rv' : 'V-REPLACE ',
 \ 'c' : 'COMMAND ',
 \}

 set statusline=%#TokyoNightStatus#                  
 set statusline+=\ %{get(g:currentmode,mode(),'')}  " Affiche le mode actif
 set statusline+=\ %F                               " Chemin du fichier
" set statusline+=\ %f                               " Nom du fichier
 set statusline+=\ %m                               " Indicateur si modification
 set statusline+=\ %r                               " Indicateur si lecture seule

 set statusline+=%=                                 " Alignement à droite
 
 set statusline+=\ %y                               " Type de fichier
 set statusline+=\ %{&fileencoding?&fileencoding:&encoding} " Encodage
 set statusline+=\ [%l/%L]                          " Ligne actuelle / Total ligne
 set statusline+=\ (%c)                             " Colonne actuelle
 set statusline+=\ %p%%\                            " Pourcentage de lecture


" Couleurs de la barre d'état (Violet Tokyo Night discret)
highlight TokyoNightStatus guifg=#ffffff guibg=#24283b gui=bold
highlight StatusLine       guifg=#ffffff guibg=#24283b gui=none
highlight StatusLineNC     guifg=#565f89 guibg=#1f2335 gui=none " Fenêtre Vim inactive


