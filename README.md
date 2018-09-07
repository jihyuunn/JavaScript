# 1 Promises

프로미스는 자바스크립트 비동기 처리에 사용되는 객체  
( 비동기 처리 : 특정 코드의 처리가 완료될 때까지 기다리지않고 다음 코드를 실행하는 것 )  
#### 프로미스가 왜 필요한지?
비동기처리하는 특성때문에 다음 코드에서 받아야할 데이터를 받지 않고 화면에 처리하려고 하면 오류가 나타나기 때문이다  
이런 문제를 해결하는 것이 프로미스 !   
#### 프로미스의 3가지 상태
* pending 
```javascript
new Promise();
```
new Promise()를 호출시에 펜딩상태가 된다   
* fulfilled
resolve 실행시에 이행하게 되는 것이고 코드를 완료하는 것  
```javascript
new Promise(function(resolve, reject) { 
    resolve();
}); 
```
콜백 함수 인자 -> resolve, reject   
여기에서 처리한 함수의 결과값을 받아서 다음 코드로 넘길 수 있다   
* rejected
reject 실행시에 rejected(실패)상태가 된다   
```javascript
new Promise(function(resolve, reject) { 
    reject();
}); 
```
실패시에는 실패한 이유를 catch()로 받을 수 있다   

# 2 Const vs Let

ES6 이전에는 var이 사용 되었는데 var이라는 것은 function 바깥에서 선언이 되면 globally scoped되고, function안에서
선언이 되면 locally scoped되는 것임   
그래서 나타나는 문제점은 function바깥에서 선언한 var를 function안에서 다른 값으로 선언하면 바깥에서도 바뀌게 된다  
```javascript
var jihyun = 25;
var a = 0;
if (jihyun > 20) {
    var a = 2;
}
console.log(a) //2가 되어버림
```
다른 여러 파트에서도 바뀌게 되기 때문에 여러 버그가 생기게 되었고 이것이 const, let을 만드는 이유가 됨
* let
let은 block바깥에서 선언이 되면 바깥에서 update는 되지만, re-declare되지는 않는다  
그러나 block안에서 선언이 되면 block안에서만 적용이 되기 때문에 같은 이름이라도 사용 가능하다  
```javascript
let favorite = 'choco';
favorite = 'cookie'; //가능(update)

let favorite = 'choco';
let favorite = 'cookie'; //불가능(redeclare)

let favorite = 'choco';
if (true) {
    let favorite = 'cookie';
    console.log(favorite) //cookie
}
console.log(favorite) //choco
```
* const
const는 constant value를 유지  
그래서 let과 다른점은 update, redeclare모두 안된다는 점이다  
```javascript
const favorite = 'choco';
favorite = 'cookie'; //불가능(update)

const favorite = 'choco';
const favorite = 'cookie'; //불가능(redeclare)
```
하지만 const의 object는 업데이트가 가능하다
```javascript
const favorite = {
    firtst : 'candy',
    second : 'icecream'
}
favorite.third = 'coke' //가능
```
결과적으로 const & let 은 blocked scoped이다

# 3 Arrow Functions

Arrow Function은 일반 함수보다 더 간결하게 표현이 가능하다  
기존의 함수에서 function(x) 이라고 써야했던 것을 (x) => 라고 줄일 수 있다  
파라미터가 한개라면 괄호까지 생략이 가능하다 x => 라고 하면 그냥 파라미터가 x한개인 것  
```javascript
const function = () => {}; //parameter 0개
const function = x => {}; //parameter 1개
const function = x => x * x; //{}까지 줄일 수도 있다
const function = (x, y) => {}; //parameter 2개
```

# 4 Array Methods (map, reduce, filter, slice, splice)

* map  
원래 있던 array의 모든 요소들에 함수를 적용하여 새로운 array를 만드는 것  
```javascript
let random = [1, 2, 3, 4];
let random1 = random.map(x => x*x);
console.log(random1) // [1, 4, 9, 16]
```

* reduce  
accumulator와 배열의 각 요소에 대해 한가지 값으로 줄이는 함수  
array.reduce((누적값, 현잿값, 인덱스, 요소) => { return : 결과값}, 초깃값);  
초깃값을 적어주지 않으면 자동으로 0부터 시작한다  
초깃값을 array로 하면 결과값이 array로 나올 수 있다  

* filter
요소들을 걸러내는 것이 목적이다  
function을 통해서 걸러진 요소들만 가지고 새로운 array를 만드는 방법  

* slice
array.slice(시작index, 끝index) 라고 하면 끝index의 앞에있는 요소까지 포함된 새로운 array를 return  
그러나 원래의 array가 바뀌는 것은 아니다  

* splice 
array에 새로운 요소를 추가하거나 없애서 원래의 array를 변경시킨다  
array.splice(시작index, 배열에서 제거할 요소의 수, 추가하는 items)  
시작index부터 변경을 하게 된다, 배열에서 제거할 요소의 수가 0이면 아무것도 제거되지 않는다, 추가하는 아이템이 없으면 
삭제만 하게 된다  

# 5 Spread Operator (Array/Object Spread)

스프레드 연산자는 iterable object = 열거 가능한 것들을 하나씩 전개한다  
변수 앞에 '...'를 찍어서 나타내면 된다  
string spread는 한글자 한글자씩 요소가 되는 array로 만들 수 있다  
* Array Spread  
--------------
```javascript
let one = [1, 2];
let two = [3, 4];
let spread = [0, ...one, 6, ...two];
console.log(spread); // [0, 1, 2, 6, 3, 4]
```

* Object Spread
---------------
```javascript
let a = [{a : 1}, {b : 2}];
let b = [{c : 3}, ...a];
console.log(b) // [{c : 3}, {a : 1}, {b : 2}]
```

# 6 Export / import

* Export
파일안의 함수나 객체를 Export하는 것  
named exports와 default exports가 있다  
named exports는 export된 이름을 사용하여 import하면 사용가능하고, 여러가지를 export할 수 있다  
default export는 모듈 당 한개만 가능하기 때문에 메인이 되는 것을 default export해야한다  

* Import
외부 스크립트에서 Export된 함수나 객체를 가져오는데 사용된다  
