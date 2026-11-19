# 照片重建 · 地标 / Landmark Reconstructions from Public Photos

用公开的 CC 许可照片（Wikimedia Commons、Flickr）重建的带米制比例的 3D 地标模型，以及可在浏览器里旋转、量距、与真实照片逐张对比的查看页面。

Metric-scale 3D reconstructions of landmarks built only from openly licensed photos (Wikimedia Commons, Flickr), with browser viewers for orbiting, measuring and comparing against each source photo.

## 在线查看 / Live pages

| 页面 | 地址 |
|---|---|
| 地标图库（乐山大佛、镰仓大佛、金阁寺） | https://lil-shake.github.io/landmark-recon/ |
| 乐山大佛查看器（量距 + 照片对比） | https://lil-shake.github.io/landmark-recon/leshan-viewer/ |

页面需要 WebGL；首次加载一个模型约 10–30 MB。

## 3D 模型 / Models

`models/` 里是完整分辨率的 GLB（glTF 2.0 二进制）。单位为米，+Y 朝上，原点在底部中心；顶点属性 `_EVIDENCE` 记录每个顶点被几张照片看到。

| 文件 | 对象 | 注册照片 | 比例依据 |
|---|---|---|---|
| `leshan_v6_1.glb` | 乐山大佛 v6.1 | 110 | 通高 71 m（UNESCO 世界遗产 779 号，ICOMOS 1996 评估） |
| `leshan_v7c2.glb` | 乐山大佛 v7c2（自由空间雕刻 + 补洞） | 251 | 同上，经与 v6 共有照片的相机间距换算 |
| `kamakura_daibutsu_v2h.glb` | 镰仓大佛 | 261 | 佛身高 11.312 m（高德院官方数据） |
| `kinkakuji_v1.glb` | 金阁寺 v1 | 514 | 总高 12.5 m（旅游指南数据，低置信） |
| `kinkakuji_v2.glb` | 金阁寺 v2（天空遮罩 + 雕刻） | 514 | 同上 |

可用 Blender（File → Import → glTF 2.0）或任意 glTF 查看器打开。页面里用的是减面到约 20–45 万面的网页版，存放在 `docs/lm/*/`。

## 方法 / Pipeline

照片抓取与筛选 → COLMAP 稀疏重建 → 稠密重建 → Poisson 网格化 → 用公开的官方尺寸定米制比例 → 照片贴图烘焙 → 网格清理与补洞 → 与每张源照片同机位渲染对比。

## 已知问题 / Known limitations

- 照片拍不到的区域（头顶、背面、被遮挡处）没有几何证据；页面的「证据」模式会标出这些区域，补洞面以紫色显示。
- 金阁寺两个版本质量都偏低：v1 屋顶边缘有天空色毛边，v2 毛边少但孔洞多。
- 包围盒包含崖壁和平台，所以比佛像本身大。

## 许可与署名 / Licence and attribution

- 所有源照片的标题、作者、许可证和来源页面逐张列在 [ATTRIBUTION.md](ATTRIBUTION.md)。源照片的许可证为 CC0、公有领域、CC BY 和 CC BY-SA 各版本。
- 由于部分源照片为 CC BY-SA，本仓库的模型、贴图和缩略图以 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) 共享；再分发时请保留 ATTRIBUTION.md。
- The models, textures and thumbnails are shared under CC BY-SA 4.0 because some source photos are CC BY-SA. Keep ATTRIBUTION.md when redistributing.
