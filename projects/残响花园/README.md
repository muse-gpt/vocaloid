# 残响花园

原创 Vocaloid 风格 MV 案例的 **20 秒副歌纵切**（非残光效果对齐样）。

- `muse.von`：`landscape`（16:9）/ `vertical`（9:16 · 1080×1920）/ `data`
- 共享音乐时钟 `0s..20s`、BPM 120、歌词 timing JSON、绑定音轨声明
- 歌词为原创占位词；导引 WAV 本机生成（见 `assets/audio/README.md`）

```text
muse check --project projects/残响花园
muse render --project projects/残响花园 --entry landscape --max-duration 2
muse render --project projects/残响花园 --entry vertical --max-duration 2
```
