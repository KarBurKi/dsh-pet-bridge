# dsh-pet-bridge

DSH 桌宠桥接插件：**纯本地写盘，不联网、不订阅 mux、不读控制队列**。

订阅 DSH 的 agent 生命周期事件，把状态追加写入共享桥目录下的 `dsh-{pid}.jsonl`：

- 多实例分区：每个 host 进程一个文件，消费端 glob `dsh*.jsonl` 即可（兼容旧的单文件 `dsh.jsonl`）
- 桌宠侧（DshMonitor）以 byte-offset 方式 tail 读取，**不回放历史**
- 可选 watchdog：宿主进程消失时写一条收尾记录，避免桌宠状态卡死

## 安装

`link:` 进 profile 的 `dependencies` 与 `dsh.profile.bundles`，重启 DSH。桥目录默认在 `~/.dsh/pet.json` 指向的位置（见 `pet.json` 的 `bridgeDir`）。

## 文件

| 文件 | 说明 |
|---|---|
| `index.js` | 插件主体，零依赖 |
| `cordis.patch.yml` | 挂载声明 |
| `verify_import.mjs` | 自检脚本：`node verify_import.mjs` |

## 许可

MIT
