## commit与issue关联
!!! info ""
    在提交变更时，commit信息中可以通过`#issue_id`来与issue实现关联。

### 通过commit关闭issue
!!! info "同仓库关闭issue"
    在提交信息时，在commit信息中添加issue关键字和issue编号，即可实现对指定issue的关闭
    关键字有：**close/closes/closed/fix/fixes/fixed/resolve/resolves/resolved**,

    例如，使用`Fixes #16`,就可以使得变更在提交到默认分支后，仓库中的第16号issue会随之关闭

!!! info "关闭多个issue"
    再提交信息里，可以写多组`关键字+#issue_id`, 实现对多个指定的issue进行关闭操作。

----

## 用例
![](/images/close_issue_1.png)
![](/images/close_issue_2.png)
