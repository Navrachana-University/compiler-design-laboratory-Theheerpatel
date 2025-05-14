# Custom Compiler Project

This project implements a customized compiler that translates source code with specialized keywords into three-address code. It uses Flex for lexical analysis and Bison for parsing.

## Requirements

To build and run this project, you'll need:

- Flex (Fast Lexical Analyzer Generator)
- Bison (GNU Parser Generator)
- GCC or another C compiler

## Project Files

- `n.l`: Flex file defining the lexical analyzer for customized keywords
- `n.y`: Bison file defining the grammar and parsing rules
- `main.c`: Main program that handles file I/O
- `input.txt`: Source file with code written using custom keywords
- `Makefile`: Build configuration for make
- `build_win.bat`: Windows build script
- `build_unix.sh`: macOS/Linux build script

## Customized Keywords

The compiler supports the following translations:

- `bataay` → printf
- `jo` → if
- `nahitoh` → else
- `jyasudhi` → while
- `cid` → switch
- `case` → case
- `break` → break

## Three-Address Code Generation

The compiler generates three-address code following these patterns:

### While Loop

```
L: if E==1 goto L1
goto exit
L1: S
goto L
exit:
```

### Switch-Case

```
t = E
if t==1 goto L1
if t==2 goto L2
goto L3
L1: S1
goto exit
L2: S2
goto exit
L3: S3
goto exit
Exit:
```

### If-Else

```
if x < 100 goto L2
goto L3
L3: if x > 200 goto L4
goto exit
L4: if x != y goto L2
goto exit
L2: x = 0
exit:
```

## Building and Running

### macOS and Linux

1. Make the build script executable:
   ```
   chmod +x build_unix.sh
   ```

2. Run the build script:
   ```
   ./build_unix.sh
   ```

This will compile the program and run it, processing `input.txt` and generating `output.txt`.

Alternatively, you can use make:
```
make clean
make
./compiler
```

### Windows

1. Run the batch file:
   ```
   build_win.bat
   ```

Or manually with:
```
flex n.l
bison -y -d n.y
gcc -o compiler lex.yy.c y.tab.c main.c -lfl
.\compiler.exe
```

## Troubleshooting

### Common Issues

1. **Missing Flex/Bison**: Ensure Flex and Bison are installed on your system.

2. **Linking Issues**:
   - On macOS, you might need to use `-ll` instead of `-lfl`
   - On Windows with MinGW, you might need to edit the linking flags
   - If all else fails, try compiling without the flex library:
     ```
     gcc -o compiler lex.yy.c y.tab.c main.c
     ```

3. **Path Issues**: Ensure your terminal is in the project directory when running commands.

## Output

The compiled program will:
1. Read code from `input.txt`
2. Process it according to the defined grammar
3. Generate three-address code in `output.txt`
4. Display the generated code in the terminal