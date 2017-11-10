# 되짚어 보는 JavaScript 

 - ECMAScript 5 명세를 기준으로 작성되었다.

   ​



### 생각해볼 문제들

1. ==, === 차이점

   ```javascript
   var number1 = 5;
   var number2 = '5';

   if( number1 == number2 ) console.log('number1 == number2');
   if( number1 === number2 ) console.log('number1 === number2');
   ```




1. '', "" 무엇이 맞을까?

   ```javascript
   var msg = "Hello World!";
   var msg2 = 'Hello World!';

   if(msg === msg2) console.log(true);
   ```

   ​

2. 마침표 꼭 붙여야 할까?

   ```javascript
   var name = 'Park Jun';
   var contry = 'korea'
   ```
   ​

3. 숫자 - 문자열 결과는?

   ```javascript
   var message = 'Hello World!';
   var number = 33;

   console.log(number - message);
   ```




5. 객체 참조

   ```javascript
   var object1 = {
       value : 10
   };

   var obejct2 = object1;

   console.log(object1) //출력값 10
   console.log(obejct2) //출력값 10

   object1.value = 300;

   console.log(object1) //출력값 300
   console.log(obejct2) //출력값 ??
   ```



6. || 사용 변수 초기화

   ```javascript
   var global = { path:''};
   var filePath = global.path || 'C:/home/data';

   console.log(filePath); //출력값 ?

   global.path = '/home/common/data';

   filePath = global.path || 'C:/home/data';
   console.log(filePath); //출력값 ?
   ```

   ​


- 구글 자바스크립트 스타일가이드

  https://google.github.io/styleguide/javascriptguide.xml?showone=Strings#var

  https://google.github.io/styleguide/jsguide.html

- jQuery 가이드

  http://docs.jquery.com/JQuery_Core_Style_Guidelines





### 1. 자바스크립트 기본 타입 

```javascript
//숫자 타입
var intNumber = 77;
var floatNumber = 0.77;

//문자열타입
var message = 'Hello World!!';

//불린 타입
var flagVar = true;

//undefined 타입
var emptyVar;

//null 타입
var nullVar = null;
```



### 2. 객체

```javascript
//Object() 생성자 함수 이용
var person = new Object();
person.name = 'Jun Park';
person.age = 35;
person.contry = 'korea';

console.log(person.name);
console.log(person['contry']);


//객체 리터럴 방식 이용
var caculator = {
    num1:2,
    num2:5,
    add: function() {
        console.log(this.num1+this.num2);  
    }
}

var github = {
    id : 'miso360',
  	name : 'Jun Park',
  	url : '',
  	email : ''
}

console.log(github.id);
console.log(github['name']);


//객체 출력
var object;
for(object in github){
    console.log(object, github[object]);
}


//배열 생성 방법
var arrayObject1 = new Array(); //var arrayObject2 = new Array();
var arrayObject2 = ['t1', 't2', 't3']; //var arrayObject = [];

//배열 원소 추가 방법들
arrayObject2.color = 'blue;'
arrayObject2.push('t4');
arrayObject2[4] = 't5';

//배열 출력 방법들
console.log(arrayObject2);
console.dir(arrayObject2);

for(var object in arrayObject2){
    console.log(object, arrayObject2[object])
}

for(var i=0; i<arrayObject2.length; i++){
    console.log(i, arrayObject2[i]);
}
```



### 3. 함수

- 자바스크립트에서는 함수도 객체다.

```javascript
function add(x, y){
	return x+y;
}

console.log( add(3,4) ); //출력값 7 

add.result = add(3,4);

console.log( add.result ); //출력값 7
```

  ​

#### 3. 1 함수 선언

```javascript
//함수 선언문(function statement)
function add(x, y){
    return x+y;
}

//함수 표현식(function expression), 함수 리터럴
var minus = function(x, y){
    return x-y;
};


console.log( add (3,4) );
console.log( minus(15,8) );
```



### 4. 클래스, 생성자, 메서드

```javascript
//클래스
function Github(id){
    this.id = id;
  	this.url;
  
  	this.getId = function(){
        return this.id;
    }
    
    this.setId = function(value){
        this.id = value;
    }
    
    this.getUrl = function(){
        return this.url;
    }
    
    this.setUrl = function(value){
        this.url = value;
    }
}

var myGithub = new Github('miso360');
console.log( myGithub.getId())// 출력값 miso360

myGithub.setUrl('https://github.com/miso360');
console.log( myGithub.getUrl() ); //출력값 https://github.com/miso360
```

