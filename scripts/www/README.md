# P3R · 计时与日程（DAILY CONSOLE）

一个 P3R（Persona 3 Reload）UI 风格的单页小工具，只有两个功能：

1. **计时器** —— 正计时 / 倒计时，可自定义时间，带背景音乐
2. **日历 + 日程清单** —— 月份、日期、星期与真实时间对应，含节假日

蓝色单色系、斜角板块、描边斜体大字、荧光青 + 洋红点缀，以及一直轻微在动的水光/气泡；背景是主角落水后的水下画面无缝循环，右侧小窗是主角坐电车的画面无缝循环。打开时会先播放一段同风格的开场动画（约 2.5 秒，点击或按键可跳过）。

---

## 打开方式

双击 `index.html` 即可（推荐 Edge / Chrome）。无需安装、无需联网、不会上传任何数据。

> 浏览器要求先有一次点击/按键才允许播放声音，这是正常的；开场动画的那一下点击就会解锁音频。

---

## 计时器

- **STOPWATCH 正计时 / COUNTDOWN 倒计时**：右上角切换
- **预设**：05 / 15 / 25 / 45 分钟
- **SET 自定义时间**：
  - 倒计时模式下设定「倒数多久」
  - 正计时模式下设定「从多少开始累计」（起点）
  - 时/分/秒 三格输入，`↑↓` 微调，`Enter` 确认，`Esc` 取消
- **键盘**：`空格` 开始 / 暂停，`R` 重置，`1`–`4` 选预设
- **水面**：计时时面板底部的真实水位会随时间匀速变化，但永远不碰上下边缘——
  - **倒计时**：从接近顶部（约 80%）开始往下退，退到底部上方就停住；最后约 6% 的时间里水位保持不变
  - **正计时**：从半高偏高（约 46%）开始上涨，约 10 分钟升到顶部下方（约 80%）后保持不动
- 倒计时归零会出现 **TIME UP** 提示并响一声轻提示音；计时状态会自动保存，刷新后接着走

### 背景音乐

- 计时开始时会淡入播放你给的 `私が守るから -Reload-`，暂停 / 重置 / 计时结束时淡出
- 控制条右侧的 **♪ ON / OFF** 可以随时开关（会记住选择）
- 音乐循环播放，音量默认压得比较低，不盖过按键音

### 按键音

所有可点的东西都有对应的按键音，来自你给的四个文件：

| 文件 | 用在哪 |
|---|---|
| `确认.mp3` | 开始/暂停、添加日程、完成打勾、弹窗「设定」等确认操作 |
| `选择.mp3` | 点日期、选预设、点输入框、切换月份、回到今天等选择操作 |
| `返回.mp3` | 重置、删除日程、关闭提示、取消等返回/撤销操作 |
| `切换.mp3` | 左右切换 TIMER / CALENDAR、切换正倒计时、开关 BGM |

---

## 日历 / 日程

- 左上角是月份：`10 ◀ 11 ▶ 12`，点箭头或相邻月份即可切换，`T` 键回到今天
- 点选日期后，右侧白色面板显示当天的日程
- **添加**：底部输入时间 + 内容，按 `Enter` 或点 `＋`
- **完成**：单击日程行打勾 / 取消
- **修改**：双击标题可直接编辑（`Enter` 保存，`Esc` 取消）
- **删除**：点行尾的 `×`，或选中行按 `Delete`
- **选日**：点日期，或用方向键（`←→` 前后一天，`↑↓` 前后一周）
- 今天的日期是洋红色三角，有日程的日期下方有蓝色小点
- 日程保存在浏览器本地（localStorage），刷新、关闭浏览器都不会丢

### 节假日

日历里会自动标出节日，日期下方有一行小字：

- **法定节假日**（春节、元旦、清明、劳动节、端午、中秋、国庆、除夕）——数字和小字是洋红色
- **其他节日**（元宵、七夕、重阳、腊八、情人节、母亲节、父亲节、万圣夜、感恩节、平安夜、圣诞节等）——小字是青色
- 选中某一天时，右侧日程面板顶部会出现当天的节日名与「节假日 / 节日」标签；那天没有安排时，空状态也会提示「今天是××」
- 底部统计里会显示「节日 N」（当月节日数量）
- 农历节日（春节、中秋等）按浏览器的中国农历计算，闰月不会误判；清明按节气公式计算

