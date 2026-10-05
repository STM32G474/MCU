```text
STM32G474-MCU-Project/
├── .github/                     # GitHub 工作流與 CI/CD 設定
│   └── workflows/
│       ├── build.yml            # 自動化編譯測試 (GitHub Actions)
│       └── code-format.yml      # clang-format 程式碼風格檢查
│
├── .vscode/                     # VS Code 開發環境設定檔
│   ├── c_cpp_properties.json   # C/C++ IntelliSense 標頭檔路徑
│   ├── launch.json              # ST-LINK / J-Link GDB 偵錯與下載設定
│   ├── tasks.json               # 自動化 Build / Clean 任務
│   └── settings.json            # 編輯器與格式化規則設定
│
├── Build/                       # 編譯產出目錄 (.elf, .bin, .hex, .map)
│
├── Core/                        # STM32CubeMX 自動生成的系統核心
│   ├── Inc/                     # 系統底層標頭檔
│   │   ├── main.h               # 系統主入口標頭檔與全域 GPIO 定義
│   │   ├── main_config.h        # 專案特化巨集與 Feature Toggle 開關
│   │   ├── stm32g4xx_hal_conf.h # HAL 庫功能模組開啟/關閉配置
│   │   └── stm32g4xx_it.h      # 中斷服務函式 (ISR) 宣告
│   └── Src/                     # 系統底層原始碼
│       ├── main.c               # 系統初始化 (Clock, Peripherals) 與主迴圈
│       ├── stm32g4xx_hal_msp.c  # MCU 級別週邊初始化
│       ├── stm32g4xx_it.c       # 硬體中斷服務函式實現
│       └── system_stm32g4xx.c   # CMSIS 系統時脈設定
│
├── Drivers/                     # 底層晶片與硬體驅動層
│   ├── CMSIS/                   # ARM Cortex-M4 標準庫與晶片寄存器映射
│   ├── STM32G4xx_HAL_Driver/    # ST 官方 HAL / LL 庫
│   └── BSP/                     # 板級支援包 (Board Support Package)
│       ├── Inc/
│       │   ├── bsp_led.h        # 板載 LED 介面
│       │   ├── bsp_button.h     # 板載按鍵介面
│       │   └── bsp_debug_uart.h # 偵錯串口 (printf 重導向)
│       └── Src/
│           ├── bsp_led.c
│           ├── bsp_button.c
│           └── bsp_debug_uart.c
│
├── Hardware/                    # 外接周邊模組與感測器驅動
│   ├── Inc/
│   │   ├── lcd_st7789.h         # LCD 顯示螢幕驅動標頭檔
│   │   └── ina219.h             # 電流/電壓監測晶片驅動
│   └── Src/
│       ├── lcd_st7789.c
│       └── ina219.c
│
├── Middlewares/                 # 第三方中間件與軟體庫
│   └── Third_Party/
│       └── FreeRTOS/            # 即時作業系統 (RTOS)
│
├── Application/                 # 上層應用邏輯與業務代碼 (App Layer)
│   ├── Inc/
│   │   ├── app_main.h           # 應用層主要框架入口
│   │   └── app_power_control.h  # 數位電源 / HRTIM PWM 控制演算法
│   └── Src/
│       ├── app_main.c           # 應用層主流程
│       └── app_power_control.c  # HRTIM 控制迴路 (如 PID)
│
├── Utility/                     # 通用演算法與工具函式庫 (無硬體依賴)
│   ├── Inc/
│   │   ├── pid_controller.h     # PID 控制演算法介面
│   │   └── ring_buffer.h        # 環形緩衝區
│   └── Src/
│       ├── pid_controller.c
│       └── ring_buffer.c
│
├── Toolchain/                   # 編譯器與下載工具鏈相關設定
│   ├── STM32G474RETX_FLASH.ld   # GNU GCC 鏈結檔
│   └── startup_stm32g474xx.s    # ARM 組合語言啟動檔
│
├── Docs/                        # 專案設計文件與說明
├── Tools/                       # 輔助腳本與開發工具
├── .gitignore                   # Git 忽略檔案清單
├── CMakeLists.txt               # CMake 建置腳本
├── STM32G474.ioc                # STM32CubeMX 硬體配置專案原始檔
├── LICENSE                      # 開放原始碼授權協議
└── README.md                    # 專案說明文件
![image](739e3d12f1fb1d1c97e6d4abe9c0ef38.gif_
