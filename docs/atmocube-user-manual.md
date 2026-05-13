# Atmocube Home Assistant Integration — User Manual
# Atmocube Home Assistant 整合 — 使用手冊

<p align="center">
  <img src="../wo_Logotype_SYM_BL.png" alt="WOOW Logo" width="200"/>
</p>

---

## Table of Contents / 目錄

1. [Pair Atmocube to App & Dashboard / 配對 Atmocube 至 App 及 Dashboard](#1-pair-atmocube-to-app--dashboard--配對-atmocube-至-app-及-dashboard)
2. [Enable Modbus TCP/IP on Dashboard / 在 Dashboard 啟用 Modbus TCP/IP](#2-enable-modbus-tcpip-on-dashboard--在-dashboard-啟用-modbus-tcpip)
3. [Install Atmocube Integration in Home Assistant / 安裝 Atmocube 整合至 Home Assistant](#3-install-atmocube-integration-in-home-assistant--安裝-atmocube-整合至-home-assistant)
4. [Setup Atmocube Integration in Home Assistant / 設定 Atmocube 整合](#4-setup-atmocube-integration-in-home-assistant--設定-atmocube-整合)

---

## 1. Pair Atmocube to App & Dashboard / 配對 Atmocube 至 App 及 Dashboard

### Prerequisites / 前置需求

- Atmocube device (powered on via USB-C, 24V AC/DC, or PoE)
- Atmocube 裝置（透過 USB-C、24V AC/DC 或 PoE 供電並開機）
- Smartphone with Bluetooth enabled
- 已開啟藍牙的智慧型手機
- Wi-Fi network (2.4GHz) or Ethernet connection
- Wi-Fi 網路（2.4GHz）或乙太網路連線

### Step 1.1: Download the Atmotube App / 下載 Atmotube App

Download the **Atmotube** app from your app store:

從應用程式商店下載 **Atmotube** App：

- **iOS**: Search "Atmotube" in the App Store
- **iOS**：在 App Store 搜尋「Atmotube」
- **Android**: Search "Atmotube" in Google Play
- **Android**：在 Google Play 搜尋「Atmotube」

### Step 1.2: Create an Account / 建立帳號

1. Open the Atmotube app and tap **Sign Up**.
2. Enter your email address and create a password.
3. Verify your email address via the confirmation link.
4. Log in with your new account.

---

1. 開啟 Atmotube App，點選 **Sign Up（註冊）**。
2. 輸入電子郵件地址並建立密碼。
3. 透過確認信中的連結驗證電子郵件。
4. 使用新帳號登入。

### Step 1.3: Power on Atmocube / 開啟 Atmocube 電源

Connect power to the Atmocube using one of the following methods:

使用以下其中一種方式為 Atmocube 供電：

| Method / 方式 | Details / 說明 |
|---|---|
| USB-C | 5V @ 2A |
| Direct wiring / 直接配線 | 24V AC/DC |
| PoE | Power over Ethernet |

The Atmocube LED indicators will light up when powered on.

Atmocube 開機後 LED 指示燈會亮起。

### Step 1.4: Pair via Bluetooth / 透過藍牙配對

1. In the Atmotube app, tap the **"+"** icon to add a new device.
2. The app will scan for nearby Atmocube devices via Bluetooth.
3. Select your Atmocube from the list (e.g., `CUBE_77AC`).
4. Follow the on-screen prompts to complete pairing.
5. During pairing, configure the network connection:
   - **Wi-Fi**: Select your 2.4GHz Wi-Fi network and enter the password.
   - **Ethernet**: If connected via Ethernet cable, it will be detected automatically.

---

1. 在 Atmotube App 中，點選 **「+」** 圖示以新增裝置。
2. App 會透過藍牙掃描附近的 Atmocube 裝置。
3. 從清單中選擇您的 Atmocube（例如 `CUBE_77AC`）。
4. 依照螢幕上的提示完成配對。
5. 配對過程中，設定網路連線方式：
   - **Wi-Fi**：選擇您的 2.4GHz Wi-Fi 網路並輸入密碼。
   - **乙太網路**：若已接上乙太網路線，會自動偵測。

### Step 1.5: Verify on Atmotube Dashboard / 在 Atmotube Dashboard 確認

1. Open a web browser and go to **https://atmocube.app/**
2. Log in with the same account used in the Atmotube app.
3. You should see your Atmocube device listed on the Dashboard with an **Online** status.

---

1. 開啟瀏覽器，前往 **https://atmocube.app/**
2. 使用與 Atmotube App 相同的帳號登入。
3. 您應該能在 Dashboard 上看到您的 Atmocube 裝置，狀態顯示為 **Online**。

![Dashboard Overview / Dashboard 概覽](images/dashboard-overview.png)

---

## 2. Enable Modbus TCP/IP on Dashboard / 在 Dashboard 啟用 Modbus TCP/IP

### Step 2.1: Navigate to Device Settings / 前往裝置設定

1. On the Dashboard, click **Devices** in the left sidebar.
2. Find your Atmocube device in the device list.
3. Click the **Edit** button (pencil icon) in the **Actions** column.

---

1. 在 Dashboard 上，點選左側選單中的 **Devices**。
2. 在裝置清單中找到您的 Atmocube 裝置。
3. 點選 **Actions** 欄位中的**編輯**按鈕（鉛筆圖示）。

![Devices List / 裝置清單](images/devices-list.png)

### Step 2.2: Find Device Diagnostics / 找到裝置診斷資訊

Scroll down on the device edit page to find the **Device Diagnostics** section. Here you can see:

在裝置編輯頁面向下捲動，找到 **Device Diagnostics（裝置診斷）** 區塊。您可以在此看到：

| Field / 欄位 | Description / 說明 |
|---|---|
| Device IP | The current IP address of your Atmocube on the local network / Atmocube 在區域網路上的 IP 位址 |
| Connection Type | `wifi` or `ethernet` / 連線類型：`wifi` 或 `ethernet` |
| Wi-Fi Name | Connected Wi-Fi network SSID / 已連線的 Wi-Fi 網路名稱 |
| Device RSSI | Wi-Fi signal strength (lower is better) / Wi-Fi 訊號強度（數值越低越好） |

> **IMPORTANT / 重要**: Note down the **Device IP** address — you will need it when setting up the Home Assistant integration.
>
> 請記下 **Device IP** 位址 — 設定 Home Assistant 整合時會需要用到。

### Step 2.3: Enable Modbus IP / 啟用 Modbus IP

1. In the **Device Diagnostics** section, find the **Modbus IP** heading.
2. Check the **Enabled** checkbox to turn on Modbus TCP/IP.
3. Set the **Modbus IP Port** to `502` (default, recommended).
4. Click the **Save** button at the bottom of the page.

---

1. 在 **Device Diagnostics** 區塊中，找到 **Modbus IP** 標題。
2. 勾選 **Enabled** 核取方塊以啟用 Modbus TCP/IP。
3. 將 **Modbus IP Port** 設為 `502`（預設值，建議使用）。
4. 點選頁面底部的 **Save** 按鈕儲存設定。

![Device Diagnostics - Modbus TCP Settings / 裝置診斷 - Modbus TCP 設定](images/device-diagnostics-modbus.png)

> **Tip / 提示**: It is recommended to assign a **static IP address** to your Atmocube via your router's DHCP reservation feature. This prevents the IP from changing after a power cycle or network restart.
>
> 建議透過路由器的 DHCP 保留功能，為 Atmocube 設定**固定 IP 位址**。這可以避免斷電或網路重啟後 IP 位址改變。

### Modbus IP Settings Reference / Modbus IP 設定參考

| Setting / 設定 | Default / 預設值 | Range / 範圍 |
|---|---|---|
| Port / 埠號 | 502 | 0 – 65535 |
| Device ID (Slave ID) / 裝置 ID | 1 | 1 – 247 |

---

## 3. Install Atmocube Integration in Home Assistant / 安裝 Atmocube 整合至 Home Assistant

### Method A: HACS (Recommended) / 方法 A：HACS（建議）

> **Prerequisite / 前置需求**: [HACS](https://hacs.xyz/) must be installed in your Home Assistant instance.
>
> 您的 Home Assistant 必須已安裝 [HACS](https://hacs.xyz/)。

**Step 3A.1: Add Custom Repository / 新增自訂儲存庫**

1. Open Home Assistant and navigate to **HACS** in the sidebar.
2. Click the **three-dot menu** (⋮) in the top-right corner.
3. Select **Custom repositories**.
4. In the dialog:
   - **Repository**: Enter `https://github.com/WOOWTECH/woow_ha_atmocube`
   - **Type**: Select **Integration**
5. Click **Add**.

---

1. 開啟 Home Assistant，在側邊欄點選 **HACS**。
2. 點選右上角的**三點選單**（⋮）。
3. 選擇 **Custom repositories（自訂儲存庫）**。
4. 在對話框中：
   - **Repository**：輸入 `https://github.com/WOOWTECH/woow_ha_atmocube`
   - **Type**：選擇 **Integration**
5. 點選 **Add（新增）**。

**Step 3A.2: Install the Integration / 安裝整合**

1. In HACS → **Integrations**, search for **Atmocube**.
2. Click on **Atmocube Air Quality Sensor**.
3. Click **Download** (or **Install**).
4. Select the latest version and confirm.

---

1. 在 HACS → **Integrations** 中，搜尋 **Atmocube**。
2. 點選 **Atmocube Air Quality Sensor**。
3. 點選 **Download（下載）**（或 **Install（安裝）**）。
4. 選擇最新版本並確認。

**Step 3A.3: Restart Home Assistant / 重新啟動 Home Assistant**

1. Go to **Settings → System → Restart**.
2. Click **Restart** and wait for Home Assistant to come back online.

---

1. 前往 **Settings（設定）→ System（系統）→ Restart（重新啟動）**。
2. 點選 **Restart** 並等待 Home Assistant 重新上線。

---

### Method B: Manual Installation / 方法 B：手動安裝

**Step 3B.1: Download the Integration Files / 下載整合檔案**

Download or clone the repository:

下載或複製儲存庫：

```bash
git clone https://github.com/WOOWTECH/woow_ha_atmocube.git
```

**Step 3B.2: Copy Files / 複製檔案**

Copy the `custom_components/atmocube` folder to your Home Assistant configuration directory:

將 `custom_components/atmocube` 資料夾複製到 Home Assistant 的設定目錄中：

```
<HA config directory>/
├── configuration.yaml
├── custom_components/
│   └── atmocube/
│       ├── __init__.py
│       ├── config_flow.py
│       ├── const.py
│       ├── coordinator.py
│       ├── manifest.json
│       ├── sensor.py
│       └── strings.json
```

For Home Assistant OS / Supervised, the config directory is typically `/config/`.

Home Assistant OS / Supervised 的設定目錄通常在 `/config/`。

**Step 3B.3: Restart Home Assistant / 重新啟動 Home Assistant**

1. Go to **Settings → System → Restart**.
2. Click **Restart** and wait for Home Assistant to come back online.

---

1. 前往 **Settings（設定）→ System（系統）→ Restart（重新啟動）**。
2. 點選 **Restart** 並等待 Home Assistant 重新上線。

---

## 4. Setup Atmocube Integration in Home Assistant / 設定 Atmocube 整合

### Step 4.1: Add the Integration / 新增整合

1. Go to **Settings → Devices & Services**.
2. Click **+ Add Integration** (bottom-right corner).
3. Search for **Atmocube** and select it.

---

1. 前往 **Settings（設定）→ Devices & Services（裝置與服務）**。
2. 點選右下角的 **+ Add Integration（新增整合）**。
3. 搜尋 **Atmocube** 並選擇它。

### Step 4.2: Configure Connection / 設定連線

Enter the connection details in the configuration dialog:

在設定對話框中輸入連線資訊：

| Field / 欄位 | Description / 說明 | Default / 預設值 |
|---|---|---|
| **Host** | IP address of your Atmocube (from Step 2.2) / Atmocube 的 IP 位址（來自步驟 2.2） | — |
| **Port** | Modbus TCP port (from Step 2.3) / Modbus TCP 埠號（來自步驟 2.3） | `502` |
| **Modbus Slave ID** | Device ID of the Atmocube / Atmocube 的裝置 ID | `1` |

Click **Submit**. The integration will validate the connection by reading a Modbus register from the Atmocube.

點選 **Submit（送出）**。整合會透過讀取 Atmocube 的 Modbus 暫存器來驗證連線。

> If you see a **"Failed to connect"** error, verify:
> - The Atmocube is powered on and connected to the network.
> - The IP address and port are correct.
> - Modbus IP is enabled on the Dashboard (Step 2.3).
> - Home Assistant and the Atmocube are on the same network.
>
> 如果出現 **「Failed to connect（連線失敗）」** 錯誤，請確認：
> - Atmocube 已開機且已連線至網路。
> - IP 位址和埠號正確。
> - 已在 Dashboard 啟用 Modbus IP（步驟 2.3）。
> - Home Assistant 和 Atmocube 在同一個網路上。

### Step 4.3: Verify Sensor Entities / 驗證感測器實體

After successful setup, the integration creates **20 sensor entities** grouped under one **Atmocube** device.

設定成功後，整合會在一個 **Atmocube** 裝置下建立 **20 個感測器實體**。

To verify:

驗證方式：

1. Go to **Developer Tools → States**.
2. Filter for `atmocube`.
3. You should see 20 entities with values.

---

1. 前往 **Developer Tools（開發者工具）→ States（狀態）**。
2. 篩選 `atmocube`。
3. 您應該會看到 20 個帶有數值的實體。

### Sensor List / 感測器清單

| Sensor / 感測器 | Unit / 單位 | Description / 說明 |
|---|---|---|
| TVOCs / 總揮發性有機化合物 | ppb | Total volatile organic compounds |
| PM 1.0 / 懸浮微粒 1.0 | µg/m³ | Particulate matter ≤ 1.0 µm |
| PM 2.5 / 懸浮微粒 2.5 | µg/m³ | Particulate matter ≤ 2.5 µm |
| PM 4 / 懸浮微粒 4 | µg/m³ | Particulate matter ≤ 4 µm |
| PM 10 / 懸浮微粒 10 | µg/m³ | Particulate matter ≤ 10 µm |
| CO2 / 二氧化碳 | ppm | Carbon dioxide |
| Temperature / 溫度 | °C | Ambient temperature |
| Humidity / 相對濕度 | % | Relative humidity |
| Absolute Humidity / 絕對濕度 | g/m³ | Absolute humidity |
| Pressure / 氣壓 | hPa | Atmospheric pressure |
| Noise / 噪音 | dB | Sound pressure level |
| Light / 光照度 | lx | Illuminance |
| NO2 / 二氧化氮 | ppb | Nitrogen dioxide |
| CO / 一氧化碳 | ppb | Carbon monoxide |
| O3 / 臭氧 | ppb | Ozone |
| Formaldehyde / 甲醛 | ppb | Formaldehyde (CH₂O) |
| Color Temperature / 色溫 | K | Light color temperature |
| People Index / 人員舒適指數 | — | People comfort index (0–100) |
| VOC Index / VOC 指數 | — | VOC index |
| NOx Index / NOx 指數 | — | NOx index |

### Step 4.4: Add a Dashboard Card (Optional) / 新增儀表板卡片（選用）

Add a quick overview card to your Home Assistant dashboard:

在 Home Assistant 儀表板新增概覽卡片：

1. Go to your Dashboard and click the **pencil icon** (Edit) in the top-right.
2. Click **+ Add Card**.
3. Select **Entities** card.
4. Add the Atmocube sensors you want to display.

Or use YAML mode to add this card:

或使用 YAML 模式新增此卡片：

```yaml
type: entities
title: Atmocube Air Quality / 空氣品質
entities:
  - entity: sensor.atmocube_temperature
  - entity: sensor.atmocube_humidity
  - entity: sensor.atmocube_co2
  - entity: sensor.atmocube_pm2_5
  - entity: sensor.atmocube_tvocs
  - entity: sensor.atmocube_pressure
  - entity: sensor.atmocube_noise
  - entity: sensor.atmocube_light
```

---

## Troubleshooting / 疑難排解

### All sensors show "unavailable" / 所有感測器顯示「unavailable」

1. Check network connectivity: `ping <Atmocube IP>`
2. Verify Modbus TCP is enabled on the Dashboard (Step 2.3).
3. Check that the port and slave ID match between Dashboard and Home Assistant.

---

1. 檢查網路連線：`ping <Atmocube IP>`
2. 確認已在 Dashboard 啟用 Modbus TCP（步驟 2.3）。
3. 確認 Dashboard 與 Home Assistant 的埠號和從機 ID 一致。

### Sensors show "unknown" / 感測器顯示「unknown」

- Wait 60 seconds for the first measurement cycle. The Atmocube measures every 60 seconds.
- 等待 60 秒讓第一個測量週期完成。Atmocube 每 60 秒測量一次。

### Connection drops intermittently / 連線斷斷續續

- Use **Ethernet** instead of Wi-Fi for the Atmocube (more stable).
- Assign a **static IP** to the Atmocube via router DHCP reservation.
- Check for IP address conflicts on the network.

---

- Atmocube 使用**乙太網路**取代 Wi-Fi（更穩定）。
- 透過路由器 DHCP 保留功能為 Atmocube 設定**固定 IP**。
- 檢查網路上是否有 IP 位址衝突。

### Enable debug logging / 啟用除錯日誌

Add to your `configuration.yaml`:

加入 `configuration.yaml`：

```yaml
logger:
  default: warning
  logs:
    custom_components.atmocube: debug
```

---

## Reference Links / 參考連結

| Resource / 資源 | URL |
|---|---|
| Atmocube Dashboard | https://atmocube.app/ |
| Atmocube Support | https://atmotube.com/atmocube-support/ |
| Atmocube Modbus Setup Guide | https://support.atmotube.com/en/articles/10449835-modbus-setup-guide |
| HACS (Home Assistant Community Store) | https://hacs.xyz/ |
| Integration Repository / 整合儲存庫 | https://github.com/WOOWTECH/woow_ha_atmocube |
