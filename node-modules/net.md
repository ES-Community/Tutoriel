# Net (TCP focus)

Le module net permet de créer un serveur TCP/IPC asynchrone. Un serveur socket va vous permettre de **Compléter** ... 

- [ ] Schéma et exemples de production réel.

## Require 

Pour utiliser le module `Net` il va vous falloir le require comme ceci : 

```js
const net = require('net');
```

## Premier serveur

Pour commencer nous allons créer notre premier serveur socket TCP. Plus tard nous y connecterons nos différents client(s) (utilisateurs ou machines). 

```js
const net = require('net'); 

const server = net.createServer(function(socket) {
    console.log('Nouveau socket initialisé');

    socket.on('data',(buffer) => { // Traitement de la data (buffer).
        console.log(buffer.toString()); // Convertir le buffer en String.
    });

    socket.on('close',() => { // Quand la connexion socket est close. Aucun argument.
        console.log('Socket clos');
    });

    socket.on('error',(error) => { // Retourne un objet <Error>.
        console.log(error.message); // Ont affiche le message d'erreur.
    });
});

server.listen(3000); // Ont écoute sur le port 3000.
```

> Vous noterez l'utlisation de function "arrow" dans l'objectif de conserver le scope parent du serveur socket. Cela va permettre nottament d'enregistrer des nouvelles variables sur le scope de la fonction principale pour les ré-utiliser dans les functions enfants.

Suivre avec **explication sommaire du code**...

## Premier client

Dans cet étape nous allons créer un client en utilisant le même module (net). Nôtre objectif va être de se connecter à nôtre serveur socket précédemment crée. 

```js
const net = require('net'); 

const options = {
    port: 3000
};

const client = net.connect(options,function() {
    console.log('Client connecté avec succès au serveur socket distant'); 
    client.write('Hello world!\n');
});

client.on('data',function(buffer) {
    console.log(buffer.toString());
});

client.on('close',function(had_error) {
    if(had_error) {
        console.log('Une erreur à été rencontré, la connexion au serveur distant à été clos!');
    }
    else {
        console.log('La connexion au serveur distant à été clos!');
    }
});

client.on('error',function(error) {
    console.log(error.message);
});
```

Suivre avec **explication sommaire du code**...