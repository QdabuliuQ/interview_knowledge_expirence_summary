`react hook`的`useCallback`是作为一种优化的方式；

前提：子组件更新的条件是：自身的状态`state`发生了改变，或者是`props`发生了改变，或者了父组件重新渲染，子组件也会触发更新。通常会使用`shouldComponentUpdate / React.memo`来减少不必要的`render`
`shouldComponentUpdate / React.memo`比较比较的时候是浅比较，只对比引用地址是否发生了变化
`useCallback`是针对于函数，传递给子组件的函数

```react
let cb = useCallback(() => {
  // 回调函数
}, [/* 依赖项 */])
// 当依赖项发生变化的时候，才会返回新的函数
```

当父组件的状态修改`setState`的时候，其子组件的`props`并没有发生修改，但由于父组件重新渲染了，也就会导致子组件重新渲染，即使子组件使用`shouldComponentUpdate / React.memo`，因为父组件状态变化，内部的数据会重新分配，也就导致了子组件接收到的函数和之前的函数的引用地址不相同，所以需要进行更新。

```react
const ParentComponent = () => {
  const [count, setCount] = useState(0);
  const handleChildren = () => {
    console.log('clicked ChildrenComponent');
  };
  const handleChildrenCallback = useCallback(() => {  // 进行缓存 handleChildrenCallback 函数不会发送变化，返回的还是之前那个函数，所以也就不会导致子组件无意义的render
    handleChildren();
  }, []);

  const handleParent = () => {
    console.log('clicked ParentComponent');
    setCount(preCount => preCount + 1);  // 更新父组件的状态 会触发子组件重新更新
  };

  return (
    <div>
      <div onClick={handleParent}>ParentComponent --count =={count} </div>
      <ChildrenComponent handleChildren={handleChildrenCallback} />
    </div>
  );
};

const ChildrenComponent = memo(({ handleChildren }) => {
  console.log('ChildrenComponent rending');
  return <div onClick={handleChildren}>ChildrenComponent </div>;
});
```

`useMemo`和`useCallback`类似，都是用于优化。针对的是组件的一些高开销的计算，可以将这些计算进行缓存。

```react
let value = useMemo(() => {
  return count * 100
}, [count])  // 当count发生改变的时候，才会执行useMemo的函数 重新计算
```

区别：
相同点：都是进行缓存，当依赖的数据发生的变化的时候才会执行；
不同点：`useMemo`返回的是计算后结果，是一个值，而`useCallback`返回的是一个函数