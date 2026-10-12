# 原创 Vocaloid 风格 MV 计划

本计划是参考 `vocaloid-style-mv-pipeline` 的制作方法而写的方案。当前阶段优先**本地对齐效果**（见 `EFFECT_ALIGN.md` 与 gitignored 的 `_local_ref/`）；参考素材可以拷到本机对照，**先不提交**。入库与发布时再换成原创或明确授权素材。

## 项目目标

制作一首约 3 分钟的原创电子 / Vocaloid 风格歌曲，并从同一 Muse project 生成：

- 横屏 16:9 预览帧和视频计划
- 竖屏 9:16 重新构图的预览帧和视频计划
- 带节拍 / 歌词标记的 WAV 导引音轨
- MIDI 或 MusicXML 乐谱
- 歌词 timing JSON、镜头清单和源 hash manifest

## 原创设定

工作名：`残响花园`。主题是「一个声音在城市停电后留下的可见回声」。主角、歌曲、歌词、配色和资产全部重新创作。

视觉母题：

- 环形声纹
- 断开的电缆
- 会发光的纸花
- 由夜景到晨光的色彩变化

禁止使用参考曲中的人物、地名、道具组合或歌词句子。

## 时间与结构

歌曲先由原创音频和歌词生成 beat grid、bars、sections、stops、energy 和词级 timing。下面只定义可迁移的结构角色，不填入参考曲的原句或具体镜头。

| 段落 | 时间目标 | 视觉职责 | 主要产物数据 |
| --- | ---: | --- | --- |
| intro | 0:00–0:12 | 单一声纹、标题和世界规则 | beat markers |
| verse-a | 0:12–0:42 | 城市建立、角色首次出现 | shot list + lyric timing |
| pre-chorus-a | 0:42–1:00 | 收紧、留白、一次停顿 | stop intervals |
| chorus-a | 1:00–1:28 | 纸花爆发、歌词前后景分层 | cue events |
| interlude | 1:28–1:38 | 一段可替换的序列素材 | image sequence refs |
| verse-b | 1:38–2:06 | 反转母题、色彩切换 | palette cues |
| pre-chorus-b | 2:06–2:22 | 声纹与角色动作对齐 | word/beat alignment |
| bridge | 2:22–2:45 | 极简黑场、记忆碎片 | hold/freeze events |
| final-chorus | 2:45–3:12 | 母题回收、由夜到晨 | transition cues |
| outro | 3:12–3:20 | 标题回收和静默尾卡 | end-card + credits |

## Entry 设计

根目录 `muse.von` 中使用三个入口（scenes）：


- `landscape`：16:9 主剪辑，负责完整歌词层和主镜头
- `vertical`：9:16 独立构图，复用时间和资产 id，但允许重新排镜头与文字安全区
- `data`：不画面，输出 beat grid、歌词 timing、shot manifest 和源 hash，供复查与其他 entry 消费

每个入口可以有多个 output。生成区必须按 entry 隔离；清理 `artifacts/vertical/` 不得影响横屏或源资产。

## 镜头约定

每个镜头至少包含：`id`、`start`、`end`、`scene`、`params`、`layers`、`transition`、`accessibility`。

`scene` 是可替换的渲染函数名，不是把实现代码嵌进 `.muse` 的自由脚本。

图层顺序固定为：

```text
背景 → 程序效果 → 角色/道具 → 歌词 → 前景文字或遮罩 → 后期
```

歌词层不能被背景后期模糊；高闪烁和纯白闪帧必须通过硬约束检查。

## 阶段门禁

1. 原创音频、歌词和版权说明就绪，生成 beat/lyric timing JSON。
2. 编写 `landscape.muse` 与 `vertical.muse`，`muse check` 无错误。
3. 生成 contact sheet，复查镜头边界、歌词安全区、停顿和闪烁规则。
4. 生成 WAV、乐谱、帧预览和两个方向的 manifest；视频编码在 Muse 的已验证后端可用时才启用。
5. 只删除 `artifacts/` 后重建，比较 manifest 中的源 hash 与 output id，确认结果可复现。

## 素材边界

- **本地对齐：** `_local_ref/`、`assets/` 下的二进制与参考拷贝可以存在，全部 gitignore，用于对画面与节奏。
- **提交 / 发布：** 不把参考仓歌曲、歌词、角色图、成片写进 Git；换成原创或明确授权素材后再考虑入库。
- 效果对齐清单见 [`EFFECT_ALIGN.md`](./EFFECT_ALIGN.md)。
