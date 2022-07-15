> 岁月静美，在于它必然的流逝。
>
> 春花秋月，夏日冬雪。
>
> 你若盛开，清风自来。
 
> ***心中无尘，码字如神。*** 这个口号好嗨，回头补一份在 [Markdown 官方教程](https://markdown.com.cn/basic-syntax/ "Markdown 官方教程") 上学习使用 `Markdown` 的笔记。
## 前言
心血来潮，想试试把自己的笔记同步到 GitHub 上，于是乎就从网上学习了一些使用方法，把这次的过程记录在此，供以后查阅。

这次使用的是 GitHub $+$ Visual Studio Code 的组合，GitHub 作为远程托管库，本地通过 Visual Studio Code (VS Code) 作为编辑器进行记录书写。

如果今后遇到什么问题，我会回来补充。

---

## 前期准备工作
在进行配置部署前我们需要做两项前期准备工作：

1.在本地创建一组 SSH Key 用于从 GitHub 上同步远程代码库。不过这是一步可选操作，因为在 VS Code 完全可以使用 HTTPS 的方式对 GitHub 进行仓库获取。

2.在本地创建一组 GPG KEY 用于对本地提交的代码进行签名认证。

### 创建 SSH Key Pair
对于 Windows 系统，详细的内容可以参阅微软帮助文档：[适用于 Windows 的 OpenSSH 密钥管理 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_keymanagement "适用于 Windows 的 OpenSSH 密钥管理 | Microsoft Docs")。这里我们需要做的是在正确安装 OpenSSH 之后，**在具有管理员权限的终端中运行：**

> `ssh-keygen -t ed25519 -C "your_email@example.com"`

**需要特别注意的是，`your_email@example.com` 需要填写 GitHub 里认证过的邮箱，否则在连接时会报错。**

### 创建 GPG Key Pair
在 Git 中内置了 GPG Key 生成，可以参照[在 Github 上使用 GPG 的全过程](https://zhuanlan.zhihu.com/p/76861431 "在 Github 上使用 GPG 的全过程")里的流程生成一组密钥对。**同样地，密钥对生成过程中的邮箱需要填写在 GitHub 里认证过的邮箱。**

如果使用的是在[ GunPG 官网](https://gnupg.org/download/index.html)上下载的程序进行密钥对生成，则需要将密钥对导入到 Git 中，方法是：在 *Git Bash* 中 使用 `gpg --import [your key path]` 命令。

## 在 GitHub 上创建远程代码库
这部分比较简单，注册个账号就可，然后在账号设置中将前期准备的 SSH Key 和 GPG Key 的公钥添加到账号中，就大功告成了。

## 在 VS Code 上进行本地编辑和上传
从 GitHub 上克隆代码比较简单，将仓库的链接复制到 VS Code 里的资源管理器中就行，一切按照提示来应该问题不大。只是需要注意按以下步骤进行本地仓库的初始化。在 VS Code 自带的终端中，进入到本地仓库的地址，然后执行：

1.初始化用户名，此处最好是你的 GitHub 账号名称。
> `git config --local user.name "your_name"`

2.初始化邮箱地址，此处**必须**是你的 GitHub 账号里的认证邮箱。
> `git config --loacl user.email "your_email"`

3.设置将对你的提交进行签名的 GPG 密钥，`your_key_id` 是在生成过程中的一段字符，可以在 GitHub [SSH and GPG keys](https://github.com/settings/keys "GitHub SSH and GPG keys") 中查看。
> `git config --local user.signingkey "your_key_id"`

4.若想每次提交时都进行 GPG 签名，可以输入命令。
> `git config --local commit.gpgsign true`

## 完

---