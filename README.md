### 컴포넌트 최적화
* React.memo(컴포넌트) - 컴포넌트의 props가 변경되지 않으면 리렌더링 X

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

> 출처<br>
> [https://nomadcoders.co/react-for-beginners](https://nomadcoders.co/react-for-beginners)
