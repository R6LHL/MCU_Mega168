# MCU_Mega168
Интерфейсный класс для микроконтроллера AVR8 Mega168.

Идея позаимствована отсюда: https://habr.com/ru/post/459642/

## Описание функций

### 18.06.22 Добавлены функции управления питанием в регистре PRR
```C++
//ADC power management
MCU::Core::ADC_powerUp();
MCU::Core::ADC_powerDown();

//USART0 power management
MCU::Core::USART0_powerUp();
MCU::Core::USART0_powerDown();

//SPI power management
MCU::Core::SPI_powerUp();
MCU::Core::SPI_powerDown();

//Timer1 power management
MCU::Core::TC1_powerUp();
MCU::Core::TC1_powerDown();

//Timer0 power management
MCU::Core::TC0_powerUp();
MCU::Core::TC0_powerDown();

//Timer2 power management
MCU::Core::TC2_powerUp();
MCU::Core::TC2_powerDown();

//TWI power management
MCU::Core::TWI_powerUp();
MCU::Core::TWI_powerDown();

### Добавлены функции для работы с WatchDog timer

bool is_WDT_I_Flag_Set();         //Is WatchDog timer interrupt flag set?
void set_WDT_I_Flag();            //Set WatchDog timer interrupt flag
void clear_WDT_I_Flag();          //Clear WatchDog timer interrupt flag
void WDT_Interrupt_Enable();      //Enable WatchDog timer interrupt
void WDT_Interrupt_Disable();     //Disable WatchDog timer interrupt
bool is_WDT_Interrupt_Enabled();  //Is WatchDog timer interrupt enabled?

```

