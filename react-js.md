# React and Javascript Cheatsheet

In these examples, I am using MUI Material UI as the main React Component Library.

Contents:
- [`useState` Hooks with React]()

***
### `useState` Hooks with React

```js
import { useState } from "react";
import { Button, Typography } from '@mui/material';

function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count => count + 1);
  }

  return (
    <>
      <Typography>{count} times</Typography>
      <Button onClick={handleClick}>Add 1</Button>
    </>
  );
}
```

***
