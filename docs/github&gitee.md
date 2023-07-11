## 1

-   gitee SSH公钥设置

    [SSH 公钥设置 | Gitee 产品文档](https://help.gitee.com/base/account/SSH公钥设置)

-   github SSH key 设置

    账户添加SSH: [Adding a new SSH key to your GitHub account - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

    生成SSH: [Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## 2

上传文件至仓库：

```bash
git add --all
git commit -m "..." # 会在仓库对应文件的处显示，应该是用于标记哪一次上传
git push -u origin [ master / main ]
```

## 3

gitee pages 更细需要手动点击更新，

github pages 可以自动更新