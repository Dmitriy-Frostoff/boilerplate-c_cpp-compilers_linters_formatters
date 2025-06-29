# boilerplate-c_cpp-compilers_linters_formatters

It's an boilerplate for usage of `C/C++` and it's `tools` in a future project. Check out the docs below to be in an `actual tune`!

---

### !Important

It was used only at actual `Windows 10 x64` (TODO! check the `Linux`)!

Do all the steps from [C/C++ for Visual Studio Code](https://code.visualstudio.com/docs/languages/cpp) before usage.

**!note:** `eslint, prettier, execa` are **not necessary for C++ project!** (and by the way `husky` with `commitlint` too, but they're very convinient for following `Git-flow` principles).
So just take what you really need from the project.

!Strongly required the next list of tools to be used / installed / present at your PC:

- actual `VSCode` (was tested with v1.96.4);
- [C/C++ for Visual Studio Code](https://github.com/microsoft/vscode-cpptools);
- [C/C++ Extension Pack for Visual Studio Code](https://github.com/microsoft/vscode-cpptools);
- [C/C++ Extension UI Themes for Visual Studio Code](https://github.com/Microsoft/vscode-cpptools);
- [Clangd Extension for Visual Studio Code (for linting)](https://github.com/clangd/vscode-clangd);
- [EditorConfig for Visual Studio Code](https://github.com/editorconfig/editorconfig-vscode);
- [g++](https://gcc.gnu.org/releases.html);
- [gcc](https://gcc.gnu.org/releases.html);
- [gdb](https://www.sourceware.org/gdb/download/);
- [clang, clang++, clang-tidy, clang-format and LLVM tools](https://releases.llvm.org/download.html);

optional:

- [Format Code Action for Visual Studio Code](https://github.com/rohit-gohri/vscode-format-code-action);
- [VS Code ESLint extension](https://github.com/Microsoft/vscode-eslint);
- [Prettier Formatter for Visual Studio Code](https://github.com/prettier/prettier-vscode);

**note:** It's a common practice for `C/C++ languages tools` collect them and place apart of your system (mean `C:/Program Files` etc). E.g. `C:/Tools`. It's expected in the project `C:/Tools` with adding to the Windows 's `path environment variables`.

Currently (`Windows 10 x64`):

- `C:/Tools/msys64/ucrt64/bin` - GCC, the GNU Compiler Collection;
- `C:/Tools/LLVM/bin` - The LLVM Compiler Infrastructure Project;

Also this pathes **must be added** to the **PATH** environment ([How to: Add Tool Locations to the PATH Environment Variable](<https://learn.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/ee537574(v=office.14)>)).

### The boilerplate structure and brief descriptions:

- `.husky` - folder for husky's hooks (with hooks config);
- `.vscode/settings.json` - settings for appropraite work of `C/C++ core` in the project at first and then (optionally) the `ESlint` and `Prettier` VSCode extensions in a project (with a help of `Format Code Action` extension). There're settings and scripts for a usage of the configs (and ignore) files in the project (i.e. links to ones config files) and there's `end-of-line(EOF)` property that is set to `LF` (i.e. `"files.eol": "\n"`);
- `.vscode/launch.json` - settings for `C/C++` code debugging;
- `configs/` - the folder includes config and ignore files for: `ESlint`, `Prettier`, `Commitlint` packages. Currently about ignore files: `node_modules` and a few more folders are ignored (check `.gitignore` file);
- `.editorconfig` - the project common settings (as for now it's as in RSSchool recommended check the [EditorConfig for VS Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) for more.  
  **notice**: `EditorConfig` IDE extension required!);
- `build/` - built binaries of the project (**note**: `build/compile_commands.json` are strongly required for linter!);
- `.gitignore` - exlude `node_modules` and a few more folders from git watching (like `dist` etc, check the file for more);
- `LICENSE.txt` - license file;
- `package.json` - the heart of all.
  Check the scripts (especially, the paths for linting/prettier'ing. Currently: `'./src'`). Scripts already have CLI prefixes to link with config and ignore files;

It's assumed that `C/C++ lang tools` are placed at their own folders inside `C:/Tools/` and added to the `PATH environment variable` of `Windows`! Check the [To add a path to the PATH environment variable](<https://learn.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/ee537574(v=office.14)#to-add-a-path-to-the-path-environment-variable>) for more.

### Compilers usage

- in `VSCode` create new `PowerShell terminal` (`Bash` won't suit, you'll get an error via compilation at Windows [collect2.exe: error: ld returned 116 exit status / when using g++ with git bash and including <iostream>](https://stackoverflow.com/a/78977857/20705648));
- from `cwd` go to the folder with your `*.c` or `*.cpp` (or `C/C++` languages relative) files (e.g. `cd src`);
- create `helloworld.c` with `C` code insdie (don't forget to include headers);
- run `gcc helloworld.c -o helloworld.exe`;
- run your new `.exe` file (e.g. `./helloworld.exe`);
- the result will be in the terminal;

Check [https://code.visualstudio.com/docs/languages/cpp#\_create-a-hello-world-app](https://code.visualstudio.com/docs/languages/cpp) for more;

Also useful [Создание первой программы (RU)](https://metanit.com/cpp/tutorial/1.2.php);

Another way is to use [Code Runner VSCode extenion](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) to ease the compilation and execution processes. Don't forget to check the VSCode settings (**Code-runner: Executor Map**) to set the extension to proper way like this:

```json
 "code-runner.executorMap": {
    "c": "cd $dirWithoutTrailingSlash && clang --target=x86_64-w64-windows-gnu -g -std=c17 $fileName -o $fileNameWithoutExt && ./$fileNameWithoutExt",
    "cpp": "cd $dirWithoutTrailingSlash && clang++ --target=x86_64-w64-windows-gnu -g -std=c++20 $fileName -o $fileNameWithoutExt && ./$fileNameWithoutExt",
 }
```

about **$fileName**, **$fileNameWithoutExt**, **$dirWithoutTrailingSlash** read the `Code Runner` docs.

**Debugging**  
`-g` flag is required for debugging ([VSCode Debug C++: Why does the flow not stop at breakpoint?](https://stackoverflow.com/questions/38417280/vscode-debug-c-why-does-the-flow-not-stop-at-breakpoint));

to ease the debugging process add `.vscode/launch.json`.
the two main settings are:

- `"program"` => e.g. `"program": "${fileDirname}/${fileBasenameNoExtension}.exe",` path to the example_file.exe for debugging
- `"miDebuggerPath"` => e.g. `"miDebuggerPath": "C:\\Tools\\msys64\\ucrt64\\bin\\gdb.exe",`, path to the debugger (currently it's a `gdb`).

`${fileDirname}`, `${fileBasenameNoExtension}` here are `VSCode variables`. Learn about them (**note**: extremely usefull tool!) via [Variables reference with examples (VSCode)](https://code.visualstudio.com/docs/reference/variables-reference);

---

**note!**  
**clang** and **clang++** compilers won't work standalone!!! They're **strongly required libs!!!**, so that's why flag `--target=x86_64-w64-windows-gnu` is must be nested (for actual `Windows` especially)! Otherwise one'll have got the compilation error like this:

```bash
$ clang -std=c17 ./task.c -o task,exe
clang: warning: unable to find a Visual Studio installation; try running Clang from a developer command prompt [-Wmsvc-not-found]
task.c:2:10: fatal error: 'stdio.h' file not found
    2 | #include <stdio.h>
      |          ^~~~~~~~~
1 error generated.
```

check the [using Clang in windows 10 for C/C++](https://stackoverflow.com/a/63914740/20705648) for more.

### Linters, Formatters

it's required to be installed at your PC (and added to the `PATH environment variable` of `Windows`) / in `VSCode` :

- [LLVM](https://releases.llvm.org/) (e.g. `LLVM-20.1.5-win64.exe` and installed to `C:/Tools/LLVM`);
- [clangd for Visual Studio Code](https://github.com/clangd/vscode-clangd);
- [Clang-Format for Visual Studio Code](https://github.com/xaverh/vscode-clang-format);

then add following lines to the `./.vscode/settings.json`

```json
...
 "[c]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "llvm-vs-code-extensions.vscode-clangd"
  },
  "[cpp]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "llvm-vs-code-extensions.vscode-clangd"
  },
  "clangd.path": "C:\\Tools\\LLVM\\bin\\clangd.exe", // path to Clangd, required
  "clangd.arguments": [
    "--log=verbose",  // logs of extension work
    "--pretty", // logs formatting
    "--background-index", // for indexing files
    "--clang-tidy", // use clang-tidy in real time
    "--header-insertion=iwyu", // include headers automatically (or set 'never')
    "--completion-style=detailed",  // autocomplete
    "--enable-config" // required for .clangd config usage
  ],
  "C_Cpp.intelliSenseEngine": "disabled", // disable C/C++
  //  extension intelliSense because we're using the clangd extension.
  // Clangd conflicts with C/C++. Clangd is able "on fly" to show errors.
```

`build/compile_commands.json` are `strongly required` for linter proper work! if they don't exist build binaries via `Cmake` + `Ninja` with

```txt
# enable build/compile_commands.json
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
```

in the `./CMakeLists.txt`.

**note:** Check the paths to `msys64` folder (e.g. `C/Tools/msys64/ucrt64`)!
[`clang-tidy`](https://clang.llvm.org/extra/clang-tidy/) is a `Linter` for `C` and `C++`;

---

**note**  
for technical reasons, `.clang-format`, `.clang-tidy`, `.clangd` configs **work only from the root of the project**.
Do not nest them to the `./configs/`... (**untidy**, don't like that kind).

---

- `./.clang-format` - contains rules for formatting the `C` and `C++` files' code. Feel free to change it as your wish (currently it's a custom K&R style, based on `LLVM` style, but with `IndentWidth: 2` instead of `IndentWidth: 4`).
- `./.clang-tidy` - config for code lintering ([Clang-Tidy docs](https://clang.llvm.org/extra/clang-tidy/). Currently set particularly to `Mozilla` checks with AirBnB style param naming).
- `./.clangd` - config for Clangd VSCode extenion ([clangd teach your editor C++](https://clangd.llvm.org/installation))
  and don't forget about it's settings in the `./.vscode/settings.json`.

`Clangd` works **only with clang, clang++ compilers** (with `--target=x86_64-w64-windows-gnu`), no other way. Check the settings and params at `./.clangd` and via official docs. Also check in the `clangd settings`: `Clangd: Path` => path to the clangd.exe (e.g. `C:\\Tools\\LLVM\\bin\\clangd.exe`) and don't forget to update the extension's databases (or enable `Clangd: Check Updates` in the `Clangd` extension settings).

### Execa usage:

`Execa` is a powerful tool for `NodeJS` based projects. it gives possibility to create `CI/CD` processes and to automate routine actions (like updating and regression testing of the boilerplate / project).

To install `Execa` run (as devDependencies)

```bash
npm i -D execa
```

Check the `configs/execa/main.js` script for details (it update's the boilerplate's packages and create `configs/execa/update-error.log` with result of the process).

for ease of use add the command to the `package.json/scripts`:

```json
"scripts": {
    "update:packages": "node ./configs/execa/main.js"
  },
```

---

**suggestion**:  
one can automate process even more by creating script that update and run regression tesing of all the projects / boilerplates.

e.g. the directory of all projects / boilerplates is `E:/Code learning`. Then create script, let's name it `update_all_packages.mjs` with this logic (**pay attention**: `E:/Code learning` doesn't contain any npm packages! `update_all_packages.mjs` just `import`s `Execa` from the closest existing repo to prevent catalog pollution and bloating!):

<details>
  <summary><b>E:/Code learning/update_all_packages.mjs</b> example (click to view)</summary>

```javascript
import {
  execaNode,
  ExecaError,
} from './boilerplate-eslint-prettier-husky/node_modules/execa/index.js';
import fs from 'fs/promises';
import path from 'path';

/**
 * Write log file with date and `No errors logged.` inner.
 * If `update-error.log` doesn't exist one will be created beside the script
 *
 * @param {string} pathToLogFile - path (absolute is prefered) to the log file
 * @param {string} logMessage - log message for writing into the log file
 *
 * @returns {Promise<void>}
 * @throws Error writing log: ${error.message}
 */
async function writeSuccessLogFile(pathToLogFile, logMessage) {
  try {
    // write logfile beside the script
    await fs.appendFile(
      pathToLogFile,
      `[${new Date().toLocaleString()}]\n No errors logged.\n\n${logMessage}`,
    );
    console.log(`Log has been written to the ${pathToLogFile}`);
  } catch (error) {
    console.error(`Error writing log: ${error.message}`);
  }
}

/**
 * Write log file with date and error message inside.
 * If `update-error.log` doesn't exist one will be created beside the script
 *
 * @param {string} pathToLogFile - path (absolute is prefered) to the log file
 * @param {Error | ExecaError} error - object Error
 *
 * @returns {Promise<void>}
 * @throws Error writing log: ${error.message}
 */
async function writeErrorLogFile(pathToLogFile, error) {
  try {
    // write logfile beside the script
    await fs.appendFile(
      pathToLogFile,
      `[${new Date().toLocaleString()}] ${error.message}${
        (error instanceof ExecaError ? error.stderr : error) ??
        'No stderr available.'
      }\n`,
    );
    console.log(`Log has been written to the ${pathToLogFile}`);
  } catch (error) {
    console.error(`Error writing log: ${error.message}`);
  }
}

/**
 * Execute NodeJS command `node path/to/script.js` for every path in the {@link array}.
 * P.S. independantly to OS.
 *
 * @param {string[]} array - array of paths (strings)
 *    to boilerplate's / project ' s `configs/execa/main(js|ts)`
 * @returns {Promise<string[]>}
 * @throws ExecaError occur: ${error.message} - if error was thrown from the Execa
 * @throws ${error.message} - if error happend in another one case
 */
async function runNodeScript(array) {
  /** @type {string[]} */
  const arrOfLogs = [];

  for (const pathToScript of array) {
    /** @type {string} */
    const pathToScriptNormalized = path.resolve(pathToScript);
    // configs/execa/main.(j|t)s is a folder with execa script (JavaScript or TypeScript one)
    // this sctructure is the same (and must be the same!) in every project / boilerplate
    /** @type {string} */
    const currentScriptCWD = pathToScript.replace(
      /\/configs\/execa\/main\.(j|t)s$/gi,
      '',
    );
    // use `cwd` option to prevent paths problems!!!
    try {
      /**
       * @type {import("./boilerplate-eslint-prettier-husky/node_modules/execa/index.d.ts").Result}
       * @example
       *    string like this:
       *    'start checking for outdated packages...
       *    All packages are up-to-date. Skipping npm update.
       *    Log has been written to the
       *      E:\Code learning\integration-playground__webpack-react-ts\configs\execa\update-error.log'
       */
      const { stdout } = await execaNode(pathToScriptNormalized, {
        cwd: currentScriptCWD,
        verbose: 'full',
        cleanup: true,
      });

      arrOfLogs.push(stdout ?? 'empty stdout');

      console.log(`${currentScriptCWD}: successfully executed!`);
    } catch (error) {
      if (error instanceof ExecaError) {
        console.error(`ExecaError occur: ${error.message}`);
      } else {
        console.error(error.message);
      }
    }
  }

  return arrOfLogs;
}

/**
 * Update the project's | bolerplate's packages and run commands / tests
 * for regression testing and compatibility. If errors occur check the `update-projects-packages.log`
 * or `update-error.log` in the boilerplate's / project's configs/execa/update-error.log
 *
 * @returns {Promise<void>}
 * @throws An error occured: ${error.message}
 */
async function main() {
  const currentDir = path.resolve();

  const logFile = path.resolve(currentDir, `./update-projects-packages.log`);

  /** @type {string[]} */
  const arrOfScriptpaths = [
    './integration-playground__webpack-react-ts/configs/execa/main.js',
    './integration-playground__webpack-react-js/configs/execa/main.js',
    './boilerplate-webpack-gulp-html-scss-ts-components/configs/execa/main.js',
    './boilerplate-webpack-gulp-html-scss-js-components/configs/execa/main.js',
    './design-patterns/configs/execa/main.js',
    './boilerplate-codewars/configs/execa/main.js',
    './boilerplate-eslint-prettier-husky/configs/execa/main.js',
    './boilerplate-jest/configs/execa/main.js',
    './boilerplate-webpack-react-js/configs/execa/main.js',
    './boilerplate-webpack-react-ts/configs/execa/main.js',
    './rs_school/rsschool-cv/configs/execa/main.js',
    './youtube-dl_utility/configs/execa/main.js',
  ];

  // clean up the log file
  await fs.writeFile(logFile, '');

  console.log(`start running updating scripts...`);

  try {
    /** @type {string[]} */
    const logMessage = await runNodeScript(arrOfScriptpaths);

    // write logfile beside the script
    await writeSuccessLogFile(logFile, logMessage.join('\n\n'));
  } catch (error) {
    console.error(`An error occured: ${error.message}`);

    // write logfile beside the script
    await writeErrorLogFile(logFile, error);
  }
}

main();
```

</details>
<br/>

then just run `node update_all_packages.mjs` from the `E:/Code learning` and check logs in the terminal and `E:/Code learning/update-projects-packages.log` for details.

---

`Execa` contains all the necessary types annotations and it's scripts can be written in `TypeScript` ([Execa and TypeScript](https://github.com/sindresorhus/execa/blob/main/docs/typescript.md)). In a next coming releases of `NodeJS` that will support `TypeScript` as native one it will be pretty sweet for usage)

### Integration with [`Connections`](#Connections) links:

To integrate the boilerplate do the following steps (**note**: copy the project structure as is!!!):  
@note all the next pathes are **cwd** relative.  
It's assumed that `LLVM` (with `clang-tidy` and `clang-format`)
is installed in your system and added to the `path environment` => `C:/Tools/LLVM/bin` and compilers are installed:

- `clang`, `clang++` (and `path environment` => `C:/Tools/LLVM/bin`) (must have for `clangd` real time linter, won't work otherwise)
  and `gcc`, `g++`, `gdb` (and `path environment` => `C:/Tools/msys64/ucrt64/bin`)

- copy:  
  `.clang-format`  
  `.clang-tidy`  
  `.clangd`  
  `.editorconfig`  
  `.gitignore`  
  `build`  
  `.vscode`

- check out files and pathes to the compilers / debuggers to suit your system and folders layout!!!  
  (currently => `C:/Tools/`):  
  `.vscode/c_cpp_properties.json`:
  - `configurations...{intelliSenseMode...}`, `configurations...{compilerPath...}`, `configurations...{compileCommands...}`, `configurations...{cStandard...}`, `configurations...{cppStandard...}`

  `.vscode/settings.json`:
  - `"[c]"`, `"[cpp]"`, `"clangd.path"`, `"clangd.arguments"`, `"C_Cpp.default.compilerPath"`

  `.vscode/launch.json`:
  - `"configurations"...{ "miDebuggerPath" }`

  use [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd) and [Doxygen Documentation Generator](https://marketplace.visualstudio.com/items?itemName=cschlosser.doxdocgen) extensions for `VSCode`.

  **optionally** (`TS/JS` linting / formatting, `Husky` for commit messages checking (to suit to `git - flow`)):  
  @note all the next pathes are **cwd** relative.

  copy:
  - `configs`, `.husky`

  install the npm packages:

  ```bash
  npm i -D @commitlint/cli @commitlint/config-conventional eslint-config-airbnb-base eslint-config-prettier eslint eslint-plugin-import execa husky prettier
  ```

copy from `.vscode/settings.json` all the data till `"[c]"...`
use [`format-code-action`](https://marketplace.visualstudio.com/items?itemName=rohit-gohri.format-code-action) extension for `VSCode` (real - time linting and formatting on save).

**With the new packages releases, the ones above can turn to pumpkin, so check'em out with official docs!!!**

### Links:

#### C/C++ tutorials:

- [C (RU)](https://metanit.com/c/);
- [C++ (RU)](https://metanit.com/cpp/);

#### C/C++ compilers:

- [vscode-cpptools](https://github.com/microsoft/vscode-cpptools);
- [C/C++ for Visual Studio Code](https://code.visualstudio.com/docs/languages/cpp);
- [C/C++ for Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools);
- [Clangd Extension for Visual Studio Code (for linting)](https://github.com/clangd/vscode-clangd);
- [gcc official GitHub repo](https://github.com/gcc-mirror/gcc);
- [GCC, the GNU Compiler Collection, official documentation](https://gcc.gnu.org/);
- [GDB: The GNU Project Debugger, official documentation](https://sourceware.org/gdb/);
- [clang, clang++, clang-tidy, clang-format and LLVM tools](https://releases.llvm.org/download.html);
- [VSCode Debug C++: Why does the flow not stop at breakpoint?](https://stackoverflow.com/questions/38417280/vscode-debug-c-why-does-the-flow-not-stop-at-breakpoint);
- [How to setup VS Code for C++ with clangd support?](https://stackoverflow.com/questions/51885784/how-to-setup-vs-code-for-c-with-clangd-support);
- [How can I find out the version of MSYS2 from its bash shell](https://stackoverflow.com/questions/55559604/how-can-i-find-out-the-version-of-msys2-from-its-bash-shell);
- [How to determine the LLVM version?](https://stackoverflow.com/a/76834710/20705648);
- [Variables reference (VSCode settings)](https://code.visualstudio.com/docs/reference/variables-reference);

#### LLVM, Linters, Formatters:

- [LLVM](https://llvm.org/);
- [LLVM (github releases)](https://github.com/llvm/llvm-project/releases);
- [clang, clang++, clang-tidy, clang-format and LLVM tools](https://releases.llvm.org/download.html);
- [clangd for Visual Studio Code](https://github.com/clangd/vscode-clangd);
- [clangd: teach your editor C++](https://clangd.llvm.org/installation);
- [clang-tidy official documentation](https://clang.llvm.org/extra/clang-tidy/);
- [Clang-Format for Visual Studio Code](https://github.com/xaverh/vscode-clang-format);
- [using Clang in windows 10 for C/C++](https://stackoverflow.com/a/63914740/20705648);

#### VSCode usage' links:

- [Using Prettier and ESLint to automate formatting and fixing JavaScript by Rob O'Leary (Feb 11, 2022)](https://blog.logrocket.com/using-prettier-eslint-automate-formatting-fixing-javascript/);

#### ESLint:

- [ESlint official documentation](https://eslint.org/docs/latest/);  
  Changes with ESlint v9.0.0 coming soon! (flat config, ES modules).  
   TODO! Change then the `eslintrc.cjs` => `eslint.config.js` and dig deeper using Docs!
- [VS Code ESLint extension by Microsoft](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint);
- [eslint rules recommended](https://eslint.org/docs/latest/rules/);
- [eslint-config-airbnb-base by airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb-base);
- [eslint-config-airbnb-typescript at npmjs.com](https://www.npmjs.com/package/eslint-config-airbnb-typescript);
- [The official github of the eslint-config-airbnb-typescript](https://github.com/iamturns/eslint-config-airbnb-typescript?tab=readme-ov-file);
- [The official website of typescript-eslint](https://typescript-eslint.io/);
- [The official github of the typescript-eslint](https://github.com/typescript-eslint/typescript-eslint);
- [@typescript-eslint/eslint-plugin at npmjs.com](https://www.npmjs.com/package/@typescript-eslint/eslint-plugin);  
  **note**: deprecated now! Check the typescript-eslint Setup for actual one.
- [@typescript-eslint/parser at npmjs.com](https://www.npmjs.com/package/@typescript-eslint/parser);  
  **note**: deprecated now! Check the typescript-eslint Setup for actual one.
- [Actual typescript-eslint Setup](https://typescript-eslint.io/getting-started/);
- [Legacy typescript-eslint Setup](https://typescript-eslint.io/getting-started/legacy-eslint-setup/);
- [plugin:@typescript-eslint/recommended rules](https://typescript-eslint.io/rules/);
- [the official page of eslint-plugin-import at npmjs.com](https://www.npmjs.com/package/eslint-plugin-import);
- [the official github repo of eslint-plugin-import](https://github.com/import-js/eslint-plugin-import);
- [eslint-config-prettier by prettier](https://github.com/prettier/eslint-config-prettier);
- [In an eslint config, do 'extends' in an 'overrides' replace or do they merge with 'extends' up in the main section?](https://github.com/eslint/eslint/discussions/17174);

#### Prettier:

- [Prettier official documentation](https://prettier.io/docs/en/);
  TODO! Changes coming soon, check the prettier configs;
- [Prettier Formatter for Visual Studio Code by Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode);

#### Husky:

- [Husky official documentation](https://typicode.github.io/husky/);  
  Changes coming soon! New features will take place.
  TODO! Change the husky and commitlint configs!

- [Commitlint official documentation](https://commitlint.js.org/#/);

- [conventional-changelog official documentation for validating commit messages (code worldwide usaging keywords)](/https://github.com/conventional-changelog/commitlint);

#### Execa:

- [Execa at npmjs.com](https://www.npmjs.com/package/execa);
- [Execa official GitHub repo](https://github.com/sindresorhus/execa);
- [Execa official documentation](https://github.com/sindresorhus/execa/blob/main/readme.md#documentation);
- [Execa guide at jsdocs.io](https://www.jsdocs.io/package/execa);
- [Execa tutorial at blog.logrocket.com](https://blog.logrocket.com/running-commands-with-execa-in-node-js/);

#### Connections:

- [to be done!]();

#### done: June 29, 2025
