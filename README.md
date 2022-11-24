### 📌 TODO APP을 만들어보며 React 활용 복습하기

- [Project Repository](https://github.com/DINGUNOTE/react-todo)

### 📌 SPA에서 화면 변경을 일으키는 방법

- HTML5의 History API를 사용해서 현재 페이지 내에서 화면 이동이 일어난 것 처럼 작동하게 해준다.
- react-router-dom을 주로 사용하게 되는데, 이 또한 History API를 사용하는 것이다.
- `History API`
  - History.back() - 세션 기록의 바로 뒤 페이지로 이동하는 비동기 메서드(브라우저의 뒤로 가기를 누르는 것과 같은 효과)
  - History.forward() - 세션 기록의 바로 앞 페이지로 이동하는 비동기 메서드(브라우저의 앞으로 가기를 누르는 것과 같은 효과)
  - History.go() - 특정 세션 기록으로 이동하게 해 주는 비동기 메서드(1을 호출하면 바로 앞 페이지로, -1을 호출하면 바로 뒤 페이지로 이동)
  - History.pushState() - 주어진 데이터를 세션 기록 스택에 넣는다. 직렬화 가능한 모든 Javascript 객체를 저장할 수 있다.
  - History.replaceState() - 최근 세션 기록 스택의 내용을 주어진 데이터로 교체한다.

### 📌 React에서 JSX를 사용하는 이유

- 모든 UI를 만들 때 마다 JS의 createElement를 사용해서 컴포넌트를 생성해서 사용하기에는 너무 번거롭기 때문에 JSX를 사용해서 코드를 작성하고, 그 코드를 바벨이 다시 createElement로 변환해주도록 사용한다.

### 📌 JSX에서 반복 요소에 key 속성이 필요한 이유

- 리액트가 Virtual DOM을 활용해서 바뀐 부분을 확인할 때 반복 요소에서 `key` 속성을 이용해서 어떤 부분이 바뀌었는지 인식하기 때문이다.
- key 속성이 없다면 모든 요소가 새롭게 된거라고 인식을 해서 모든 자식 엘리먼트를 새롭게 그린다.

### 📌 컴포넌트 최적화

- React.memo(컴포넌트) - 컴포넌트의 props가 변경되지 않으면 리렌더링 X

### 📌 useLayoutEffect()

- `useEffect()` Hook은 화면에 그려진(Paint) 이후 실행되는 Hook이기 때문에 최초에 데이터가 없는 상태의 경우 화면의 깜빡임 등의 현상이 발생할 수 있다.
- `useLayoutEffect()` Hook은 화면에 Paint되기 이전에 실행되기 때문에 이러한 현상을 방지할 수 있다.

### 📌 useTransition()

- 동시에 많은 렌더링을 발생시키는 작업일 때 우선 순위가 높은 작업, 낮은 작업을 분리해서 리액트가 최적화시켜주게 할 수 있는 Hook
- `startTransition()` 내부에 우선 순위가 낮은 작업을 작성하고 외부에 우선 순위가 높은 작업을 작성한다.
- `loading`이 같이 제공되는데 우선 순위가 높은 작업이 발생 중 로딩 상태를 제어할 수 있다.

### 📌 useDeferredValue()

- 성능에 따라서 덜 중요한 상태를 명시적으로 선언을 해놓고 필요할 때마다 선택적으로 렌더링의 우선 순위를 지정해줄 수 있는 Hook

### 📌 Props의 Type을 체크할 수 있는 속성 - PropType

```javascript
function Btn({ btnTitle, fontSize }) {
  return <button style={{
    fontSize: fontSize,
  }}>{btnTitle}</button>
}
Btn.propTypes = {
  btnTitle: PropTypes.string, // btnTitle의 Type: String
  fontSize: PropTypes.number // fontSize의 Type: Number
  changeValue: PropTypes.func.isRequired // isRequired를 붙이면 필수 값으로 설정
}
function App() {
  return (
    <div>
      <Btn btnTitle={value} fontSize={false} changeValue={changeValue} /> {/* fontSize type error */}
      <Btn btnTitle={0} fontSize={18} /> {/* btnTitle type error, changeValue 없음 error */}
    </div>
  )
}
const root = document.getElementById('root');
ReactDOM.render(<App />, root)
```

> 출처<br> > [https://nomadcoders.co/react-for-beginners](https://nomadcoders.co/react-for-beginners) > [https://www.inflearn.com/course/따라하는-리액트](https://www.inflearn.com/course/따라하는-리액트)
