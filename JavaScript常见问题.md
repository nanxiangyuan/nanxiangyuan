## js 里面的 ?? 和 || 的区别


- 1. ** `||` 的行为: 遇到 falsy 就用右边的值 **

```js
0 || 10                 // → 10      (0 是 falsy)
"" || "default"         // → "default" (空字符串是 falsy)
false || true           // → true    (false 是 falsy)
null || "abc"           // → "abc"
undefined || "abc"      // → "abc"
NaN || 1                // → 1
```

- 2. ** `??` 的行为: 只有在遇到 `null` 或者是 `undefined` 才用右边的值 **

```js
0 ?? 10                 // → 0       ✅ 保留 0
"" ?? "default"         // → ""      ✅ 保留空字符串
false ?? true           // → false   ✅ 保留 false
null ?? "abc"           // → "abc"
undefined ?? "abc"      // → "abc"
NaN ?? 1                // → NaN
```

## Typescript 里面 interface 和 type 的区别

- `interface` 用于定义对象的形状;
    - 不支持基础类型的定义
    - 在 OOP 语言里面可以被类实现 (implements)
    - 可以使用 extends 关键字实现继承;
    - 可以重复定义;
- `type` 用于创建类型别名, 可以给任意类型取一个名字, 包括原始类型, 联合类型, 元组, 对象等;
    - 支持基础类型定义;
    - 不可以被重复定义;


## react 里面的 useMemo, useCallback hook 的作用以及用法

- `useMemo` 用于缓存计算结果, 避免在每次渲染时都进行昂贵的计算;
    - 第一个参数为一个函数, 返回需要缓存的值;
    - 第二个参数为依赖数组, 只有当依赖项变化时, 才会重新计算;
- `useCallback` 用于缓存函数本身, 避免函数在每次渲染时重新创建;
    - 返回一个记忆化的函数;
    - 只有当依赖项变化时, 才会返回新的函数实例;
    - 主要用于传递给子组件的回调函数, 防止子组件因父组件重新渲染而不必要的重新渲染;





