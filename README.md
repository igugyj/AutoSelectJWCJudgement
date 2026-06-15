# 教学评价自动填写工具

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

> 一键自动完成「学生评教」表单：所有单选题默认选第一项，主观题统一填写“无”。

## 功能说明

- **单选题**：自动勾选每个单选题的第一个选项（通常是“非常满意”或类似评价）。
- **主观题**：自动将所有文本框内容填充为 `无`。
- **触发事件**：模拟 `change` 和 `input` 事件，确保页面上的任何监听逻辑被正确触发。

## 使用方法

1. 打开浏览器的**开发者工具**（快捷键 `F12`）。
2. 切换到 **控制台（Console）** 标签页。
3. **复制下方所有代码**（点击右上角复制按钮或手动全选 `Ctrl+A` + `Ctrl+C`）。
4. 粘贴到控制台中（`Ctrl+V`），然后按 `Enter` 键执行。
5. 看到控制台输出 `已完成自动选择` 即表示执行成功。

```javascript
/*
 * 教学评价自动填写工具
 * 版权信息：本脚本采用 CC BY-NC-ND 4.0 许可（署名-非商业性使用-禁止演绎）
 * 作者：Pfolg
 * 链接：https://github.com/igugyj/AutoSelectJWCJudgement
 * 许可证详情：https://creativecommons.org/licenses/by-nc-nd/4.0/
 * 说明：不得用于商业目的，不得修改/二次分发，使用必须保留此版权声明
 * 用法：复制（Ctrl + A; Ctrl + C）文件内容粘贴（Ctrl + V）到终端（F12 转 Console）回车
 */

// 选择所有单选题的第一项
document.querySelectorAll('.qBox.objective').forEach(question => {
    const firstOption = question.querySelector('.option-list .option-item:first-child input');
    if (firstOption) {
        firstOption.checked = true;
        firstOption.dispatchEvent(new Event('change', { bubbles: true }));
    }
});

// 填写主观题为"无"
document.querySelectorAll('.qBox.subjective').forEach(question => {
    const textarea = question.querySelector('textarea');
    if (textarea) {
        textarea.value = "无";
        textarea.dispatchEvent(new Event('input', { bubbles: true }));
    }
});

console.log('已完成自动选择');
```
## 重要提醒

在使用本脚本前，请务必阅读并遵守以下原则：

- 遵守校方规则：请在使用前确认你所在学校/机构是否允许学生通过自动脚本填写评教。如有明确禁止，请勿使用。

- 合理使用：本脚本仅供个人学习或提高效率使用，不得用于任何违反校纪校规或法律法规的场合。

- 按实际填写：自动勾选的“第一个选项”可能不符合你的真实评价。建议在提交前人工逐项核对，并根据实际情况手动修改。

- 辅助作用：本脚本仅作为一个辅助工具，不保证能完美适配所有评教系统，也不对因使用本脚本导致的任何后果（如数据错误、账号受限等）承担责任。使用者应自行判断并承担风险。

## 常见问题 (FAQ)

**Q1：为什么执行后控制台提示“已完成自动选择”，但页面上没有任何变化？**  
**A1**：请确认你当前所在的页面是否为**具体的评教答题页**（即能看到所有单选题和文本框的页面）。脚本只会在包含 `.qBox.objective` 或 `.qBox.subjective` 类名的页面中生效。如果停留在课程列表、评教说明页或已提交页面，脚本不会产生任何效果。

**Q2：在控制台粘贴代码时被提示“不允许粘贴”或没有任何反应，怎么办？**  
**A2**：部分网站（如某些在线考试系统、管理后台）会禁用控制台的粘贴操作。解决方法如下：  
- 方法一：在控制台中输入 `allow pasting` 并回车（某些浏览器安全机制会解除粘贴限制）。  
- 方法二：先将代码粘贴到记事本中，然后**逐行手动输入**到控制台（不推荐，效率较低）。  
- 方法三：将代码保存为浏览器书签（“小书签”），点击书签即可注入脚本。具体做法：新建书签，地址栏填写 `javascript:` 后接压缩后的代码（移除换行和注释）。  
- 方法四：使用 Chrome 开发者工具 – 点击控制台右上角的 **设置图标**（⚙️） → 取消勾选 “Eager evaluation” 或检查是否开启了 “Disable JavaScript” 之类的选项。

**Q3：执行后一部分题目填上了，另一部分没有变化，是怎么回事？**  
**A3**：可能是由于评教系统的页面结构与脚本使用的选择器不匹配。例如：  
- 某些单选题可能使用了不同的类名（如 `.radio-group` 而非 `.option-list`）。  
- 某些文本框可能不是 `<textarea>` 而是 `<input type="text">`。  
- 页面采用动态加载，部分题目在滚动后才出现。建议先滚动页面确保所有题目完全加载，再运行脚本；如果仍有遗漏，可以根据实际页面结构**微调选择器**（右键检查元素，修改对应的 CSS 选择器）。

**Q4：我填错了，想撤销自动填写的所有内容，可以一键清空吗？**  
**A4**：本脚本不提供“撤销”功能。如需重置，请直接**刷新页面**（F5 或 Ctrl+R），刷新后页面会恢复到未填写的初始状态。提交前强烈建议刷新一次，手动核对或重新填写。

**Q5：脚本执行后可以自动提交吗？**  
**A5**：本脚本**仅负责填写**，不会自动点击“提交”按钮。你需要在确认所有选项符合真实意愿后，**手动点击提交按钮**。自动提交存在误操作风险，因此未纳入本工具。

**Q6：学校评教系统改版了，脚本还能用吗？**  
**A6**：如果页面布局发生重大变化（例如类名全部更换），脚本将失效。你可以尝试自行修改代码中的选择器（如 `.qBox.objective` 替换为新的类名）。如果缺乏修改能力，建议放弃使用脚本，转而手动填写。

**Q7：使用本脚本会被后台检测到吗？**  
**A7**：本脚本仅模拟普通用户的点击和输入行为，不会发送任何额外请求。但理论上，学校系统可以通过记录“所有选项均选第一项且主观题全部填‘无’”的行为模式来推断使用了脚本。请自行评估风险，并始终遵守学校关于评教的相关规定。

## 注意事项

- 本脚本针对特定评教系统的 DOM 结构编写（类名 `.qBox.objective`、`.subjective`、`.option-list .option-item` 等）。如果页面结构不同，需要相应调整选择器。
- 请确保在评教页面完全加载后再执行脚本。
- 建议执行后人工快速核对一遍，避免因页面结构变动导致漏填或误填。

## 许可证

本工具采用 [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](https://creativecommons.org/licenses/by-nc-nd/4.0/) 许可。  
简而言之：您可以自由分享（复制、分发本作品），但**不得用于商业目的**，**不得修改/演绎**，且**必须署名原始作者**。
