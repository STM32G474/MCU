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
├── Build/                       # 編譯產出目錄 (執行檔, .elf, .bin, .hex, .map)
│                                # 注：此目錄應列入 .gitignore
│
├── Core/                        # STM32CubeMX 自動生成的系統核心
│   ├── Inc/                     # 系統底層標頭檔
│   │   ├── main.h               # 系統主入口標頭檔與全域 GPIO 定義
│   │   ├── main_config.h        # 專案特化巨集與 Feature Toggle 開關
│   │   ├── stm32g4xx_hal_conf.h # HAL 庫功能模組開啟/關閉配置
│   │   └── stm32g4xx_it.h      # 中斷服務函式 (ISR) 宣告
│   └── Src/                     # 系統底層原始碼
│       ├── main.c               # 系統初始化 (Clock, Peripherals) 與主迴圈
│       ├── stm32g4xx_hal_msp.c  # MCU 級別週邊初始化 (GPIO, NVIC, DMA 置位)
│       ├── stm32g4xx_it.c       # 硬體中斷服務函式實現 (SysTick, UART, HRTIM)
│       └── system_stm32g4xx.c   # CMSIS 系統時脈 (SystemCoreClock) 設定
│
├── Drivers/                     # 底層晶片與硬體驅動層
│   ├── CMSIS/                   # ARM Cortex-M4 標準庫與晶片寄存器映射
│   │   ├── Include/             # CMSIS Core 標頭檔 (core_cm4.h 等)
│   │   └── Device/ST/STM32G4xx/ # STM32G474 暫存器與啟動檔 (.s)
│   ├── STM32G4xx_HAL_Driver/    # ST 官方 HAL / LL 庫
│   │   ├── Inc/                 # HAL/LL 標頭檔 (stm32g4xx_hal_hrtim.h 等)
│   │   └── Src/                 # HAL/LL 原始碼 (.c)
│   └── BSP/                     # 板級支援包 (Board Support Package)
│       ├── Inc/
│       │   ├── bsp_led.h        # 板載 LED 介面
│       │   ├── bsp_button.h     # 板載按鍵介面 (帶軟體去彈跳)
│       │   └── bsp_debug_uart.h # 偵錯串口 (printf 重導向)
│       └── Src/
│           ├── bsp_led.c
│           ├── bsp_button.c
│           └── bsp_debug_uart.c
│
├── Hardware/                    # 外接周邊模組與感測器驅動 (Modules / Devices)
│   ├── Inc/
│   │   ├── lcd_st7789.h         # LCD 顯示螢幕驅動標頭檔
│   │   ├── eeprom_24cxx.h       # I2C EEPROM 記憶體驅動
│   │   └── ina219.h             # I2C 電流/電壓監測晶片驅動
│   └── Src/
│       ├── lcd_st7789.c
│       ├── eeprom_24cxx.c
│       └── ina219.c
│
├── Middlewares/                 # 第三方中間件與軟體庫 (根據專案需求選用)
│   ├── Third_Party/
│   │   ├── FreeRTOS/            # 即時作業系統 (RTOS)
│   │   │   ├── Source/          # FreeRTOS 核心程式碼與 Tasks/Queues
│   │   │   └── portable/        # ARM_CM4F 平台適配層與記憶體管理 (heap_4.c)
│   │   └── Segger_RTT/          # SEGGER RTT 高速 Log 偵錯工具
│   └── ST/                      # ST 官方中間件 (如 USB-Device, TouchGFX)
│
├── Application/                 # 上層應用邏輯與業務代碼 (App Layer)
│   ├── Inc/
│   │   ├── app_main.h           # 應用層主要框架入口
│   │   ├── app_power_control.h  # 數位電源 / HRTIM PWM 控制演算法
│   │   ├── app_display.h        # 畫面UI與顯示邏輯
│   │   └── app_cli.h            # 命令列交互介面 (Command Line Interface)
│   └── Src/
│       ├── app_main.c           # 應用層主流程 (可由 main.c 呼叫)
│       ├── app_power_control.c  # HRTIM 高解析度定時器控制 loop (如 PID 閉迴路)
│       ├── app_display.c
│       └── app_cli.c
│
├── Utility/                     # 通用演算法與工具函式庫 (無硬體依賴)
│   ├── Inc/
│   │   ├── pid_controller.h     # PID 控制演算法介面
│   │   ├── ring_buffer.h        # 環形緩衝區 (常用於 UART 接收)
│   │   └── filter.h             # 數位濾波器 (卡爾曼濾波, 滑動平均)
│   └── Src/
│       ├── pid_controller.c
│       ├── ring_buffer.c
│       └── filter.c
│
├── Toolchain/                   # 編譯器與下載工具鏈相關設定
│   ├── STM32G474RETX_FLASH.ld   # GNU GCC 鏈結檔 (Linker Script, 記憶體配置)
│   ├── startup_stm32g474xx.s    # ARM 組合語言啟動檔 (Vector Table)
│   └── STM32G474.svd            # Peripheral SVD 檔 (用於 GDB 暫存器視窗檢視)
│
├── Docs/                        # 專案設計文件與說明
│   ├── Architecture.md          # 系統架構圖與模組說明
│   ├── Hardware_Schematic.pdf   # 硬體原理圖 (Schematics)
│   └── HRTIM_PWM_Timing.png     # PWM 時序圖範例
│
├── Tools/                       # 輔助腳本與開發工具
│   ├── flash_device.sh          # OpenOCD / ST-LINK 命令行一鍵燒錄腳本
│   └── format_code.sh           # 全專案程式碼自動排版腳本 (clang-format)
│
├── .clang-format                # C/C++ 程式碼風格規範設定檔
├── .gitignore                   # Git 忽略檔案清單 (排除 .o, .elf, .bin 等)
├── CMakeLists.txt               # CMake 建置腳本 (支援跨平台與 VS Code)
├── Makefile                     # (可選) GNU Make 建置檔
├── STM32G474.ioc                # STM32CubeMX 硬體配置專案原始檔
├── LICENSE                      # 開放原始碼授權協議 (如 MIT)
└── README.md                    # 專案主要說明文件
