# greenfire-project
Windows 10

Node v12.13.1

## Project setup
```
npm install
```
If you don't have Node installed already, grab it from https://nodejs.org/en/download/

You'll need an api key from nomics. Make a file named `.env` in the root of the project with this single line: 

```
VUE_APP_APIKEY=yourkey
```
replacing `yourkey` with your api key

### Compiles and hot-reloads for development
```
npm run electron:serve
```

### Compiles and minifies for production
```
npm run electron:build
```
