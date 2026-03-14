



lsi mmbasic functons

Common MMBasic functions include these groups, though the exact set varies by platform/version:

Category	Examples
Math	ABS(), ASC(), ATN(), COS(), EXP(), INT(), LOG(), RND(), SGN(), SIN(), SQR(), TAN()
String	CHR$(), HEX$(), INSTR(), LCASE$(), LEFT$(), LEN(), MID$(), RIGHT$(), STR$(), UCASE$(), VAL()
Date/Time	DATE$, TIME$
I/O / Hardware	PIN(), ADC()
Serial / Comms	INPUT$()
System / Info	MM.INFO(…), CWD$
File / Misc	EOF(), LOC(), Lof()
A couple of useful points:

In MMBasic, a function returns a value, unlike a command. 

OPTION LIST is a command, not a function. It lists changed permanent option settings at the command prompt. 

The official manuals say the full built-in function list is in the Functions section, and newer ports like PicoMite add platform-specific functions. 

For the full authoritative list, use the official MMBasic manuals and site. 

If you want, I can give you:

a full alphabetic list, or

a table of functions with one-line descriptions.


alphavetical list just function names

Alphabetical list of common/core MMBasic function names from the base language manual:

ABS
ASC
ATN
BIN$
CHR$
CINT
COS
DEG
EOF
EXP
FIELD$
FIX
FORMAT$
HEX$
INKEY$
INP
INPUT$
INSTR
INT
LCASE$
LEFT$
LEN
LOC
LOG
LOOKUP
LTRIM$
MID$
MM.ERRMSG$
MM.INFO$
MM.VER
OCT$
PEEK
POS
RAD
RIGHT$
RND
RTRIM$
SGN
SIN
SPACE$
SQR
STR$
STRING$
TAB$
TAN
UCASE$
VAL

These are from the base MMBasic language and extra ports like PicoMite, Colour Maximite 2, Armmite, etc. add more hardware-specific functions. 

For the authoritative source, the MMBasic Language Manual is here. 

If you want, I can next give you the PicoMite-specific alphabetical function list.


list ms  word replace escaped charaters for new line etc

In Microsoft Word Find/Replace, these are the main special codes:

Meaning	Find/Replace code
Paragraph mark / new line	^p
Manual line break / soft return	^l
Tab	^t
Section break	^b
Page break	^m
Column break	^n
Any character	^?
Any digit	^#
Any letter	^$
Any whitespace	^w
Caret character	^^
Clipboard contents	^c
Em dash	^+
En dash	^=
Nonbreaking hyphen	^-
Optional hyphen	^~
Nonbreaking space	^s
Graphic	^g
Footnote mark	^f
Endnote mark	^e
Field	^d
A few useful examples:

Task	Find	Replace
Double paragraph to single	^p^p	^p
Line breaks to paragraph marks	^l	^p
Tabs to spaces	^t	
Multiple spaces to one	^w	
Notes:

^p = paragraph end

^l = manual line break made with Shift+Enter

In Word, these are usually called special characters or search codes, not escape characters

For formatting searches, Word also supports things like:

^& = replace with found text

Use More >> Special in Find/Replace to insert these without memorising them

I can also give you a complete Word wildcard cheat sheet if that is what you are after.


can notepad++ be configured to highlight function in a .bas file using UDL


Thought for 4s
Yes.

Syntax highlighting for a .bas file can be done with a User Defined Language (UDL) in Notepad++. UDL lets you define keywords, comments, numbers, delimiters, operators, and folding rules. 

Function names can be highlighted by putting them into one of the UDL keyword groups, so things like ABS, MID$, LEFT$, INSTR, etc. can be colored as keywords. UDL supports multiple keyword lists for exactly this kind of token highlighting. 

If by “highlight function” you mean the Function List panel on the side, that is not handled by UDL alone. For that, you also need a Function List parser XML and an overrideMap.xml entry to map your UDL language to that parser. 

So the practical answer is:

Goal	UDL only?	Notes
Color built-in function names	Yes	Add them as keywords in the UDL. 
Color comments/strings/operators	Yes	Native UDL capability. 
Code folding for SUB / FUNCTION / IF...END IF	Yes	UDL has folding definitions. 
Populate the Function List panel	No, not by itself	Needs a separate Function List definition. 
For an MMBasic .bas setup, the usual approach is:

Create a UDL for .bas

Put commands and functions into keyword groups

Define ' or REM comments

Add folding for SUB/END SUB, FUNCTION/END FUNCTION, maybe IF/END IF

