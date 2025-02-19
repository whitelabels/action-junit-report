<div align="center">
  :octocat:
</div>
<h1 align="center">
  action-junit-report
</h1>

<p align="center">
    ... reports JUnit test results as GitHub pull request check.
</p>

<div align="center">
  <img src=".github/images/action.png"/>
</div>

<div align="center">
  <a href="https://github.com/mikepenz/action-junit-report">
		<img src="https://github.com/mikepenz/action-junit-report/workflows/CI/badge.svg"/>
	</a>
</div>
<br />

-------

<p align="center">
    <a href="#whats-included-">What's included 🚀</a> &bull;
    <a href="#setup">Setup 🛠️</a> &bull;
    <a href="#sample-%EF%B8%8F">Sample 🖥️</a> &bull;
    <a href="#contribute-">Contribute 🧬</a> &bull;
    <a href="#license">License 📓</a>
</p>

-------

### What's included 🚀

- Flexible JUnit parser with wide support
- Supports nested test suites
- Blazingly fast execution
- Lighweight
- Rich build log output

This action processes JUnit XML test reports on pull requests and shows the result as a PR check with summary and annotations.

Based on action for [Surefire Reports by ScaCap](https://github.com/ScaCap/action-surefire-report)

## Setup

### Configure the workflow

```yml
name: build
on:
  pull_request:

jobs:
  build:
    name: Build and Run Tests
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v1
      - name: Build and Run Tests
        run: # execute your tests generating test results
      - name: Publish Test Report
        uses: mikepenz/action-junit-report@v3
        if: always() # always run even if the previous step fails
        with:
          report_paths: '**/build/test-results/test/TEST-*.xml'
```

### Inputs

| **Input**      | **Description**                                                                                                                                                       |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `report_paths`    | **Required**. [Glob](https://github.com/actions/toolkit/tree/master/packages/glob) expression to junit report paths. The default is `**/junit-reports/TEST-*.xml`. |
| `token`           | Optional. GitHub token for creating a check run. Set to `${{ github.token }}` by default.                                                                          |
| `exclude_sources` | Optional. Provide `,` seperated array of folders to ignore for source lookup. Defaults to: `/build/,/__pycache__/`                                                  |
| `check_name`      | Optional. Check name to use when creating a check run. The default is `JUnit Test Report`.                                                                         |
| `suite_regex`     | Optional. Regular expression for the named test suites. E.g. `Test*`                                                                                               |
| `commit`          | Optional. The commit SHA to update the status. This is useful when you run it with `workflow_run`.                                                                 |
| `fail_on_failure` | Optional. Fail the build in case of a test failure.                                                                                                                |
| `require_tests`   | Optional. Fail if no test are found..                                                                                                                              |
| `check_retries`         | Optional. If a testcase is retried, ignore the original failure.                                                                                             |
| `check_title_template`  | Optional. Template to configure the title format. Placeholders: {{FILE_NAME}}, {{SUITE_NAME}}, {{TEST_NAME}}.                                                |
| `summary`         | Optional. Additional text to summary output                                                                                                                        |
| `update_check`    | Optional. Uses an alternative API to update checks, use for cases with more than 50 annotations.                                                                   |
| `annotate_only`   | Optional. Will only annotate the results on the files, won't create a check run.                                                                                   |

## Sample 🖥️

<div align="center">
  <img src=".github/images/annotated.png"/>
</div>

<div align="center">
  <img src=".github/images/annotations.png"/>
</div>

## Contribute 🧬

```bash
# Install the dependencies  
$ npm install

# Verify lint is happy
$ npm run lint -- --fix

# Build the typescript and package it for distribution
$ npm run build && npm run package

# Run the tests, use to debug, and test it out
$ npm test
```

### Credits

Original idea and GitHub Actions by: https://github.com/ScaCap/action-surefire-report

## Other actions

- [release-changelog-builder-action](https://github.com/mikepenz/release-changelog-builder-action)
- [xray-action](https://github.com/mikepenz/xray-action/)
- [jira-release-composition-action](https://github.com/mikepenz/jira-release-composite-action)

## License

    Copyright (C) 2022 Mike Penz

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
