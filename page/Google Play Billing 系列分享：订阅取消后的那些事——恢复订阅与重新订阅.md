Google Play Billing 系列内容专为中文开发者打造，旨在解答 Play Billing 中常见的疑惑。今天，我们将探讨用户取消订阅后的两种操作——**恢复订阅**和**重新订阅**，并分析它们的区别及注意事项。

---

## 恢复订阅与重新订阅的区别

在与开发者的交流中，我们发现许多人对 Play 提供的 **Restore**（恢复订阅）和 **Resubscribe**（重新订阅）功能感到困惑。以下是两者的核心区别：

### 恢复订阅（Restore）
恢复订阅的关键在于“恢复”，它有以下几个条件：
1. 用户已取消订阅。
2. 订阅尚未过期。
3. 只能通过 Play 订阅中心操作。

恢复订阅实际上是对原订阅的恢复，**purchaseToken** 不会发生变化。

### 重新订阅（Resubscribe）
重新订阅本质上是一次新的订阅购买，特点如下：
- 适用于已过期的订阅（不超过 1 年）。
- 用户可通过应用内或 Play 订阅中心完成操作。
- 重新订阅会生成新的 **purchaseToken**。

---

## 两者的对比

以下表格直观展示了恢复订阅与重新订阅的差异：

| 功能         | 恢复订阅（Restore）                  | 重新订阅（Resubscribe）            |
|--------------|--------------------------------------|------------------------------------|
| 操作条件     | 取消订阅但未过期                     | 订阅已过期（不超过 1 年）          |
| 操作方式     | 仅限 Play 订阅中心                   | 应用内或 Play 订阅中心             |
| purchaseToken | 不变                                 | 生成新的 purchaseToken             |

---

## 特殊场景与注意事项

### 取消订阅未到期时的重新购买
当用户取消订阅但尚未到期时再次购买，新的订阅会替换旧订阅，并在同一到期日期续订。此时：
- 新的订阅会生成新的 **purchaseToken**。
- 旧的 **purchaseToken** 仍然有效，开发者需及时标记为失效。

开发者可通过 **linkedPurchaseToken** 字段获取旧订阅的 **purchaseToken**，但请注意：
- 不要依赖 **linkedPurchaseToken** 判断订阅是否有效。
- 应通过 Google Developer API 的 **expiryTimeMillis** 字段获取订阅的准确到期时间。

### 交易确认
对于重新购买的交易，开发者需及时确认，尤其是使用 Play Billing Library 2.0 或以上版本的开发者。未在 3 天内确认的交易将被 Play 取消。

---

## 相关资源

以下是一些官方文档链接，供开发者参考：
- [销售订阅内容](https://developer.android.google.cn/google/play/billing/subs)
- [订阅到期之前](https://developer.android.google.cn/google/play/billing/subs#resubscribe-before)
- [Google Developer API 的订阅接口](https://developers.google.cn/android-publisher/api-ref/rest/v3/purchases.subscriptions/get)
- [实时开发者通知参考指南](https://developer.android.google.cn/google/play/billing/rtdn-reference)

---

## 总结

恢复订阅和重新订阅是 Play Billing 中两个重要的功能，开发者需根据用户的具体操作场景正确处理相关逻辑。如果您对订阅功能还有疑问，欢迎进一步探索官方文档或与我们交流。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)