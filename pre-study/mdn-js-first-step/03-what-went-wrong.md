# 뭐가 잘못됐을까요? JavaScript 문제 해결

<https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/What_went_wrong>

## 오류의 종류

* 구문 오류: 코드에 잘못된 철자가 있으면 발생하는 오류로, 프로그램이 아예 구동하지 못하거나 중간에 멈춰버리는 현상을 일으키며, 모종의 오류 메시지도 나타납니다. 올바른 도구와, 메시지의 뜻만 파악하고 있으면 그럭저럭 고칠 만합니다!
* 논리 오류: 구문은 올바르지만 의도한 동작과 실제 코드에 차이가 있는 경우입니다. 따라서 프로그램은 성공적으로 돌아가지만 잘못된 결과를 낳습니다. 보통 오류를 직접 가리키는 메시지가 없기 때문에 구문 오류보다 고치기도 힘든 편입니다.

## 오류를 포함한 예제

1. 시작하려면 로컬 복사본을 선호하는 텍스트 편집기와 브라우저에서 열어주세요.
2. 게임 플레이를 시도해 보세요. "Submit guess" 버튼을 눌러도 아무 일이 없다는 걸 볼 수 있습니다.

## 구문 오류 고치기

앞선 과정에서 JavaScript 개발자 도구 콘솔 (en-US)에 간단한 JavaScript 명령을 입력해 봤었습니다. (콘솔을 여는 방법이 기억나지 않으면 링크에서 알아보세요) 하지만 콘솔은 단순히 명령을 입력하는 기능보다 유용한데, 브라우저의 JavaScript 엔진이 읽은 JavaScript 안에 구문 오류가 존재하면 콘솔에 그 오류가 기록되기 때문입니다. 오류를 잡아 봅시다.

1. `number-game-errors.html`을 연 탭으로 이동해서 JavaScript 콘솔을 여세요. 스크린샷과 비슷한 내용의 오류 메시지를 볼 수 있어야 합니다.
2. 이 오류는 찾기 쉬운 편이고, 브라우저도 도움이 될 다양한 정보를 제공합니다. (위의 스크린샷은 Firefox에서 촬영했지만 다른 브라우저도 비슷한 정보를 제공합니다) 우리가 알 수 있는 사실은, 왼쪽에서 오른쪽으로...
   * 붉은 "x"는 오류라는 뜻입니다.
   * 오류 메시지는 무엇이 잘못됐는지 나타냅니다. "TypeError: guessSubmit.addeventListener is not a function"
   * "Learn More" 링크는 오류의 뜻을 더 자세히 알아볼 수 있는 MDN 페이지로 향합니다.
   * JavaScript 파일 이름은 개발자 도구의 디버거 탭을 엽니다. 이 링크를 따라가면 오류가 발생한 정확한 위치를 볼 수 있습니다.
   * 오류가 발생한 줄 번호와, 오류를 처음으로 마주한 문자 번호를 볼 수 있습니다. 이 예제에서는 86번째 줄, 3번째 글자입니다.
3. 코드 편집기에서 86번째 줄을 보면 다음 코드를 볼 수 있습니다. `guessSubmit.addeventListener('click', checkGuess);`
4. 오류 메시지 "guessSubmit.addeventListener is not a function"은 우리가 호출한 함수를 JavaScript 인터프리터가 인식하지 못했다는 뜻입니다. 보통 이 오류는 철자를 잘못 적은 경우 발생합니다. 구문의 올바른 철자가 확실하지 않을 땐 MDN에서 기능 참고서를 살펴보는 게 도움이 되곤 합니다. 선호하는 검색 엔진에서 "mdn '기능 이름'"을 검색해 보세요. 하지만 지금은 시간을 아끼기 위해 링크를 바로 드리겠습니다. `addEventListener()`입니다.
5. `addEventListener()` 페이지를 보니, 함수 이름을 잘못 적었네요! JavaScript는 대소문자를 구분한다는 점을 기억하세요. 철자는 물론 대소문자도 잘못 적으면 오류가 발생합니다. `addeventListener`를 `addEventListener`로 수정하면 될 겁니다. 지금 해보세요.

