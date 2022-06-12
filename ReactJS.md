---
title: React JS
date: 2022-05-26
updated: 2022-05-30
---

### **Table of contents**

---

[**1. React Hook**](#react-hook)

* [useState](#usestate)

* [useEffect](#useeffect)

* [React Memo](#react-memo)

* [useCallback](#usecallback)

* [useMemo](#usememo)

* [useRef](#useref)

* [useReducer](#usereducer)

* [Context API](#context-api)

[**2. Redux**](#redux)



### React Hook

---

1. #### useState

* Thể hiện trạng thái dữ liệu, dữ liệu thay đổi thì giao diện thay đổi
* Sử dụng khi: Khi dữ liệu thay đổi thì giao diện tự cập nhật lại (re-render)

```jsx
import { useState } from "react";

const Component = () => {
  const [state, setState] = useState(initState);
}
```

* Lưu ý:

  * Component sẽ re-render sau mỗi lần `setState` 
  * `initState` chỉ được sử dụng cho lần đầu tiên
  * setState với callback

  ```jsx
  import { useState } from "react";
  
  const Component = () => {
    const [state, setState] = useState(1);
    
    //case 1:
    const updateState = () => {
      setState(state + 1);
      setState(state + 1);
      setState(state + 1);
    } 
    // => state ở 3 lần gọi là giống nhau nên state mới chỉ tăng lên 1 lần
    
    //case 2:
    const updateState = () => {
      setState((prevState) => prevState + 1);
      setState((prevState) => prevState + 1);
      setState((prevState) => prevState + 1);
    }
    // => prevState ở 3 lần gọi là khác nhau nên state mới tăng lên 3 lần
  }
  ```

  * initState với callback: tránh lặp lại 1 logic gì đấy không cần thiết mỗi lần re-render



2. #### useEffect

* Dùng khi cần thực hiện side effect (update dom, call api, listen/remove event)
* Callback trong useEffect chạy sau khi Component render

```jsx
import { useEffect } from "react";

const Component = () => {
  //case 1:
 	useEffect(() => {
  	//logic  
  });
  
  //case 2:
 	useEffect(() => {
    //logic
  }, []);
  
  //case 3:
  useEffect(() => {
    //logic
  }, [dependency]);
}
```

* Các trường hợp:

  * Case 1: callback without dependency - callback trong useEffect sẽ được chạy lại mỗi lần Component re-render
  * Case 2: callback with empty dependency - callback chỉ được chạy duy nhất 1 lần sau khi Component render lần đầu tiên (mount)
  * Case 3: callback with dependency - callback chạy sau lần đầu tiên Component render (mount) và sau mỗi lần dependency thay đổi
  * return function in callback (cleanup function) được gọi khi Component unmount. Thường được dùng để clear các hàm setInterval, setTimeout, hoặc gỡ các eventListener

  ```jsx
  useEffect(() => {
    return () => {
      // logic
    }
  }, [])
  ```

  

3. #### React.memo

* Là 1 Higher Order Component. Dùng để bọc bên ngoài các Component
* memo giúp lưu lại prop của Component và quyết định xem có cần thiết phải render lại lại Component đấy không giựa trên giá trị prop

```jsx
import { memo } from "react";

export default memo(function Component (props) {
  return (
  	//jsx
  );
}, (prevProps, nextProps) => {
  //logic
})
```



4. #### useCallback

* Sử dụng trong component nhưng tạo ra tham chiếu của 1 function từ ngoài component, function chỉ được tạo 1 tham chiếu mới trong trường hợp dependency thay đổi.
* Có thể sử dụng kết hợp với React Memo trong trường hợp memo Component nhận vào prop là 1 function mà không muốn component re-render với mỗi lần Component cha tạo ra tham chiếu mới của function.

```jsx
import { useCallback, memo } from "react";

function Component() {
  const handle = useCallback(() => {
    // logic
  }, []);
  
  return (
  	<ChildComponent onHandle={handle} />
  );
}

memo(function ChildComponent({ onHandle }) {
  return (
  	<button onClick={onHandle}></button>
  );
})

// => Mỗi lần Component re-render sẽ không tạo ra tham chiếu mới của handle function nên ChildComponent sẽ không bị re-render
```



5. #### useMemo

* Sử dụng để tránh việc một function bị gọi một cách không cần thiết khi Component re-render

```jsx
import { useMemo, useState } from "react";

const Component = () => {
  const [input, setInput] = useState("");
  const [list, setList] = useState([]);
  
  const handleResult = useMemo(() => {
    //logic
  }, [list])
  
  // Trong trường hợp handleResult không được bọc bởi useMemo thì function sẽ được gọi mỗi lần Component re-render. Sau khi bọc bởi useMemo và có dependency thì chỉ được gọi mỗi khi dependency thay đổi
  
}
```



6. #### useRef

* Mỗi lần Component re-render thì sẽ tạo ra một phạm vi biến (param) mới. Trong trường hợp muốn lưu lại giá trị 1 biến cho những lần re-render sau thì sử dụng useRef
* useRef tạo ra một giá trị tham chiếu từ bên ngoài
* Có thể sử dụng trong trường hợp muốn lưu lại giá trị trước đó của state để so sánh với state hiện tại
* Ngoài ra còn có thể truy cập vào các thẻ trong DOM thông qua ref trên các thể

```jsx
import { useRef } from "react";

const Component = () => {
  const ref = useRef(initValue);
  
  console.log(ref.current);
}
```



7. #### useReducer

* Trường hợp nâng cao của useState, dùng để quản lý một tổ hợp lớn số lượng state và có độ phức tạp cao.
* Hàm reducer nhận 2 tham số là state và action trả về newState sau khi thực hiện action **`(state, action) => newState`**

* Thức tự các bước thực hiện trong useReducer
  * B1: Khởi tạo giá trị - initial State
  * B2: Tạo các action dùng để thay đổi state
  * B3: Tạo reducer
  * B4: Dispatch kích hoạt action thay đổi state

```jsx
import React, { useReducer } from 'react'

//B1: khởi tạo state
const initState = 0;

//B2: Định nghĩa action
const ACTION_UP = "up";
const ACTION_DOWN = "down"

//B3: Tạo Reducer
const reducer = (state, action) => {
    switch (action) {
        case ACTION_DOWN:
            return state - 1;
        case ACTION_UP:
            return state + 1;
        default:
            throw new Error("Invalid Action");
    }
}

export default function Demo () {
    const [count, dispatch] = useReducer(reducer, initState);
    return (
        <>
            <div>Count: {count}</div>
      			//B4: dispatch action
            <button onClick={() => dispatch(ACTION_UP)}>UP</button>
            <button onClick={() => dispatch(ACTION_DOWN)}>DOWN</button>
        </>
    )
}

```



8. #### Context API

* Context cung cấp một cách để truyền dữ liệu xuống cây component nhưng không cần thông qua props
* Thứ tự
  * Tạo Context
  * Provider: Truyền dữ liệu
  * Consumer: Nhận dữ liệu

```jsx
import { createContext, useContext } from "react";

const Context = createContext();

const Provider = ({children}) => {
  
  const value = {
    //Các dữ liệu cần được truyền qua các component có thể là dữ liệu hoặc các phương thức.
  }
  
  return (
  	<Context.Provider value={value}>
    	{children}
    </Context.Provider>
  );
}


const App = () => {
  //Value nhận được thông qua prop value ở Provider. Có thể gọi lại ở bất cứ component con nào.
  const value = useContext(Context);
  
  return (
  	<Provider>
    	// child component
    </Provider>
  );
}
```



### Redux

---

1. #### useSelector



2. #### useDispatch





3. #### Setup Redux Store

* 1 App có nhiều loại state khác nhau tương tự với các nhóm reducer khác nhau => rootReducer để kết hợp lại việc quản lý các nhóm reducer này cho App của mình
