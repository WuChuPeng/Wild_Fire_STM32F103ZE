# Reset
There are three types of reset, defined as:
- System Reset
- Power Reset
- Backup Domain Reset

# 1. System Reset

## 1.1 Introduction
A system reset sets all registers to their **reset values**, except the reset flags in:
- **the RCC_CSR register** (Control / Status Register) 
- **the registers in the Backup Domain**

## 1.2 Occur Condition
A system reset is generated when one of the following events occurs:
1. A low level on the **NRST** pin (external reset).
2. Window watchdog end of count condition (**WWDG** reset).
3. Independent watchdog end of count condition (**IWDG** reset).
4. A software reset (**SW** reset).
5. Low-power management reset.

> Notes: The reset source can be identified by checking the reset flags in **the RCC_CSR**.

## 1.3 Software Reset 
The **SYSRESETREQ** bit in Cortex-M3 **Application Interrupt and Reset Control Register** must be set to force a software reset on the device.

> Notes: Refer to the STM32F10xxx Cortex-M3 programming manual.

## 1.4 Low-Power management reset
There are two ways to generate a low-power management reset:

1. Reset generated when entering the Standby Mode
2. Reset when entering the Stop Mode

In the Standby Mode, reset is enabled by resetting **nRST_STDBY** bit in **User Option Bytes**. In this case, whenever a Standby Mode entry sequence is successfully executed, the device is reset instead of entering the Standby Mode.

In the Stop Mode, reset is enabled by resetting **nRST_STOP** bit in **User Option Bytes**. In this case, whenever a Stop Mode entry sequence is successfully executed, the device is reset instead of entering the Stop Mode.

> Notes: For further information on the **User Option Bytes**, refer to the STM32F10xxx Flash programming manual.

## 2. Power Reset 

## 2.1 Introduction
A power reset sets all registers to their reset values except **the Backup domain**.

## 2.2 Occur Condition
A power reset is generated when one of the following events occurs:
1. Power-on / Power-off reset (**POR/PDR** reset)
2. When exiting the Standby Mode

# 3. Backup Domain Reset

## 3.1 Introduction
The backup domain has two specific resets that affect only the backup domain.

## 3.2 Occur Condition
A backup domain is generated when one of the following events occurs:
1. Software reset, triggered by setting the **BDRST** bit in **RCC_BDCR** (the Backup Domain Control Register)
2. Vdd or Vbat power on, if both supplies have previously been powered off.

# 4. Action on Reset Event

## 4.1 Behavior
These sources act on the **NRST** pin and it is always kept **low** during the delay phase. The system reset signal provided to the device is output on the **NRST** pin. The pulse generator guarantees a minimum reset pulse duration of **20 us** for each reset source (external or internal reset). In case of an external reset, the reset pulse is generated while the **NRST** pin is asserted low.

## 4.2 Serive Routine Address 
The **RESET** service routine is fixed at address **0x0000_0004** in the memeory map.

# 5. Simplified Diagram of the Reset Circuit
![image](https://user-images.githubusercontent.com/101664225/160645528-dd49585a-0f49-41f1-ba81-29ae69342d33.png)

# 6. Mind Map of this chapter
![image](https://user-images.githubusercontent.com/101664225/160645339-5638797b-7105-4966-8fcb-364891230121.png)

