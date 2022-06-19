# MCU_Mega168
Интерфейсный класс для микроконтроллера AVR8 Mega168.

Идея позаимствована отсюда: https://habr.com/ru/post/459642/

## Описание функций

### 18.06.22 Добавлены функции управления питанием в регистре PRR
```C++
//ADC power management
void MCU::Core::ADC_powerUp(void);
void MCU::Core::ADC_powerDown(void);

//USART0 power management
void MCU::Core::USART0_powerUp(void);
void MCU::Core::USART0_powerDown(void);

//SPI power management
void MCU::Core::SPI_powerUp(void);
void MCU::Core::SPI_powerDown(void);

//Timer1 power management
void MCU::Core::TC1_powerUp(void);
void MCU::Core::TC1_powerDown(void);

//Timer0 power management
void MCU::Core::TC0_powerUp(void);
void MCU::Core::TC0_powerDown(void);

//Timer2 power management
void MCU::Core::TC2_powerUp(void);
void MCU::Core::TC2_powerDown(void);

//TWI power management
void MCU::Core::TWI_powerUp(void);
void MCU::Core::TWI_powerDown(void);
```
### 19.06.22 Добавлены функции для работы с WatchDog timer
```C++
//WDT interrupt flag functions
bool MCU::Core::is_WDT_I_Flag_Set();         //Is WatchDog timer interrupt flag set?
void MCU::Core::set_WDT_I_Flag();            //Set WatchDog timer interrupt flag
void MCU::Core::clear_WDT_I_Flag();          //Clear WatchDog timer interrupt flag

//WDT interrupt enable flag functions
void MCU::Core::WDT_Interrupt_Enable();      //Enable WatchDog timer interrupt
void MCU::Core::WDT_Interrupt_Disable();     //Disable WatchDog timer interrupt
bool MCU::Core::is_WDT_Interrupt_Enabled();  //Is WatchDog timer interrupt enabled?

//WDT Change enable flag functions
void MCU::Core::WDT_Change_Enable(void);
void MCU::Core::WDT_Change_Disable(void);

//WDT System reset enable flag functions
void MCU::Core::WDT_System_reset_enable(void);
void MCU::Core::WDT_System_reset_disable(void);

//WDT prescaler functions
void MCU::Core::WDT_setPrescaler_2048(void);     //16ms at 5v power supply
void MCU::Core::WDT_setPrescaler_4096(void);     //32ms at 5v power supply
void MCU::Core::WDT_setPrescaler_8192(void);     //64ms at 5v power supply
void MCU::Core::WDT_setPrescaler_16348(void);    //128ms at 5v power supply
void MCU::Core::WDT_setPrescaler_32768(void);    //256ms at 5v power supply
void MCU::Core::WDT_setPrescaler_65536(void);    //512ms at 5v power supply
void MCU::Core::WDT_setPrescaler_131072(void);   //1024ms at 5v power supply
void MCU::Core::WDT_setPrescaler_262144(void);   //2048ms at 5v power supply
void MCU::Core::WDT_setPrescaler_524288(void);   //4096ms at 5v power supply
void MCU::Core::WDT_setPrescaler_1048576(void);  //8192ms at 5v power supply

//WDT Configurations if WDTON fuse bit is not set
void MCU::Core::WDT_stop(void);
void MCU::Core::WDT_interrupt_mode(void);
void MCU::Core::WDT_SystemReset_mode(void);
void MCU::Core::WDT_Interrupt_And_SystemReset_mode(void);

```

