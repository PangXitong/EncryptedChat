# EncryptedChat
端到端加密聊天，汉化自[https://github.com/triestpa/Open-Cryptochat](https://github.com/triestpa/Open-Cryptochat)
以下为汉化后的原版介绍

# 浅谈在Javascript中使用公钥密码

## 打开Cryptochat-教程

密码学很重要。如果没有加密，我们所知道的互联网是不可能的——网上发送的数据就像在拥挤的房间里大喊的信息一样容易被拦截。密码学也是时事中的一个主要话题，在[执法调查]中发挥着越来越重要的作用(https://en.wikipedia.org/wiki/FBI%E2%80%93Apple_encryption_dispute)和[政府立法](https://www.politico.com/tipsheets/morning-cybersecurity/2017/11/10/texas-shooting-could-revive-encryption-legislation-223290)。

加密对于记者、活动家、民族国家、企业和普通人来说是一种宝贵的工具，他们需要保护自己的数据免受黑客、间谍和广告机构的威胁。

了解如何利用强加密对于现代软件开发至关重要。在本教程中，我们不会深入研究密码学的基本数学和理论；相反，重点将放在如何将这些技术用于您自己的应用程序上。

![Screenshot 5](https://cdn.patricktriest.com/blog/images/posts/e2e-chat/screenshot_5.png)

在本教程中，我们将介绍端到端2048位[RSA加密]的基本概念和实现(https://en.wikipedia.org/wiki/RSA_（密码系统）信使。我们将使用[Vue.js](https://vuejs.org/)用于协调前端功能以及[Node.js](https://nodejs.org/en/)使用[Socket.io]的后端(https://socket.io/)用于在用户之间发送消息。

-实时预览-https://chat.patricktriest.com
-Github存储库-https://github.com/triestpa/Open-Cryptochat

我们在本教程中介绍的概念是用Javascript实现的，并且主要是与平台无关的。我们将构建一个传统的基于浏览器的web应用程序，但您可以调整此代码以在预构建的桌面中工作（使用[Electron](https://electronjs.org/))或移动（[Rreact Native](https://facebook.github.io/react-native/)，[离子](https://ionicframework.com/)，[科多瓦](https://cordova.apache.org/))如果您关心基于浏览器的应用程序安全性，请使用应用程序二进制。[^1]同样，在另一种编程语言中实现类似的功能应该相对简单，因为大多数语言都有信誉良好的开源加密库；基本语法将发生变化，但核心概念仍然通用。

>免责声明-这是端到端加密实现的入门，而不是构建浏览器聊天应用程序Fort Knox的最终指南。我一直致力于提供有关向Javascript应用程序添加加密的有用信息，但我不能100%保证生成的应用程序的安全性。在这个过程的各个阶段都可能出现很多问题，尤其是在本教程未涵盖的阶段，例如设置网络托管和保护服务器。如果你是一名安全专家，并且你在教程代码中发现了漏洞，请随时通过电子邮件联系我(patrick.triest@gmail.com)或在下面的评论部分。

要阅读更多信息，请访问-https://github.com/triestpa/Open-Cryptochat
___

这个应用程序是100%开源的，您可以随意使用代码。

```

MIT许可证（MIT）
版权所有（c）2018 Patrick Triest
特此免费许可任何人获得副本
本软件和相关文档文件（“软件”），以处理
在软件中不受限制，包括但不限于权利
使用、复制、修改、合并、发布、分发、分许可和/或销售
软件的副本，并允许软件的使用者
按照以下条件提供：
上述版权声明和本许可声明应包含在
软件的副本或实质部分。
软件是“按原样”提供的，没有任何形式的担保，明示或
隐含的，包括但不限于适销性保证，
适用于特定目的和不侵权。在任何情况下
作者或版权持有人应对任何索赔、损害或其他
责任，无论是在合同诉讼、侵权行为还是其他方面，由，
与软件、使用或其他交易有关
软件。

```