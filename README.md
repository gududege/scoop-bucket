# Scoop Bucket

Scoop manifests for Windows apps built by [gududege](https://github.com/gududege).

## Installation

```powershell
scoop bucket add scoop-bucket https://github.com/gududege/scoop-bucket
```

The bucket name (`scoop-bucket` above) is just a local alias — you can use any name you like.
Then install any manifest from the list below:

```powershell
scoop install scoop-bucket/<app>
```

## Apps

| Manifest | Description | Upstream |
| --- | --- | --- |
| `tool-center` | Desktop app for managing and running CLI tools through a plugin-based UI | [tool-center](https://github.com/gududege/tool-center) |
| `tcp-log-collector` | Multi-connection TCP log collector with a native UI and rotating SQLite storage | [tcp-log-collector](https://github.com/gududege/tcp-log-collector) |
| `node-red-portable` | Self-contained Node-RED bundle with its own Node.js runtime and launcher | [node-red-portable](https://github.com/gududege/node-red-portable) |
| `csv-template-renderer` | Render Liquid templates over CSV rows with a native desktop UI | [csv-template-renderer](https://github.com/gududege/csv-template-renderer) |
| `extractor` | Extract structured data from text with named-group regexes (JSON, CSV or SQLite) | [golang-toolkit/extractor](https://github.com/gududege/golang-toolkit/tree/main/extractor) |
| `tia-scan-calls` | Scan Siemens TIA Portal block files and emit a JSON cross-reference call graph | [golang-toolkit/tia-scan-calls](https://github.com/gududege/golang-toolkit/tree/main/tia-scan-calls) |
| `tia-tree-calls` | Render a call hierarchy tree from the JSON graph produced by tia-scan-calls | [golang-toolkit/tia-tree-calls](https://github.com/gududege/golang-toolkit/tree/main/tia-tree-calls) |
| `cli-print` | Debug helper that prints CLI arguments, environment variables, working directory and exit code | [golang-toolkit/cli-print](https://github.com/gududege/golang-toolkit/tree/main/cli-print) |
| `dotnet-runtime-extractor` | Download .NET SDK archives and extract runtime components | [golang-toolkit/dotnet-runtime-extractor](https://github.com/gududege/golang-toolkit/tree/main/dotnet-runtime-extractor) |
| `track-repository` | Enrich GitHub repository metadata via GraphQL and embed it into an HTML page | [golang-toolkit/track-repository](https://github.com/gududege/golang-toolkit/tree/main/track-repository) |

## Updating

Every manifest declares `checkver` and `autoupdate`, so new upstream releases are detected by Scoop:

```powershell
scoop update
scoop update tool-center
```

The [Excavator](https://github.com/ScoopInstaller/GitHub-Actions) workflow in
`.github/workflows/excavator.yml` also bumps manifests automatically once GitHub Actions are
enabled for this repository.

## Notes

- `tool-center`: the `plugins` directory is shipped with the app bundle and is replaced on
  update. Keep custom plugins outside the Scoop app directory, or back them up before updating.
- `tcp-log-collector`: the `data` directory (config, application logs, SQLite databases) is
  persisted across updates.
- `node-red-portable`: run `node-red` and browse to <http://127.0.0.1:1880/>. Flows and
  settings live in the persistent `data` directory.
- `csv-template-renderer`: the installed executable is named `csv-liquid-renderer.exe`.

## Development

Manifests live in `bucket/`. With [Scoop](https://scoop.sh) and PowerShell installed:

```powershell
# check the latest upstream version of one manifest or all of them
.\bin\checkver.ps1 tool-center
.\bin\checkver.ps1 *

# lint all manifests (requires the BuildHelpers and Pester modules)
.\bin\test.ps1
```

See the [App Manifests](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests) wiki page for
manifest authoring.

## License

The manifests in this bucket are released into the public domain under the [Unlicense](LICENSE).
Each app keeps its own license; see the `license` field of its manifest for details.