### 구문 오류 2회차

1. 페이지를 저장하고 새로고침하세요. 오류가 사라진 모습을 확인할 수 있어야 합니다.
2. 이제 숫자를 입력하고 Submit guess 버튼을 누르면... 다른 오류네요!
3. 이번 오류는 78번째 줄에서 "TypeError: lowOrHi is null"입니다.
4. 78번째 줄을 보면 다음 코드를 볼 수 있습니다. `lowOrHi.textContent = 'Last guess was too high!';`
5. 위의 코드에서는 lowOrHi 상수의 textContent 속성에 텍스트 문자열을 할당하려고 시도했지만, lowOrHi에 들어있어야 할 값이 없어서 동작하지 못했습니다. 이유를 알아봅시다. 코드 내에서 lowOrHi가 등장하는 다른 곳을 탐색해 보세요. JavaScript에서 lowOrHi가 제일 먼저 등장하는 곳은 48번째 줄입니다. `const lowOrHi = document.querySelector('lowOrHi');`
6. 여기서는 문서 HTML의 요소 참조를 변수에 저장하려고 시도하고 있습니다. 48번째 줄이 실행된 후에 lowOrHi가 null인지 확인해 봅시다. 49번째 줄에 아래의 코드를 추가하세요. `console.log(lowOrHi);`
7. 저장하고 새로고침하세요. console.log()가 콘솔에 기록한 결과를 볼 수 있을 겁니다. lowOrHi의 값이 명백히 null이므로, 48번째 줄에 문제가 있는 게 틀림없습니다.
8. 어떤 문제일지 생각해 봅시다. 48번째 줄은 document.querySelector() 메서드를 사용해, CSS 선택자로 선택한 요소의 참조를 가져옵니다. 우리 파일의 더 위쪽에서 우리가 찾으려는 문단을 볼 수 있습니다. `<p class="lowOrHi"></p>`
9. 보아하니 우리가 사용했어야 하는 선택자는 마침표(.)로 시작하는 클래스 선택자였는데, 48번째 줄의 querySelector() 메서드에 제공한 선택자에는 마침표가 없습니다. 이게 문제일 수 있겠네요! lowOrHi를 .lowOrHi로 바꿔보세요.
10. 저장 후 다시 새로고침해보면 console.log() 명령문이 우리가 원하는 `<p>` 요소를 반환하는 모습을 볼 수 있습니다. 휴, 다른 오류를 고쳤네요. 이제 console.log()는 지워도 되고, 아니면 나중에 다시 보기 위해 남겨놔도 됩니다. 선호하는 쪽으로 선택하세요.

### 구문 오류 3회차

1. 이제는 게임을 성공적으로 플레이할 수 있습니다. 올바른 숫자를 입력하거나, 턴을 모두 소모하기 전까지는요.
2. 게임이 정상적으로 끝나야 하는 순간, 다시 실패해버립니다. 맨 처음 봤던 것과 같은 종류의 오류, "TypeError: resetButton.addeventListener is not a function"과 함께요. 하지만 이번에는 94번째 줄에서 발생할 겁니다.
3. 94번째 줄을 확인하면 똑같은 실수가 있었다는 걸 알 수 있습니다. addeventListener를 addEventListener로 바꾸기만 하면 됩니다. 바로 수정해 보세요.

## 논리 오류

1. randomNumber 변수에 무작위 수를 설정하는 부분을 찾아보세요. 게임을 시작할 때 맞혀야 하는 무작위 수는 44번째 줄 부근에서 저장합니다. `let randomNumber = Math.floor(Math.random()) + 1;`
2. 후속 라운드를 시작할 때 새로운 무작위 수를 생성하는 코드는 113번째 줄 근처입니다. `randomNumber = Math.floor(Math.random()) + 1;`
3. 위의 두 줄이 정말 문제일까요? 이전에 만났던 console.log()를 다시 꺼내옵시다. 각각의 줄 바로 밑에 다음 코드를 추가하세요. `console.log(randomNumber);`
4. 저장, 새로고침, 그리고 몇 판 플레이해 보세요. 콘솔에 기록하는 시점에서, randomNumber가 정말 1임을 볼 수 있습니다.

