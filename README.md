\documentclass[11pt]{article}

    \usepackage[breakable]{tcolorbox}
    \usepackage{parskip} % Stop auto-indenting (to mimic markdown behaviour)
    
    \usepackage{iftex}
    \ifPDFTeX
    	\usepackage[T1]{fontenc}
    	\usepackage{mathpazo}
    \else
    	\usepackage{fontspec}
    \fi

    % Basic figure setup, for now with no caption control since it's done
    % automatically by Pandoc (which extracts ![](path) syntax from Markdown).
    \usepackage{graphicx}
    % Maintain compatibility with old templates. Remove in nbconvert 6.0
    \let\Oldincludegraphics\includegraphics
    % Ensure that by default, figures have no caption (until we provide a
    % proper Figure object with a Caption API and a way to capture that
    % in the conversion process - todo).
    \usepackage{caption}
    \DeclareCaptionFormat{nocaption}{}
    \captionsetup{format=nocaption,aboveskip=0pt,belowskip=0pt}

    \usepackage{float}
    \floatplacement{figure}{H} % forces figures to be placed at the correct location
    \usepackage{xcolor} % Allow colors to be defined
    \usepackage{enumerate} % Needed for markdown enumerations to work
    \usepackage{geometry} % Used to adjust the document margins
    \usepackage{amsmath} % Equations
    \usepackage{amssymb} % Equations
    \usepackage{textcomp} % defines textquotesingle
    % Hack from http://tex.stackexchange.com/a/47451/13684:
    \AtBeginDocument{%
        \def\PYZsq{\textquotesingle}% Upright quotes in Pygmentized code
    }
    \usepackage{upquote} % Upright quotes for verbatim code
    \usepackage{eurosym} % defines \euro
    \usepackage[mathletters]{ucs} % Extended unicode (utf-8) support
    \usepackage{fancyvrb} % verbatim replacement that allows latex
    \usepackage{grffile} % extends the file name processing of package graphics 
                         % to support a larger range
    \makeatletter % fix for old versions of grffile with XeLaTeX
    \@ifpackagelater{grffile}{2019/11/01}
    {
      % Do nothing on new versions
    }
    {
      \def\Gread@@xetex#1{%
        \IfFileExists{"\Gin@base".bb}%
        {\Gread@eps{\Gin@base.bb}}%
        {\Gread@@xetex@aux#1}%
      }
    }
    \makeatother
    \usepackage[Export]{adjustbox} % Used to constrain images to a maximum size
    \adjustboxset{max size={0.9\linewidth}{0.9\paperheight}}

    % The hyperref package gives us a pdf with properly built
    % internal navigation ('pdf bookmarks' for the table of contents,
    % internal cross-reference links, web links for URLs, etc.)
    \usepackage{hyperref}
    % The default LaTeX title has an obnoxious amount of whitespace. By default,
    % titling removes some of it. It also provides customization options.
    \usepackage{titling}
    \usepackage{longtable} % longtable support required by pandoc >1.10
    \usepackage{booktabs}  % table support for pandoc > 1.12.2
    \usepackage[inline]{enumitem} % IRkernel/repr support (it uses the enumerate* environment)
    \usepackage[normalem]{ulem} % ulem is needed to support strikethroughs (\sout)
                                % normalem makes italics be italics, not underlines
    \usepackage{mathrsfs}
    

    
    % Colors for the hyperref package
    \definecolor{urlcolor}{rgb}{0,.145,.698}
    \definecolor{linkcolor}{rgb}{.71,0.21,0.01}
    \definecolor{citecolor}{rgb}{.12,.54,.11}

    % ANSI colors
    \definecolor{ansi-black}{HTML}{3E424D}
    \definecolor{ansi-black-intense}{HTML}{282C36}
    \definecolor{ansi-red}{HTML}{E75C58}
    \definecolor{ansi-red-intense}{HTML}{B22B31}
    \definecolor{ansi-green}{HTML}{00A250}
    \definecolor{ansi-green-intense}{HTML}{007427}
    \definecolor{ansi-yellow}{HTML}{DDB62B}
    \definecolor{ansi-yellow-intense}{HTML}{B27D12}
    \definecolor{ansi-blue}{HTML}{208FFB}
    \definecolor{ansi-blue-intense}{HTML}{0065CA}
    \definecolor{ansi-magenta}{HTML}{D160C4}
    \definecolor{ansi-magenta-intense}{HTML}{A03196}
    \definecolor{ansi-cyan}{HTML}{60C6C8}
    \definecolor{ansi-cyan-intense}{HTML}{258F8F}
    \definecolor{ansi-white}{HTML}{C5C1B4}
    \definecolor{ansi-white-intense}{HTML}{A1A6B2}
    \definecolor{ansi-default-inverse-fg}{HTML}{FFFFFF}
    \definecolor{ansi-default-inverse-bg}{HTML}{000000}

    % common color for the border for error outputs.
    \definecolor{outerrorbackground}{HTML}{FFDFDF}

    % commands and environments needed by pandoc snippets
    % extracted from the output of `pandoc -s`
    \providecommand{\tightlist}{%
      \setlength{\itemsep}{0pt}\setlength{\parskip}{0pt}}
    \DefineVerbatimEnvironment{Highlighting}{Verbatim}{commandchars=\\\{\}}
    % Add ',fontsize=\small' for more characters per line
    \newenvironment{Shaded}{}{}
    \newcommand{\KeywordTok}[1]{\textcolor[rgb]{0.00,0.44,0.13}{\textbf{{#1}}}}
    \newcommand{\DataTypeTok}[1]{\textcolor[rgb]{0.56,0.13,0.00}{{#1}}}
    \newcommand{\DecValTok}[1]{\textcolor[rgb]{0.25,0.63,0.44}{{#1}}}
    \newcommand{\BaseNTok}[1]{\textcolor[rgb]{0.25,0.63,0.44}{{#1}}}
    \newcommand{\FloatTok}[1]{\textcolor[rgb]{0.25,0.63,0.44}{{#1}}}
    \newcommand{\CharTok}[1]{\textcolor[rgb]{0.25,0.44,0.63}{{#1}}}
    \newcommand{\StringTok}[1]{\textcolor[rgb]{0.25,0.44,0.63}{{#1}}}
    \newcommand{\CommentTok}[1]{\textcolor[rgb]{0.38,0.63,0.69}{\textit{{#1}}}}
    \newcommand{\OtherTok}[1]{\textcolor[rgb]{0.00,0.44,0.13}{{#1}}}
    \newcommand{\AlertTok}[1]{\textcolor[rgb]{1.00,0.00,0.00}{\textbf{{#1}}}}
    \newcommand{\FunctionTok}[1]{\textcolor[rgb]{0.02,0.16,0.49}{{#1}}}
    \newcommand{\RegionMarkerTok}[1]{{#1}}
    \newcommand{\ErrorTok}[1]{\textcolor[rgb]{1.00,0.00,0.00}{\textbf{{#1}}}}
    \newcommand{\NormalTok}[1]{{#1}}
    
    % Additional commands for more recent versions of Pandoc
    \newcommand{\ConstantTok}[1]{\textcolor[rgb]{0.53,0.00,0.00}{{#1}}}
    \newcommand{\SpecialCharTok}[1]{\textcolor[rgb]{0.25,0.44,0.63}{{#1}}}
    \newcommand{\VerbatimStringTok}[1]{\textcolor[rgb]{0.25,0.44,0.63}{{#1}}}
    \newcommand{\SpecialStringTok}[1]{\textcolor[rgb]{0.73,0.40,0.53}{{#1}}}
    \newcommand{\ImportTok}[1]{{#1}}
    \newcommand{\DocumentationTok}[1]{\textcolor[rgb]{0.73,0.13,0.13}{\textit{{#1}}}}
    \newcommand{\AnnotationTok}[1]{\textcolor[rgb]{0.38,0.63,0.69}{\textbf{\textit{{#1}}}}}
    \newcommand{\CommentVarTok}[1]{\textcolor[rgb]{0.38,0.63,0.69}{\textbf{\textit{{#1}}}}}
    \newcommand{\VariableTok}[1]{\textcolor[rgb]{0.10,0.09,0.49}{{#1}}}
    \newcommand{\ControlFlowTok}[1]{\textcolor[rgb]{0.00,0.44,0.13}{\textbf{{#1}}}}
    \newcommand{\OperatorTok}[1]{\textcolor[rgb]{0.40,0.40,0.40}{{#1}}}
    \newcommand{\BuiltInTok}[1]{{#1}}
    \newcommand{\ExtensionTok}[1]{{#1}}
    \newcommand{\PreprocessorTok}[1]{\textcolor[rgb]{0.74,0.48,0.00}{{#1}}}
    \newcommand{\AttributeTok}[1]{\textcolor[rgb]{0.49,0.56,0.16}{{#1}}}
    \newcommand{\InformationTok}[1]{\textcolor[rgb]{0.38,0.63,0.69}{\textbf{\textit{{#1}}}}}
    \newcommand{\WarningTok}[1]{\textcolor[rgb]{0.38,0.63,0.69}{\textbf{\textit{{#1}}}}}
    
    
    % Define a nice break command that doesn't care if a line doesn't already
    % exist.
    \def\br{\hspace*{\fill} \\* }
    % Math Jax compatibility definitions
    \def\gt{>}
    \def\lt{<}
    \let\Oldtex\TeX
    \let\Oldlatex\LaTeX
    \renewcommand{\TeX}{\textrm{\Oldtex}}
    \renewcommand{\LaTeX}{\textrm{\Oldlatex}}
    % Document parameters
    % Document title
    \title{DSWS\_Median\_Index\_Data\_NB\_006}
    
    
    
    
    
% Pygments definitions
\makeatletter
\def\PY@reset{\let\PY@it=\relax \let\PY@bf=\relax%
    \let\PY@ul=\relax \let\PY@tc=\relax%
    \let\PY@bc=\relax \let\PY@ff=\relax}
\def\PY@tok#1{\csname PY@tok@#1\endcsname}
\def\PY@toks#1+{\ifx\relax#1\empty\else%
    \PY@tok{#1}\expandafter\PY@toks\fi}
\def\PY@do#1{\PY@bc{\PY@tc{\PY@ul{%
    \PY@it{\PY@bf{\PY@ff{#1}}}}}}}
\def\PY#1#2{\PY@reset\PY@toks#1+\relax+\PY@do{#2}}

\expandafter\def\csname PY@tok@w\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.73,0.73}{##1}}}
\expandafter\def\csname PY@tok@c\endcsname{\let\PY@it=\textit\def\PY@tc##1{\textcolor[rgb]{0.25,0.50,0.50}{##1}}}
\expandafter\def\csname PY@tok@cp\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.74,0.48,0.00}{##1}}}
\expandafter\def\csname PY@tok@k\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@kp\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@kt\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.69,0.00,0.25}{##1}}}
\expandafter\def\csname PY@tok@o\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@ow\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.67,0.13,1.00}{##1}}}
\expandafter\def\csname PY@tok@nb\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@nf\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.00,1.00}{##1}}}
\expandafter\def\csname PY@tok@nc\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.00,1.00}{##1}}}
\expandafter\def\csname PY@tok@nn\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.00,1.00}{##1}}}
\expandafter\def\csname PY@tok@ne\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.82,0.25,0.23}{##1}}}
\expandafter\def\csname PY@tok@nv\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.10,0.09,0.49}{##1}}}
\expandafter\def\csname PY@tok@no\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.53,0.00,0.00}{##1}}}
\expandafter\def\csname PY@tok@nl\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.63,0.63,0.00}{##1}}}
\expandafter\def\csname PY@tok@ni\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.60,0.60,0.60}{##1}}}
\expandafter\def\csname PY@tok@na\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.49,0.56,0.16}{##1}}}
\expandafter\def\csname PY@tok@nt\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@nd\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.67,0.13,1.00}{##1}}}
\expandafter\def\csname PY@tok@s\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@sd\endcsname{\let\PY@it=\textit\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@si\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.73,0.40,0.53}{##1}}}
\expandafter\def\csname PY@tok@se\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.73,0.40,0.13}{##1}}}
\expandafter\def\csname PY@tok@sr\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.40,0.53}{##1}}}
\expandafter\def\csname PY@tok@ss\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.10,0.09,0.49}{##1}}}
\expandafter\def\csname PY@tok@sx\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@m\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@gh\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.00,0.50}{##1}}}
\expandafter\def\csname PY@tok@gu\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.50,0.00,0.50}{##1}}}
\expandafter\def\csname PY@tok@gd\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.63,0.00,0.00}{##1}}}
\expandafter\def\csname PY@tok@gi\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.63,0.00}{##1}}}
\expandafter\def\csname PY@tok@gr\endcsname{\def\PY@tc##1{\textcolor[rgb]{1.00,0.00,0.00}{##1}}}
\expandafter\def\csname PY@tok@ge\endcsname{\let\PY@it=\textit}
\expandafter\def\csname PY@tok@gs\endcsname{\let\PY@bf=\textbf}
\expandafter\def\csname PY@tok@gp\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.00,0.50}{##1}}}
\expandafter\def\csname PY@tok@go\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.53,0.53,0.53}{##1}}}
\expandafter\def\csname PY@tok@gt\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.27,0.87}{##1}}}
\expandafter\def\csname PY@tok@err\endcsname{\def\PY@bc##1{\setlength{\fboxsep}{0pt}\fcolorbox[rgb]{1.00,0.00,0.00}{1,1,1}{\strut ##1}}}
\expandafter\def\csname PY@tok@kc\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@kd\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@kn\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@kr\endcsname{\let\PY@bf=\textbf\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@bp\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.50,0.00}{##1}}}
\expandafter\def\csname PY@tok@fm\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.00,0.00,1.00}{##1}}}
\expandafter\def\csname PY@tok@vc\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.10,0.09,0.49}{##1}}}
\expandafter\def\csname PY@tok@vg\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.10,0.09,0.49}{##1}}}
\expandafter\def\csname PY@tok@vi\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.10,0.09,0.49}{##1}}}
\expandafter\def\csname PY@tok@vm\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.10,0.09,0.49}{##1}}}
\expandafter\def\csname PY@tok@sa\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@sb\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@sc\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@dl\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@s2\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@sh\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@s1\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.73,0.13,0.13}{##1}}}
\expandafter\def\csname PY@tok@mb\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@mf\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@mh\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@mi\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@il\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@mo\endcsname{\def\PY@tc##1{\textcolor[rgb]{0.40,0.40,0.40}{##1}}}
\expandafter\def\csname PY@tok@ch\endcsname{\let\PY@it=\textit\def\PY@tc##1{\textcolor[rgb]{0.25,0.50,0.50}{##1}}}
\expandafter\def\csname PY@tok@cm\endcsname{\let\PY@it=\textit\def\PY@tc##1{\textcolor[rgb]{0.25,0.50,0.50}{##1}}}
\expandafter\def\csname PY@tok@cpf\endcsname{\let\PY@it=\textit\def\PY@tc##1{\textcolor[rgb]{0.25,0.50,0.50}{##1}}}
\expandafter\def\csname PY@tok@c1\endcsname{\let\PY@it=\textit\def\PY@tc##1{\textcolor[rgb]{0.25,0.50,0.50}{##1}}}
\expandafter\def\csname PY@tok@cs\endcsname{\let\PY@it=\textit\def\PY@tc##1{\textcolor[rgb]{0.25,0.50,0.50}{##1}}}

\def\PYZbs{\char`\\}
\def\PYZus{\char`\_}
\def\PYZob{\char`\{}
\def\PYZcb{\char`\}}
\def\PYZca{\char`\^}
\def\PYZam{\char`\&}
\def\PYZlt{\char`\<}
\def\PYZgt{\char`\>}
\def\PYZsh{\char`\#}
\def\PYZpc{\char`\%}
\def\PYZdl{\char`\$}
\def\PYZhy{\char`\-}
\def\PYZsq{\char`\'}
\def\PYZdq{\char`\"}
\def\PYZti{\char`\~}
% for compatibility with earlier versions
\def\PYZat{@}
\def\PYZlb{[}
\def\PYZrb{]}
\makeatother


    % For linebreaks inside Verbatim environment from package fancyvrb. 
    \makeatletter
        \newbox\Wrappedcontinuationbox 
        \newbox\Wrappedvisiblespacebox 
        \newcommand*\Wrappedvisiblespace {\textcolor{red}{\textvisiblespace}} 
        \newcommand*\Wrappedcontinuationsymbol {\textcolor{red}{\llap{\tiny$\m@th\hookrightarrow$}}} 
        \newcommand*\Wrappedcontinuationindent {3ex } 
        \newcommand*\Wrappedafterbreak {\kern\Wrappedcontinuationindent\copy\Wrappedcontinuationbox} 
        % Take advantage of the already applied Pygments mark-up to insert 
        % potential linebreaks for TeX processing. 
        %        {, <, #, %, $, ' and ": go to next line. 
        %        _, }, ^, &, >, - and ~: stay at end of broken line. 
        % Use of \textquotesingle for straight quote. 
        \newcommand*\Wrappedbreaksatspecials {% 
            \def\PYGZus{\discretionary{\char`\_}{\Wrappedafterbreak}{\char`\_}}% 
            \def\PYGZob{\discretionary{}{\Wrappedafterbreak\char`\{}{\char`\{}}% 
            \def\PYGZcb{\discretionary{\char`\}}{\Wrappedafterbreak}{\char`\}}}% 
            \def\PYGZca{\discretionary{\char`\^}{\Wrappedafterbreak}{\char`\^}}% 
            \def\PYGZam{\discretionary{\char`\&}{\Wrappedafterbreak}{\char`\&}}% 
            \def\PYGZlt{\discretionary{}{\Wrappedafterbreak\char`\<}{\char`\<}}% 
            \def\PYGZgt{\discretionary{\char`\>}{\Wrappedafterbreak}{\char`\>}}% 
            \def\PYGZsh{\discretionary{}{\Wrappedafterbreak\char`\#}{\char`\#}}% 
            \def\PYGZpc{\discretionary{}{\Wrappedafterbreak\char`\%}{\char`\%}}% 
            \def\PYGZdl{\discretionary{}{\Wrappedafterbreak\char`\$}{\char`\$}}% 
            \def\PYGZhy{\discretionary{\char`\-}{\Wrappedafterbreak}{\char`\-}}% 
            \def\PYGZsq{\discretionary{}{\Wrappedafterbreak\textquotesingle}{\textquotesingle}}% 
            \def\PYGZdq{\discretionary{}{\Wrappedafterbreak\char`\"}{\char`\"}}% 
            \def\PYGZti{\discretionary{\char`\~}{\Wrappedafterbreak}{\char`\~}}% 
        } 
        % Some characters . , ; ? ! / are not pygmentized. 
        % This macro makes them "active" and they will insert potential linebreaks 
        \newcommand*\Wrappedbreaksatpunct {% 
            \lccode`\~`\.\lowercase{\def~}{\discretionary{\hbox{\char`\.}}{\Wrappedafterbreak}{\hbox{\char`\.}}}% 
            \lccode`\~`\,\lowercase{\def~}{\discretionary{\hbox{\char`\,}}{\Wrappedafterbreak}{\hbox{\char`\,}}}% 
            \lccode`\~`\;\lowercase{\def~}{\discretionary{\hbox{\char`\;}}{\Wrappedafterbreak}{\hbox{\char`\;}}}% 
            \lccode`\~`\:\lowercase{\def~}{\discretionary{\hbox{\char`\:}}{\Wrappedafterbreak}{\hbox{\char`\:}}}% 
            \lccode`\~`\?\lowercase{\def~}{\discretionary{\hbox{\char`\?}}{\Wrappedafterbreak}{\hbox{\char`\?}}}% 
            \lccode`\~`\!\lowercase{\def~}{\discretionary{\hbox{\char`\!}}{\Wrappedafterbreak}{\hbox{\char`\!}}}% 
            \lccode`\~`\/\lowercase{\def~}{\discretionary{\hbox{\char`\/}}{\Wrappedafterbreak}{\hbox{\char`\/}}}% 
            \catcode`\.\active
            \catcode`\,\active 
            \catcode`\;\active
            \catcode`\:\active
            \catcode`\?\active
            \catcode`\!\active
            \catcode`\/\active 
            \lccode`\~`\~ 	
        }
    \makeatother

    \let\OriginalVerbatim=\Verbatim
    \makeatletter
    \renewcommand{\Verbatim}[1][1]{%
        %\parskip\z@skip
        \sbox\Wrappedcontinuationbox {\Wrappedcontinuationsymbol}%
        \sbox\Wrappedvisiblespacebox {\FV@SetupFont\Wrappedvisiblespace}%
        \def\FancyVerbFormatLine ##1{\hsize\linewidth
            \vtop{\raggedright\hyphenpenalty\z@\exhyphenpenalty\z@
                \doublehyphendemerits\z@\finalhyphendemerits\z@
                \strut ##1\strut}%
        }%
        % If the linebreak is at a space, the latter will be displayed as visible
        % space at end of first line, and a continuation symbol starts next line.
        % Stretch/shrink are however usually zero for typewriter font.
        \def\FV@Space {%
            \nobreak\hskip\z@ plus\fontdimen3\font minus\fontdimen4\font
            \discretionary{\copy\Wrappedvisiblespacebox}{\Wrappedafterbreak}
            {\kern\fontdimen2\font}%
        }%
        
        % Allow breaks at special characters using \PYG... macros.
        \Wrappedbreaksatspecials
        % Breaks at punctuation characters . , ; ? ! and / need catcode=\active 	
        \OriginalVerbatim[#1,codes*=\Wrappedbreaksatpunct]%
    }
    \makeatother

    % Exact colors from NB
    \definecolor{incolor}{HTML}{303F9F}
    \definecolor{outcolor}{HTML}{D84315}
    \definecolor{cellborder}{HTML}{CFCFCF}
    \definecolor{cellbackground}{HTML}{F7F7F7}
    
    % prompt
    \makeatletter
    \newcommand{\boxspacing}{\kern\kvtcb@left@rule\kern\kvtcb@boxsep}
    \makeatother
    \newcommand{\prompt}[4]{
        {\ttfamily\llap{{\color{#2}[#3]:\hspace{3pt}#4}}\vspace{-\baselineskip}}
    }
    

    
    % Prevent overflowing lines due to hard-to-break entities
    \sloppy 
    % Setup hyperref package
    \hypersetup{
      breaklinks=true,  % so long urls are correctly broken across lines
      colorlinks=true,
      urlcolor=urlcolor,
      linkcolor=linkcolor,
      citecolor=citecolor,
      }
    % Slightly bigger margins than the latex defaults
    
    \geometry{verbose,tmargin=1in,bmargin=1in,lmargin=1in,rmargin=1in}
    
    

\begin{document}
    
    \maketitle
    
    

    
    \hypertarget{datastream-api-dsws-median-index-data}{%
\section{Datastream API (DSWS) Median Index
Data}\label{datastream-api-dsws-median-index-data}}

    \href{https://developers.refinitiv.com/en/article-catalog/article/dsws-median-index-data}{This
article comes from the Developer Community Portal, where you may find
more such articles.}

In this article, we will create a Python function that will take the
median measure of all (non `NaN') values of a specific field for any
index (or list of indices) of choice using Refinitiv's
\href{https://www.refinitiv.com/en/products/datastream-macroeconomic-analysis}{DataStream}
Web Services (DSWS).

    \hypertarget{contents}{%
\subsection{Contents:}\label{contents}}

\begin{itemize}
\tightlist
\item
  \hyperref[getcoding]{Get Coding}

  \begin{itemize}
  \tightlist
  \item
    \hyperref[importlibraries]{Import Libraries}
  \item
    \hyperref[collectingdata]{Collecting Data: A Simple Example}
  \item
    \hyperref[creatingpythonfunctiontoprogrammaticallycollectdata]{Creating Python Function to programmatically collect data}

    \begin{itemize}
    \tightlist
    \item
      \hyperref[exampletrack_progresandadd_to_global_dftotrue]{Example setting track_progress and add_to_global_DF to True}
    \end{itemize}
  \end{itemize}
\end{itemize}

    \hypertarget{get-coding}{%
\subsection{Get Coding }\label{get-coding}}

    \hypertarget{import-libraries}{%
\subsubsection{Import Libraries }\label{import-libraries}}

    \[ \\ \] For full replication, note that the version of libraries used

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{1}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{k+kn}{import} \PY{n+nn}{sys} \PY{c+c1}{\PYZsh{} \PYZsq{} sys \PYZsq{} is only needed to display our Pyhon version}
\PY{n+nb}{print}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{This code is running on Python version }\PY{l+s+s2}{\PYZdq{}} \PY{o}{+} \PY{n}{sys}\PY{o}{.}\PY{n}{version}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{:}\PY{l+m+mi}{5}\PY{p}{]}\PY{p}{)}
\end{Verbatim}
\end{tcolorbox}

    \begin{Verbatim}[commandchars=\\\{\}]
This code is running on Python version 3.7.7
    \end{Verbatim}

    \[ \\ \] We need to gather our data. Since \textbf{Refinitiv's
\href{https://www.refinitiv.com/en/products/datastream-macroeconomic-analysis}{DataStream}
Web Services (DSWS)} allows for access to ESG data covering nearly 70\%
of global market cap and over 400 metrics, naturally it is more than
appropriate. We can access DSWS via the Python library
``DatastreamDSWS'' that can be installed simply by using
\(\textit{pip install}\).

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{2}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{k+kn}{import} \PY{n+nn}{DatastreamDSWS} \PY{k}{as} \PY{n+nn}{DSWS}

\PY{c+c1}{\PYZsh{} We can use our Refinitiv\PYZsq{}s Datastream Web Socket (DSWS) API keys that allows us to be identified by}
\PY{c+c1}{\PYZsh{} Refinitiv\PYZsq{}s back\PYZhy{}end services and enables us to request (and fetch) data:}
\PY{c+c1}{\PYZsh{} Credentials are placed in a text file so that it may be used in this code without showing it itself.}
\PY{p}{(}\PY{n}{DSWS\PYZus{}username}\PY{p}{,} \PY{n}{DSWS\PYZus{}password}\PY{p}{)} \PY{o}{=} \PY{p}{(}\PY{n+nb}{open}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Datastream\PYZus{}username.txt}\PY{l+s+s2}{\PYZdq{}}\PY{p}{,}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{r}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}\PY{p}{,}
                                  \PY{n+nb}{open}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Datastream\PYZus{}password.txt}\PY{l+s+s2}{\PYZdq{}}\PY{p}{,}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{r}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}\PY{p}{)}

\PY{n}{ds} \PY{o}{=} \PY{n}{DSWS}\PY{o}{.}\PY{n}{Datastream}\PY{p}{(}\PY{n}{username} \PY{o}{=} \PY{n+nb}{str}\PY{p}{(}\PY{n}{DSWS\PYZus{}username}\PY{o}{.}\PY{n}{read}\PY{p}{(}\PY{p}{)}\PY{p}{)}\PY{p}{,}
                     \PY{n}{password} \PY{o}{=} \PY{n+nb}{str}\PY{p}{(}\PY{n}{DSWS\PYZus{}password}\PY{o}{.}\PY{n}{read}\PY{p}{(}\PY{p}{)}\PY{p}{)}\PY{p}{)}

\PY{c+c1}{\PYZsh{} It is best to close the files we opened in order to make sure that we don\PYZsq{}t stop any other}
\PY{c+c1}{\PYZsh{} services/programs from accessing them if they need to.}
\PY{n}{DSWS\PYZus{}username}\PY{o}{.}\PY{n}{close}\PY{p}{(}\PY{p}{)}
\PY{n}{DSWS\PYZus{}password}\PY{o}{.}\PY{n}{close}\PY{p}{(}\PY{p}{)}


\PY{c+c1}{\PYZsh{} \PYZsh{} Alternatively one can use the following:}
\PY{c+c1}{\PYZsh{} import getpass}
\PY{c+c1}{\PYZsh{} dsusername = input()}
\PY{c+c1}{\PYZsh{} dspassword = getpass.getpass()}
\PY{c+c1}{\PYZsh{} ds = DSWS.Datastream(username = dsusername, password = dspassword)}
\end{Verbatim}
\end{tcolorbox}

    The libraries in the cell bellow are native to Python.

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{3}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{k+kn}{import} \PY{n+nn}{calendar} \PY{c+c1}{\PYZsh{} This library will be used to get the last day of any one month.}
\PY{k+kn}{from} \PY{n+nn}{datetime} \PY{k+kn}{import} \PY{n}{date} \PY{c+c1}{\PYZsh{} \PYZsq{} datetime \PYZsq{} and \PYZsq{} date \PYZsq{} is crucial to manipulate dates.}
\PY{k+kn}{import} \PY{n+nn}{datetime} \PY{c+c1}{\PYZsh{} \PYZsq{} datetime \PYZsq{} and \PYZsq{} date \PYZsq{} is crucial to manipulate dates.}
\end{Verbatim}
\end{tcolorbox}

    The libraries in the cell bellow are not native to Python - \emph{id
est} (\emph{i.e.}): they are not installed upon Python's installation.
This means that they have their own version independently of Python's
version used.

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{4}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{k+kn}{import} \PY{n+nn}{dateutil} \PY{c+c1}{\PYZsh{} \PYZsq{} datetime \PYZsq{} and \PYZsq{} date \PYZsq{} is crucial to manipulate dates.}
\PY{k+kn}{import} \PY{n+nn}{numpy} \PY{k}{as} \PY{n+nn}{np}
\PY{k+kn}{import} \PY{n+nn}{pandas} \PY{k}{as} \PY{n+nn}{pd}
\PY{k}{for} \PY{n}{i}\PY{p}{,}\PY{n}{j} \PY{o+ow}{in} \PY{n+nb}{zip}\PY{p}{(}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{dateutil}\PY{l+s+s2}{\PYZdq{}}\PY{p}{,} \PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{np}\PY{l+s+s2}{\PYZdq{}}\PY{p}{,}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{pd}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{p}{,}
               \PY{p}{[} \PY{n}{dateutil}\PY{p}{,}   \PY{n}{np}\PY{p}{,}  \PY{n}{pd}\PY{p}{]}\PY{p}{)}\PY{p}{:}
    \PY{n+nb}{print}\PY{p}{(}\PY{l+s+sa}{f}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{The }\PY{l+s+si}{\PYZob{}}\PY{n}{i}\PY{l+s+si}{\PYZcb{}}\PY{l+s+s2}{ library imported in this code is version: }\PY{l+s+si}{\PYZob{}}\PY{n}{j}\PY{o}{.}\PY{n}{\PYZus{}\PYZus{}version\PYZus{}\PYZus{}}\PY{l+s+si}{\PYZcb{}}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}
\end{Verbatim}
\end{tcolorbox}

    \begin{Verbatim}[commandchars=\\\{\}]
The dateutil library imported in this code is version: 2.8.1
The np library imported in this code is version: 1.18.5
The pd library imported in this code is version: 1.1.4
    \end{Verbatim}

    \hypertarget{collecting-data-a-simple-example}{%
\subsubsection{Collecting Data: A simple Example
}\label{collecting-data-a-simple-example}}

    1st: We have to specify our list of fields. In this example, we have: *
EVT1FD12: Enterprise Value's ForwarD contract with 12 month maturity
(12FRW). * EBT1FD12: Earnings Before Taxes' 12FRW. * EBD1FD12: Earnings
Before Depreciation and amortisation's 12FRW. *
X(CPS1FD12)\emph{X(IBNOSH): product of the Cashflow Per Share amount's
12FRW and the Institutional Brokers Estimate Service( i.e.: I/B/E/S
pulled from datastream's estimate data)`s Number Of Shares. *
X(MV)\textasciitilde{}IBCUR: Market Value IBES currency. * PEFD12:
market share Price to Equity ratio's 12FRW. * SAL1FD12: SALes' 12FRW. }
X(BPS1FD12)*X(IBNOSH): product of the Book value Per Share's 12FRW and
the Institutional Brokers Estimate Service's Number Of Shares.

N.B.: X is the variable, so X(\ldots{})*X(\ldots{}) means that we
multiply them

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{5}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{list\PYZus{}of\PYZus{}fields} \PY{o}{=} \PY{p}{[}\PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{EVT1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{EBT1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{EBD1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(CPS1FD12)*X(IBNOSH)}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
                  \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(MV)\PYZti{}IBCUR}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{PEFD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{SAL1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(BPS1FD12)*X(IBNOSH)}\PY{l+s+s1}{\PYZsq{}}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

    Now that we know the fields that we want to capture, we will ask for
DSWS to collect such data for all constituents of the
\href{https://product.datastream.com/browse/search.aspx?dsid=ZRQW955\&AppGroup=DSAddin\&q=MSWRLD\%24\&prev=99_MSCI+World}{MSCI
World Index}. We need to do a few changed to the mnemonics/tickers used
in the DSWS function ' ds.get\_data `: * We need to add an 'L' at the
start to indicate that we are requesting for the list of the
constituents of the index. * We need to remove `\$' as it is not
recognised by the backend. We need to remove all currency symbols for
this to work. * We need to add the month and year (in mmyy format) at
the end to specify the point in time that we are trying to replicate.
This means that we are capturing data for the list of constituents of
that index on that month. * We need to add `\textbar{}L' at the end to
indicate to the DSWS service that we are requesting data for a list, not
a single object.

N.B.: \texttt{start\ =\ \textquotesingle{}2013-08-31\textquotesingle{}}
collects data from August 2013. If someone was to use
\texttt{ds.get\_data("LMSWRLD0313\textbar{}L",\ start\ =\ \textquotesingle{}2014-08-31\textquotesingle{})},
they'd be collecting data starting in August 2014 for the constituents
listed under the MSWRLD index back in March 2013.

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{6}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{df} \PY{o}{=} \PY{n}{ds}\PY{o}{.}\PY{n}{get\PYZus{}data}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{LMSWRLD0313|L}\PY{l+s+s2}{\PYZdq{}}\PY{p}{,}
                 \PY{p}{[}\PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{NAME}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
                  \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}\PY{p}{]}\PY{p}{,}
                 \PY{n}{start} \PY{o}{=} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{2013\PYZhy{}08\PYZhy{}31}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
                 \PY{n}{kind} \PY{o}{=} \PY{l+m+mi}{0}\PY{p}{)}
\end{Verbatim}
\end{tcolorbox}

    Now that we have stored the data we are looking for in the Python object
`df', we can sort through it:

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{7}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{c+c1}{\PYZsh{} \PYZsq{} df[\PYZdq{}Datatype\PYZdq{}] == \PYZdq{}EVT1FD12\PYZdq{} \PYZsq{} here sieves through \PYZsq{} df \PYZsq{} and only}
\PY{c+c1}{\PYZsh{}    returns data where what is in the outer most square brackets is}
\PY{c+c1}{\PYZsh{}    true, i.e.: where values in the \PYZsq{}Datatype\PYZsq{} column is \PYZsq{}EVT1FD12\PYZsq{}.}
\PY{n}{df}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Datatype}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{EVT1FD12}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{c+c1}{\PYZsh{} Note that \PYZsq{} \PYZdq{}EVT1FD12\PYZdq{} \PYZsq{} is the same as \PYZsq{} list\PYZus{}of\PYZus{}fields[0] \PYZsq{}}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{7}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
     Instrument  Datatype    Value       Dates
1608   MS:65955  EVT1FD12       NA  2013-08-31
1609    MS:1016  EVT1FD12  49373.9  2013-08-31
1610     MS:388  EVT1FD12  52651.6  2013-08-31
1611      MS:10  EVT1FD12  54133.7  2013-08-31
1612   MS:96942  EVT1FD12  77434.2  2013-08-31
{\ldots}         {\ldots}       {\ldots}      {\ldots}         {\ldots}
3211   MS:65552  EVT1FD12  11510.2  2013-08-31
3212    MS:3695  EVT1FD12  6298.67  2013-08-31
3213    MS:3698  EVT1FD12       NA  2013-08-31
3214    MS:4502  EVT1FD12       NA  2013-08-31
3215    MS:2138  EVT1FD12  82122.3  2013-08-31

[1608 rows x 4 columns]
\end{Verbatim}
\end{tcolorbox}
        
    There are a lot of repeated values, let's use ' .unique() ' to only
retrieve unique values within the `Instrument' column:

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{8}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{df}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Instrument}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Instrument}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{o}{.}\PY{n}{unique}\PY{p}{(}\PY{p}{)}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}\PY{p}{]} \PY{c+c1}{\PYZsh{} \PYZsq{} [0] \PYZsq{} here is needed to indicate that we want the 0th unique value in question.}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{8}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
     Instrument  Datatype                Value       Dates
0      MS:65955      NAME  A P MOLLER MAERSK A  2013-08-31
1608   MS:65955  EVT1FD12                   NA  2013-08-31
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{9}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{df}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Datatype}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{9}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
     Instrument  Datatype    Value       Dates
1608   MS:65955  EVT1FD12       NA  2013-08-31
1609    MS:1016  EVT1FD12  49373.9  2013-08-31
1610     MS:388  EVT1FD12  52651.6  2013-08-31
1611      MS:10  EVT1FD12  54133.7  2013-08-31
1612   MS:96942  EVT1FD12  77434.2  2013-08-31
{\ldots}         {\ldots}       {\ldots}      {\ldots}         {\ldots}
3211   MS:65552  EVT1FD12  11510.2  2013-08-31
3212    MS:3695  EVT1FD12  6298.67  2013-08-31
3213    MS:3698  EVT1FD12       NA  2013-08-31
3214    MS:4502  EVT1FD12       NA  2013-08-31
3215    MS:2138  EVT1FD12  82122.3  2013-08-31

[1608 rows x 4 columns]
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{10}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n+nb}{print}\PY{p}{(}\PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}\PY{p}{)} \PY{c+c1}{\PYZsh{} Printing out the field of interest\PYZsq{}s name}
\PY{n}{df}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Datatype}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}\PY{p}{]}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Value}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{!=} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{NA}\PY{l+s+s1}{\PYZsq{}}\PY{p}{]}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Value}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{o}{.}\PY{n}{median}\PY{p}{(}\PY{p}{)} \PY{c+c1}{\PYZsh{} \PYZsq{} .median() \PYZsq{} gets us \PYZhy{} you guessed it \PYZhy{} the median value.}
\end{Verbatim}
\end{tcolorbox}

    \begin{Verbatim}[commandchars=\\\{\}]
EVT1FD12
    \end{Verbatim}

    \begin{Verbatim}[commandchars=\\\{\}]
C:\textbackslash{}Users\textbackslash{}U6082174.TEN\textbackslash{}AppData\textbackslash{}Roaming\textbackslash{}Python\textbackslash{}Python37\textbackslash{}site-
packages\textbackslash{}ipykernel\_launcher.py:2: UserWarning: Boolean Series key will be
reindexed to match DataFrame index.

    \end{Verbatim}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{10}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
11409.6
\end{Verbatim}
\end{tcolorbox}
        
    \hypertarget{creating-python-function-to-programmatically-collect-data}{%
\subsubsection{Creating Python Function to programmatically collect data
}\label{creating-python-function-to-programmatically-collect-data}}

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{11}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{k}{def} \PY{n+nf}{DSWS\PYZus{}Median\PYZus{}Index\PYZus{}Data}\PY{p}{(}\PY{n}{indices} \PY{o}{=} \PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{MSWRLD}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{p}{,}
                           \PY{n}{list\PYZus{}of\PYZus{}fields} \PY{o}{=} \PY{p}{[}\PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{EVT1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{EBT1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{EBD1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(CPS1FD12)*X(IBNOSH)}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
                                             \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(MV)\PYZti{}IBCUR}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{PEFD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{SAL1FD12}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(BPS1FD12)*X(IBNOSH)}\PY{l+s+s1}{\PYZsq{}}\PY{p}{]}\PY{p}{,} \PY{c+c1}{\PYZsh{} Don\PYZsq{}t include non numerical fields like \PYZsq{}GDSCN\PYZsq{}.}
                          \PY{n}{start} \PY{o}{=} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{2013\PYZhy{}01\PYZhy{}01}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
                          \PY{n}{end} \PY{o}{=} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{2021\PYZhy{}01\PYZhy{}31}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
                          \PY{n}{track\PYZus{}progress} \PY{o}{=} \PY{k+kc}{False}\PY{p}{,}
                          \PY{n}{add\PYZus{}to\PYZus{}global\PYZus{}DF} \PY{o}{=} \PY{k+kc}{False}\PY{p}{)}\PY{p}{:}
    \PY{l+s+sd}{\PYZdq{}\PYZdq{}\PYZdq{}}
\PY{l+s+sd}{    \PYZsq{} DSWS\PYZus{}Median\PYZus{}Index\PYZus{}Data \PYZsq{} requests data defined in \PYZsq{} list\PYZus{}of\PYZus{}fields \PYZsq{} from Datastream\PYZsq{}s API \PYZhy{} DataStream Web}
\PY{l+s+sd}{    Services (DSWS) \PYZhy{} for a series of indices of choice \PYZhy{} defined in \PYZsq{}indices\PYZsq{} \PYZhy{} and returns three lists full of Pandas data\PYZhy{}frames:}
\PY{l+s+sd}{    1st \PYZhy{} the raw output from the requests (with columns \PYZsq{}Instrument\PYZsq{}, \PYZsq{}Datatype\PYZsq{}, \PYZsq{}Value\PYZsq{} and \PYZsq{}Dates\PYZsq{});}
\PY{l+s+sd}{    2nd \PYZhy{} the monthly median from the raw output from the requests (with columns of the requested metrics and an index of dates);}
\PY{l+s+sd}{    3rd \PYZhy{} the raw data pulled from the DSWS request (and where issues are most likely to lie).}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    One could re\PYZhy{}write this basing themselves off datetime objects, it would be equivalent; its code may look neater too.}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    indices (list): List of strings of the DSWS mnemonic for the index for which data is requested.}
\PY{l+s+sd}{    Default: indices = [\PYZdq{}MSWRLD\PYZdq{}]}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    list\PYZus{}of\PYZus{}fields (list): List of strings of the DSWS fields we are after. This has to be comprised of 49 elements or less.}
\PY{l+s+sd}{    Don\PYZsq{}t include non numerical fields like \PYZsq{}GDSCN\PYZsq{}. That will result in a printed error}
\PY{l+s+sd}{    Default: list\PYZus{}of\PYZus{}fields = [\PYZsq{}EVT1FD12\PYZsq{}, \PYZsq{}EBT1FD12\PYZsq{}, \PYZsq{}EBD1FD12\PYZsq{}, \PYZsq{}X(CPS1FD12)*X(IBNOSH)\PYZsq{}, \PYZsq{}X(MV)\PYZti{}IBCUR\PYZsq{}, \PYZsq{}PEFD12\PYZsq{}, \PYZsq{}SAL1FD12\PYZsq{}, \PYZsq{}X(BPS1FD12)*X(IBNOSH)\PYZsq{}, \PYZsq{}(X(SAL1FD12)*X(IBUNIT))\PYZsq{}, \PYZsq{}354E(X)\PYZsq{}, \PYZsq{}X(INC1FD12)*X(IBUNIT)\PYZsq{}, \PYZsq{}X(FCF1FD12)*X(IBNOSH)\PYZsq{}, \PYZsq{}X(FCF1FD12)*X(IBNOSH)*X(IBUNIT)\PYZsq{}, \PYZsq{}GDSCN\PYZsq{}]}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    start (str): String of the start date from which we are asking for data in \PYZsq{}yyy\PYZhy{}mm\PYZhy{}dd\PYZsq{} format.}
\PY{l+s+sd}{    Default: start = \PYZsq{}2013\PYZhy{}01\PYZhy{}01\PYZsq{}}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    end (str): String of the end date until which we are asking for data in \PYZsq{}yyy\PYZhy{}mm\PYZhy{}dd\PYZsq{} format.}
\PY{l+s+sd}{    Default: end = \PYZsq{}2021\PYZhy{}01\PYZhy{}31\PYZsq{}}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    track\PYZus{}progress (Boolean): If set to True, the \PYZsq{} DSWS\PYZus{}Median\PYZus{}Index\PYZus{}Data \PYZsq{} function will print out each mnemonic requested of DSWS}
\PY{l+s+sd}{    Default: track\PYZus{}progress = False}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    }
\PY{l+s+sd}{    track\PYZus{}progress (Boolean): If set to True, each string of the transformed index will be printed off \PYZhy{} remember that there is one per month.}
\PY{l+s+sd}{    Default: track\PYZus{}progress = False}
\PY{l+s+sd}{    }
\PY{l+s+sd}{    add\PYZus{}to\PYZus{}global\PYZus{}DF (Boolean): If set to True, on top of returning the 3 lists of Pandas data\PYZhy{}frames described above, this function will append lists named DF, \PYZus{}DF, and debug\PYZus{}df.}
\PY{l+s+sd}{    This does mean that you need to include a line such as \PYZsq{}DF, \PYZus{}DF, debug\PYZus{}df = [], [], []\PYZsq{} beforehand as a result.}
\PY{l+s+sd}{    Default: add\PYZus{}to\PYZus{}global\PYZus{}DF = False}
\PY{l+s+sd}{    \PYZdq{}\PYZdq{}\PYZdq{}}
    
    \PY{c+c1}{\PYZsh{} We would like to keep the name of the companies in question.}
    \PY{k}{if} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{NAME}\PY{l+s+s1}{\PYZsq{}} \PY{o+ow}{not} \PY{o+ow}{in} \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{:}
        \PY{n}{list\PYZus{}of\PYZus{}fields} \PY{o}{=} \PY{p}{[}\PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{NAME}\PY{l+s+s1}{\PYZsq{}}\PY{p}{]} \PY{o}{+} \PY{n}{list\PYZus{}of\PYZus{}fields}
    
    \PY{c+c1}{\PYZsh{} We are often going to need to split our dates into more useful objects, that is what \PYZsq{}Proccess\PYZus{}Date\PYZsq{} does: }
    \PY{k}{def} \PY{n+nf}{Proccess\PYZus{}Date}\PY{p}{(}\PY{n}{date}\PY{p}{)}\PY{p}{:}
        \PY{n}{d} \PY{o}{=} \PY{n}{date}\PY{o}{.}\PY{n}{split}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{\PYZhy{}}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}
        \PY{n}{year}\PY{p}{,} \PY{n}{year\PYZus{}2}\PY{p}{,} \PY{n}{month} \PY{o}{=} \PY{n}{d}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}\PY{p}{,} \PY{n}{d}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}\PY{p}{[}\PY{l+m+mi}{2}\PY{p}{:}\PY{l+m+mi}{4}\PY{p}{]}\PY{p}{,} \PY{n}{d}\PY{p}{[}\PY{l+m+mi}{1}\PY{p}{]}
        \PY{n}{day} \PY{o}{=} \PY{n}{calendar}\PY{o}{.}\PY{n}{monthrange}\PY{p}{(}\PY{n+nb}{int}\PY{p}{(}\PY{n}{year}\PY{p}{)}\PY{p}{,} \PY{n+nb}{int}\PY{p}{(}\PY{n}{month}\PY{p}{)}\PY{p}{)}\PY{p}{[}\PY{l+m+mi}{1}\PY{p}{]} \PY{c+c1}{\PYZsh{} gets last day for that month}
        \PY{k}{return}\PY{p}{(}\PY{n}{year}\PY{p}{,} \PY{n}{year\PYZus{}2}\PY{p}{,} \PY{n}{month}\PY{p}{,} \PY{n}{day}\PY{p}{)}
    
    \PY{c+c1}{\PYZsh{} Finding the number of months between \PYZsq{} start \PYZsq{} and \PYZsq{} end \PYZsq{}.}
    \PY{n}{from\PYZus{}year}\PY{p}{,} \PY{n}{from\PYZus{}year\PYZus{}2}\PY{p}{,} \PY{n}{from\PYZus{}month}\PY{p}{,} \PY{n}{from\PYZus{}day} \PY{o}{=} \PY{n}{Proccess\PYZus{}Date}\PY{p}{(}\PY{n}{date} \PY{o}{=} \PY{n}{start}\PY{p}{)}
    \PY{n}{to\PYZus{}year}\PY{p}{,} \PY{n}{to\PYZus{}year\PYZus{}2}\PY{p}{,} \PY{n}{to\PYZus{}month}\PY{p}{,} \PY{n}{to\PYZus{}day} \PY{o}{=} \PY{n}{Proccess\PYZus{}Date}\PY{p}{(}\PY{n}{date} \PY{o}{=} \PY{n}{end}\PY{p}{)}
    \PY{n}{start\PYZus{}date} \PY{o}{=} \PY{n}{datetime}\PY{o}{.}\PY{n}{datetime}\PY{p}{(}\PY{n+nb}{int}\PY{p}{(}\PY{n}{from\PYZus{}year}\PY{p}{)}\PY{p}{,} \PY{n+nb}{int}\PY{p}{(}\PY{n}{from\PYZus{}month}\PY{p}{)}\PY{p}{,} \PY{n+nb}{int}\PY{p}{(}\PY{n}{from\PYZus{}day}\PY{p}{)}\PY{p}{)}
    \PY{n}{end\PYZus{}date} \PY{o}{=} \PY{n}{datetime}\PY{o}{.}\PY{n}{datetime}\PY{p}{(}\PY{n+nb}{int}\PY{p}{(}\PY{n}{to\PYZus{}year}\PY{p}{)}\PY{p}{,} \PY{n+nb}{int}\PY{p}{(}\PY{n}{to\PYZus{}month}\PY{p}{)}\PY{p}{,} \PY{n+nb}{int}\PY{p}{(}\PY{n}{to\PYZus{}day}\PY{p}{)}\PY{p}{)}
    \PY{n}{num\PYZus{}months} \PY{o}{=} \PY{p}{(}\PY{n}{end\PYZus{}date}\PY{o}{.}\PY{n}{year} \PY{o}{\PYZhy{}} \PY{n}{start\PYZus{}date}\PY{o}{.}\PY{n}{year}\PY{p}{)} \PY{o}{*} \PY{l+m+mi}{12} \PY{o}{+} \PY{p}{(}\PY{n}{end\PYZus{}date}\PY{o}{.}\PY{n}{month} \PY{o}{\PYZhy{}} \PY{n}{start\PYZus{}date}\PY{o}{.}\PY{n}{month}\PY{p}{)} \PY{o}{+} \PY{l+m+mi}{1} \PY{c+c1}{\PYZsh{} \PYZsq{} + 1 \PYZsq{} to include the last month.}
    
    \PY{k}{if} \PY{n}{add\PYZus{}to\PYZus{}global\PYZus{}DF} \PY{o}{==} \PY{k+kc}{True}\PY{p}{:}
        \PY{c+c1}{\PYZsh{} If the user is afraid that the function could fail halfway through,}
        \PY{c+c1}{\PYZsh{}    (s)he can append an existing data\PYZhy{}frame via this if statement.}
        \PY{k}{global} \PY{n}{DF}
        \PY{k}{global} \PY{n}{\PYZus{}DF}
        \PY{k}{global} \PY{n}{debug\PYZus{}df}
    \PY{k}{else}\PY{p}{:}
        \PY{n}{DF}\PY{p}{,} \PY{n}{\PYZus{}DF}\PY{p}{,} \PY{n}{debug\PYZus{}df} \PY{o}{=} \PY{p}{[}\PY{p}{]}\PY{p}{,} \PY{p}{[}\PY{p}{]}\PY{p}{,} \PY{p}{[}\PY{p}{]} \PY{c+c1}{\PYZsh{} These ate the lists of the data\PYZhy{}frames of interest that will be populated in the following loop.}
    
    \PY{k}{for} \PY{n}{a} \PY{o+ow}{in} \PY{n}{indices}\PY{p}{:} \PY{c+c1}{\PYZsh{} Iterating through the list of indices:}
        \PY{n}{df\PYZus{}list} \PY{o}{=} \PY{p}{[}\PY{p}{]} \PY{c+c1}{\PYZsh{} List to be appended/populated with the for loop bellow.}
        \PY{c+c1}{\PYZsh{} for d in range(num\PYZus{}months+2): \PYZsh{} \PYZsq{} +1 \PYZsq{} since the \PYZsq{} range \PYZsq{} function is exclusive with respect to its upper limit, and an additional 1 for go over the month inclusive n the range of the argument.}
        \PY{k}{for} \PY{n}{d} \PY{o+ow}{in} \PY{n+nb}{range}\PY{p}{(}\PY{n}{num\PYZus{}months}\PY{p}{)}\PY{p}{:}
            \PY{n}{\PYZus{}start\PYZus{}date} \PY{o}{=} \PY{n}{start\PYZus{}date} \PY{o}{+} \PY{n}{dateutil}\PY{o}{.}\PY{n}{relativedelta}\PY{o}{.}\PY{n}{relativedelta}\PY{p}{(}\PY{n}{months}\PY{o}{=}\PY{o}{+}\PY{n}{d}\PY{p}{)}
            \PY{n}{from\PYZus{}year}\PY{p}{,} \PY{n}{from\PYZus{}year\PYZus{}2}\PY{p}{,} \PY{n}{from\PYZus{}month}\PY{p}{,} \PY{n}{from\PYZus{}day} \PY{o}{=} \PY{n}{Proccess\PYZus{}Date}\PY{p}{(}\PY{n}{date} \PY{o}{=} \PY{n}{\PYZus{}start\PYZus{}date}\PY{o}{.}\PY{n}{strftime}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{\PYZpc{}}\PY{l+s+s2}{Y\PYZhy{}}\PY{l+s+s2}{\PYZpc{}}\PY{l+s+s2}{m\PYZhy{}}\PY{l+s+si}{\PYZpc{}d}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}\PY{p}{)}

            \PY{k}{if} \PY{n}{track\PYZus{}progress} \PY{o}{==} \PY{k+kc}{True}\PY{p}{:}
                \PY{n+nb}{print}\PY{p}{(}\PY{l+s+sa}{f}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{L}\PY{l+s+si}{\PYZob{}}\PY{n}{a}\PY{l+s+si}{\PYZcb{}}\PY{l+s+si}{\PYZob{}}\PY{n}{from\PYZus{}month}\PY{l+s+si}{\PYZcb{}}\PY{l+s+si}{\PYZob{}}\PY{n}{from\PYZus{}year\PYZus{}2}\PY{l+s+si}{\PYZcb{}}\PY{l+s+s2}{|L}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}

            \PY{n}{df\PYZus{}list}\PY{o}{.}\PY{n}{append}\PY{p}{(}
                \PY{n}{ds}\PY{o}{.}\PY{n}{get\PYZus{}data}\PY{p}{(}
                    \PY{n}{tickers} \PY{o}{=} \PY{l+s+sa}{f}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{L}\PY{l+s+si}{\PYZob{}}\PY{n}{a}\PY{l+s+si}{\PYZcb{}}\PY{l+s+si}{\PYZob{}}\PY{n}{from\PYZus{}month}\PY{l+s+si}{\PYZcb{}}\PY{l+s+si}{\PYZob{}}\PY{n}{from\PYZus{}year\PYZus{}2}\PY{l+s+si}{\PYZcb{}}\PY{l+s+s2}{|L}\PY{l+s+s2}{\PYZdq{}}\PY{p}{,}
                    \PY{n}{fields} \PY{o}{=} \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{,}
                    \PY{n}{start} \PY{o}{=} \PY{n}{\PYZus{}start\PYZus{}date}\PY{o}{.}\PY{n}{strftime}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{\PYZpc{}}\PY{l+s+s2}{Y\PYZhy{}}\PY{l+s+s2}{\PYZpc{}}\PY{l+s+s2}{m\PYZhy{}}\PY{l+s+si}{\PYZpc{}d}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}\PY{p}{,}
                    \PY{n}{kind} \PY{o}{=} \PY{l+m+mi}{0}\PY{p}{)}\PY{p}{)}

        \PY{n}{df} \PY{o}{=} \PY{n}{pd}\PY{o}{.}\PY{n}{concat}\PY{p}{(}\PY{n}{df\PYZus{}list}\PY{p}{)}\PY{o}{.}\PY{n}{reset\PYZus{}index}\PY{p}{(}\PY{n}{drop} \PY{o}{=} \PY{k+kc}{True}\PY{p}{)}
        
        \PY{n}{date\PYZus{}range} \PY{o}{=} \PY{n}{df}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Dates}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{o}{.}\PY{n}{notna}\PY{p}{(}\PY{p}{)}\PY{p}{]}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Dates}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{o}{.}\PY{n}{unique}\PY{p}{(}\PY{p}{)}
        
        \PY{n}{debug\PYZus{}df}\PY{o}{.}\PY{n}{append}\PY{p}{(}\PY{n}{df}\PY{p}{)}
        
        \PY{c+c1}{\PYZsh{} This try loop is in case a field value requests non\PYZhy{}numerical data that would break the code (since a median value could then not be computed).}
        \PY{k}{try}\PY{p}{:}
            \PY{n}{\PYZus{}df} \PY{o}{=} \PY{n}{pd}\PY{o}{.}\PY{n}{DataFrame}\PY{p}{(}
                \PY{n}{data} \PY{o}{=} \PY{p}{[}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Value}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{!=} \PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{NA}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Datatype}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{n}{i}\PY{p}{]}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Dates}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{n}{j}\PY{p}{]}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Value}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{o}{.}\PY{n}{median}\PY{p}{(}\PY{p}{)}
                         \PY{k}{for} \PY{n}{i} \PY{o+ow}{in} \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{[}\PY{l+m+mi}{1}\PY{p}{:}\PY{p}{]}\PY{p}{]} \PY{k}{for} \PY{n}{j} \PY{o+ow}{in} \PY{n}{date\PYZus{}range}\PY{p}{]}\PY{p}{,} \PY{c+c1}{\PYZsh{} \PYZsq{} list\PYZus{}of\PYZus{}fields[1:] \PYZsq{} as opposed to \PYZsq{} list\PYZus{}of\PYZus{}fields \PYZsq{} because we don\PYZsq{}t want \PYZsq{}NAME\PYZsq{}.}
                \PY{n}{columns} \PY{o}{=} \PY{n}{pd}\PY{o}{.}\PY{n}{MultiIndex}\PY{o}{.}\PY{n}{from\PYZus{}product}\PY{p}{(}\PY{p}{[}\PY{p}{[}\PY{n}{a}\PY{p}{]}\PY{p}{,} \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{[}\PY{l+m+mi}{1}\PY{p}{:}\PY{p}{]}\PY{p}{]}\PY{p}{,}
                                                     \PY{n}{names} \PY{o}{=} \PY{p}{[}\PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{Index}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{Metrics}\PY{l+s+s1}{\PYZsq{}}\PY{p}{]}\PY{p}{)}\PY{p}{,}
                \PY{n}{index} \PY{o}{=} \PY{n}{date\PYZus{}range}\PY{p}{)}
        \PY{k}{except}\PY{p}{:}
            \PY{k}{for} \PY{n}{i} \PY{o+ow}{in} \PY{n}{list\PYZus{}of\PYZus{}fields}\PY{p}{[}\PY{l+m+mi}{1}\PY{p}{:}\PY{p}{]}\PY{p}{:}
                \PY{k}{for} \PY{n}{j} \PY{o+ow}{in} \PY{n}{date\PYZus{}range}\PY{p}{:}
                    \PY{k}{try}\PY{p}{:}
                        \PY{n}{df}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Value}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{!=} \PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{NA}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Datatype}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{n}{i}\PY{p}{]}\PY{p}{[}\PY{n}{df}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Dates}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]} \PY{o}{==} \PY{n}{j}\PY{p}{]}\PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{Value}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{o}{.}\PY{n}{median}\PY{p}{(}\PY{p}{)}
                    \PY{k}{except}\PY{p}{:}
                        \PY{n+nb}{print}\PY{p}{(}\PY{l+s+sa}{f}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{field }\PY{l+s+s2}{\PYZsq{}}\PY{l+s+si}{\PYZob{}}\PY{n}{i}\PY{l+s+si}{\PYZcb{}}\PY{l+s+s2}{\PYZsq{}}\PY{l+s+s2}{ does not return numerical data; a median could thus not be computed for it.}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}
                        \PY{n+nb}{print}\PY{p}{(}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{The program has stopped. Please run it again without this field.}\PY{l+s+s2}{\PYZdq{}}\PY{p}{)}
        
        \PY{n}{DF}\PY{o}{.}\PY{n}{append}\PY{p}{(}\PY{n}{df}\PY{p}{)}
        \PY{n}{\PYZus{}DF}\PY{o}{.}\PY{n}{append}\PY{p}{(}\PY{n}{\PYZus{}df}\PY{p}{)}
    \PY{k}{return} \PY{n}{DF}\PY{p}{,} \PY{n}{\PYZus{}DF}\PY{p}{,} \PY{n}{debug\PYZus{}df}
\end{Verbatim}
\end{tcolorbox}

    \hypertarget{example-setting-track_progress-and-add_to_global_df-to-true}{%
\paragraph{Example setting `track\_progress' and `add\_to\_global\_DF'
to True:
}\label{example-setting-track_progress-and-add_to_global_df-to-true}}

    Note that - in this example - we made sure to normalize all
currency-denominated values to the same currency (USD), otherwise taking
the median value of different currencies wouldn't make much sense.

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{12}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{DF}\PY{p}{,} \PY{n}{\PYZus{}DF}\PY{p}{,} \PY{n}{debug\PYZus{}df} \PY{o}{=} \PY{p}{[}\PY{p}{]}\PY{p}{,} \PY{p}{[}\PY{p}{]}\PY{p}{,} \PY{p}{[}\PY{p}{]}

\PY{n}{test1}\PY{p}{,} \PY{n}{test1\PYZus{}df}\PY{p}{,} \PY{n}{test1\PYZus{}deb\PYZus{}df} \PY{o}{=} \PY{n}{DSWS\PYZus{}Median\PYZus{}Index\PYZus{}Data}\PY{p}{(}
    \PY{n}{indices} \PY{o}{=} \PY{p}{[}\PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{MSWRLD}\PY{l+s+s2}{\PYZdq{}}\PY{p}{,} \PY{l+s+s2}{\PYZdq{}}\PY{l+s+s2}{S\PYZam{}PCOMP}\PY{l+s+s2}{\PYZdq{}}\PY{p}{]}\PY{p}{,}
    \PY{n}{list\PYZus{}of\PYZus{}fields} \PY{o}{=} \PY{p}{[}\PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(EVT1FD12)\PYZti{}USD}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(EBT1FD12)\PYZti{}USD}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(EBD1FD12)\PYZti{}USD}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(CPS1FD12)\PYZti{}USD*X(IBNOSH)}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
                      \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(MV)\PYZti{}USD}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(PEFD12)}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(SAL1FD12)\PYZti{}USD}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{X(BPS1FD12)\PYZti{}USD*X(IBNOSH)}\PY{l+s+s1}{\PYZsq{}}\PY{p}{]}\PY{p}{,}
    \PY{n}{start} \PY{o}{=} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{2013\PYZhy{}01\PYZhy{}01}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
    \PY{n}{end} \PY{o}{=} \PY{l+s+s1}{\PYZsq{}}\PY{l+s+s1}{2013\PYZhy{}03\PYZhy{}01}\PY{l+s+s1}{\PYZsq{}}\PY{p}{,}
    \PY{n}{track\PYZus{}progress} \PY{o}{=} \PY{k+kc}{True}\PY{p}{,}
    \PY{n}{add\PYZus{}to\PYZus{}global\PYZus{}DF} \PY{o}{=} \PY{k+kc}{True}\PY{p}{)}
\end{Verbatim}
\end{tcolorbox}

    \begin{Verbatim}[commandchars=\\\{\}]
LMSWRLD0113|L
LMSWRLD0213|L
LMSWRLD0313|L
    \end{Verbatim}

    \begin{Verbatim}[commandchars=\\\{\}]
C:\textbackslash{}Users\textbackslash{}U6082174.TEN\textbackslash{}AppData\textbackslash{}Roaming\textbackslash{}Python\textbackslash{}Python37\textbackslash{}site-
packages\textbackslash{}ipykernel\_launcher.py:96: UserWarning: Boolean Series key will be
reindexed to match DataFrame index.
    \end{Verbatim}

    \begin{Verbatim}[commandchars=\\\{\}]
LS\&PCOMP0113|L
LS\&PCOMP0213|L
LS\&PCOMP0313|L
    \end{Verbatim}

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{13}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{test1}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{13}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
      Instrument                   Datatype                Value       Dates
0       MS:65955                       NAME  A P MOLLER MAERSK A  2013-01-31
1        MS:1016                       NAME  A P MOLLER MAERSK B  2013-01-31
2         MS:388                       NAME            ABB LTD N  2013-01-31
3          MS:10                       NAME  ABBOTT LABORATORIES  2013-01-31
4       MS:96942                       NAME               ABBVIE  2013-01-31
{\ldots}          {\ldots}                        {\ldots}                  {\ldots}         {\ldots}
43447   MS:65552  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)               6266.1  2013-03-31
43448    MS:3695  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              3074.03  2013-03-31
43449    MS:3698  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              34543.6  2013-03-31
43450    MS:4502  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              4837.31  2013-03-31
43451    MS:2138  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              20133.9  2013-03-31

[43452 rows x 4 columns]
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{14}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{test1\PYZus{}df}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{14}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
Index               MSWRLD                                  \textbackslash{}
Metrics    X(EVT1FD12)\textasciitilde{}USD X(EBT1FD12)\textasciitilde{}USD X(EBD1FD12)\textasciitilde{}USD
2013-01-31       9768.0295        1008.731       1159.4745
2013-02-28       9748.7150         993.057       1166.6150
2013-03-31       9876.2530        1000.378       1151.1720

Index                                                                     \textbackslash{}
Metrics    X(CPS1FD12)\textasciitilde{}USD*X(IBNOSH) X(MV)\textasciitilde{}USD X(PEFD12) X(SAL1FD12)\textasciitilde{}USD
2013-01-31                 1033.7630  9083.045   13.9340       5136.3315
2013-02-28                 1045.0710  9107.255   14.3305       5113.3065
2013-03-31                 1037.7785  9345.155   14.8205       5117.3000

Index
Metrics    X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)
2013-01-31                 5321.7885
2013-02-28                 5254.4770
2013-03-31                 5243.3455
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{15}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{test1\PYZus{}df}\PY{p}{[}\PY{l+m+mi}{1}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{15}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
Index              S\&PCOMP                                  \textbackslash{}
Metrics    X(EVT1FD12)\textasciitilde{}USD X(EBT1FD12)\textasciitilde{}USD X(EBD1FD12)\textasciitilde{}USD
2013-01-31        14746.49        1403.990       1956.5220
2013-02-28        15450.20        1404.525       1910.5655
2013-03-31        15799.75        1411.040       1921.3090

Index                                                                      \textbackslash{}
Metrics    X(CPS1FD12)\textasciitilde{}USD*X(IBNOSH)  X(MV)\textasciitilde{}USD X(PEFD12) X(SAL1FD12)\textasciitilde{}USD
2013-01-31                 1353.3355  13275.135   14.0380        9011.652
2013-02-28                 1371.0870  13112.900   14.4570        9073.121
2013-03-31                 1368.2955  13821.085   14.8685        9089.930

Index
Metrics    X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)
2013-01-31                  5988.997
2013-02-28                  5870.180
2013-03-31                  5936.011
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{16}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{test1\PYZus{}deb\PYZus{}df}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{16}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
      Instrument                   Datatype                Value       Dates
0       MS:65955                       NAME  A P MOLLER MAERSK A  2013-01-31
1        MS:1016                       NAME  A P MOLLER MAERSK B  2013-01-31
2         MS:388                       NAME            ABB LTD N  2013-01-31
3          MS:10                       NAME  ABBOTT LABORATORIES  2013-01-31
4       MS:96942                       NAME               ABBVIE  2013-01-31
{\ldots}          {\ldots}                        {\ldots}                  {\ldots}         {\ldots}
43447   MS:65552  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)               6266.1  2013-03-31
43448    MS:3695  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              3074.03  2013-03-31
43449    MS:3698  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              34543.6  2013-03-31
43450    MS:4502  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              4837.31  2013-03-31
43451    MS:2138  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              20133.9  2013-03-31

[43452 rows x 4 columns]
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{17}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{DF}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{17}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
      Instrument                   Datatype                Value       Dates
0       MS:65955                       NAME  A P MOLLER MAERSK A  2013-01-31
1        MS:1016                       NAME  A P MOLLER MAERSK B  2013-01-31
2         MS:388                       NAME            ABB LTD N  2013-01-31
3          MS:10                       NAME  ABBOTT LABORATORIES  2013-01-31
4       MS:96942                       NAME               ABBVIE  2013-01-31
{\ldots}          {\ldots}                        {\ldots}                  {\ldots}         {\ldots}
43447   MS:65552  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)               6266.1  2013-03-31
43448    MS:3695  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              3074.03  2013-03-31
43449    MS:3698  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              34543.6  2013-03-31
43450    MS:4502  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              4837.31  2013-03-31
43451    MS:2138  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              20133.9  2013-03-31

[43452 rows x 4 columns]
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{18}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{\PYZus{}DF}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{18}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
Index               MSWRLD                                  \textbackslash{}
Metrics    X(EVT1FD12)\textasciitilde{}USD X(EBT1FD12)\textasciitilde{}USD X(EBD1FD12)\textasciitilde{}USD
2013-01-31       9768.0295        1008.731       1159.4745
2013-02-28       9748.7150         993.057       1166.6150
2013-03-31       9876.2530        1000.378       1151.1720

Index                                                                     \textbackslash{}
Metrics    X(CPS1FD12)\textasciitilde{}USD*X(IBNOSH) X(MV)\textasciitilde{}USD X(PEFD12) X(SAL1FD12)\textasciitilde{}USD
2013-01-31                 1033.7630  9083.045   13.9340       5136.3315
2013-02-28                 1045.0710  9107.255   14.3305       5113.3065
2013-03-31                 1037.7785  9345.155   14.8205       5117.3000

Index
Metrics    X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)
2013-01-31                 5321.7885
2013-02-28                 5254.4770
2013-03-31                 5243.3455
\end{Verbatim}
\end{tcolorbox}
        
    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{19}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{debug\PYZus{}df}\PY{p}{[}\PY{l+m+mi}{0}\PY{p}{]}
\end{Verbatim}
\end{tcolorbox}

            \begin{tcolorbox}[breakable, size=fbox, boxrule=.5pt, pad at break*=1mm, opacityfill=0]
\prompt{Out}{outcolor}{19}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
      Instrument                   Datatype                Value       Dates
0       MS:65955                       NAME  A P MOLLER MAERSK A  2013-01-31
1        MS:1016                       NAME  A P MOLLER MAERSK B  2013-01-31
2         MS:388                       NAME            ABB LTD N  2013-01-31
3          MS:10                       NAME  ABBOTT LABORATORIES  2013-01-31
4       MS:96942                       NAME               ABBVIE  2013-01-31
{\ldots}          {\ldots}                        {\ldots}                  {\ldots}         {\ldots}
43447   MS:65552  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)               6266.1  2013-03-31
43448    MS:3695  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              3074.03  2013-03-31
43449    MS:3698  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              34543.6  2013-03-31
43450    MS:4502  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              4837.31  2013-03-31
43451    MS:2138  X(BPS1FD12)\textasciitilde{}USD*X(IBNOSH)              20133.9  2013-03-31

[43452 rows x 4 columns]
\end{Verbatim}
\end{tcolorbox}
        
    You can find information inscribed inbetween the triple double quotes
(\emph{i.e.}:""" """) above with the Python functino ' help() ':

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{20}{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]
\PY{n}{help}\PY{p}{(}\PY{n}{DSWS\PYZus{}Median\PYZus{}Index\PYZus{}Data}\PY{p}{)}
\end{Verbatim}
\end{tcolorbox}

    \begin{Verbatim}[commandchars=\\\{\}]
Help on function DSWS\_Median\_Index\_Data in module \_\_main\_\_:

DSWS\_Median\_Index\_Data(indices=['MSWRLD'], list\_of\_fields=['EVT1FD12',
'EBT1FD12', 'EBD1FD12', 'X(CPS1FD12)*X(IBNOSH)', 'X(MV)\textasciitilde{}IBCUR', 'PEFD12',
'SAL1FD12', 'X(BPS1FD12)*X(IBNOSH)'], start='2013-01-01', end='2021-01-31',
track\_progress=False, add\_to\_global\_DF=False)
    ' DSWS\_Median\_Index\_Data ' requests data defined in ' list\_of\_fields ' from
Datastream's API - DataStream Web
    Services (DSWS) - for a series of indices of choice - defined in 'indices' -
and returns three lists full of Pandas data-frames:
    1st - the raw output from the requests (with columns 'Instrument',
'Datatype', 'Value' and 'Dates');
    2nd - the monthly median from the raw output from the requests (with columns
of the requested metrics and an index of dates);
    3rd - the raw data pulled from the DSWS request (and where issues are most
likely to lie).

    One could re-write this basing themselves off datetime objects, it would be
equivalent; its code may look neater too.

    indices (list): List of strings of the DSWS mnemonic for the index for which
data is requested.
    Default: indices = ["MSWRLD"]

    list\_of\_fields (list): List of strings of the DSWS fields we are after. This
has to be comprised of 49 elements or less.
    Don't include non numerical fields like 'GDSCN'. That will result in a
printed error
    Default: list\_of\_fields = ['EVT1FD12', 'EBT1FD12', 'EBD1FD12',
'X(CPS1FD12)*X(IBNOSH)', 'X(MV)\textasciitilde{}IBCUR', 'PEFD12', 'SAL1FD12',
'X(BPS1FD12)*X(IBNOSH)', '(X(SAL1FD12)*X(IBUNIT))', '354E(X)',
'X(INC1FD12)*X(IBUNIT)', 'X(FCF1FD12)*X(IBNOSH)',
'X(FCF1FD12)*X(IBNOSH)*X(IBUNIT)', 'GDSCN']

    start (str): String of the start date from which we are asking for data in
'yyy-mm-dd' format.
    Default: start = '2013-01-01'

    end (str): String of the end date until which we are asking for data in
'yyy-mm-dd' format.
    Default: end = '2021-01-31'

    track\_progress (Boolean): If set to True, the ' DSWS\_Median\_Index\_Data '
function will print out each mnemonic requested of DSWS
    Default: track\_progress = False


    track\_progress (Boolean): If set to True, each string of the transformed
index will be printed off - remember that there is one per month.
    Default: track\_progress = False

    add\_to\_global\_DF (Boolean): If set to True, on top of returning the 3 lists
of Pandas data-frames described above, this function will append lists named DF,
\_DF, and debug\_df.
    This does mean that you need to include a line such as 'DF, \_DF, debug\_df =
[], [], []' beforehand as a result.
    Default: add\_to\_global\_DF = False

    \end{Verbatim}

    \begin{tcolorbox}[breakable, size=fbox, boxrule=1pt, pad at break*=1mm,colback=cellbackground, colframe=cellborder]
\prompt{In}{incolor}{ }{\boxspacing}
\begin{Verbatim}[commandchars=\\\{\}]

\end{Verbatim}
\end{tcolorbox}


    % Add a bibliography block to the postdoc
    
    
    
\end{document}
