
# 

---

## 遊戲程式碼架構與邏輯原理

這個氣球射擊遊戲是使用純HTML、CSS和JavaScript實現的，沒有依賴任何外部庫。以下是詳細的架構和邏輯原理解析：

### HTML結構

遊戲的HTML結構主要由以下部分組成：

1. 遊戲容器（gameContainer）：整個遊戲的主要容器
2. 武器選擇區（weaponSelection）：讓玩家選擇不同武器
3. 倒數計時器（countdown）：顯示遊戲開始前的倒數
4. 遊戲計時器（timer）：顯示遊戲剩餘時間
5. 分數顯示（score）：顯示當前得分
6. 結果顯示（results）：顯示遊戲結束後的分數和命中率
7. 武器圖像（weapon-image）：顯示所選武器的圖像

### CSS樣式

CSS部分主要定義了遊戲的視覺效果：

1. 遊戲容器的尺寸和背景
2. 武器選擇按鈕的樣式和懸停效果
3. 氣球的外觀，包括基本形狀和氣球底部的繩子（使用:before偽元素）
4. 計時器、分數和結果顯示的樣式
5. 武器圖像的位置和大小

### JavaScript邏輯

遊戲的核心邏輯由以下幾個主要函數和變量組成：

#### 全局變量

```javascript
let score = 0;        // 玩家得分
let shots = 0;        // 射擊次數
let hits = 0;         // 命中次數
let gameActive = false; // 遊戲是否進行中
let balloons = [];    // 存儲所有氣球元素的數組
let selectedWeapon = ''; // 選擇的武器
let weaponImages = {}; // 存儲武器圖像的對象
```


#### 主要函數

1. **selectWeapon(weapon)**
    - 記錄玩家選擇的武器
    - 隱藏武器選擇界面
    - 顯示倒數計時
    - 顯示武器圖像
    - 啟動5秒倒數計時器，結束後調用startGame()
2. **startGame()**
    - 設置gameActive為true
    - 隱藏倒數計時，顯示遊戲計時器和分數
    - 啟動10秒遊戲計時器
    - 調用createBalloons()開始生成氣球
    - 為遊戲容器添加點擊事件監聽器
3. **createBalloons()**
    - 設置間隔計時器，每秒創建1-2個氣球
    - 如果遊戲不再活躍，清除計時器
4. **createBalloon()**
    - 創建一個氣球DOM元素
    - 設置隨機位置和顏色
    - 將氣球添加到遊戲容器和balloons數組
    - 設置氣球在2-4秒後自動消失
5. **shootBalloon(event)**
    - 增加shots計數
    - 創建射擊視覺效果
    - 檢查是否擊中氣球
    - 如果擊中，增加hits和score，並移除被擊中的氣球
6. **endGame()**
    - 設置gameActive為false
    - 移除所有氣球和點擊事件監聽器
    - 計算命中率
    - 顯示最終結果
7. **restartGame()**
    - 重置所有計數器和遊戲狀態
    - 隱藏結果顯示
    - 顯示武器選擇界面

### 遊戲流程原理

1. **初始化階段**：
    - 頁面加載時顯示武器選擇界面
    - 玩家選擇武器後進入倒數階段
2. **倒數階段**：
    - 顯示5秒倒數計時
    - 倒數結束後進入遊戲階段
3. **遊戲階段**：
    - 開始10秒計時
    - 隨機生成氣球
    - 玩家點擊屏幕射擊
    - 記錄射擊次數和命中次數
    - 計算並顯示分數
4. **結束階段**：
    - 時間結束後停止遊戲
    - 計算並顯示最終分數和命中率
    - 提供重新開始選項

### 技術實現要點

1. **事件驅動編程**：
    - 使用事件監聽器處理用戶交互
    - 點擊事件用於射擊機制
2. **計時器管理**：
    - 使用setInterval和setTimeout控制遊戲時間和氣球生成
    - 適時清除計時器避免內存泄漏
3. **DOM操作**：
    - 動態創建和移除氣球元素
    - 更新分數和計時器顯示
4. **碰撞檢測**：
    - 使用getBoundingClientRect()獲取元素位置
    - 檢查點擊坐標是否在氣球範圍內
5. **數據封裝**：
    - 使用全局變量跟踪遊戲狀態
    - 函數間清晰的職責分工
6. **自包含設計**：
    - 使用Base64編碼的SVG圖像，無需外部資源
    - 所有邏輯和樣式都包含在單個HTML文件中