Add a separate Function List XML if you want the sidebar to detect routines. 

A likely catch:

If your .bas files could also be VB/VBA/FreeBasic/QBasic-style code, one UDL may be too blunt because the syntax differs. In that case, make a dedicated MMBasic UDL rather than using generic BASIC keywords. This is an inference based on how UDL works by simple token/delimiter rules rather than deep language parsing. 

I can draft a starter MMBasic UDL XML and a matching Function List XML for .bas files.


ok


Thought for 6s
Yes — here is a starter setup for MMBasic .bas in Notepad++:

1) UDL idea
Use a UDL to highlight:

comments: ' and REM

strings: "

operators: + - * / = < > \ ^

keywords:

flow/control: IF, THEN, ELSE, FOR, NEXT, DO, LOOP, SELECT, CASE

declarations: SUB, FUNCTION, END SUB, END FUNCTION, DIM, LOCAL, STATIC

built-in functions: ABS, ASC, ATN, CHR$, COS, EXP, HEX$, INKEY$, INSTR, INT, LCASE$, LEFT$, LEN, LOG, MID$, RIGHT$, RND, SGN, SIN, SQR, STR$, TAN, UCASE$, VAL

UDL supports keyword groups, delimiters, comments and folding, so this part is straightforward. 

2) Function List XML
This is what makes View → Function List show SUB and FUNCTION names.

Create a file like:

%AppData%\Notepad++\functionList\udl_mmbasic.xml

Paste this:

<?xml version="1.0" encoding="UTF-8" ?>
<NotepadPlus>
    <functionList>
        <parser
            id="mmbasic_function"
            displayName="MMBasic"
            commentExpr="(?i)(?:'|REM\b).*?$">
            
            <function
                mainExpr="(?-isx)^[ \t]*(?:SUB|FUNCTION)[ \t]+([A-Za-z_][A-Za-z0-9_\.\$]*)">
                <functionName>
                    <nameExpr expr="(?-isx)([A-Za-z_][A-Za-z0-9_\.\$]*)$" />
                </functionName>
            </function>
            
        </parser>
    </functionList>
</NotepadPlus>
3) overrideMap.xml entry
Then edit:

%AppData%\Notepad++\functionList\overrideMap.xml

Add this inside <associationMap>:

<association id="udl_mmbasic.xml" userDefinedLangName="MMBasic" />
The userDefinedLangName must exactly match your UDL name, and overrideMap.xml is the file used to map a UDL to its Function List parser. 

4) File extension
In your UDL, assign:

bas
to the extension list so .bas files open under that UDL.

5) What this will detect
This parser should pick up lines like:

SUB TestRoutine
FUNCTION CalcTotal(x, y)
FUNCTION MM.MyFunc$
SUB Init_Stuff
6) Limitation
This simple parser assumes the SUB or FUNCTION declaration starts at the beginning of a line with optional spaces. That matches how Notepad++ Function List parsers usually work via regex-based XML rules rather than full language parsing. 

7) Extra regex if you want stricter matching
If you want to ignore commented-out declarations more aggressively, use this mainExpr instead:

mainExpr="(?-isx)^[ \t]*(?!')(?!REM\b)(?:SUB|FUNCTION)[ \t]+([A-Za-z_][A-Za-z0-9_\.\$]*)"
8) Suggested keyword groups for the UDL
You can use groups roughly like this:

Group	Words
Keywords 1	IF THEN ELSE ELSEIF ENDIF FOR NEXT DO LOOP WHILE WEND SELECT CASE TO STEP GOTO GOSUB RETURN
Keywords 2	SUB FUNCTION END DIM LOCAL STATIC CONST AS INTEGER FLOAT STRING
Keywords 3	PRINT INPUT OPEN CLOSE SEEK KILL NAME FILES CHDIR MKDIR RMDIR
Keywords 4	ABS ASC ATN CHR$ COS EXP HEX$ INKEY$ INSTR INT LCASE$ LEFT$ LEN LOG MID$ RIGHT$ RND SGN SIN SQR STR$ TAN UCASE$ VAL
9) Quick path summary
Item	Location
UDL definition	Language menu / UDL dialog
Function List parser XML	%AppData%\Notepad++\functionList\udl_mmbasic.xml
Mapping file	%AppData%\Notepad++\functionList\overrideMap.xml
If you want, I’ll write a complete importable UDL XML next, not just the Function List parser.


describe MMBASIC.XML a UDL for Notepad++ for a git readme.md


Thought for 5s
Here is a clean README.md description you can use for MMBASIC.XML:

