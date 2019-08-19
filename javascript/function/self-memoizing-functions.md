# 自记忆函数

```javascript
function isPrime(value) {
  if (!isPrime.answers) {
    isPrime.answers = {};
  }

  if (isPrime.answers[value] !== undefined) {
    return isPrime.answers[value];
  }

  let prime = value !== 0 && value !== 1; // 1 is not a prime

  for (let i = 2; i < value; i++) {
    if (value % i === 0) {
      prime = false;
      break;
    }
  }

  return isPrime.answers[value] = prime;
}
```

这个方法具有两个优点：

- 由于函数调用时会寻找之前调用所得到到的，所以用户最终会乐于看到所获得的性能收益。
- 它几乎是无缝地发生在后台，最终用户和页面作者都不需要执行任何特殊请求，也不需要做任何额外初始化，就能顺利进行工作。

当然这种方法并不是像玫瑰和提琴一样完美，还要权衡利弊：

- 任何类型的缓存都必然会为性能牺牲内存。
- 纯粹主义者会认为缓存逻辑不应该和业务逻辑混合，函数或方法只需要把一件事做好。
- 对于这类问题很难做负载均衡测试或估计算法复杂度，因为结果依赖于函数之前的输入。
