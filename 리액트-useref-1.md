---
title: "[리액트] useRef (1)"
date: 2026-01-12
lastEdited: 2026-01-12
notionId: 2e66530a-99b0-80a7-97eb-ca7ce45ec37f
---


## 1. useRef는 뭘까?

- useRef는 렌더링과 무관한 데이터를 저장하기 위해 사용하는 훅이다.
- useState는 값이 바뀌면 렌더링을 유발하여 성능에 영향을 줄 수 있다.
- **UI에 영향을 주지 않으면서, 렌더링 이후에도 값을 유지하고 싶은 경우에 사용하는 훅이다.**
- **또한, useRef는 HTML 요소에 직접 접근하고 싶을 때 사용하는 훅이다.**

> 💡 useState - 값 변경에 따른 렌더링 유발 = useRef


## 2. 예제코드


**2.1. 값을 유지하고 싶을 때**


```typescript
import { useRef } from 'react';

function MyComponent() {
  // 1. 훅 호출 (초기값 0 설정)
  const myRef = useRef(0); 

  const increment = () => {
    // 2. 값 변경 (current 속성을 통해 접근)
    myRef.current += 1; 
    
    // 3. 로그는 찍히지만, 화면은 변하지 않음 (리렌더링 X)
    console.log("현재 값:", myRef.current); 
  };

  return (
    <button onClick={increment}>값 올리기</button>
  );
}
```


**2.2. HTML 요소에 직접 접근할 때**


```typescript
import { useRef } from 'react';

function FocusExample() {
  // 1. ref 객체를 생성합니다. (초기값은 null)
  const inputRef = useRef(null);

  const handleClick = () => {
    // 3. inputRef.current는 실제 <input> 엘리먼트를 가리킵니다.
    // DOM API를 직접 사용하여 포커스를 줍니다.
    inputRef.current.focus();
    
    // 추가로 스타일을 직접 조작할 수도 있습니다.
    inputRef.current.style.backgroundColor = "yellow";
  };

  return (
    <div>
      {/* 2. 접근하고 싶은 HTML 태그의 ref 속성에 위에서 만든 ref를 연결합니다. */}
      <input ref={inputRef} type="text" placeholder="여기에 포커스가 잡힙니다" />
      
      <button onClick={handleClick}>
        입력창으로 포커스 이동!
      </button>
    </div>
  );
}
```

