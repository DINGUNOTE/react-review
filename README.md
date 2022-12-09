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

### 📌 React에서 불변성을 지켜야 하는 이유

- 참조 타입에서 객체나 배열의 값이 변할 때 원본 데이터가 변경되기 때문에 이 원본 데이터를 참조하고 있는 다른 객체에서 예상하지 못한 오류가 발생할 수 있으므로, 프로그래밍의 복잡도가 올라간다.
- 리액트에서 화면을 업데이트할 때 불변성을 지켜서 값을 이전 값과 비교해서 변경된 사항을 확인 후 업데이트하기 때문에 불변성을 지켜줘야 한다.(불변성을 지키지 않으면 이전 값도 변경된다.)

### 📌 React에서 불변성을 지키는 방법

- 참조 타입에서 값을 바꿨을 때 Call Stack 주소 값은 같은데 Heap 메모리 값만 바꿔주기 때문에 불변성을 유지할 수 없다. 그러므로 아예 새로운 배열을 반환하는 메소드를 사용하면 된다.
- spread operator, map, filter, slice, reduce, ...
- 원본 데이터를 변경하는 메소드 : splice, push, ...

### 📌 컴포넌트 최적화

- `React.memo(컴포넌트)` - 컴포넌트의 props가 변경되지 않으면 해당 컴포넌트 자체를 리렌더링 되지 않게 해서 불필요한 렌더링을 줄일 수 있다.
- `useCallback(콜백함수, 의존성 배열)` - 컴포넌트가 리렌더링되면 그 컴포넌트 안의 함수들도 다시 만들어진다. 만약 그 함수가 자식 컴포넌트에 props로 내려주고 있는 함수라면 그 함수를 포함하고 있는 자식 컴포넌트도 계속 리렌더링 될 것이다. 이런 현상을 막기 위해서 useCallback을 사용한다. 함수 내부에서 참조하는 state, props가 있다면 의존성 배열에 추가하면 된다. 함수 내부의 데이터가 변하지 않으면 함수를 새로 생성하지 않게 되므로 불필요한 렌더링을 줄일 수 있다. 의존성 배열에 아무것도 존재하지 않는다면 최초의 렌더링 시에만 리렌더링된다.
- `useMemo(함수, 의존성 배열)` - Memoization이란 비용이 많이 드는 함수 호출의 결과를 저장해서 동일한 입력이 다시 발생했을 때 캐시된 결과를 반환해서 프로그램의 속도를 높이는 데 사용되는 최적화 기술이다. 컴포넌트 내의 시간이 오래 걸리고 복잡한 연산을 수행하는 함수가 있을 때, 리렌더링 된다면 계속 해당 함수도 다시 실행될 것이기 때문에 성능에 안 좋은 영향을 미치고 UI 지연 현상도 일어날 것이다. 이런 현상을 해결하기 위해서 사용하는 것이 useMemo다. 함수에 넘겨주는 값이 변하지 않는다면 이전에 연산한 결과와 동일할 것이기 때문에 Memoizing 해뒀다가 같은 값이 들어온다면 재활용을 하면서 성능을 최적화시켜줄 수 있다.
- 크롬 익스텐션 React 개발자 도구를 활용하면 실시간으로 리렌더링되는 부분을 확인할 수 있다.

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

### 📌 React에서의 TDD(Test Driven Development, 테스트 주도 개발)

- TDD란? 실제 코드를 작성하기 전에 테스트 코드를 먼저 작성해서 해당 테스트 코드를 통과한 코드로 실제 코드를 작성하는 방법을 테스트 주도 개발(TDD)라고 한다.
- TDD를 하면 많은 기능을 테스트하기 때문에 소스 코드에 안정감이 부여되고, 이로 인해서 실제 개발을 할 때 디버깅 시간이 줄어들기 때문에 개발의 효율성을 올릴 수 있다.

  ### `React Testing Library`

  - React 구성 요소 작업을 위한 API를 추가해서 DOM Testing Library 위에 구축된다.
  - DOM Testing Library란 DOM Node를 테스트하기 위한 가벼운 솔루션이다.(리액트 컴포넌트를 테스트하는 가벼운 솔루션)
  - Create React App으로 생성된 프로젝트는 즉시 React Testing Library를 지원한다. 그렇지 않은 경우에는 `npm i -D @testing-library/react` 명령어를 통해 추가할 수 있다.
  - React Testing Library는 에어비앤비에서 만든 Enzyme이라는 솔루션을 대처하는 솔루션이다.
  - Enzyme은 구성 요소의 구현 세부 정보를 테스트하는 `구현 주도 테스트(Implementation Driven Test)`로 이루어지는 반면 React Testing Library는 개발자를 리액트 앱 사용자 입장에 두고 행위 `주도 테스트(Behavior Driven Test)`로 이루어진다.

  ### `Jest`

  - Facebook에서 만든 테스팅 프레임워크
  - 최소한의 설정으로 동작하고 Test Case를 만들어서 어플리케이션 코드가 잘 돌아가는지 확인해준다.
  - `단위(Unit)` 테스트를 위해서 이용한다.
  - {filename}.`test`.js, {filename}.`spec`.js, `tests` 폴더 내부에 있는 모든 파일로 Test 파일을 찾는다

> 출처<br>
>
> [https://nomadcoders.co/react-for-beginners](https://nomadcoders.co/react-for-beginners) <br>[https://www.inflearn.com/course/따라하는-리액트](https://www.inflearn.com/course/따라하는-리액트)
