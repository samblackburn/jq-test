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
