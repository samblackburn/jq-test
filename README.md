# jq-test

Repo to repro what appears to be a bug in bash.

[The GitHub Actions workflow](.github/workflows/test.yml) contains the repro itself:
```
echo 'Console.WriteLine("{ \"Hello World\": [1, 2, 3] }");' > Program.cs
dotnet run | jq
```
## Expected behaviour
`jq` should pretty-print the json array to the workflow run log. [This run](https://github.com/samblackburn/jq-test/actions/runs/5356531849/jobs/9716165600) did not reproduce the issue.

## Observed behaviour
`jq` exits before `dotnet` has produced any output. [This run](https://github.com/samblackburn/jq-test/actions/runs/5356934491) reproduced the issue.

## Root cause

Package | Buggy version | Fixed version | Release notes
------- | ------------- | --------------| --------------
git     | 2.40.1        | 2.41.1        | [here](https://github.com/git-for-windows/build-extra/blob/main/ReleaseNotes.md#changes-since-git-for-windows-v2410-june-1st-2023)
cygwin  | 3.4.6         | 3.4.7         | [here](https://github.com/cygwin/cygwin/commit/e5fcc5837c9594ccb7d0d6f40af69f266f606c5b)
