# Event 

Le module event va vous permettre de créer un "conteneur" et émettre/recevoir des évènements à l'intérieur de celui-ci. La plupart des modules du core NodeJS sont construit autour
de celui-ci pour répondre à une architecture orienté évènements. 

- Event-driven ? **Explication et schéma**
 
## Require

```js
const emitter = require('events'); 
```

## Un premier conteneur

Dans ce chapitre nous allons créer un conteneur d'évènements vraiment très simple et appeler notre évènements toutes les 1 secondes dans un setInterval NodeJS.

```js
const emitter = require('events'); 

const EventWrapper = new emitter(); 
EventWrapper.on('sayHello',function() {
    console.log('hello world!');
});

setInterval(function() {
    EventWrapper.emit('sayHello');
},1000); 
```

## Avec une class 

Dans ce chapitre nous allons intégrer un Emitter à une class. Cela va nous permettre tout comme notre conteneur précédemment crée d'envoyer ou de recevoir des évènements à l'intérieur de notre class.

```js
const emitter = require('events');

class Test extends emitter {

    constructor() {
        super();
        process.nextTick(() => {
            this.emit('msg','hello world!');
        });
    }

}

const A = new Test();
A.on('msg',function(str) {
    console.log(str);
});
```