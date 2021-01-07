# 4일차

9. 폼
10. state 끌어올리기

<br/>

## 9. 폼

### HTML의 폼

HTML의 `<input>`, `<textarea>`, `<select>` 같은 **폼 엘리먼트**는 사용자의 입력에 따라 자신의 state를 관리 및 업데이트 합니다.

```html
<form>
  <label>
    Name
    <input type="text" name="userName" />
  </label>
  <input type="submit" value="Submit" />
</form>
```

javascript 함수로 input 값을 얻고 폼의 제출을 처리하는 추가적인 과정을 거쳐야합니다.

그러나 react의 경우 **제어 컴포넌트**라는 기술을 통해 입력값, 제출 처리 등을 한 번에 할 수 있습니다.

> 💡 `name` 속성은 **input 양식 컨트롤의 이름**입니다.

<br/>

### 제어 컴포넌트

제어 컴포넌트란 React에 의해 값이 제어되는 **입력 폼 엘리먼트** 입니다.
