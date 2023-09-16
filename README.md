# gitversion-prototype

A test project to try out the gitversion tool.

## Build locally

```bash
docker build --build-arg VERSION="local" -t gitversion-prototype:local ./src
```

## Useful snippets

Get the contents of version.txt from the image:

```bash
docker run --rm -it gitversion-prototype:local cat version.txt
```

Create an empty commit:

```bash
git commit --allow-empty -m "$(date -u +"%Y-%m-%dT%H:%M:%SZ")" && git push
```
