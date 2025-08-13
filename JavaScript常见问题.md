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





