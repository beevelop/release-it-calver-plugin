# release-it-calver-plugin

> NOTE: This repository is a maintenance fork focused on reducing CVEs and keeping dependencies and CI up-to-date. No new features will be added in this fork.

## Calender Versioning (calver) plugin for Release It!

This plugin enables Calendar Versioning (calver) with Release It! This is especially useful for application projects in a continuous delivery environment. 

### Installation

This package is not published to npm. Install directly from GitHub:

```bash
# Install from GitHub (recommended)
npm install --save-dev beevelop/release-it-calver-plugin

# Or using the full git URL:
npm install --save-dev git+https://github.com/beevelop/release-it-calver-plugin.git
```

### Configuration

In your [release-it](https://github.com/release-it/release-it) config:

```json
"plugins": {
  "release-it-calver-plugin": {
    "format": "yyyy.mm.minor",
    "increment": "calendar"
  }
}
```

#### Configuration examples:

##### Defaults
```json
{
    "format": "yy.mm.minor",
    "increment": "calendar",
    "fallbackIncrement": "minor"
}
```
##### Output in November and December 2024
```
24.11.0
24.11.1
24.12.1
24.12.2
```

##### Custom
```json
{
    "format": "yyyy.mm.minor",
    "increment": "calendar.minor"
}
```
##### Output in November and December 2024
```
2024.11.0
2024.11.1
2024.12.0
2024.12.1
```

More information on available format tags can be found here: [calver](https://github.com/muratgozel/node-calver)

## Releasing

- Releases should be performed from the `main` branch.
- This package is **not** published to npm; releases are GitHub-only.
- To create a release locally, run:

```bash
# ensure you're on main and working tree is clean
git checkout main
git pull --ff-only

# run the release command
npm run release
```
