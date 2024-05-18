---
title: 搭建自己的chatgpt
comments: true
tags: 资料
categories: Web
description: 搭建自己的chatgpt

[//]: # (sticky: 10000)
abbrlink: 1683208917
date: 2023-05-04 00:00:00
from:
url:
author:
about:
avatar:
top: 999
---

# 搭建自己的chatgpt



## 项目选型

1、这里我们选择 [ChatGPT-Next-Web](https://github.com/Yidadaa/ChatGPT-Next-Web) 项目（其他项目也行，看自己的喜好），选择这个项目是因为天然契合本次教程，UI 也还可以，还内置了海量的内置 prompt 列表。

![[图片]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042150636.png)

![[图片]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042150856.png)





2. 项目部署选择了 Vercel，这个前端的小伙伴应该都比较熟悉，其实一开始考虑过 Github Pages，但 GitHub 的问题在于国内访问速度很慢，所以这里选用了 Vercel，相比于 GitHub Pages，国内访问 Vercel 的速度更快，而且无需科学上网，并且个人使用还是免费的！

3. 选择 [CloudFlare](https://dash.cloudflare.com/) 进行域名管理与 CDN 加速，我个人比较喜欢将域名解析交给 [CloudFlare](https://so.csdn.net/so/search?q=CloudFlare&spm=1001.2101.3001.7020) 管理，并且可以将其纳管的站点传送到全球多个地点，大大提高网站的速度和性能。

4. 准备工作
   本教程选用 ChatGPT-Next-Web 项目，Vercel 部署，CloudFlare 进行域名管理与加速，所以需要提前准备好：

   1、Github 账号。

   2、Vercel 账号。

   3、CloudFlare 账号。

   4、OpenAI API KEY。

   5、一个域名，若没有，需要购买，后面会介绍怎么买。

部署工作
1、Github 中 Fork ChatGPT-Next-Web 项目到个人仓库。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-L6YfjD5L-1681127653637)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=OWE5ODlhZTI4NTQzNzZmYjk1MTBkYTM2ZjAyNzI3M2Jfdk5tVHo0M1lnMzBLbVp3TGlUdkFyTzJUR2Vsa3VpQVlfVG9rZW46RHM5eGI2dmd3b0hQTmh4OWRoZWNjS0VsbmhMXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042153742.png)

2、在 Vercel 中点击“Add New Projct”，选择从 Github 部署。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-VIuzhGD3-1681127653638)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=YTUxYjI0MmFhYjk0ODQ5MGQwN2I3NTYxYmIyOWUyNDdfSVVjNVlNOVFvVEFiM2VoN05BdENXZWdmWTVaNUs0N0xfVG9rZW46TG9ORmJNMFREb2w4cEF4VnI4d2NHaERFbkRlXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042153313.png)

3、选择刚刚我们 Fork 的项目进行导入。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-LXzOl5dy-1681127653639)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=MjdlMDUwYjBkMTczOTI0ODk5MGExODZkZDBlNjJjMGNfYnVNeU9UdlBpbDBnYjdCSEJNWE40ZUoyYjBsbGN5TEdfVG9rZW46TGY4QmJMUzlQb2d3MDd4bW4wNWNzZGlMbmhmXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042153903.png)

4、配置参数，这里主要添加如下两个参数：

CODE 代表网站的访问控制，这里填一个你记得住的密码。
OPENAI_API_KEY 填你的 OpenAI 账户的 Key。
我这里是举例 111 和 222，以你实际为主。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-9422AdRA-1681127653639)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=YjVkNWY3OGE0OGU4NWQ0ZmFjNGRkOGVjNmZmZTI5ZmJfRk5Fa1lrWUFjaHZpWXVFSGRFWG1Bd1FQUWZyMzdvWUNfVG9rZW46S1ZKSGJIelg4b0FCdnB4VW9DemNFbHNkbnpkXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042153487.png)

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-T2omwbEt-1681127653640)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=YjM4MWRkM2NmMTVmOWM1NmRmZjIwMWVlYzc4ZmYzNjZfdkJQYUxMUHdYUUVORWJSWTZEdTFyM3NnTVBrQmVDNkZfVG9rZW46RUo1cWJHTldib1p1N3d4YXF6eGNOYWxSbnpkXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042153852.png)

