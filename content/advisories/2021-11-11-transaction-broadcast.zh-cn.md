
+++
title = "告示：对交易自动重试的回复"
date = "2021-11-11"
[ author ]
  name = "Dogecoin Foundation"
+++

注意：本公告的先前版本使用“我们”来指代独立于基金会的团体。它已被编辑以澄清。

币安今天暂停了狗狗币的提款，并表示他们在狗狗币中发现了一个“小问题”。基金会想说明一下这个问题：

几个月前（请注意，虽然较早的帖子说是一年，但首次确认提及是4月）币安通知狗狗币钱包维护人员他们有交易卡住的情况，这意味着他们没有被成功挖出。维护人员建议币安在这些交易中使用 RBF（replace by fee），这将用支付更高费用的新交易替换原始交易。值得注意的是，建议这样做是因为按费用替换会使之前的交易无效（因此称之为“替换”）。由于交易禁用了 RBF，维护人员当时建议手动创建一个新交易，这将具有相同的效果来强制使之前的交易无效。

一段时间后，币安说他们有帐户对帐问题。维护人员无法使用币安提供的数据重现这些问题，但建议（几个月前，现在）使用“-zapwallettxes”命令行选项来缓解该问题。这是值得注意的，因为维护人员相信这也可以防止这个问题。

在11月10日，维护人员收到通知，在v1.14.5更新之后，之前卡住的交易突然中继成功；可能是因为转账费率在v1.14.5中降低了，使得以前有效但不可中继的交易可以中继。维护人员从币安获得的唯一案例是其费用自 v1.14.5 起有效的一笔交易，但在 1.14.3 及之前无效（太低）。请注意，币安最近几天直接从 v1.14.3 更新到 1.14.5。

目前维护人员认为这种情况是因为之前卡住的交易已自动重试，就像升级后每个节点重新启动时会发生的那样-并且通过了，因为现在所需的最低中继费用较低。这是费用降低后的一种正确行为。

## 教训

* 取消交易的正确处理是将要取消的交易的输入用于不同的交易，这会使第一个交易失效。
  * 理想情况下，请尽量使用“replace-by-fee”，不然就重新创建一个交易并用之前的费用作为手续费，以此将先前的交易失效。
* 请注意，转账交易没有具体的超时期限，但通常由于内存限制而被丢弃。

## 指导

基金会没有收到关于这种情况的进一步报告。对于任何担心停滞无效交易的提供商，我们建议您停止节点，删除mempool.dat文件以防万一，然后使用“-zapwallettxes”启动节点。

对于有顾虑的个人用户，请注意将您所有的狗狗币发送回自己（理想情况下是一个新地址，但您可以使用现有地址）也将花费任何先前的交易输出，并使此类“卡住”的交易失效。

