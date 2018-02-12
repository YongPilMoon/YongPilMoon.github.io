### iterable, iterator

- 어떤 객체가 iterable하다 라는 것은 그 객체가 iterable protocol을 구현하였다는 것을 의미한다. 이는 객체가 iterator 객체를 반환하는 [Symbol.iterator] 메소드를 구현하고 있음을 의미한다. 
- iterator 객체는 next 메소드를 가지고 있고 이는 다음 값을 나타내는  value와 순회 완료 여부를 나타내는 done속성을 가지고있는 객체를  반환한다. 이러한 스펙을 iterator protocol이라고 한다.
- 기본적으로 배열, String, MAP, SET, DOM data등의 객체에는 [Symbol.iterator]가 구현되어 있고 이러한 객체들은for...of 구문에서 사용이 가능하다.
- for...of 구문은 for...in의 여러 약점(배열 순회시 순서 보장안됨, 프로토타입에 추가된 프로퍼티까지 순회)을 보완하기 위해 ES6에서 추가된 구문이다. 
- 여기서 Symbol은 es6에서 추가된 자료형으로 유니크한 Key값을 생성하기위해 사용된다. 원래는 iterator라는 이름으로[Symbol.iterator]를 명명 할 수 있었지만 기존에 이미 iterator라는 프로퍼티를 정의하여 사용하고 있는 객체들이 있을 수 있으므로 Symbol.iterator를 사용하여 충돌을 피하고 호환성을 증가 시켰다.

그럼 iterator의 존재를 확인해 보자.

```javascript
const arr = [1,2,3];
const it = arr[Symbol.iterator]() // Symbol은 대괄호[]로만 접근 가능하다. 

> it.next()
{ valud: 1, done: flase}
> it.next()
{ valud: 2, done: flase}
> it.next()
{ valud: 3, done: flase}
> it.next()
{ valud: undefined, done: true} // 순회가 끝나면 done은 true값을  갖는다.

```

간단한 iterable 한 객체의 예

```javascript
var zeroesForeverIterator = {
  [Symbol.iterator]: function () {
    return this;
  },
  next: function () {
    return {done: false, value: 0};
  }
};
```

### 일반객체는 iterable 하지 않다

자바스크립트의 일반 객체는 iterable하지않다.

```javascript
	for (const x of {}) { // TypeError: {} is not iterable
		console.log(x);
	}
```
그럼 왜 일반 객체는 iterable 하지 않는가? 그 이유는 다음과 같다.
자바스크립트에서 순회는 2가지로 나눌 수 있다.

1. program 순회: 모든 프로퍼티를 순회하는 것, 그 프로그램의 구조를 파악하는 것을 의미한다.
2. data 순회: 모든 데이터를 순회하는 것, 프로그램을 통해 모든 데이터를 파악하는 것을 의미한다. 

일반 객체를 기본으로 순회하게 하는것은 이 두가지를 섞는것을 의미하고 그 경우에는 다음과 같은 단점이 있다.

1. data 순회로써 모든 프로퍼티를 순회 할 수 없다.
2. program 순회로써 객체를 순회를 하다 그 객체에 데이터가 들어갈 경우 코드가 망가질 수 있다.

일반 객체에서 순회가 필요할때는 Map을 고려 하는것이 좋다.

참고 자료
- http://exploringjs.com/es6/ch_iteration.html#objectEntries 
- https://developer.ibm.com/node/2015/07/16/introduction-to-es6-iterators/
- http://hacks.mozilla.or.kr/2015/08/es6-in-depth-iterators-and-the-for-of-loop/


