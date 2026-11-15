# 项目工坊管理系统

一个面向工坊团队的网页管理系统，用于组织项目、任务、成果和成员协作。本仓库保留界面调整前的设备预约和共享资料入口；AI 知识问答服务及接口在本公开版中停用。

## 项目内容

- 工作台：项目、任务、成果验收、成员及权限等功能，基于 Leantime 3.12.0 扩展。
- 扩展服务：`services/` 保存协作、考勤、设备预约和网关的试用配置及适配源码。这些服务需要单独安装、配置和联调，并非以下核心演示的一键启动部分。
- 数据与配置：仓库不包含本机数据库、业务文件、测试账号、密钥或历史数据。

## 获取代码

下载并解压仓库中的 `workshop-project-source.zip`，在解压后的目录执行下面的命令。压缩包包含完整的工坊扩展源码、配置和许可文件。

## 本机运行核心演示

需要 Docker Desktop（含 Docker Compose）和 Python 3。先启动 Docker Desktop，然后在仓库目录执行：

```sh
python3 setup.py
docker compose up -d --build
```

打开 <http://127.0.0.1:18773/install>，按照页面完成初始安装和管理员账号设置。安装完成后，在仓库目录执行：

```sh
docker compose exec app php bin/leantime workshop:install
```

然后登录 <http://127.0.0.1:18773/workshop>。停止演示使用 `docker compose stop`；再次启动使用 `docker compose up -d`。数据保存在 Docker 卷中，`.env` 仅保存在本地。

该命令启动的是项目管理核心的独立演示：聊天、共享资料、考勤和设备预约依赖 `services/` 中的独立服务及其身份、权限配置，不能仅凭核心演示视为已联通。完整系统原为本机试用环境，其公网部署、邮件、完整权限回收和容量测试尚未完成，请勿直接作为生产环境使用。

## 目录

- `overlay/`：工坊扩展和界面文件；构建镜像时覆盖到官方 Leantime 镜像。
- `services/`：协作、考勤、设备预约及网关的试用配置与适配文件。
- `Dockerfile`、`compose.yaml`：核心演示的镜像和容器配置。

## 上游项目和许可

核心基于 [Leantime](https://github.com/Leantime/leantime) 3.12.0，保留其 GPL-3.0 许可证，见 [LICENSE](LICENSE)。协作适配使用 Nextcloud；试用服务涉及 Frappe HR 和 LibreBooking，各项目的许可证和部署要求分别适用。界面内第三方资源说明见 `overlay/public/workshop-assets/THIRD_PARTY_NOTICES.md`。
