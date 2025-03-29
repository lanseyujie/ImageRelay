# ImageRelay

> 支持但不限于 docker.io、ghcr.io、gcr.io、registry.k8s.io 仓库中的超大镜像中继。

## 使用说明

0. *Use this template* 使用本仓库为模板创建**私有**仓库（Fork 只能创建公开仓库，欢迎 Watch、Fork、Star 三连本仓库）。

1. *Settings* - *Secrets and variables* - *Actions-New repository secret* 按需创建以下密钥：

> [!TIP]
>
> 临时中继时 `REPOSITORY` 可设置为匿名仓库 [ttl.sh](https://ttl.sh)，为避免镜像被覆盖，可适当增加自定义前缀，如 `ttl.sh/my-custom-prefix`。

|      名称       | 是否必选 |      备注      |
| :-------------: | :------: | :------------: |
| `SRC_USERNAME`  |   可选   |  源仓库用户名  |
| `SRC_PASSWORD`  |   可选   |   源仓库密码   |
| `DEST_USERNAME` |   可选   | 目标仓库用户名 |
| `DEST_PASSWORD` |   可选   |  目标仓库密码  |
|  `REPOSITORY`   |   必选   |  目标仓库地址  |

2. *Issues* - *Labels* - *New label* 依次创建三个标签：`relay-job`、`success`、`failure`。

3. *Settings* - *Actions* - *General* - *Workflow permissions* 修改为 **Read and write permissions** 以开启 workflow 读写 issue 权限。

4. workflow 已设定仅对仓库所有者发起的 issue 有效，使用 relay-job 作为 issue 模板，每个镜像一行，示例：

```
docker.io/library/alpine:latest
# 对于 docker.io 上的镜像可直接写镜像名称
nginx:latest
registry.k8s.io/kube-apiserver:latest
```
