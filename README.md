# 🎄 Merry Christmas — 3D 粒子圣诞树（网页版）

由 [ZekangLi-Zico/Christmas-Tree](https://github.com/ZekangLi-Zico/Christmas-Tree) 的 Pygame 版**逐行移植**为
零依赖单文件网页：`index.html`（约 23 KB，无任何外部请求，双击即可离线运行）。

## 在线地址

https://yelaing.github.io/xmas/

## 原版 → 网页版 对应关系

| 原版（tree.py） | 网页版 |
| --- | --- |
| `gen_tree_points()` 50000 点，70% 螺旋灯带 + 30% 蓬松填充 | 同参数，`buildTree()` |
| `gen_ground_points()` 6 圈地面光环 | 同参数，`buildGround()` |
| `gen_star_points()` 空中亮点 | 同参数，`buildStars()` |
| `gen_heart_points()` 隐式方程 `(x²+y²−1)³ − x²y³ ≤ 0` 爱心 | 同参数，`buildHeart()` |
| `project_point()` 旋转 + 俯仰投影 | 同公式，内联进主循环 |
| `sort(key=depth, reverse=True)` 深度排序 | 256 桶计数排序（O(n)，免 GC） |
| `pygame.draw.circle` | `ImageData` 直接写像素 + 圆形精灵表 |
| 前景 2D 大雪花 | 径向渐变精灵 + `drawImage` |
| Pygame 60 FPS 主循环 | `requestAnimationFrame` + `dt` 时间步 |

## 相对原版增加的东西

- **Bloom 泛光层**：1/4 分辨率放大 + `mix-blend-mode: screen`，粒子有真实灯光的光晕
- **移动端自适应**：竖屏时画面按高度放大居中裁切，树不会被缩成一小条
- **WebAudio 合成《Jingle Bells》**：零音频文件，点右下角 ♪ 开启
- **10 万级粒子下仍保持流畅**：预分配 TypedArray、计数排序、隔帧泛光

## 自定义

打开 `index.html`，改文件顶部：

```js
var CONFIG = {
  title:    'Merry Christmas',
  subtitle: '愿为你亮着的灯，一颗都不落',
  signer:   '2025 · 圣诞快乐'
};
```

想改粒子密度就调 `var N_TREE = 50000;` 这一行（手机端会自动按 `Q` 系数降采样）。

## 交互

- 点击画面：加速旋转
- 双击：全屏
- 右下角 ♪：音乐开关

---

原版版权归 [ZekangLi-Zico](https://github.com/ZekangLi-Zico)；网页移植版仅作节日祝福用途。
