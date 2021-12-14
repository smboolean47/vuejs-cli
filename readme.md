# Guida Vuejs CLI

## Installazione
### Node.js
Installiamo Node.js seguendo le istruzioni riportate sulla documentazione a questo [link](https://nodejs.org/it/download)
verifichiamo la corretta installazione con
```bash
node -v
```
### Vue CLI
 installiamo Vue CLI a livello globale
```bash
npm install -g @vue/cli
```
verifichiamo la corretta installazione con
```bash
vue --version
```

> ⚠️ Utenti Windows
> Chiudere e riaprire il terminare come amministratori e lanciare il seguente comando

```bash
Set-ExecutionPolicy remotesigned
```
## Creazione di un nuovo progetto
Creo la cartella di progetto e la apro con VSCode.
Dal terminale di VSCode lancio
```bash
vue create .
```
### Opzioni da selezionare
- ✅ Manually select features
- ✅ Aggiungo CSS Pre-processors
- ✅  Versione 2.x
- ✅ Sass/SCSS (with dart-sass)
- ✅ ESLint with error prevention only
- ✅ Config for Babel, ESLint ect. in dedicated config files
Per avviare il server di sviluppo:
```bash
npm run serve
```

## Clonazione di un progetto
Dopo aver clonato la repo ed aperto il progetto con VSCode.
Dal terminale di VSCode lancio:
```bash
npm install
```
per installare tutte le dipendenze del progetto.

Per avviare il server di sviluppo:
```bash
npm run serve
```

## Installazione Pacchetti

### Fontawesome
Installo la libreria tramite npm
```bash
npm install --save-dev @fortawesome/fontawesome-free
```

Nel file **main.js** aggiungo gli import della libreria prima della creazione dell'istanza di Vue:
```js
import '@fortawesome/fontawesome-free/css/all.css'
import '@fortawesome/fontawesome-free/js/all.js'
```
Ora posso utilizzare le icone nei miei componenti.

[Link alla Fonte](https://medium.com/front-end-weekly/how-to-use-fon-awesome-5-on-vuejs-project-ff0f28310821)

### Bootstrap 5
TBD

## Sviluppo Locale
Per avviare il server di sviluppo locale
```bash
npm run serve
```

## Building per la produzione
Per buildare il progetto 
```bash
npm run build
```
### Percorsi relativi
Aggiungere un file **vue.config.js** nella root del progetto con la seguente istruzione
```js
module.exports = {
	publicPath: './'
};
```

## Troubleshooting

### Visualizzare immagine con percorso locale salvato nei data del component
Potrebbe capitarci di voler utilizzare il valore di una variabile come src di un tag immagine.

❌ **Esempio non funzionante:**

```html
<template>
    <div>
        <img :src="localImage">
    </div>
</template>

<script>
export default {
    name: 'ComponentName',
    data() {
        return {
            localImage: '../assets/image.png'
        }
    }
}
</script>
```
In questo caso l'immagine non verrebbe visualizzata in quanto Webpack, il module bundler che compila il nostro sorgente in codice comprensibile dal browser, non trasforma correttamente il percorso dell'immagine in /img/image.png.
Per forzare questo comportamento possiamo utilizzare la funzione **require()** passandogli come argomento il percorso all'immagine.

✅ **Esempio funzionante:**
```html
<template>
    <div>
        <img :src="localImage">
    </div>
</template>

<script>
export default {
    name: 'ComponentName',
    data() {
        return {
            localImage: require('../assets/image.png')
        }
    }
}
</script>
```

[Link alla fonte](https://vue-loader.vuejs.org/guide/asset-url.html#transform-rules)