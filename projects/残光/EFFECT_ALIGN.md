# 残光 · 效果对齐

本地参考：`_local_ref/`（gitignore）。不要把整包参考提交进仓。

| 对照 | 路径 |
| --- | --- |
| contact sheet / 竖屏 / 调色 | `_local_ref/zanko/gallery/` |
| beat / 分析 | `_local_ref/zanko/analysis/`（参考曲无独立歌词轨） |
| 镜头参数 | `_local_ref/zanko/timeline.js` |
| 程序 demo 曲 | `_local_ref/demo/` |

**样品说明：** 参考片里出现的字/汉字是 **shot 动画效果**（如 kanjiSlam），不是单独渲染的歌词层；对齐时按程序效果 / 镜头语义做，不要拆独立 lyric track。

工作流：

1. 需要静帧时，从 gallery 拷到 `assets/textures/`（gitignore）供 `image "..."` 引用
2. 改 `assets/scenes/*.muse`
3. `muse check --project .`
4. `muse preview --project . --entry landscape` → `library/landscape/preview`
5. `muse render --project . --entry landscape --format mp4 --max-duration N` → `library/landscape/out.mp4`
6. 满意后再提交源与 meta（不提交 `_local_ref` / textures 二进制）

## 对齐进度（GPU 产出）

| 项 | 状态 | 备注 |
| --- | --- | --- |
| palette 底板 `image` | 进行中 | `palette_plate.png`（本地 textures） |
| `vignette 0.35` | 进行中 | 对齐 `_local_ref` timeline 默认 post |
| `grain 0.06` | 进行中 | 同默认 post；随帧时间抖动 |
| `bloom 0.3` | 进行中 | 单 pass 高光软糊；非完整 Kawase |
| `lut P2 0.25` | 进行中 | 内置渐变贴图 P1–P5；也可 `lut "path.png" mix` |
| `shot` + `visual … scene` | 进行中 | compose 按 t 叠 scene 层；manifest `active_shots` |
| 程序字效（shot FX） | 进行中 | `fx pulse`；`fx stamp "残"`（几何底 + 系统字体真字，`MUSE_FONT` 可覆盖） |
| shot 转场 | 进行中 | `xfade` / `flash` / `iris` / `cut` + bars；compose 混前后 look（iris 圆心开窗） |

