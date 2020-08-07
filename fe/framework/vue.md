## 生命周期

beforeCreate、created、

beforeMount、mounted、

beforeUpdate、updated、

beforeDestroy、destoryed

## 异步更新

vue 的更新会存储在一个队列 `flushSchedulerQueue`，同一个更新不会 push 两次。vue 在 nextTick 时将更新队列全部更新。