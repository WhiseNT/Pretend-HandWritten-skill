# 示例代表性代码片段

这些片段不仅用于“模仿怎么写”，也用于帮助下游模型理解：哪些写法是稳定主风格，哪些只是包装层、对照片段或频率判断样本。

## snippet-python-core-01

- 语言：Python
- 路径：src/order/service.py
- 层级：业务实现
- 来源类别：本人稳定手写
- 用途：展示语义化局部变量名、早返回和低注释密度
- 建议上下文：4 行

```python
def build_order_summary(order_items):
    if not order_items:
        return []
    summary_rows = []
    for item in order_items:
        summary_rows.append(item.to_row())
    return summary_rows
```

## snippet-python-test-01

- 语言：Python
- 路径：tests/test_order_service.py
- 层级：测试
- 来源类别：本人稳定手写
- 用途：展示测试命名和场景构造方式
- 建议上下文：5 行

```python
def test_build_order_summary_returns_empty_list_for_empty_input():
    result = build_order_summary([])
    assert result == []
```

## snippet-ts-core-01

- 语言：TypeScript
- 路径：src/services/orderService.ts
- 层级：业务实现
- 来源类别：本人稳定手写
- 用途：展示 named export、顺序分支和保守兜底
- 建议上下文：4 行

```ts
export function resolveOrderState(code: string): string {
  if (code === 'paid') return 'done';
  if (code === 'pending') return 'waiting';
  return 'unknown';
}
```

## snippet-ts-wrapper-contrast-01

- 语言：TypeScript
- 路径：src/adapters/orderAdapter.ts
- 层级：包装 / 兼容层
- 来源类别：本人加 AI / 对照片段
- 用途：展示高注释密度与解释性风格，供频率判断和风格对照，不作为主模仿基线
- 建议上下文：6 行

```ts
// Normalize upstream state codes so downstream modules can keep a smaller state set.
export function normalizeRemoteState(input: string): string {
  if (input === 'paid' || input === 'done') return 'done';
  if (input === 'pending' || input === 'created') return 'waiting';
  return 'unknown';
}
```

## snippet-frequency-note-01

- 语言：Mixed
- 路径：core vs wrapper comparison
- 层级：频率对照
- 来源类别：分析辅助片段
- 用途：提醒下游模型注意“核心业务低注释、包装层高注释”这一频率差异，不要把高注释密度误复制到全部代码
- 建议上下文：3 行

```text
Core business files: mostly sparse comments, direct intent through naming.
Wrapper/adaptor files: denser comments, more explanatory phrasing.
Imitation default: follow the lower-comment-density core style unless nearby files show otherwise.
```