---

## 文件夹结构

```
index.html                        # 全部界面、样式和逻辑（单文件）
assets/audio/confirm.mp3          # 按键音 · 确认
assets/audio/select.mp3           # 按键音 · 选择
assets/audio/back.mp3             # 按键音 · 返回
assets/audio/switch.mp3           # 按键音 · 切换
assets/audio/bgm.mp3              # 计时背景音乐（已压到 128kbps）
assets/video/underwater.mp4       # 水下循环背景（无缝循环、已压缩）
assets/video/tram.mp4             # 电车小窗（无缝循环、已压缩）
assets/img/underwater-poster.jpg  # 背景视频首帧（视频加载前显示）
assets/img/tram-poster.jpg        # 电车视频首帧
README.md
```

## 手机 / APK 打包

页面本身已经按「铺满屏幕 + 刘海适配」做好了：

- `viewport-fit=cover`，用 `env(safe-area-inset-*)` 给刘海和底部手势条让位，背景（视频、水色、暗角）始终铺到屏幕最边缘；
- `<meta name="theme-color">` 与 `html/body` 背景都是 `#01040f`，不会出现白边；
- 竖屏时会自动把背景向左裁切，落水的主角始终在画面里（横屏显示完整画面）；
- 触屏设备会自动隐藏 `SPACE` / `R` / `1–4` / `ENTER` 这类键盘提示，换成「点 START」「点一下打勾」的点按说明；接键盘的电脑仍然显示快捷键；
- 禁用页面缩放和横向滚动，按钮去掉了点按高亮和 300ms 延迟。

打包 APK 时，WebView 外层还要做一次全屏设置，否则状态栏/导航栏那一条仍是系统默认颜色（这部分页面控制不到）：

```kotlin
// 1) 让内容铺到状态栏 / 导航栏下面
WindowCompat.setDecorFitsSystemWindows(window, false)
window.statusBarColor = Color.TRANSPARENT
window.navigationBarColor = Color.TRANSPARENT
WindowInsetsControllerCompat(window, window.decorView).apply {
    isAppearanceLightStatusBars = false
    isAppearanceLightNavigationBars = false
}
// 刘海屏：允许内容进入刘海区域
window.attributes.layoutInDisplayCutoutMode =
    WindowManager.LayoutParams.LAYOUT_IN_DISPLAY_CUTOUT_MODE_SHORT_EDGES

// 2) WebView
webView.setBackgroundColor(0xFF01040F.toInt())
webView.settings.apply {
    javaScriptEnabled = true
    domStorageEnabled = true
    mediaPlaybackRequiresUserGesture = false   // 计时开始时 BGM 才能自动播放
    allowFileAccess = true
    allowContentAccess = true
    builtInZoomControls = false
    displayZoomControls = false
}
webView.loadUrl("file:///android_asset/index.html")
```

如果你用的是「网页转 APK」之类的工具，对应选项勾上：全屏 / 沉浸式、透明状态栏、允许媒体自动播放、开启 JavaScript 与 DOM Storage、禁止缩放；App 主题背景色设为 `#01040F`。如果工具自带的标题栏出现，那是外壳的界面，不是页面，在工具里关掉即可。

> 页面里的音频、视频都使用相对路径，把整个文件夹（含 `assets/`）原样放进 APK 的 `assets` 目录即可。

## 说明

- 按键音做了音量归一化（原文件偏轻），保留四个文件各自的音色；背景音乐压成 128kbps MP3 以减小体积。
- 素材来自你提供的视频与图片，视频重新压制并做了交叉淡化接缝；原图仅用于生成视频首帧海报。
- 字体使用系统自带字体（Bahnschrift / Impact / 微软雅黑），换电脑会回退到相近字体，布局不受影响。
- 所有日程只存在你这台电脑的浏览器里；清除浏览器站点数据会同时清除日程。
- 建议把文件夹固定放在一个位置（例如桌面）使用，不要频繁改名或移动。
