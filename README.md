# Minimalist HUD for GTA V

![Minimalist HUD for GTA V](https://media.discordapp.net/attachments/743527527271628911/760337617798692895/Sem_Titulo-1.jpg)

## Iniciando
Você precisará [vue-cli](https://cli.vuejs.org/) 3.x.
Você precisará [vrp_hud](git@github.com:lucianfialhobp/vrpex_hud.git) || Você precisará [esx_hud](git@github.com:lucianfialhobp/esx_hud.git)

```
npm install -g @vue/cli
```

### 1. Clonando repositório
```
git clone git@github.com:lucianfialhobp/hud.git html
```

### 2. Instalando dependencias

```
cd html
npm install
```

### 3. Build

```
npm run build
```

### 4. Adicione os arquivos dentro seu manifesto
```
...

files {
    'html/dist/index.html'
}

ui_page 'html/dist/index.html'
```
## Commandos
### Rode o serve localmente para desenvolvimento
```
npm run serve
```
