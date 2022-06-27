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

#### namespace MCU::EXINT_
```C++
```

#### namespace MCU::TC0_
```C++
void MCU::TC0_::PowerUp(void);
void MCU::TC0_::PowerDown(void);
```

#### namespace MCU::TC1_
```C++
void MCU::TC1_::PowerUp(void);
void MCU::TC1_::PowerDown(void);
```
#### namespace MCU::TC2_
```C++
void MCU::TC2_::PowerUp(void);
void MCU::TC2_::PowerDown(void);
void MCU::TC2_::TimerStop(void);
```
##### namespace MCU::TC2_::Prescaler
```C++
void MCU::TC2_::Prescaler::reset(void);
void MCU::TC2_::Prescaler::set_1(void);
void MCU::TC2_::Prescaler::set_8(void);
void MCU::TC2_::Prescaler::set_32(void);
void MCU::TC2_::Prescaler::set_64(void);
void MCU::TC2_::Prescaler::set_128(void);
void MCU::TC2_::Prescaler::set_256(void);
void MCU::TC2_::Prescaler::set_1024(void);
```
##### namespace MCU::TC2_::Interrupt_source
```C++
void MCU::TC2_::Interrupt_source::Overflow_Enable(void);
void MCU::TC2_::Interrupt_source::Overflow_Disable(void);
```

#### namespace MCU::SPI_
```C++
void MCU::SPI_::powerUp(void);
void MCU::SPI_::powerDown(void);

void MCU::SPI_::Enable(void);
void MCU::SPI_::Disable(void);

void MCU::SPI_::Interrupt_Enable(void);
void MCU::SPI_::Interrupt_Disable(void);

void MCU::SPI_::Set_As_Master(void);
void MCU::SPI_::Set_As_Slave(void);

uint8_t MCU::SPI_::recieve(void);
void MCU::SPI_::transmit(uint8_t v);

bool MCU::SPI_::is_TRX_Complete(void);
bool MCU::SPI_::is Data_Collision(void);
```
##### namespace MCU::SPI_::Data_Order
```C++
void MCU::SPI_::Data_Order::MSB_first(void);
void MCU::SPI_::Data_Order::LSB_first(void);
```
##### namespace MCU::SPI_::Mode
```C++
void MCU::SPI_::SCK_Setup::Mode::Set_0(void);
void MCU::SPI_::SCK_Setup::Mode::Set_1(void);
void MCU::SPI_::SCK_Setup::Mode::Set_2(void);
void MCU::SPI_::SCK_Setup::Mode::Set_3(void);
```
##### namespace MCU::SPI_::SCK_Setup::Rate
```C++
void MCU::SPI_::SCK_Setup::Rate::F_div_2(void);
void MCU::SPI_::SCK_Setup::Rate::F_div_4(void);
void MCU::SPI_::SCK_Setup::Rate::F_div_8(void);
void MCU::SPI_::SCK_Setup::Rate::F_div_16(void);
void MCU::SPI_::SCK_Setup::Rate::F_div_32(void);
void MCU::SPI_::SCK_Setup::Rate::F_div_32x2(void);
void MCU::SPI_::SCK_Setup::Rate::F_div_64(void);
void MCU::SPI_::SCK_Setup::Rate::F_div_128(void);
```
#### namespace MCU::USART0_
```C++
uint8_t MCU::USART0_::RX(void);
void MCU::USART0_::TX(uint8_t v);
uint16_t MCU::USART0_::RX_9bit(void);
bool MCU::USART0_::is_RX_Complete(void);
bool MCU::USART0_::is_TX_Complete(void);
void MCU::USART0_::TX_Complete(void);
void MCU::USART0_::TX_9bit(uint16_t value);
bool MCU::USART0_::is_Data_Register_Empty(void);
bool MCU::USART0_::is_Frame_Error(void);
bool MCU::USART0_::is_Data_Overrun(void);
bool MCU::USART0_::is_Parity_Error(void);
void MCU::USART0_::RX_Complete_Interrupt_Enable(void);
void MCU::USART0_::RX_Complete_Interrupt_Disable(void);
void MCU::USART0_::TX_Complete_Interrupt_Enable(void);
void MCU::USART0_::TX_Complete_Interrupt_Disable(void);
```
##### namespace MCU::USART0_::Set
```C++
void MCU::USART0_::Set::BuadRate_div_16(void);
void MCU::USART0_::Set::BuadRate_div_8(void);
void MCU::USART0_::Set::Multiprocessor_Mode(void);
void MCU::USART0_::Set::noMultiprocessor_Mode(void);
void MCU::USART0_::Set::Stop_1bit(void);
void MCU::USART0_::Set::Stop_2bits(void);
void MCU::USART0_::Set::Clock_polarity0(void);
void MCU::USART0_::Set::Clock_polarity1(void);
```
###### namespace MCU::USART0_::Set::Character_size
```C++
void MCU::USART0_::Set::Character_size::5_bit(void);
void MCU::USART0_::Set::Character_size::6_bit(void);
void MCU::USART0_::Set::Character_size::7_bit(void);
void MCU::USART0_::Set::Character_size::8_bit(void);
void MCU::USART0_::Set::Character_size::9_bit(void);
```
###### namespace MCU::USART0_::Set::Mode
```C++
void MCU::USART0_::Set::Mode::Asynchronous(void);
void MCU::USART0_::Set::Mode::Synchronous(void);
void MCU::USART0_::Set::Mode::MasterSPI(void);
```

###### namespace MCU::USART0_::Set::Parity_control
```C++
void MCU::USART0_::Set::Parity_control::disable(void);
void MCU::USART0_::Set::Parity_control::even(void);
void MCU::USART0_::Set::Parity_control::odd(void);
```
