1.0 cmake --build build/Debug --clean-first --verbose指令可以在构建过程中输出详细命令;

1.1 将 Core/Src/main.c 编译为 main.c.obj 的命令(已修改为PowerShell7的多行命令格式, 实际运行通过):
C:/ST/STM32CubeCLT_1.21.0/GNU-tools-for-STM32/bin/arm-none-eabi-gcc.exe `
-DDATA_CACHE_ENABLE=1 `
-DDEBUG -DEXTERNAL_CLOCK_VALUE=12288000 `
-DHSE_STARTUP_TIMEOUT=100 `
-DHSE_VALUE=8000000 `
-DHSI_VALUE=16000000 `
-DINSTRUCTION_CACHE_ENABLE=1 `
-DLSE_STARTUP_TIMEOUT=5000 `
-DLSE_VALUE=32768 `
-DLSI_VALUE=32000 `
-DPREFETCH_ENABLE=1 `
-DSTM32F401xE `
-DUSE_FULL_LL_DRIVER `
-DVDD_VALUE=3300 `
-IC:/code/STM32_Refresh/cmake/stm32cubemx/../../Core/Inc `
-IC:/code/STM32_Refresh/cmake/stm32cubemx/../../Drivers/STM32F4xx_HAL_Driver/Inc `
-IC:/code/STM32_Refresh/cmake/stm32cubemx/../../Drivers/CMSIS/Device/ST/STM32F4xx/Include `
-IC:/code/STM32_Refresh/cmake/stm32cubemx/../../Drivers/CMSIS/Include `
-mcpu=cortex-m4 `
-mfpu=fpv4-sp-d16 `
-mfloat-abi=hard `
-Wall `
-fdata-sections `
-ffunction-sections `
-fstack-usage `
-O0 `
-g3 `
-std=gnu11 `
-fdiagnostics-color=always `
-MD `
-MT CMakeFiles/STM32_Refresh.dir/Core/Src/main.c.obj `
-MF CMakeFiles/STM32_Refresh.dir/Core/Src/main.c.obj.d `
-o CMakeFiles/STM32_Refresh.dir/Core/Src/main.c.obj `
-c C:/code/STM32_Refresh/Core/Src/main.c

1.2 将各个目标文件链接为 STM32_Refresh.elf 的命令(已修改为PowerShell7的多行命令格式, 实际运行通过):
C:/ST/STM32CubeCLT_1.21.0/GNU-tools-for-STM32/bin/arm-none-eabi-gcc.exe `
-mcpu=cortex-m4 `
-mfpu=fpv4-sp-d16 `
-mfloat-abi=hard `
-Wall -fdata-sections `
-ffunction-sections `
-fstack-usage `
-O0 `
-g3 `
-T 'C:/code/STM32_Refresh/STM32F401xx_FLASH.ld' `
--specs=nano.specs `
'-Wl,-Map=STM32_Refresh.map' `
'-Wl,--gc-sections' `
'-Wl,--print-memory-usage' `
cmake/stm32cubemx/CMakeFiles/STM32_Drivers.dir/__/__/Core/Src/system_stm32f4xx.c.obj `
cmake/stm32cubemx/CMakeFiles/STM32_Drivers.dir/__/__/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_gpio.c.obj `
cmake/stm32cubemx/CMakeFiles/STM32_Drivers.dir/__/__/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_usart.c.obj `
cmake/stm32cubemx/CMakeFiles/STM32_Drivers.dir/__/__/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_dma.c.obj `
cmake/stm32cubemx/CMakeFiles/STM32_Drivers.dir/__/__/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_rcc.c.obj `
cmake/stm32cubemx/CMakeFiles/STM32_Drivers.dir/__/__/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_utils.c.obj `
cmake/stm32cubemx/CMakeFiles/STM32_Drivers.dir/__/__/Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_exti.c.obj `
CMakeFiles/STM32_Refresh.dir/Core/Src/main.c.obj `
CMakeFiles/STM32_Refresh.dir/Core/Src/gpio.c.obj `
CMakeFiles/STM32_Refresh.dir/Core/Src/usart.c.obj `
CMakeFiles/STM32_Refresh.dir/Core/Src/stm32f4xx_it.c.obj `
CMakeFiles/STM32_Refresh.dir/Core/Src/sysmem.c.obj `
CMakeFiles/STM32_Refresh.dir/Core/Src/syscalls.c.obj `
CMakeFiles/STM32_Refresh.dir/startup_stm32f401xe.s.obj `
-o STM32_Refresh.elf `
-lm

1.3 手动执行编译链接命令时, 必须进入实际构建文件夹, build/Debug或者build/Release, 否则会报错找不到文件或者文件夹.

