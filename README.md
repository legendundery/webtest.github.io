flowchart LR
    CLK["clk 100MHz"] --> DIV["时钟分频模块"]
    BTN["按键输入"] --> KEY["按键消抖与边沿检测模块"]

    DIV -- tick_1ms --> KEY
    KEY -- key_pulse --> FSM["控制状态机"]

    DIV -- tick_10ms --> TIMER["BCD计时模块"]
    FSM -- state --> TIMER
    TIMER -- min_flag --> FSM

    DIV -- tick_1ms --> DISP["数码管扫描与译码模块"]
    TIMER -- time_digits --> DISP
    DISP -- an --> AN["数码管位选"]
    DISP -- seg --> SEG["数码管段选"]

    TIMER -- min_flag --> LEDMIN["led_min"]

    FSM -- alarm_state --> ALARM["报警输出模块"]
    DIV -- ticks --> ALARM
    ALARM -- alarm_toggle --> LEDALARM["led_alarm"]
    ALARM -- beep_freq --> BUZZER["buzzer"]
