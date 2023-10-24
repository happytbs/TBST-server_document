---
description: by 草方块 等待补全
---

# TAPI文档



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
