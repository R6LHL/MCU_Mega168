# MCU_Mega168
Интерфейсный класс для микроконтроллера AVR8 Mega168.

Идея позаимствована отсюда: https://habr.com/ru/post/459642/

## Объявления функций в файле RegisterBase.hpp
```C++
void Set(uint8_t value);            //set register value
uint8_t Get(void);                  //get register value
bool GetBit(uint8_t bit_number);    //get specified bit value
void SetBit(uint8_t bit_number);    //set specified bit
void ClearBit(uint8_t bit_number);  //clear specified bit
```
## Объявления функций в файле IO_port_basic.hpp
```C++
void pullupAll(void); //set all port pins with pullup
void Hi_Z_All(void);  //set all port pins with Hi-Z impendance
```
## Для работы с регистрами GPIOR0...2 используйте функции из RegisterBase.hpp: все регистры наследуют их.
### Например
```C++
MCU::IO_::GPIOR0_::Set(0xfa);
```
## Для работы с портами ВВ PORTB...D используйте функции из RegisterBase.hpp и IO_port_basic.hpp: все регистры ВВ наследуют их.
### Например
```C++
MCU::IO_::PORTB_::SetBit(3);
MCU::IO_::PORTD_::pullupAll();
```
## Объявления функций в файле MCU_Mega_168.hpp
### namespace MCU
#### namepace MCU::IO_
```C++
struct PORTB_ : public IO_port_basic;
struct PORTC_ : public IO_port_basic;
struct PORTD_ : public IO_port_basic;

struct GPIOR0_ : public RegisterBase;
struct GPIOR1_ : public RegisterBase;
struct GPIOR2_ : public RegisterBase;
```
#### namepace MCU::Sleep_
```C++
void MCU::Sleep_::Enable(void);    // разрешает переход контроллера в спящий режим по команде sleep
void MCU::Sleep_::Disable(void);   // запрещает переход контроллера в спящий режим по команде sleep
void MCU::Sleep_::Go(void);        // переход в спячку
```
##### namepace MCU::Sleep_::Mode
```C++
void MCU::Sleep_::Mode::Idle(void);
void MCU::Sleep_::Mode::ADC_NoiseReduction(void);
void MCU::Sleep_::Mode::PowerDown(void);
void MCU::Sleep_::Mode::PowerSave(void);
void MCU::Sleep_::Mode::Standby(void);
void MCU::Sleep_::Mode::ExtendedStandby(void);
```
#### namespace MCU::Core
```C++
struct SREG_ : public RegisterBase;
struct SPL_ : public RegisterBase;
struct SPH_ : public RegisterBase;
struct MCUCR_ : public RegisterBase;

// MCU status register - indicates which event is reset occured
// 0x01 - if power-on
// 0x02 - if external reset
// 0x04 - if brown-out reset
// 0x08 - if watchdog reset
struct MCUSR_ : public RegisterBase;
			
// Oscillator calibration register
struct OSCCAL_ : public RegisterBase;
	
//Clock Precaler register
struct CLKPR_ : public RegisterBase;

//Power reduction register
struct PRR_ : public RegisterBase;
```
#### namespace MCU::Watchdog
```C++
bool MCU::Watchdog::is_I_Flag_Set(void);
void MCU::Watchdog::set_I_Flag(void);
void MCU::Watchdog::clear_I_Flag(void);
void MCU::Watchdog::Interrupt_Enable(void);
bool MCU::Watchdog::is_InterruptEnabled(void);
void MCU::Watchdog::Change_Disable(void);
void MCU::Watchdog::Change_Enable(void);
void MCU::Watchdog::System_reset_enable(void);
void MCU::Watchdog::System_reset_disable(void);
```
##### namespace MCU::Watchdog::Prescaler
```C++
void MCU::Watchdog::Prescaler::set_2048(void);
void MCU::Watchdog::Prescaler::set_4096(void);
void MCU::Watchdog::Prescaler::set_8192(void);
void MCU::Watchdog::Prescaler::set_16348(void);
void MCU::Watchdog::Prescaler::set_32768(void);
void MCU::Watchdog::Prescaler::set_65536(void);
void MCU::Watchdog::Prescaler::set_131072(void);
void MCU::Watchdog::Prescaler::set_262144(void);
void MCU::Watchdog::Prescaler::set_524288(void);
void MCU::Watchdog::Prescaler::set_1048576(void);
```
##### namespace MCU::Watchdog::Mode
```C++
void MCU::Watchdog::Mode::stop(void);
void MCU::Watchdog::Mode::interrupt(void);
void MCU::Watchdog::Mode::SystemReset(void);
void MCU::Watchdog::Mode::Interrupt_And_SystemReset(void);
```
#### namespace 

## ******************************************************
_________________________________________________
### 3.06.22 Добавлены функции управления таймером2
```C++
//TC2 prescaler setup functions
void MCU::TC::TC2_::TimerStop(void);
void MCU::TC::TC2_::SetPrescaler1(void);
void MCU::TC::TC2_::SetPrescaler8(void);
void MCU::TC::TC2_::SetPrescaler32(void);
void MCU::TC::TC2_::SetPrescaler64(void);
void MCU::TC::TC2_::SetPrescaler128(void);
void MCU::TC::TC2_::SetPrescaler256(void);
void MCU::TC::TC2_::SetPrescaler1024(void);

//TC2 interrupt setup functions
void MCU::TC::TC2_::Ovf_Int_Enable(void);
void MCU::TC::TC2_::Ovf_Int_Disable(void);
```
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
void MCU::Core::WDT_Interrupt_Enable();         //Enable WatchDog timer interrupt
void MCU::Core::WDT_Interrupt_Disable();        //Disable WatchDog timer interrupt
bool MCU::Core::is_WDT_Interrupt_Enabled();     //Is WatchDog timer interrupt enabled?

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
### Добавлены функции включения/отключения цифрового буфера ввода на ADC и AC-выводах (энергопотребление)
#### Функции для АЦП
```C++
void MCU::IO_::ADC_digital_Input_Disable(uint8_t adc_pin_number);
void MCU::IO_::ADC_digital_Input_Enable(uint8_t adc_pin_number);
```
#### Функции для аналогового компаратора
```C++
void MCU::IO_::AC_digital_Input_Enable(uint8_t ac_pin_number);
void MCU::IO_::AC_digital_Input_Disable(uint8_t ac_pin_number);
```
### Добавлены функции для работы с режимами спячки
#### Установка режимов спячки
```C++
void MCU::Core::sleepMode_Idle(void);
void MCU::Core::sleepMode_ADC_NoiseReduction(void);
void MCU::Core::sleepMode_PowerDown(void);
void MCU::Core::sleepMode_PowerSave(void);
void MCU::Core::sleepMode_Standby(void);
void MCU::Core::sleepMode_ExtendedStandby(void);
```
#### Разрешение/запрещение спячки
```C++
void MCU::Core::sleepEnable(void); // разрешает переход контроллера в спящий режим по команде sleep
void MCU::Core::sleepDisable(void); // запрещает переход контроллера в спящий режим по команде sleep
```
