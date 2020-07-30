# LGTM
LGTM is a code analysis platform for development teams to identify vulnerabilities early and prevent them from reaching production.
* [Home Site](https://lgtm.com/#)
* [Help Document](https://lgtm.com/help/lgtm/about-lgtm)


## Supported Programming Languages
* C and C++
* C#
* Go, also known as Golang
* Java
* JavaScript/TypeScript
* Python


## How To Use
1. Login LGTM with github account
1. Add github project to 'My Projects List'
1. After a moment you will get a email from LGTM (the email address associated with github account)
1. Click the link inside the email to see the LGTM project(default tab is the first analysis results)


## Analysis
1. When a new project is added, LGTM analyzes the most recent revision.(for larger projects this may take a few days)
1. Any new commits are analyzed immediately
1. By default, LGTM analysis is only run on the default branch in the repository host


## Project Badges
1. You can copy the badges from LGTM project's integrations tab to README.md


## Integrate LGTM Into CI Workflow [link](https://lgtm.com/help/lgtm/getting-started)
1. If you own or administer a repository that's analyzed by LGTM, you can turn on automated code review for pull requests [Link](https://lgtm.com/help/lgtm/about-automated-code-review)
1. Enabling automated review of pull requests doesn�ft block the merging of pull requests
1. Install The LGTM.com GitHub App [Link](https://lgtm.com/help/lgtm/github-apps-integration#install-github-app)
1. Remove repositories & uninstall the app in github project settings > Integrations > LGTM.com Configure 
1. Deactive the automated code review in LGTM project manage page > Integrations tab > click the management icon in the right of 'Automated code review'


## Queries
1. LGTM runs queries to find problems in code, which are then reported as alerts.
1. You can view some example queries in [Queries Console](https://lgtm.com/query)

Property | Description | Sample
-------------------- | -------------------------------------------- | --------------------------
Query pack           | Pack that the query belongs to               | com.lgtm/java-queries
Query ID             | Query identifier                             | java/useless-tostring-call
Language             | Programming language                         | Java
Severity             | error/warning/recommendation                 | Recommendation
Tags                 | Labels that are used to categorize the query | maintainability
Displayed by default | whether alerts are displayed by default      | No


## How To Customize Queries
1. The technology behind LGTM is CodeQL.Using CodeQL, you can write a query to find a bug in your projects.


## Show/Hide Query Results
1. You can customize how projects are analyzed and how their results are displayed in LGTM by adding an lgtm.yml(configure file)

### Sample1 (show query results in all the queries except bar)
```yaml
queries:
  - exclude: foo
  - include: "*"
  - exclude: bar
```

### Sample2 (show query results in all the queries except bar)
```yaml
queries:
  - include:
      severity: "error"
      tags:
        - "exception"
        - "correctness"
  - include:
      severity: "warning"
  - exclude:
      severity: "warning"
      tags: "readability"
```


## Configure File
1. You must save the file in the root directory of the repository
1. You must call the file either lgtm.yml, or .lgtm.yml if you prefer to hide it
1. If there isn't an in-repository lgtm.yml project configuration file, LGTM uses the system defaults global configuration
1. You can find a template file in [here](https://lgtm.com/static/downloads/lgtm.template.yml)
1. You can test a customize configure file in LGTM project > logs Tab > click 'Test analysis configuration' button

Property | Description | SubProperties
-------------------- | -------------------------------------------- | --------------------------------------------------------------------------
path_classifiers     | modifies file classification                 | tag / - <file-path> / - exclude: <file-path>
queries              | controls which results are displayed         | - exclude: <query> / - include: <query>
extraction           | changes the code extraction process          | prepare / after_prepare / configure(only for C/C++) / before_index / index


