### TODO APP을 만들어보며 React 활용 복습하기

- [https://github.com/DINGUNOTE/react-todo](https://github.com/DINGUNOTE/react-todo)

### SPA에서 화면 변경을 일으키는 방법

- HTML5의 History API를 사용해서 현재 페이지 내에서 화면 이동이 일어난 것 처럼 작동하게 해준다.
- react-router-dom을 주로 사용하게 되는데, 이 또한 History API를 사용하는 것이다.
- `History API`
  - History.back() - 세션 기록의 바로 뒤 페이지로 이동하는 비동기 메서드(브라우저의 뒤로 가기를 누르는 것과 같은 효과)
  - History.forward() - 세션 기록의 바로 앞 페이지로 이동하는 비동기 메서드(브라우저의 앞으로 가기를 누르는 것과 같은 효과)
  - History.go() - 특정 세션 기록으로 이동하게 해 주는 비동기 메서드(1을 호출하면 바로 앞 페이지로, -1을 호출하면 바로 뒤 페이지로 이동)
  - History.pushState() - 주어진 데이터를 세션 기록 스택에 넣는다. 직렬화 가능한 모든 Javascript 객체를 저장할 수 있다.
  - History.replaceState() - 최근 세션 기록 스택의 내용을 주어진 데이터로 교체한다.

### 컴포넌트 최적화

- React.memo(컴포넌트) - 컴포넌트의 props가 변경되지 않으면 리렌더링 X

### Props의 Type을 체크할 수 있는 속성 - PropType

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
