---
description: by 草方块
---

# TCraftAPI文档



### 查询



玩家列表

```
/query?query=players
```

```json
{
  "player_count": 1,
  "players": ["GrassBlock2022"]
}
```

#### 服务器状态

```
/query?query=server
```

```json
{
  "vendor": "Paper",
  "tps": 20,
  "bukkit_version": "1.18.2-R0.1-SNAPSHOT"
}
```

#### FSM3状态

```
/query?query=fsm3
```

```json
{
  "version": "3.0.22-b8",
  "modules": [
    "fsm3_defense:protection_area",
    "fsm3_display:bossbar_announcement",
    "fsm3_defense:limited_area",
    "fsm3_display:custom_motd"
  ],
  "enabled_modules": [
    "fsm3_defense:item_defender",
    "fsm3_display:tab_menu",
    "fsm3_chat:chat_filter"
  ],
  "disabled_modules": []
}
```

### 身份验证

#### 创建令牌

```
/auth/create_token?name=GrassBlock2022&pwd=114514
```

```json
{
  "status": "token",
  "msg": "Qyb6RlfqPwhWm5WBQCywXdSbdL3Sdu+BopYdR6r0uSc="
}
```

#### 删除令牌

```
/auth/remove_token?token=Qyb6RlfqPwhWm5WBQCywXdSbdL3Sdu+BopYdR6r0uSc=
```

```json
{
  "status": "success",
  "msg": null
}
```

### 文件

#### 列出文件夹

```
/file/list_repos
```

```json
{
  "we_schematics": "E:/Java/Projects/FSM3/run/plugins/WorldEdit/schematics",
  "minecraft_structures": "E:/Java/Projects/FSM3/run/world/structures/generated",
  "images": "E:/Java/Projects/FSM3/run/plugin/Images"
}
```

#### 列出文件

```
/file/list_files?repo=we_structures
```

```json
{
  "6.schem": "2023/10/21 下午5:37",
  "a.txt": "2023/10/15 下午12:14",
  "test.schem": "2023/10/15 下午12:25"
}
```

#### 上传文件

```
/file/upload?repo=we_structures&file=test.schem
(需要文件内容（U8）作为负载)
```

```json
{
  "status": "existing_file",
  "msg": "E:/Java/Projects/FSM3/run/plugins/WorldEdit/schematics/test.schem"
}
```

#### 下载文件

```
/file/download?repo=we_schematics&file=a.txt
```

```
(file auto download link)
```

### AccessToken | HTTP令牌

作为大部分TCraftAPI要求的AccessToken(访问令牌)的生成模块，我们建议保持其开启。\
当然不开启也是可以的，不过你也就只能用用查询API和开放了权限组的API了。

#### 登录

利用FSM3内建凭据系统关联浏览器用户和游戏玩家的身份，生成鉴权令牌以供后续API验证。

***

路径:

```
/auth/login
```

参数:

| 名称       | 值                 | 样例              |
| -------- | ----------------- | --------------- |
| name     | 玩家名               | GrassBlock2022  |
| password | 凭据(第一次进游戏给你看的那玩意) | password@114514 |

结果:

```json
{
  "token": "(base 64 token)",
  //生成的Token值,留好它
  "lifetime": "1800"
  //剩余token存活时间
}
```

可能的错误:

| 状态码 | 错误ID               | 原因         |
| --- | ------------------ | ---------- |
| 400 | PARAMETER\_MISSING | 缺少玩家名或密码   |
| 400 | AUTHORIZE\_FAILED  | 玩家不存在或密码错误 |

#### 登出

销毁一个令牌,这个令牌将不再可以使用。

***

路径:

```
/auth/logout
```

参数:

| 名称    | 值       | 样例  |
| ----- | ------- | --- |
| token | 生成的访问令牌 | (略) |

结果:

```json
{
  "token": "(base 64 token)"
  //销毁的token，虽然这个值没啥用
}
```

可能的错误:

| 状态码 | 错误ID               | 原因                         |
| --- | ------------------ | -------------------------- |
| 400 | PARAMETER\_MISSING | 缺少AccessToken              |
| 400 | INVALID\_TOKEN     | 不是正确的AccessToken, 可能已被自动销毁 |

#### 续期

可以手动延长一个token的期限。

***

路径:

```
/auth/extand
```

参数:

| 名称    | 值        | 样例   |
| ----- | -------- | ---- |
| token | 生成的访问令牌  | (略)  |
| time  | 延长的时间(秒) | 8000 |

结果:

```json
{
  "token": "(base 64 token)",//token值
  "remain":"2000"//剩余时间
}
```

可能的错误:

| 状态码 | 错误ID               | 原因                         |
| --- | ------------------ | -------------------------- |
| 400 | PARAMETER\_MISSING | 缺少AccessToken              |
| 400 | INVALID\_TOKEN     | 不是正确的AccessToken, 可能已被自动销毁 |
