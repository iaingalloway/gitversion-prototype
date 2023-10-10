# gitversion-prototype

A test project to try out the gitversion tool.

## Build locally

```bash
docker build --build-arg VERSION="local" -t gitversion-prototype:local ./src
```

## Useful snippets

Initial testing of GitVersion:

```bash
> mkdir gitversion-source-branches && cd gitversion-source-branches && git init
Initialized empty Git repository in /home/iain/repos/gitversion-source-branches/.git/

> echo mode: Mainline > GitVersion.yaml

> git add . && git commit -m "Initial commit" && git tag v1.0.0
[main (root-commit) fb90cf6] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 GitVersion.yaml

> docker run --rm -v "$(pwd):/src" gittools/gitversion /src | grep '"MajorMinorPatch":'
  "MajorMinorPatch": "1.0.0",

> git commit --allow-empty -m "Empty commit"
[main 654fa11] Empty commit

> docker run --rm -v "$(pwd):/src" gittools/gitversion /src | grep '"MajorMinorPatch":'
  "MajorMinorPatch": "1.0.1",

> git checkout -b foo
Switched to a new branch 'foo'

> docker run --rm -v "$(pwd):/src" gittools/gitversion /src | grep '"MajorMinorPatch":'
  "MajorMinorPatch": "1.0.1",

> git commit --allow-empty -m "Empty commit"
[foo 3816e94] Empty commit

> docker run --rm -v "$(pwd):/src" gittools/gitversion /src
{
  "Major": 1,
  "Minor": 0,
  "Patch": 1,
  "PreReleaseTag": "foo.1",
  "PreReleaseTagWithDash": "-foo.1",
  "PreReleaseLabel": "foo",
  "PreReleaseLabelWithDash": "-foo",
  "PreReleaseNumber": 1,
  "WeightedPreReleaseNumber": 1,
  "BuildMetaData": 2,
  "BuildMetaDataPadded": "0002",
  "FullBuildMetaData": "2.Branch.foo.Sha.3816e94527d84b4e024239398c15f84e875a5a85",
  "MajorMinorPatch": "1.0.1",
  "SemVer": "1.0.1-foo.1",
  "LegacySemVer": "1.0.1-foo1",
  "LegacySemVerPadded": "1.0.1-foo0001",
  "AssemblySemVer": "1.0.1.0",
  "AssemblySemFileVer": "1.0.1.0",
  "FullSemVer": "1.0.1-foo.1+2",
  "InformationalVersion": "1.0.1-foo.1+2.Branch.foo.Sha.3816e94527d84b4e024239398c15f84e875a5a85",
  "BranchName": "foo",
  "EscapedBranchName": "foo",
  "Sha": "3816e94527d84b4e024239398c15f84e875a5a85",
  "ShortSha": "3816e94",
  "NuGetVersionV2": "1.0.1-foo0001",
  "NuGetVersion": "1.0.1-foo0001",
  "NuGetPreReleaseTagV2": "foo0001",
  "NuGetPreReleaseTag": "foo0001",
  "VersionSourceSha": "e469c7d420d1711ee685dd57924aa6874fe636ce",
  "CommitsSinceVersionSource": 2,
  "CommitsSinceVersionSourcePadded": "0002",
  "UncommittedChanges": 1,
  "CommitDate": "2023-10-10"
}
```

Get the contents of version.txt from the image:

```bash
docker run --rm -it gitversion-prototype:local cat version.txt
```

Create an empty commit:

```bash
git commit --allow-empty -m "$(date -u +"%Y-%m-%dT%H:%M:%SZ")" && git push
```
