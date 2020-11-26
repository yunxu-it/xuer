- 优先使用`FC`类型来声明函数组件

  ```javascript
  import { FC } from 'react'
  
  export const Conditional: FC<{ when: boolean }> = ({ when, children }) => <>{(when) && children}</>
  
  用法：
  
  <Box>
    <Conditional when={isLoading}>
      Loading...
    </Conditional>
    Other stuff.
  </Box>
  
  等效于：
  
  <Box>
    {isLoading && (
      <>
        Loading...
      </>
    )}
    Other stuff.
  </Box>
  ```

  