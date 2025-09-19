# 教程：iOS 15 上如何修复 ChatGPT 登录问题（Route Error 400 / Session Expired）

> **仅供学习交流** 本方法通过写入会话 Cookie，绕过 iOS 15 Safari 登录流程中的兼容性问题。请勿在不受信任的设备上使用，也不要分享你的 token。

 原因说明
在 iOS 15 的 Safari上，ChatGPT 网页登录常见报错：
- `Route Error 400 – Unknown Error`
- `Session expired`

通常是重定向过程中 **会话 Cookie 丢失/被阻止** 导致登录流程无法完成。
 思路（TL;DR）
1. 在一台能正常登录的桌面浏览器上复制会话 Cookie `__Secure-next-auth.session-token` 的值。
2. 在 iOS 15 设备上用书签脚本把该 Cookie 写入到 `chatgpt.com` 域。
3. 刷新页面 → 应该已处于登录状态。



 步骤详解

（1）桌面端获取 session token
1. 访问 <https://chatgpt.com> 或 <https://chat.openai.com> 并完成登录。  
2. 打开 **DevTools → Application（应用）→ Cookies**。  
3. 找到 **`__Secure-next-auth.session-token`**，复制其 **Value**（一般是一长串，以 `eyJ...` 开头）。

（2） iOS（Safari）创建书签脚本
1. 在 Safari 随便打开一个网页 → **分享** → **添加书签**（命名为 `Set Cookie`）。  
2. 打开 **书签 → 编辑 → Set Cookie**，把 URL 替换为以下脚本（把 `在这里插入你的sessiontoken` 换成上一步复制的值）：

javascript：
javascript:(function(){document.cookie="__Secure-next-auth.session-token=在这里插入你的sessiontoken; domain=chatgpt.com; path=/; secure";alert('成功');})()