# MMBASIC.XML

`MMBASIC.XML` is a **Notepad++ User Defined Language (UDL)** file for editing **MMBasic** source code in `.bas` files.

It provides syntax highlighting for common MMBasic elements such as:

- keywords and control statements
- built-in functions
- comments
- strings
- operators
- numbers

The goal is to make MMBasic programs easier to read and edit inside Notepad++ by applying a BASIC-specific colour scheme and token rules. Notepad++ supports importing UDL XML files directly through its User Defined Language system. :contentReference[oaicite:0]{index=0}

## What it does

- highlights MMBasic language keywords
- highlights built-in functions
- recognises comment styles such as `'` and `REM`
- highlights quoted strings
- improves readability of `.bas` source files

## What it does not do

This file is a **UDL definition**, not a compiler, interpreter, or linter.  
It does not validate code or provide full language parsing. For advanced features such as structured function extraction in the **Function List** panel, Notepad++ uses separate XML parser definitions rather than the UDL file alone. :contentReference[oaicite:1]{index=1}

## Installation

You can install this file in Notepad++ by either:

1. importing it through the **User Defined Language** import option, or
2. copying the XML file into the appropriate Notepad++ UDL configuration folder.

Notepad++ documents both methods in its user manual. :contentReference[oaicite:2]{index=2}

## Notes

- The XML should be saved as **UTF-8** so Notepad++ can read it correctly. :contentReference[oaicite:3]{index=3}
- This file is intended for **MMBasic** source editing, not for generic BASIC dialects such as VB, VBA, or FreeBASIC.
A shorter version:

# MMBASIC.XML

`MMBASIC.XML` is a Notepad++ User Defined Language (UDL) file for MMBasic source code.

It adds syntax highlighting for `.bas` files, including keywords, functions, comments, strings, operators, and numbers, making MMBasic programs easier to read and maintain.

This file provides editor highlighting only. It does not compile, validate, or fully parse MMBasic code.
I can also turn this into a more polished GitHub-style README with sections for install, screenshots, and known limitations.


ok

# MMBASIC.XML

`MMBASIC.XML` is a **Notepad++ User Defined Language (UDL)** definition for **MMBasic** source files.

It is intended to improve the editing experience for MMBasic programs by adding syntax highlighting for common language elements used in `.bas` files.

## Features

- Highlights **MMBasic keywords**
- Highlights **built-in functions**
- Recognises **comments**
  - apostrophe comments: `'`
  - `REM` comments
- Highlights **strings**
- Highlights **numbers**
- Highlights **operators**
- Associates the language with **`.bas`** files

## Purpose

This file makes MMBasic source code easier to read and maintain in Notepad++ by applying language-aware colour highlighting to common BASIC constructs.

It is aimed at users writing or maintaining MMBasic programs on platforms such as:

- PicoMite
- Maximite
- Colour Maximite 2
- Armmite
- other MMBasic-compatible systems

## Scope

`MMBASIC.XML` is a **syntax-highlighting definition only**.

It does **not** provide:

- compilation
- linting
- debugging
- semantic parsing
- IntelliSense

For advanced features such as the Notepad++ **Function List** panel, a separate Function List parser XML may also be required.

## Installation

### Import through Notepad++

1. Open **Notepad++**
2. Go to **Language**
3. Select **User Defined Language**
4. Choose **Define your language...**
5. Click **Import**
6. Select `MMBASIC.XML`
7. Restart Notepad++ if required

### File association

After import, associate the UDL with:

```text
.bas
Notes
This UDL is intended for MMBasic, not for all BASIC dialects

Some syntax differences may exist between MMBasic versions and hardware targets

Keyword coverage may be extended over time as needed

Typical Highlighted Elements
Keywords
Examples:

IF
THEN
ELSE
FOR
NEXT
DO
LOOP
SELECT
CASE
SUB
FUNCTION
DIM
LOCAL
CONST
Functions
Examples:

ABS
ASC
ATN
CHR$
COS
EXP
HEX$
INSTR
INT
LEFT$
LEN
MID$
RIGHT$
RND
SIN
SQR
STR$
TAN
VAL
Comments
Examples:

' This is a comment
REM This is also a comment
Why use it
MMBasic source can quickly become hard to scan in a plain-text editor.
This UDL helps by visually separating:

control flow

declarations

built-in functions

literals

comments

That makes code faster to read, review, and debug.

License
Add your preferred license here.

Contributions
Updates to keyword lists, function coverage, and style improvements are welcome.




