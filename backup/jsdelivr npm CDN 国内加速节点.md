## JSDelivr 介绍

JSDelivr 是由 **@Cloudflare** 提供的免费开源公共 CDN。

### 默认节点

- 默认提供的节点是：**cdn.jsdelivr.net**
  该节点国内几乎不可用，需要使用可用性高的节点作为替代。

### 可用的 jsDelivr 节点

- 常用于加速 GitHub/npm 项目，可通过更改节点改善项目在国内的可用性。

| 节点                      | 描述            | 可用性     |
| ------------------------- | --------------- | ---------- |
| gcore.jsdelivr.net        | Gcore 节点      | 可用性高   |
| testingcf.jsdelivr.net    | Cloudflare 节点 | 可用性高   |
| quantil.jsdelivr.net      | Quantil 节点    | 可用性一般 |
| fastly.jsdelivr.net       | Fastly 节点     | 可用性一般 |
| originfastly.jsdelivr.net | Fastly 节点     | 可用性低   |
| test1.jsdelivr.net        | Cloudflare 节点 | 可用性低   |
| cdn.jsdelivr.net          | 通用节点        | 可用性低   |

### 第三方提供的 jsDelivr 节点

- 以下是一些第三方提供的 jsDelivr 节点，可用于国内访问。

| 节点               | 来源    | 特点 |
| ------------------ | ------- | ---- |
| jsd.cdn.zzko.cn    | 国内CDN |      |
| jsd.onmicrosoft.cn | 国内CDN |      |
| jsdelivr.b-cdn.net | 台湾CDN |      |
| cdn.jsdelivr.us    | Anycast |      |

### npm 节点

- npm 节点：**unpkg.com** 国内几乎不可用，可用下方国内 cdn 节点。

| 节点                  | 来源   | 特点           |
| --------------------- | ------ | -------------- |
| npm.elemecdn.com      | 饿了么 | 同步快，缺的多 |
| npm.onmicrosoft.cn    | 公益   | 需准确的版本号 |
| unpkg.zhimg.com       | 知乎   | 同步慢         |
| npm.akass.cn          | 公益   | 需准确的版本号 |
| cdn.chuqis.com/npm/   | 公益   | 需准确的版本号 |
| code.bdstatic.com/npm | 百度   | 仅同步热门包   |

请根据项目需求和国内访问情况选择合适的 CDN 节点。

### 使用方法

如果是 GitHub 的网址，需要先转换成 jsdelivr 地址。

GitHub 原地址（访问有点慢）：

https://raw.githubusercontent.com/用户名/仓库名/main/文件夹/文件名

添加 Jsdelivr CDN 加速后的链接（提高 GitHub 静态资源的访问速度）：

https://cdn.jsdelivr.net/gh/用户名/仓库名@main/文件夹/文件名

然后使用上述任一地址替换 cdn.jsdelivr.net 部分即可。

**另外**：访问 https://cdn.jsdelivr.net/gh/用户名/仓库名@main/ 可以看到文件列表

从 GitHub 迁移到 jsDelivr

jsDelivr 是适用于 npm 和 GitHub 的免费、快速且可靠的开源 CDN。大多数 GitHub 链接都可以轻松转换为 jsDelivr 链接。

### 访问最新版
`https://cdn.jsdelivr.net/gh/${用户名}/${仓库名}/${文件路径}`

### 访问特定版本号
`https://cdn.jsdelivr.net/gh/${用户名}/${仓库名}@${发布的版本号}/${文件路径}`

### 访问特定分支
`https://cdn.jsdelivr.net/gh/${用户名}/${仓库名}@${分支名称}/${文件路径}`

### 获取目录下的文件列表，给出的目录地址最后加上 / 即可
`https://cdn.jsdelivr.net/gh/vuejs/docs/`

### css, js 类型文件支持自动创建 .min 文件
### 如果不存在，jsDelivr 将为您生成
`https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/src/jquery.min.js`

### jsDelivr如何刷新缓存
首先 CDN 缓存同步需要时间是个正常现象，像我们这样改了就要看到刷新结果的属于 ”特殊需求“ 了，但也很常见了。

方法也很简单，只要把想要刷新的文件路径的前缀 cdn 改成 **purge** 即可，看到一段返回的 json 对象，即表示刷新成功，再访问 cdn 地址就可以看到最新的版本了。

```
# 刷新前
https://cdn.jsdelivr.net/gh/user/images/my.jpg

# 刷新缓存
https://purge.jsdelivr.net/gh/user/images/my.jpg

# 返回结果
{
  "id": "783923723947294",
  "status": "finished",
  "timestamp": "2022-04-17T15:52:23.536Z",
  "paths": {
    "/gh/user/images/my.jpg": {
      "throttled": false,
      "providers": {
        "fastly": true,
        "bunny": true,
        "cloudflare": true,
        "gcore": true,
        "quantil": true
      }
    }
  }
}

# 再次访问即可
https://cdn.jsdelivr.net/gh/user/images/my.jpg
```