5、点击 “Deploy” 按钮，顺利的话稍等片刻就会弹出部署成功的页面，还有浮夸的撒花~



![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-vnRnVHPI-1681127653641)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=ODgzMjQzODdmNTcwMjQyZjgyZDJlNGYwY2IwNTA2N2VfaUZ6eFlQNWJBYXdDbGR6VzIzU0NhTzYwc2VXS3ZyaGxfVG9rZW46SDBSMWJOZ3JWb1FoWkZ4dFQzcmNDSGNKbklmXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042212378.png)

6、点击 “Continue to DashBoard” 按钮，查看部署信息。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-ikgm9o4n-1681127653643)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=MDg3MDY5OTk2NjY2MjY0ZGVjMWZhMmNmNTA3NjdhYjRfSjJsYVNyQ0txUUdLdG1VQVBkU2VVak5BYU9wT0dQMVlfVG9rZW46V200TmJUalQxb2hrcmZ4TzRpVmNrVlRnbkdkXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042154976.png)



7、可以看到，自动为我们分配好了域名 chat-gpt-next-web-liart-kappa-35.vercel.app，其实到这里就完成了，奈何 vercel.app 因为被大量使用，自然而然被墙掉了，你可以点点看，应该是访问不了的。不过好在 Vercel 官方提供了单独的 IP 和 CNAME 地址给大家，对于国内的用户来说，配置一下单独的域名解析，依然可以享受 Vercel 提供的服务。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-awwrFqqx-1681127653644)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=MzdlN2VhZDdmYWVmODk3YmJkM2MyYWZhZWNiMGE0MmFfVTZlS2dYd2xEQmtUNHJlSDR4Tmp3YzZ2aXQzbmZ5bGpfVG9rZW46TVh5VWJOYmtRb3E5SVN4U2M1U2NSQmF0bnViXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042154565.png)

8、绑定自定义域名，这里假设你已经有了一个域名（如果没有，请继续往下看），点击 “View Domains”，进入域名配置页面，输入待绑定的域名，然后点击 “Add” 按钮完成自定义域名的添加。



![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-iQAPX3rG-1681127653644)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=MjM0NDAyMjNjN2IzNWNmZjc3NjNlYjdhODAwZjI5YmRfcThIajVvOVp6cnNRVFZGRGRWalBXaExNOHNXZ1dISzNfVG9rZW46VDFvUmJPTFZNb0ZPakt4d0FudGNUUzQ3bmVoXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042154567.png)

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-NvVHFevU-1681127653645)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=YWQ5NjljNjE0MzExMmFmYjE3NDk5YmIyYjQ4YjFjMTdfVVdsbTd2VEQzWFRTMHdqRWhHV2lGTHN2dktjbXBvY0NfVG9rZW46UkJ2SmJWSXg5b0NnTjN4Nk1tOGM4NkFGbmdQXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042155401.png)

9、会弹出来一些需要做的配置，接下来需要去我们的域名提供商那里根据 Vercel 给出的要求进行配置，这一步如果不会可以参考后面的 CF 域名管理章节。

10、现在你已经可以通过自定义域名，访问到你的私人专属 ChatGPT 网站了，初次访问可能有些慢，因为此时 Vercel 正在生成 SSL 证书，耐心等一会儿再访问~





购买域名
如果没有域名，那么你需要购买一个属于你的专属域名，域名买的好，财务自由实现的早~

可以选择以下渠道进行购买：

Namesilo



