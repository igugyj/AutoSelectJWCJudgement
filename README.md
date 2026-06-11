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

## 注意事项

- 本脚本针对特定评教系统的 DOM 结构编写（类名 `.qBox.objective`、`.subjective`、`.option-list .option-item` 等）。如果页面结构不同，需要相应调整选择器。
- 请确保在评教页面完全加载后再执行脚本。
- 建议执行后人工快速核对一遍，避免因页面结构变动导致漏填或误填。

## 许可证

本工具采用 [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](https://creativecommons.org/licenses/by-nc-nd/4.0/) 许可。  
简而言之：您可以自由分享（复制、分发本作品），但**不得用于商业目的**，**不得修改/演绎**，且**必须署名原始作者**。
