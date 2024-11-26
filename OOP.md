
## 객체 생성 방법
### 객체  리터링
 -  가장 기본적인 객체 생성 방식
 ``` JavaScript
 const person = { 
	 name: "Alice", 
	 age: 25, 
	 greet: function () { 
		 console.log(`Hello, my name is ${this.name}`); 
	},
};
person.greet(); // Hello, my name is Alice
```

### 생성자 함수 
 -  객체를 생성하기 위한 템플릿처럼 사용
 ``` JavaScript
 function Person(name, age) {
  this.name = name;
  this.age = age;
}

const alice = new Person("Alice", 25);
console.log(alice.name); // Alice 
```



## 프로토타입과 상속
### 프로토 타입이란?
-  JavaScript는 프로토타입 기반 언어 
- 객체는 자신의 **프로토타입**을 통해 다른 객체의 프로퍼티와 메서드를 상속받을 수 있음
``` JavaScript
const animal = {
  speak: function () {
    console.log("Animal makes a sound");
  },
};

const dog = Object.create(animal);
dog.speak(); // Animal makes a sound
```

### 프로토타입 상속
- 프로토타입 체인을 활용한 상속
``` JavaScript
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function () {
  console.log(`${this.name} makes a sound`);
};

const dog = new Animal("Dog");
dog.speak(); // Dog makes a sound
```

## 클래스 선언
### 클래스 선언
 - ES6부터 도입된 ```class```문법
 ```JavaScript
 class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const alice = new Person("Alice", 25);
alice.greet(); // Hello, my name is Alice
```

### 클래스 상속
- ```extends```키워드를 사용하여 클래스 상속 가능
``` JavaScript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a sound`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks`);
  }
}

const dog = new Dog("Dog");
dog.speak(); // Dog barks
```



## ```this```의 동작 원리 
### ```this```란?
- 실행 컨텍스트에 따라 달라지는 동적인 참조
- **일반 함수 호출** :  ```this```는 ```undefined``` 또는 ```window```를 참조
- **메서드 호출** : ```this```는 해당 메서드를 호출한 객체를 참조


### ```this```예제
``` JavaScript
function showThis() {
  console.log(this);
}

showThis(); // undefined (엄격 모드) 또는 window

const obj = {
  name: "Alice",
  showThis: function () {
    console.log(this);
  },
};

obj.showThis(); // obj 객체
```


### ```bind```, ```call```, ```apply```
- ```this```를 명시적으로 바인딩 가능
``` JavaScript
const person = {
  name: "Alice",
};

function greet() {
  console.log(`Hello, ${this.name}`);
}

greet.call(person); // Hello, Alice
greet.apply(person); // Hello, Alice

const boundGreet = greet.bind(person);
boundGreet(); // Hello, Alice
```
