# Vue status hud
## Notice
I am no longer involved in FiveM and apart from the occasional dependency bump this project is unmaintained. PRs highly encouraged!

## Quick start
You need [vue-cli](https://cli.vuejs.org/) 3.x.
```
npm install -g @vue/cli
```
### 1. Clone repo
```
https://github.com/lucianfialhobp/status_hud.git
```

### 2. Install dependencies
```
cd html
npm install
```

### 3. Build
```
npm run build
```

### 4. Add to your resource manifest!
```
...

files {
    'status_hud/dist/index.html'
}

ui_page 'status_hud/dist/index.html'
```
## Commands
### Run locally for development
```
npm run serve
```
