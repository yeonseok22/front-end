# binding 개념과 call, apply, bind 차이점
- 출처 : [binding의 개념과 call, apply, bind](https://wooooooak.github.io/javascript/2018/12/08/call,apply,bind/)

- `binding` 개념과 `call`, `apply`, `bind` 차이점
    - `binding` : `this`를 사용하면 `window` 객체가 나타나는데, `window` 객체를 사용하고 싶지 않고 `this`를 그때 그때 알맞은 객체로 바꿔서 `this` 값에 따라 작동할 것
        - 애매하지만, `this`를 사용하면 꼭 `window`라고 말할 수는 없음
        
- `call`, `apply`
    - 함수를 호출하는 함수. 그냥 실행하는 것이 아닌 첫 번째 인자에 `this`로 setting하고 싶은 객체를 넘겨주어 `this`를 바꾸고 나서 실행
    
    ```jsx
    const obj = { name: 'Tom'};
    
    const say = function(city) {
    		console.log(`Hello, my name is ${this.name}, I live in ${city}`};
    }
    
    say("seoul");               // Hello, my name is Tom, I live in seoul. (window)
    say.call(obj, "seoul");     // Hello, my name is Tom, I live in seoul
    say.apply(obj, ["soeul"]);  // Hello, my name is Tom, I live in soeul
    ```
    
    - `call`과 `apply`의 차이점
        - 첫 번째 인자(`this`를 대체할 값)를 제외하고, 실제 say에 필요한 parameter를 입력하는 방식
            - `call`과 다르게 `apply` 함수는 두 번째 인자부터 모두 배열에 넣어야 한다.
            
- `bind`
    - `call`, `apply`와 다르게 함수를 실행하지 않고 `bound` 함수를 리턴한다.
    
    ```jsx
    const obj = { name: 'Tom'};
    
    const say = function(city) {
    		console.log(`Hello, my name is ${this.name}, I live in ${city}`};
    }
    
    const boundSay = say.bind(obj);
    boundSay("seoul");    // Hello, my name is Tom, I live in seoul.
    ```
    
    - bound 함수 (`boundSay`)는 이제부터 `this`를 `obj`로 갖고 있으므로, 나중에 사용해도 된다.
    - `bind`에 사용하는 나머지 rest 파라미터는 `call`과 `apply`와 동일함