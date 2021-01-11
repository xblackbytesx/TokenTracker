# Token Tracker

A Cryptocurrency Dashboard build with Vue JS, PWA enabled, Binance Websocket API for realtime price, amChart for displaying historical charts, SVG Sparkline Chart and Latest News feed from Cryptocompare site. 
 
## Tech Stacks

- [Vue CLI 3](https://github.com/vuejs/vue-cli)
- [Vue](http://vuejs.org/)
- [Vuex](https://github.com/vuejs/vuex)
- [Vue Router](https://github.com/vuejs/vue-router)
- [Sass](http://sass-lang.com/)
- [Bootstrap 4](https://getbootstrap.com/docs/4.1/getting-started/introduction/)
- [Binance Websocket Stream](https://github.com/binance-exchange/binance-official-api-docs/blob/master/web-socket-streams.md)
- [amcharts](https://www.amcharts.com/)
- [Cryptocompare News Api](https://min-api.cryptocompare.com/)
- [Custom sparkline chart](https://github.com/JayeshLab/vue-crypto-dashboard/blob/master/src/components/Sparkline.vue)
- [Custom Binance Websocket Api](https://github.com/JayeshLab/vue-crypto-dashboard/blob/master/src/services/api.js)
- [Docker](https://docker.com)


## Prerequisites:

- Node/Yarn
- Vue-cli 3.x

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Lints and fixes files
```
yarn run lint
```

### Run your unit tests
```
yarn run test:unit
```

## Docker
This fork has added basic Docker support which is still work in progress.

```
docker build -t tokentracker .
```
```
docker run -d -P --name tokentracker-app -p 3000:80 tokentracker
```

After running these commands you should be able to visit the app by navigation to `http://localhost:3000`.
