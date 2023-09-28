# nuget-pack-push-gh-action

GitHub action automatically creates also .snupkg with debug symbols (.pdb) next to the nuget package (.nupkg) file.

```yml
name: CD
on:
  push:
    branches: [main]
jobs:
  nuget-pack-push:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
          token: ${{ secrets.CHECKOUT_WITH_A_SECRET_IF_NEEDED }}
      - uses: ohpensource/nuget-pack-push-gh-action@main
        name: nuget pack and push
        with:
            nuget-feed-source: nuget-repo-name
            nuget-feed-url: https://your_url/index.json
            username: your-username
            password: ${{ secrets.YOUR_PASSWORD }}
            package-project: Project.Name
            include-symbols: true
```

Optional parameters:
* package-folder: "The folder prefix where the project file is. Defaults to ./"
* version-suffix: "The version suffix to append to the package version. This value will be ignored if the package Version is specified. Defaults to empty string."
* version: "The package version. This value will override Version in *.csproj. Defaults to empty string." 
* include-symbols: "Whether to generate .snupkg file with debug symbols (PDB file). Defaults to false."
