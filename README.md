# qq-agent 插件分发源

这是 qq-agent 机器人的插件自动更新源。`update-agent` 插件会从这里拉取插件清单和包，实现插件自更新。

## 目录结构

```
├── manifest.json                      ← 更新清单（每个插件的版本 + sha256 + 文件名）
├── companion-0.2.0-qq.6.tar.gz       ← 记忆与约定
├── napcat-alert-1.0.2.tar.gz         ← 掉线告警
└── update-agent-1.0.11.tar.gz        ← 自动更新
```

## 访问方式（jsDelivr CDN）

```
https://cdn.jsdelivr.net/gh/<用户名>/<仓库名>@main/manifest.json
https://cdn.jsdelivr.net/gh/<用户名>/<仓库名>@main/napcat-alert-1.0.2.tar.gz
```

把 `<用户名>` 和 `<仓库名>` 换成你的 GitHub 账号和仓库名。

## 怎么发布新版本

1. 用 `node _scripts/打包插件包.mjs <插件目录> --out _patch --with-config` 打包；
2. 把新包上传到这里，命名 `<插件id>-<版本>.tar.gz`；
3. 更新 `manifest.json` 里对应插件的 `version` / `sha256` / `file`；
4. commit + push。

> 注意：`manifest.json` 里的 `sha256` 必须和包文件一致（`sha256sum xxx.tar.gz` 得到），否则别人的 update-agent 校验失败会拒装。
