# Pixel Watch Nailong Watch Face (奶龍錶面)

Wear OS **Watch Face Format (WFF v2)** custom watch face for Pixel Watch (Wear OS 4 / 5+), matching the Pixel Watch Utility layout with an interactive tilt-wandering Nailong.

## Features

- **Pixel Watch Utility Layout:** Bold 24-hour clock (`#E8F553`), uppercase date (`THU NOV 26`), and 3 circular metric widgets (**Steps**, **Battery**, **Heart Rate** with `--` fallback).
- **Smooth Full-Face Tilt Wandering:** Nailong glides smoothly across the watch face using 30fps `EASE_OUT` `<Transform>` expressions with circular boundary clamping (zero clipping around the round bezel).
- **5 Tilt Animations + Tap Reactions:**
  - Flat (`0` unread): Idle breathing — tap Nailong to cycle **Idle → Check → Wave → Think**.
  - Tilt Left / Right (`> 12°`): Runs Left / Right.
  - Steep Top-Left / Top-Right (`> 30°`): Dedicated diagonal climb-hop + wave animation.
- **Style-Aligned Notification Badge:** When unread notifications arrive (`UNREAD_NOTIFICATION_COUNT > 0`), Nailong raises its paw holding a dark-olive + `#E8F553` lime-ringed count badge (capped at `99+`) and carries it while tilting.
- **Watch Face Editor Customization:** Long-press the watch face → **Customize** to switch **Layer** (Behind / In Front of Clock), **Home Position** (Top-Right / Center / Top-Left / Bottom-Center), and **Size** (Small / Medium / Large / Hidden).

Design doc: [`NailongWatchFace_Design_v4.pdf`](NailongWatchFace_Design_v4.pdf)

---

## 安裝到 Pixel Watch 教學

先從 [GitHub Releases](https://github.com/syhstanley/pixel-watch-nailong/releases/latest)（或本 repo 的 [`releases/nailong-watchface-v2.0.apk`](releases/nailong-watchface-v2.0.apk)）下載 APK。

### Step 1：在 Pixel Watch 開啟開發者選項與無線偵錯

1. 手錶打開 **設定 → 系統 → 關於 → 版本**。
2. 連點 **「版本號碼」7 次**，直到顯示「您現在已是開發人員」。
3. 返回 **設定 → 開發者選項**，開啟：
   - **ADB 偵錯**
   - **無線偵錯**（手錶需先連上與電腦/手機相同的 Wi-Fi）

### Step 2：安裝 APK（二選一）

#### 方法 A：用電腦透過 Wi-Fi ADB 安裝（推薦）

1. 在手錶的 **無線偵錯** 點選 **「使用配對碼配對裝置」**，記下顯示的 `IP:配對Port` 與 **6 位數配對碼**。
2. 在電腦終端機執行配對：
   ```bash
   adb pair <手錶IP>:<配對Port>
   # 依提示輸入 6 位數配對碼
   ```
3. 回到手錶的 **無線偵錯** 主畫面，記下「IP 位址和通訊埠」的 `IP:連線Port`，執行連線與安裝：
   ```bash
   adb connect <手錶IP>:<連線Port>
   adb install -r nailong-watchface-v2.0.apk
   ```

#### 方法 B：免電腦，直接用手機安裝

1. 手機下載本 repo 的 `nailong-watchface-v2.0.apk`。
2. 在手機 Play 商店安裝 **Wear Installer 2**（或 **Bugjaeger**）。
3. 依照 App 指示輸入手錶無線偵錯的配對碼與 IP:Port，選擇剛剛下載的 APK 推送安裝即可。

### Step 3：套用與自訂錶面

1. 在手錶上 **長按目前錶面** → 往右滑到最後點 **「新增」** → 選擇 **Nailong Watch Face**。
2. 套用後可再次 **長按錶面 → 點擊編輯（鉛筆）圖示**，調整前後圖層、平放位置與奶龍大小。
3. 安裝完成後，建議回 **開發者選項** 關閉「無線偵錯」以節省電力。

---

## Build from Source

```bash
./gradlew :watchface:assembleDebug
# Output: watchface/build/outputs/apk/debug/watchface-debug.apk
```

## License / Credits

- Clock & UI font (`watchface/res/font/utility_bold.ttf`): **DM Sans Bold** (SIL Open Font License 1.1, Google Fonts).