Namesilo 提供永久免费的域名隐私保护，防止别人通过 WHOIS 查询获取域名所有者的个人注册信息。作为对比，Godaddy 的隐私保护是 60 元/年，Namecheap 是免费提供第一年。
安全性高
支持账户登录二次验证和 Domain Defender，保护账户和域名安全。登录、解锁域名等，都可以设置邮件或短信提醒。
支付方便
支持支付宝、Paypal、信用卡等多种方式付款。
1、登录网站后，在大大的搜索框搜索你想要申请的域名，添加到购物车。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-QJVbVXmR-1681127653645)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTFiNzg4NWVjOGNlZDU4Y2UzYjA1ZjNjY2NkYmYxMjhfeE1MZFBlQm9Lek5XZ1E5cG5tQ1pmY3BDMVBLdFB6SHdfVG9rZW46UmYxVWJ3a1hhb2JhS3V4OFdwRmNDWGxObndkXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042156379.png)

2、再点 “Checkout” 进行结算，填入我的优惠码 tree1024 可以享受 1$ 的优惠~

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-rOMhxtzL-1681127653646)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=N2UyNDVhODBlMTRhYjllNDg4NzU0OGIzYjQ3MDE0MThfbXVRcXJqTjh0MHlBYnlIajlpN0lPTzhoWUVxd0pVd1pfVG9rZW46RVFZQ2J1azZWb3JXZFp4TTFVT2Nzb25jblplXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042156902.png)

3、接下来填写账号信息，填个大概就行，只用填带星号的，邮箱请用常用邮箱。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-08AeEPhN-1681127653647)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=YmIwMWI3ODhiYWJlOWVjN2ViMjI2NGEyZWZiMjNlOGRfeTNFcUJpZlZTZjFVT0xnQVFkUDd3cUN5bkE3NWhxYVlfVG9rZW46QzI4dGJEbUR2b1YwVFh4M1VhYmNKUEJxblFoXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042156989.png)

4、选择一种付款方式，购买成功后，你会收到官方发来的邮件。

## CF 域名管理

1、将上面购买到的域名添加到 Cloudflare 中管理，点击“添加站点”按钮，输入域名。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-WlOPszWi-1681127653647)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmRlNTZmY2I2NGM1Y2Q1NDNlYmIyMDhlMjA4YjRlZmNfcFpXNTgybkQ5QVBXUmpBWTJza3VTWUNLWDZPU0lwSHBfVG9rZW46RzdzWWJtWlB4b1FaOVl4OFJNU2NJbmNqbnhnXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042156191.png)

2、选择 Free 计划，因为我们是个人建站，用不了太多乱七八糟功能。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-AhTaWTes-1681127653648)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=ODA0Mzc2M2NmNTMwZjMyOWI5NWZmMjgwZmYxNzkzYjFfWG0yUFlDOG42SHJCUnhzSldFN0ZIOFl6TkV3Tm0zVUZfVG9rZW46QUtLSGJTOVpub3pQS2Z4TUJnZ2NtbldRbjViXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042157449.png)

3、然后就出现了概述页面，我们按照提示完成名称服务器设置。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-XryvP314-1681127653648)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=MjhmM2ZiYmZmZjc2OTY2YTQwYmJiYjhkMWNmYzVkMzdfRWVTRFl3TmFTVld3Tk1vUDZYcWxRdExUcWVnYmtkMURfVG9rZW46VUNDc2JIMFAzb0twazV4aXUzZmNpQ1hJbkFoXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042157899.png)

