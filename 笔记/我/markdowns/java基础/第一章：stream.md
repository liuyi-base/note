# 第一章：stream



## 1.1：lambda表达式

1. 函数式接口，只能有一个方法，否则映射不上。
2. default方法除外。
3. object方法除外。
4. 静态方法引用：className :: methodName
5. 非静态方法引用：new className() :: methodName

## 1.2: stream特点

1. 中间操作不执行，只是增加逻辑。
2. 终值操作只能有一个，而且放在最后。
3. 执行顺序为每一个元素走完所有流程，然后下一个元素。而非所有元素走完一个步骤（filter等）再执行下一个步骤。

