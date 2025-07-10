
# 💡 Switch-Controlled LED Blinking on STM32G070RB

## 🧠 Objective

This project demonstrates how a **single tactile switch** can control the **blinking frequency of an LED** connected to the STM32G070RB microcontroller. With each press of the switch, the LED blinks at a different frequency, cycling through four defined states.

---

## 🔁 Functionality Flow

| Press Count | LED Behavior       | Frequency | Delay (ms) |
|-------------|--------------------|-----------|------------|
| 1st Press   | LED blinks slowly  | 0.5 Hz    | 1000 ms    |
| 2nd Press   | LED blinks faster  | 1 Hz      | 500 ms     |
| 3rd Press   | LED blinks fastest | 2 Hz      | 250 ms     |
| 4th Press   | LED turns OFF      | —         | —          |
| 5th Press   | Restart cycle      | —         | —          |

---

## 🔌 Hardware Connections

| Component | STM32 Pin | Description           |
|----------:|-----------|------------------------|
| LED       | PA5       | On-board Green LED     |
| Switch    | PC13      | User push-button input |

---

## ⚙️ Peripheral Configuration

- **GPIO**
  - PA5: Output (LED)
  - PC13: Input with EXTI interrupt (Button)
- **Timer**
  - TIM3: Internal clock, interrupt enabled for blinking LED
- **UART2**
  - Optional (not used in main logic)
- **System Clock**
  - 16 MHz HSI

---

## 🧾 Code Structure

- **main.c**
  - Initializes all peripherals.
  - Sets up `TIM3` for periodic interrupts.
  - Button press tracked in EXTI interrupt, used to change blinking rate.
  - LED toggled inside timer callback.

- **HAL_TIM_PeriodElapsedCallback**
  - Toggles PA5 (LED) every timer overflow.

- **HAL_GPIO_EXTI_Callback**
  - Cycles through 4 LED states using a `press_count` variable.

---

## 💡 Power Optimization (Optional)

This design can be extended to enter low-power mode when LED is OFF (after 4th press). STM32G0 supports multiple power-saving modes.

---

## ▶️ How to Run

1. Flash the code using **STM32CubeIDE**.
2. Power up the NUCLEO-G070RB board.
3. Press the **blue button (PC13)** repeatedly.
4. Observe the **on-board LED (PA5)**:
   - Changes blinking frequency as per switch count.
   - Turns OFF on 4th press.
   - Resumes from beginning on 5th press.

---

## ✅ Assessment Criteria Checklist

- ✅ One switch and one LED used ✔️  
- ✅ LED blinks at 0.5 Hz, 1 Hz, 2 Hz ✔️  
- ✅ Stops on 4th press ✔️  
- ✅ Resumes cycle from 5th press ✔️  
- ✅ Uses HAL + TIM + EXTI ✔️  
- ✅ Can be demoed on STM32 NUCLEO-G070RB ✔️  

---

## 🗂 Project Structure

```
Switch_Led_Blink/
├── Core/
│   ├── Inc/
│   │   └── main.h
│   └── Src/
│       └── main.c
├── Drivers/
├── Switch_Led_Blink.ioc   <-- STM32CubeMX project file
└── README.md              <-- This file
```

---

## 🛠 Tools & Versions

- **STM32CubeIDE**: v6.15.0
- **HAL Drivers**: STM32G0 FW v1.6.2
- **Board**: NUCLEO-G070RB

---
