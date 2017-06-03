# Event 

Le module event va vous permettre de créer un wrapper et émettre/recevoir des évènements à l'intérieur de celui-ci. La plupart des modules du core NodeJS sont construit autour
de celui-ci pour répondre à l'architecture orienté event-driven. 

- Event-driven ? **Explication et schéma**
 
## Require

```js
const Emitter = require('events'); 
```

## Un premier wrapper

Dans ce chapitre nous allons créer un wrapper d'évènements vraiment très simple et appeler notre évènements toutes les 1 secondes dans un setInterval NodeJS.

```js
const Emitter = require('events'); 

const EventWrapper = new Emitter(); 
EventWrapper.on('sayHello',function() {
    console.log('hello world!');
});

setInterval(function() {
    EventWrapper.emit('sayHello');
},1000); 
```

## Avec une class 

Dans ce chapitre nous allons intégrer notre wrapper à une class.