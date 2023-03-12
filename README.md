# Electricity Meter Bluetooth LE TLSR8253 (Ai-Thinker TB-04)

## Устройство для дистанционного мониторинга многотарифного однофазного счетчика КАСКАД-1-МТ с последующей передачей показаний в Home Assistant.

**Включает в себя схему опротопорта и модуль от Ai-Thinker TB-04**

[Repository electricity_meter_ble](https://github.com/slacky1965/electricity_meter_ble)

[Схема устройства](https://raw.githubusercontent.com/slacky1965/electricity_meter_ble/main/doc/Schematic_Electricity_meter.jpg)

**Описание**

* Рассчитано на взаимодействие с однофазным многотарифным электросчетчиком КАСКАД-1-МТ (или аналогичными, где используется протокол МИРТЕК) через оптопорт.
* Модуль посылает команды электросчетчику и принимает ответы от него. В настоящий момент устройство может прочитать

> 1. 3 тарифа (в kWh)
> 2. силу тока (в A)
> 3. напряжение сети (в V)
> 4. мощность (в W)
> 5. оставшийся ресурс батарии прибора (в %)
> 6. полный серийный номер прибора (например 3171112520109)
> 7. дату изготовления прибора (например 04.10.2017)

* Сохраняет в энергонезависимой памяти модуля только конфигурационный данные.
* Передает показания по Bluetooth LE в 2-х рекламных пакетах в формате [BTHome V2.0](https://bthome.io/format/).
* Данные в пакетах могут быть зашифрованы [AES-CCM](https://bthome.io/encryption/).
* Первоначальная настройка происходит через [WEB-интерфейс](https://slacky1965.github.io/ble_utils/ElectricityMeterConfig.html). 
* Соединиться с модулем можно только с того устройства, с которого производили первое соединение. Первый раз соединиться можно с любого устройства. Чтобы сбросить whitelist, нужно замкнуть контакт SWS на землю более, чем на 5 секунд (или через [WEB-интерфейс](https://slacky1965.github.io/ble_utils/ElectricityMeterConfig.html), если первоначальное устройство соединения доступно).

---

**Настройка**

Заливаем прошивку с помощью [github.com/pvvx/TLSRPGM](https://github.com/pvvx/TLSRPGM). Запускаем [WEB-конфигуратор](https://slacky1965.github.io/ble_utils/ElectricityMeterConfig.html), соединяемся с модулем, вводим 

> 1. Выбираем нужный счетчик из предложенных.
> 2. Устанавливаем период опроса (в минутах).
> 3. Вводим обязательно адрес счетчика. Для КАСКАД тот, который он показывает у себя на экране, например ID-20109 (т.е. 20109). Для Меркурия это серийный номер, который напечатан на передней панели.
> 4. Если нужно шифрование передаваемых данных, вводим 16 байтный код в hex-представлении, например 231d39c1d7cc1ab1aee224cd096db932
> 5. Множитель/делитель лучше корректировать после отображения информации в Home Assistant (повторным соединением). Корректные значения - 0.001, 0.01, 0.1, 1, 10, 100, 1000.

Отправляем настройки нажатием одноименных кнопок и все.

Тарифы, мощность, напряжение в [WEB-конфигураторе](https://slacky1965.github.io/ble_utils/ElectricityMeterConfig.html) показаны в абсолютных значениях, как они хранятся в памяти.

**Собранное устройство**

Собранного законченного устройства пока нет. Сделано и проверено все на макетке. Но все работает. Удачи.

<img src="https://raw.githubusercontent.com/slacky1965/electricity_meter_ble/main/doc/images/config_html.jpg" alt="Web flasher"/>

<img src="https://raw.githubusercontent.com/slacky1965/electricity_meter_ble/main/doc/images/optoport_maket.jpg" alt="maket1"/>

<img src="https://raw.githubusercontent.com/slacky1965/electricity_meter_ble/main/doc/images/optoport_TB4kit.jpg" alt="maket2"/>

<img src="https://raw.githubusercontent.com/slacky1965/electricity_meter_ble/main/doc/images/kaskad-1-mt.jpg" alt="kackad-1-mt"/>

<img src="https://raw.githubusercontent.com/slacky1965/electricity_meter_ble/main/doc/images/home_assistant.jpg" alt="home_assistant"/>

