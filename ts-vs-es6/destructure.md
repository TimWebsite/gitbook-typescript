# 비구조화 할당

비구조화 할당은 배열, 객체의 아이템 또는 속성을 변수에 할당할 때 유용합니다.

**작성 코드:**

{% code-tabs %}
{% code-tabs-item title="TypeScript" %}
```typescript
// 배열 비구조화 할당
let [html, , body] = [document.documentElement, document.head, document.body];

// 객체 비구조화 할당
let numbers_module = {
    multiplyNumbers: (...n:number[]):number => n.reduce((a, b) => a * b),
    sumNumbers: (...n:number[]):number => n.reduce((a, b) => a + b)
};

let { sumNumbers } = numbers_module;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**컴파일 코드:**

{% code-tabs %}
{% code-tabs-item title="JavaScript" %}
```javascript
// 배열 비구조화 할당
var _a   = [document.documentElement, document.body],
    html = _a[0],
    body = _a[2];

// 객체 비구조화 할당
var numbers_module = {
  multiplyNumbers: function () {
    var n = [];
    for (var _i = 0; _i < arguments.length; _i++) {
      n[_i] = arguments[_i];
    }
    return n.reduce(function (a, b) { return a * b; });
  },
  sumNumbers: function () {
    var n = [];
    for (var _i = 0; _i < arguments.length; _i++) {
      n[_i] = arguments[_i];
    }
    return n.reduce(function (a, b) { return a + b; });
  }
};

var sumNumbers = numbers_module.sumNumbers;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

TypeScript 비구조화 할당은 ES6의 비구조화 할당에 추가적으로 다음과 같은 것을 할 수 있습니다. `sumNumbers?` 코드에서 `?`의 의미는 속성이 있을 경우 `sumNumbers` 속성에 할당하고, 없을 경우 속성 할당을 하지 않습니다. 즉, 선택적으로 존재할 경우만 속성을 할당합니다.

`sumNumbers:sum = (...n:number[]):number => n.reduce((a, b) => a + b)` 코드는 `o` 객체에 `sumNumbers` 속성이 없을 경우, 기본 값 `(...n:number[]):number => n.reduce((a, b) => a + b)`을 설정\(`=`\)한 것입니다. 그리고 `:sum`을 통해 속성 이름을 `sumNumbers` 대신 `sum`으로 사용하도록 합니다.

**작성 코드:**

{% code-tabs %}
{% code-tabs-item title="TypeScript" %}
```typescript
let numbers_module: { multiplyNumbers: () => number } = {
  multiplyNumbers: (...n: number[]): number => n.reduce((a, b) => a * b)
};

// ?는 선택적으로 설정할 때 사용합니다. (ES6에서는 지원하지 않습니다)
let o: { multiplyNumbers: () => number; sumNumbers?: any } = numbers_module;

// sumNumbers 속성이 없을 경우, sum 속성에 기본 값을 설정합니다.
let {
  multiplyNumbers: multiply,
  sumNumbers: sum = (...n: number[]): number => n.reduce((a, b) => a + b)
} = o;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**컴파일 코드:**

{% code-tabs %}
{% code-tabs-item title="JavaScript" %}
```javascript
var numbers_module = {
  multiplyNumbers: function () {
    var n = [];
    for (var _i = 0; _i < arguments.length; _i++) {
      n[_i] = arguments[_i];
    }
    return n.reduce(function (a, b) {
      return a * b;
    });
  }
};

// ? 는 선택적으로 설정할 때 사용합니다. (ES6에서는 지원하지 않습니다)
var o = numbers_module;

// sumNumbers 속성이 없을 경우, sum 속성에 기본 값을 설정합니다.
var multiply = o.multiplyNumbers,
  _a = o.sumNumbers,
  sum = _a === void 0 ? function () {
    var n = [];
    for (var _i = 0; _i < arguments.length; _i++) {
      n[_i] = arguments[_i];
    }
    return n.reduce(function (a, b) {
      return a + b;
    });
  } : _a;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% embed data="{\"url\":\"https://slides.com/yamoo9/es6\#/1\",\"type\":\"video\",\"title\":\"ECMAScript 2015 \(ES6\)\",\"description\":\"ECMAScript 2015 학습용 슬라이드.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://slides.com/favicon.ico\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://s3.amazonaws.com/media-p.slid.es/thumbnails/11b67116bd8eff286b365665fd3cb621/thumb.jpg?1512767343\",\"width\":500,\"height\":500,\"aspectRatio\":1},\"embed\":{\"type\":\"player\",\"url\":\"https://slides.com/yamoo9/es6/embed\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.2493%;\\\"><iframe src=\\\"https://slides.com/yamoo9/es6/embed\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.7778}}" %}