### 논리 파고들기

문제를 수정하기 전에 이 코드가 어떻게 동작하는지 상기해 봅시다. 먼저, 0.5675493843처럼 0과 1 사이의 무작위 10진수 숫자를 생성하는 Math.random()을 호출합니다.

```js
Math.random()
```

다음으로, Math.random()을 호출한 결과를 Math.floor()에 제공합니다. Math.floor()는 주어진 수의 버림을 반환합니다. 그리고 여기에 1을 더합니다.

```js
Math.floor(Math.random()) + 1
```

0과 1 사이의 무작위 10진수 수를 버림하면 결과는 항상 0이니, 여기에 1을 더한 결과는 항상 1입니다. 무작위 수를 버림하기 전에 먼저 100을 곱해야 원하는 숫자를 얻을 수 있을 겁니다. 다음 코드는 0부터 99까지의 무작위 수를 생성합니다.

```js
Math.floor(Math.random()*100);
```

그러므로, 여기에 1을 더하면 1과 100 사이의 수를 얻을 수 있습니다.

```js
Math.floor(Math.random()*100) + 1;
```

두 줄 모두 이렇게 고친 후에 저장하고 새로고침해보세요. 이제 처음 의도했던 대로 게임을 플레이할 수 있을 겁니다.

## 다른 일반적인 오류

### SyntaxError: missing ; before statement

변수를 어떤 값과 동일하게 만드는 할당 연산자(=)와, 어떤 값이 다른 값과 같은지 판별해서 true/false를 반환하는 일치 연산자(===)를 헷갈리지 않도록 주의하세요.

```js
const userGuess = Number(guessField.value);
const userGuess === Number(guessField.value); // wrong
```

### 어떤 값을 입력해도 항상 이겼다고 함

할당과 일치 연산자를 혼동해서 발생

```js
if (userGuess = randomNumber) {} // wrong
if (userGuess === randomNumber) {}
```

### SyntaxError: missing ) after argument list

이건 단순한 편입니다. 보통 함수나 메서드를 호출할 때 닫는 괄호를 누락하면 발생합니다.

### SyntaxError: missing : after property id

일반적으로는 JavaScript 객체를 잘못된 형태로 작성했을 때 발생하지만, 아래의 코드를

```js
function checkGuess() {} // before error

function checkGuess( { // error case
```

브라우저가 함수의 본문을 본문이 아니라 매개변수로 잘못 인식하기 때문입니다. 괄호를 주의하세요!

### SyntaxError: missing } after function body

쉬운 오류입니다. 일반적으로 함수나 조건문 구조에 사용한 중괄호를 누락할 때 발생합니다. 예컨대 `checkGuess()` 함수 끝부분의 닫는 중괄호를 하나 제거하면 오류를 재현할 수 있습니다.

### SyntaxError: expected expression, got 'string' 또는 SyntaxError: unterminated string literal

이 두 오류는 대개 문자열 값의 열거나 닫는 따옴표가 빠지면 발생합니다. 첫 번째 오류의 *string* 부분에는 브라우저가 따옴표 대신 마주친, 예상치 못한 문자 또는 문자열이 들어갑니다. 두 번째 오류는 따옴표로 닫지 않은 문자열이 있다는 뜻입니다.

* [SyntaxError: Unexpected token](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Errors/Unexpected_token)
* [SyntaxError: unterminated string literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unterminated_string_literal)

## 정리

간단한 JavaScript 프로그램에서 오류를 잡아내는 기초 방법을 알아봤습니다. 여러분의 코드에서 잘못된 곳을 찾는 일이 항상 이렇게 쉽진 않을 겁니다. 하지만 여러분의 배움 과정 초기에는 이 방법들로도 뭔가 잘못되더라도 문제 해결 속도를 약간 높여서 수면 시간을 확보하기에는 충분할 겁니다.
