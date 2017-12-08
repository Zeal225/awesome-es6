Ok donc pour déclarer des variables, voilà comment on fait :

```javascript
var myVar
let myLet
const myConst
```

#### 1. Quelle est la différence entre les mots clés ```var```, ```let``` et ```const``` ?

- ```let``` :  te permet de modifier, autant de fois que tu veux, la valeur que t'avais mis dedans.
- ```const``` :  le contraire de let, tu pourras pas modifier ce que t'as mis dedans (pas même une seule fois).

```javascript
const person = "Nick";
person = "John" // Déclenchera une erreur, person ne pouvant pas être réassigné
```

```javascript
let person = "Nick";
person = "John";
console.log(person) // "John", le réassignement est permis avec let
```

#### 2.  Pourquoi je n'utilise pas ```var``` ?
C'est  une histoire de **scope** mon gars !

Le **scope** correspond à la portée, le contexte dans lequel des valeurs, expressions sont disponibles, "visibles".

On constate plusieurs comportements anormaux chez ```var```. Parmi lesquels :

```javascript
var myVar
console.log(myVar) // undefined
var myVar = 12
console.log(myVar) // 12
```

Il devrait y avoir une erreur puisque l'on redéclare var. Si on avait mis ```let``` :

```javascript
let myLet
console.log(myLet) // undefined
let myLet = 12 // SyntaxError: Identifier 'myVar' has already been declared
console.log(myLet)
```

Ou encore :

```javascript
for (var i = 0; i < 10; i++) { 
    setTimeout(()=> console.log('This number is ' + i), 1000)   
}
This number is 10
This number is 10
This number is 10
This number is 10
This number is 10
This number is 10
This number is 10
This number is 10
This number is 10
This number is 10

```

Alors qu'avec ```let``` : 

```javascript
for (let i = 0; i < 10; i++) { 
 setTimeout(()=> console.log('This number is ' + i), 1000)   
}
This number is 0
This number is 1
This number is 2
This number is 3
This number is 4
This number is 5
This number is 6
This number is 7
This number is 8
This number is 9
```


Lorsqu'on déclare une variable en dehors des **blocs**, on dit d'elle que c'est une **variable globale**. À l'inverse, lorsqu'elles sont déclarées dans un **sous-bloc**, ce sont des **variables locales**.

- Les **variables globales** sont disponibles à l'intérieur et à l'extérieur de n'importe quel **bloc**.
- Les **variables locales** quand à elles, ne sont disponibles qu'à l'intérieur du **bloc** dans lequel elles ont été déclarées. Et par extension, dans tous les **sous-blocs** de ce **bloc**.

Pourtant avec ```var``` :

```javascript
var age = 42
if (age > 12) {
    var dogYears = age * 7
    // console.log('You are ' + dogYears + ' dog years old')
    // console.log('You are',dogYears,'dog years old')
    console.log(`You are ${dogYears} dog years old`)
    // You are 294 dog years old
}
console.log(dogYears) // 294 
if (dogYears > 45) { // on rentre dans la condition
    console.log("You're an old person")
    // You're an old person
}
```

Alors qu'avec ```let``` :

```javascript
let age = 42
if (age > 12) {
    let dogYears = age * 7
    // console.log('You are ' + dogYears + ' dog years old')
    // console.log('You are',dogYears,'dog years old')
    console.log(`You are ${dogYears} dog years old`)
}
console.log(dogYears) // ReferenceError: dogYears is not defined
if (dogYears > 45) { 
    console.log("You're an old person")
}
```

Toutefois, il y a des choses qui ne changent pas :

```javascript
    // que ce soit var, let ou const
var bool = false
const test = () => {
// function test() { // arrow function ou pas le résultat est le même 
 var bool = true // same result let bool = true
}
test()
console.log(bool) // false
```

Enfin, il y a ce qu'on appel la [*Temporal dead zone*](https://stackoverflow.com/questions/33198849/what-is-the-temporal-dead-zone) ou *TDZ*.

```javascript
console.log(pizza) // undefined
var pizza = '4 fromages'

console.log(pizza) // ReferenceError: pizza is not defined
let pizza = '4 fromages'
```


# **CONCLUSION**

J'utilise ```const``` par défaut, ```let``` si j'en ai vraiment besoin et jamais ```var```