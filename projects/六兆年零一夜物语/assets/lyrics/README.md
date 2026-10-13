# 歌词 timing

授权前：本机 `_local_ref/lyrics/song.timing.json`（由 LRC 生成，gitignore）；副歌纵切另有 `_local_ref/lyrics/chorus.timing.json`（墙钟 53–73 → 本地 0–20）。

开源仓不存放日文全文。场景：

- 全片：`asset song_lyric = "_local_ref/lyrics/song.timing.json"`
- `chorus_cut`：`asset chorus_lyric = "_local_ref/lyrics/chorus.timing.json"`

行级可选 `cue_id`（稳定语义片段）：供日后中英显示对齐，不把日语词 timing 按索引套到译文。

本机可另放 `_local_ref/lyrics/chorus.locale.json`（CueId×locale 显示表）。`chorus_cut` 用：

```muse
localized from chorus_locale
lang "zh-Hans"
```

未授权前 localization 全文不进开源仓；译文缺项时 `muse check` 失败。
