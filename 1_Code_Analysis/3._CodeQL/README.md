# CodeQL

## QL(Query Language)
1. QL is a logic programming language
1. QL is the powerful query language that underlies CodeQL, which is used to analyze code

### Sample (the result of this query is the number 42)
```QL
from int x, int y
where x = 6 and y = 7
select x * y
```


## CodeQL(Java)

### Sample
```QL
import java

from Parameter p
where not exists(p.getAnAccess())
select p
```


## CodeQL CLI
1. Software developers and security researchers can secure their code using the CodeQL CLI
1. Create a new *CodeQL HOME* directory where you can place the CLI and any queries and libraries you want to use
1. Download CLI from [here](https://github.com/github/codeql-cli-binaries/releases) codeql.zip contains the CLI for all supported platforms such as LGTM
1. unzip CodeQL CLI to CodeQL home directory (*CodeQL HOME*/codeql/...)
1. add CodeQL directory to path (*CodeQL HOME*/ql/...)
1. Obtain CodeQL queries from [CodeQL repository] (https://github.com/github/codeql)
1. Run `codeql resolve languages` to show which languages are available for database creation
1. Run `codeql resolve qlpacks` to show which QL packs the CLI can find


## CodeQL Database [Link](https://help.semmle.com/codeql/codeql-cli/procedures/create-codeql-database.html)
1. You need to create a CodeQL database containing all the data required to run queries on your code
1. Way1: Running `codeql database create <database> --language=<language-identifier>` to create a CodeQL Database
1. Way2: Download CodeQL database from LGTM project > Integrations tab > 'CodeQL databases for local analysis' section


## Analyze project in local
1. Install CodeQL CLI
1. Generate CodeQL Database for your own project
1. Run `codeql database analyze <path-of-CodeQL-database> <path-of-ql-or-ql-suits> --format=<for example csv> --output=<path-of-report-file>` to analyze your project


## Customize CodeQL
1. Create a custom-queries folder
1. Add Customize CodeQL inside the folder
1. Create a test file
1. Run `codeql test run <path-of-custom-queries>`
1. Confirm the test result file (xxx.actual)
1. Since the result is what we expected, we can update the extension to (xxx.expected)
1. Run codeql test again, it will finish by reporting `All 1 tests passed`


## Use CodeQL With Visual Studio
1. Install CodeQL extension in Visual Studio Code [Link](https://help.semmle.com/codeql/codeql-for-vscode/procedures/setting-up.html)
1. Include CodeQL database into Visual Studio
1. Include CodeQL Repository into Visual Studio
1. Right click the CodeQL file select `CodeQL: Run Query` to execute the CodeQL
1. Confirm the analyze results