1.4 编译命令各参数的作用
-DDATA_CACHE_ENABLE=1：开启L1数据Cache;
-DDEBUG：DEBUG 宏，表示调试模式;
-DEXTERNAL_CLOCK_VALUE=12288000：外部输入时钟值12.288MHz;
-DHSE_STARTUP_TIMEOUT=100：HSE高速外部晶振启动超时计数，超时判定晶振失败;
-DHSE_VALUE=8000000：HSE 外部高速晶振频率 = 8MHz;
-DHSI_VALUE=16000000：HSI 片内高速 RC 振荡器，16MHz，F401 内置高速时钟;
-DINSTRUCTION_CACHE_ENABLE=1：开启L1指令Cache;
-DLSE_STARTUP_TIMEOUT=5000：LSE 低速外部32.768K晶振启动超时;
-DLSE_VALUE=32768：LSE 外部低速晶振32768Hz，RTC 实时时钟专用;
-DLSI_VALUE=32000：LSI 片内低速RC 32KHz，内部看门狗/独立时钟源;
-DPREFETCH_ENABLE=1：Flash 预取使能，提前预读 Flash 指令，提升 Flash 执行速度;
-DSTM32F401xE：指定芯片型号宏，CMSIS 头文件靠这个选择寄存器定义、中断向量;
-DUSE_FULL_LL_DRIVER：使用LL底层库;
-DVDD_VALUE=3300：供电电压 VDD=3300mV=3.3V;
-I：Include path，编译器找.h头文件的目录列表;
-mcpu=cortex-m4：指定目标内核Cortex-M4，编译器生成M4指令集;
-mfpu=fpv4-sp-d16：启用 FPU，单精度浮点单元FPv4-SP，16 个浮点寄存器;
-mfloat-abi=hard：hard浮点ABI，函数参数直接用FPU浮点寄存器传递;
-Wall：开启编译器警告;
-fdata-sections：每个全局变量单独放到独立数据section;
-ffunction-sections：每个函数单独一个代码section;
-fstack-usage：生成栈占用报告，每个函数栈使用量，用于分析栈溢出风险;
-O0：零优化，代码和C源码一一对应;
-g3：生成最高等级调试信息;
-std=gnu11：使用GNU扩展的C11标准;
-fdiagnostics-color=always：终端输出编译报错/警告时，带彩色文字，方便看错误;
-MD：自动生成头文件依赖关系;
-MT CMakeFiles/STM32_Refresh.dir/Core/Src/main.c.obj：设置依赖规则里的目标名;
-MF CMakeFiles/STM32_Refresh.dir/Core/Src/main.c.obj.d：依赖文件输出路径（.d文件）;
-o CMakeFiles/STM32_Refresh.dir/Core/Src/main.c.obj：输出目标文件名字;
-c：Compile only，只编译和汇编，不链接;

1.5 链接命令各参数的作用
-mcpu=cortex-m4
-mfpu=fpv4-sp-d16
-mfloat-abi=hard
-Wall
-fdata-sections
-ffunction-sections
-fstack-usage
-O0
-g3
上面这些参数和编译命令一致;
-T 'C:/code/STM32_Refresh/STM32F401xx_FLASH.ld'：指定GNU链接脚本 .ld;
--specs=nano.specs：使用Newlib-Nano轻量级C标准库;
'-Wl,-Map=STM32_Refresh.map'：生成map文件，map 文件包含：所有函数/全局变量所在地址、每个段占用大小、符号分配情况;
'-Wl,--gc-sections'：垃圾回收，删除未使用段;
'-Wl,--print-memory-usage'：链接完成后，在控制台打印 Flash、RAM 使用百分比;
所有obj文件表示要链接的库;
-o STM32_Refresh.elf：指定输出elf文件;
-lm：链接libm数学库;

2.1 查看main.c.i文件;
LED0对应PA0，LED0_GPIO_Port对应GPIOA，LED0_Pin对应LL_GPIO_PIN_0;
LED0_GPIO_Port被展开成(0x40000000UL + 0x00020000UL) + 0x0000UL, 被展开成0x1UL << (0U);

2.2 查看main.c.s文件;
在1075行找到了汇编语言main过程的入口;
从1048行到1059行找到了以下的代码，应该就是++heartbeat_count对应的汇编片段;
.LFE687:
	.size	LL_GPIO_TogglePin, .-LL_GPIO_TogglePin
	.section	.bss.heartbeat_count,"aw",%nobits
	.align	2
	.type	heartbeat_count, %object
	.size	heartbeat_count, 4
heartbeat_count:
	.space	4
	.section	.bss.led_list,"aw",%nobits
	.align	2
	.type	led_list, %object
	.size	led_list, 32
在1125行和1168行各有一个bl LL_mDelay，这是跳转调用LL_mDelay的指令，正好对应源码的两次LL_mDelay调用;

3.1 对比LL_mDelay的变化;
在main.c.obj中有两次调用:
  4a:   f7ff fffe       bl      0 <LL_mDelay>
                        4a: R_ARM_THM_CALL      LL_mDelay
  8e:   f7ff fffe       bl      0 <LL_mDelay>
                        8e: R_ARM_THM_CALL      LL_mDelay
在ELF中也是两次调用:
 8001776:       f7ff fccf       bl      8001118 <LL_mDelay>
 80017ba:       f7ff fcad       bl      8001118 <LL_mDelay>
 两次调用一次地址是8001776，另一次是80017ba，最终都被定位到了地址8001118.
 在在ELF中main函数的实际地址是0800172c <main>.
 
4.0 三个自检问题.
4.1 .i 已经展开了头文件，为什么还不能直接烧录运行？
回答，main.c.i只做了预处理，展开各种宏，包括#include和#if/#ifdef，保留 # 0 "Core/Src/main.c" 这类行号标记，它本身依然是.c源码文件，自然是不能烧录运行.
4.2 为什么 main.c.obj 中存在未定义符号 LL_mDelay，整个工程仍然可以链接成功？
回答，因为.obj是可重定位目标文件，里面包含大量的浮动地址，各种没有最终确定的符号，调用函数的重定位记录，没有形成最终的地址，所以依然可以链接成功.
4.3 编译器生成的 .s 与最终 ELF 的反汇编，有哪些信息上的区别？
回答，.s是汇编源码，ELF反汇编是链接完成的机器码。汇编源码是输入给汇编器的文本，ELF是链接器处理完的最终结果。