4、我是在 NameSilo 购买的域名，所以就进入 NameSilo 的管理页面，完成名称服务器替换，登录你的 NameSilo 账号，右上角点 “Manage My Domains”，然后会看到下图，先勾选你要解析的域名，再点 “change Nameservers”。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-BWJeK83o-1681127653649)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=MjNjNDViMTQ5ZGMwMDQxZGEyZDkxMWRlODllOTIwY2NfRFFSeXlMWlhoUmd2MGdjWU1NNmNsTDJRdW1oZTJZQkNfVG9rZW46Sk4zSWJMNTQwbzAyZTR4dzZmbGNJTEs1bmdiXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042157789.png)

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-xvcLHz1z-1681127653649)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=Yzc5MzEyZjcyMzY0OGY1NGU5NjhiMWExY2I1OGYzMWJfQ25YQzBzVDFkNzdXZU5seE1JYWFkTUJCQmxyQ3BPTDNfVG9rZW46UkswQWJ6cVdxb2lZSkJ4MGVlaWNiTFQ4blFkXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042158202.png)

5、把 CloudFlare 中的名称服务器地址（**athena.ns.cloudflare.com**、**jake.ns.cloudflare.com**）填到 Namesilo 里然后保存，解析生效官方的说法是24小时，但一般半个小时之内就OK了。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-aUIkL7Aw-1681127653650)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=YWJjNTcyNzM5ZDdkY2MyYmJkNTMzNmJmNTM1NDBiZGFfTnFYYU1XM0M0ZFhlb0FmelFJWVp0QnRIS0lYaGFxa2hfVG9rZW46RUFRV2J3VFdhb2k5RWd4VEZCdmMzbmlabkpiXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042158245.png)

6、再到 CloudFlare 中，检查名称服务器，检查通过会发一封邮件

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-PUEkjs5d-1681127653650)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDg2NTcxMTY2M2EwYmM3Y2QyMTEzMDMxODRiZmUzZGRfeUdRN2l4R2pYdFpEY1N5NVh5cUtnU25NZ1JWZm00RVVfVG9rZW46Q3ZQM2IydUxkb001a0x4Q2hHUmNySU9zbjk3XzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042158605.png)

7、配置 SSL，先在 SSL/TLS 中申请**客户端 SSL 证书**：SSL/TLS -> 客户端证书 -> 创建证书，加密模式选择完全，不必保存之后生成的证书和私钥

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-l2UpJ57r-1681127653651)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=Nzc5NWNmY2Q5M2ZjNjMwOTIxMjA1MTg5MzMyM2MyYzZfa0xMYkVVVm9MSzhCdHRnUWpuek9aUHJXTVFJZFl4VVlfVG9rZW46WUhjZ2JDaWJob0JPd0d4YlVaUGNzZzJ5bmluXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042158755.png)

8、添加 CNAME 记录，DNS -> 记录 -> 添加记录。添加 CNAME 记录（**cname.vercel-dns.com**）如下，并保存，这里以 www.tree1024.xyz 为例。![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-vmhYHTUf-1681127653652)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=YjNkNGE1NDE5ZDZlY2Q2M2QxNWQyNTE2ZTEwOTlkOGVfMFRrbEdmM2pPbjJUdFdEeG05VXowTnE4RG5ydEVPMlZfVG9rZW46Sk1oaGJ5Rldmb2V5OFp4S2E4a2NsZHBjbnJoXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042159365.png)

9、添加 A 记录（可选），如果你想用根域名访问你的站点，比如 https://tree1024.xyz，需要添加一条 A 记录，直接将根域名解析到 Vercel 的服务器地址（**76.76.21.21**）即可！

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-7ylJeabY-1681127653652)(https://u5mwn062nv.feishu.cn/space/api/box/stream/download/asynccode/?code=ODQ1OTQ0YmU5MjI4MWZlODlmNWY1MzQ4ZDZjZGUwZTZfWjczbFd6Y1NBUnFIRmR1Y2dmVW1xYmZIdzEwYUJ3MGpfVG9rZW46S1FaU2J3S3Vab2gzZmt4amVTSWNieThDblFlXzE2ODExMTYwOTk6MTY4MTExOTY5OV9WNA)]](https://gitee.com/fadeway32/fadeway32/raw/master/img/202305042159868.png)

10.然后你就自己的站点了