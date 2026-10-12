# Muse Studio 工程模板

复制本目录为 `projects/<歌名>/`。布局对齐 Unity：工程合同在根目录，源在 `assets/`，可重建缓存在 `library/`。

## 目录

| 路径                                 | 角色                                       |
|--------------------------------------|--------------------------------------------|
| `muse.von`                           | 工程根合同：scenes / outputs / render      |
| `assets/scenes/*.muse`               | 场景源（真相）                             |
| `assets/scenes/*.muse.meta`          | 侧车元数据（GUID、画幅等）                 |
| `assets/audio/` · `assets/textures/` | 导入素材                                   |
| `library/`                           | 可删可重建的 preview / export（gitignore） |

不要再使用 `entries/`、`assets/ref/`、`muse.toml`、`settings/muse.von`。
