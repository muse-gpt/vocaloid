# assets/audio

导引音轨（gitignore）。副歌纵切需要本机生成占位床：

```text
# from muse-language repo root (debug napi present)
node --input-type=module -e "import { createRequire } from 'node:module'; const n=createRequire(import.meta.url)('./target/debug/muse_napi.node'); n.writePlaceholderToneWav('../vocaloid/projects/残响花园/assets/audio/chorus_bed.wav', 20, 48000);"
```

验收时用绑定轨 `chorus_bed.wav`；勿把参考曲或未授权演唱放进本目录入库。
