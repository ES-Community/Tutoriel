# Event 

Le module event va vous permettre de créer un "conteneur" et d'émettre/recevoir des évènements à l'intérieur de celui-ci. La plupart des modules du coeur NodeJS sont construit autour
de celui-ci pour répondre à une architecture orienté évènements. 

![Event Driven Architecture Schema](https://github.com/ES-Community/Tutoriels/blob/master/node-modules/event/event_driven.png)

Si vous souhaitez en savoir d'avantage sur ce type d'architecture je vous invite à suivre : [ce lien](https://fr.wikipedia.org/wiki/Architecture_orient%C3%A9e_%C3%A9v%C3%A9nements)
 
## Require

```js
const emitter = require('events'); 
```

## Un premier conteneur

Dans ce chapitre nous allons créer un conteneur d'évènements vraiment très simple et appeler notre évènement toutes les 1 secondes dans une function setInterval : 

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

Pas de limite à ce que vous pouvez définir à l'intérieur de ce conteneur. Néanmoins il est nécessaire de retenir que chaque listener est appelé de manière synchrone et ils seront exécutés dans l'ordre de leur instanciation. 

## Avec une class 

Dans ce chapitre nous allons intégrer un Emitter à une class. Cela va nous permettre tout comme notre conteneur précédemment crée d'envoyer ou de recevoir un ou plusieurs évènements à l'intérieur de notre class.

```js
const emitter = require('events');

class Test extends emitter {
    constructor() {
        super();
    }
}

const A = new Test();
A.on('msg',function(str) {
    console.log(str);
});
A.emit('msg','hello world');
```

Dans cet exemple nous fournissons un argument à notre listener (la function javascript). Il vous est possible de passer plusieurs arguments comme ceci : 

```js
A.emit('msg','a','b','c');
``` 

## Ecouter une seul fois

Dans ce chapitre nous allons voir qu'il est possible d'écouter un évènement une seul fois. Une fois que le listener sera pris en compte il sera supprimé de l'emitter définitivement. 

Reprenons un exemple similaire au premier chapitre et adaptons le légèrement : 

```js
const emitter = require('events'); 

const EventWrapper = new emitter(); 
EventWrapper.once('sayHello',function() {
    console.log('hello world!');
});

EventWrapper.emit('sayHello');
EventWrapper.emit('sayHello');
```

Cet fois si l'évènement sera appelé une seul fois. La deuxième fois le listener précedemment crée à été supprimé lors du premier apelle par l'emitter. 
