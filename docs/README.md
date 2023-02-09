# tech-study-docker (DockerHub Docs)

### 描述 Description

- 基于 `Docker` + `Node.js` 的自动化学习强国工具

### 仓库 Repository

- 关于 GitHub: [tech-study-docker](https://github.com/Xu22Web/tech-study-docker)

### 部署与运行 Deploy and Run

1. 拉取 `docker` 镜像，创建 `tech-study-docker` 容器

   1. 拉取 `docker` 镜像

      ```bash
      docker pull xuzhengze/tech-study-docker
      ```

   2. 创建 `tech-study-docker` 容器

      ```bash
      docker compose up -d
      ```

2. 启用 `PushPlus` 推送

   - 在 [PushPlus 官网](https://www.pushplus.plus/ 'PushPlus 官网') 上，注册登录账号。若有其他用户，可添加为好友，发送[好友消息](https://www.pushplus.plus/liaison.html 'PushPlus 好友消息')。

   - 更改 `Push 配置`（`config/push.ts`），设置管理员`token`（`管理员`能接收到服务推送，`用户`只能收到自己的学习推送）

     ```js
       {
        // 其他配置...
         /**
          * @description 管理员的 token
          */
         token: '管理员 token',
       }

     ```

3. 查看更改 `Schedule 配置`（`config/schedule.ts`），单或多个定时任务配置

   ```js
   [
     {
       /**
        * @description 用户昵称
        */
       nick: '用户昵称',
       /**
        * @description 管理员或者好友 token
        */
       token: '用户 token',
       /**
        * @description cron 表达式
        * @example '0 0 12 * * ?' 表示12点, ['0 0 12 * * ?', '0 0 13 * * ?'] 表示12和13点
        */
       cron: '0 0 12 * * ?',
       /**
        * @description 学习项目配置
        * @example  [文章选读, 视听学习, 每日答题, 专项练习]
        */
       taskConfig: [true, true, true, true],
       /**
        * @description 专项练习 答题失败（由于答完结算，仅包含答题异常或无答案）退出不提交
        * @example true 退出答题不提交 false 继续答题
        */
       paperExitAfterWrong: false,
     },
   ];
   ```

   ```
     # 关于`node-schedule`定时任务的`cron`表达式

     *    *    *    *    *    *
     ┬    ┬    ┬    ┬    ┬    ┬
     │    │    │    │    │    │
     │    │    │    │    │    └ 星期 (0 - 7) (0 或 7 是星期天)
     │    │    │    │    └───── 月 (1 - 12)
     │    │    │    └────────── 日 (1 - 31)
     │    │    └─────────────── 时 (0 - 23)
     │    └──────────────────── 分 (0 - 59)
     └───────────────────────── 秒 (0 - 59，可选)
   ```

4. 进入容器，启动项目

   1. 进入 `tech-study-docker` 容器

      ```bash
      docker compose exec tech-study-docker bash
      ```

   2. 启动 `node` 项目

      ```bash
      pnpm start
      ```
