# MCU_Mega168
Интерфейсный класс для микроконтроллера AVR8 Mega168.

Идея позаимствована отсюда: https://habr.com/ru/post/459642/

18.06.22 Добавлена функция включения/выключения ADC в регистре PRR
```C++
MCU::Core::ADC_turnOn();
MCU::Core::ADC_turnOff();
```

