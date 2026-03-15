# SmartAir TX – IoT Sensor Node using STM32 & FreeRTOS

SmartAir TX is an embedded system application developed using an **STM32 microcontroller and FreeRTOS**.  
The system periodically reads **temperature and humidity data** from a **DHT11 sensor** and transmits the information through **UART** to a serial terminal.

This project demonstrates the practical implementation of **real-time multitasking**, **task synchronization**, and **inter-task communication** in an embedded environment.

---

# Project Overview

SmartAir TX acts as a small **environment monitoring node** capable of collecting sensor data and transmitting it to a host system.

The application performs the following operations:

- Reads **temperature and humidity** from the DHT11 sensor
- Sends sensor data to another task using **FreeRTOS queues**
- Transmits formatted data through **UART**
- Uses **software timers for periodic operation**
- Handles **external interrupts for immediate transmission**
- Maintains transmission statistics using **Thread Local Storage**

---

# Hardware Used

- **STM32 Development Board (STM32F429 series)**
- **DHT11 Temperature and Humidity Sensor**
- **USB-UART interface**
- **User Push Button (External Interrupt)**
- **LED Indicators (optional for debugging)**

---

# Software Tools

- **STM32CubeIDE**
- **FreeRTOS**
- **STM32 HAL Drivers**
- **Serial Terminal (PuTTY / TeraTerm / CoolTerm)**

---

# System Architecture

The application is built using **FreeRTOS components** to manage multiple tasks and ensure proper synchronization.

Main modules of the system:

### Timer
A **FreeRTOS software timer** generates a periodic trigger every **3 seconds** to initiate sensor data transmission.

### Sender Task
Reads temperature and humidity from the **DHT11 sensor** and sends the values to a queue when triggered by the timer or an external interrupt.

### Receiver Task
Receives sensor data from the queue and prints the formatted output over **UART**.

### Status Task
Triggered by an **external interrupt** to display the total number of transmissions performed by the system.

---

# FreeRTOS Components Used

### Tasks
- **Sender Task** – Reads sensor data and sends it to the queue
- **Receiver Task** – Receives data from queue and transmits via UART
- **Status Task** – Displays transmission statistics when triggered

### Queue
Used for **inter-task communication** between the Sender Task and Receiver Task.

### Semaphore
Binary semaphore used for **signaling between ISR and tasks**.

### Mutex
Protects **UART access** to prevent multiple tasks from using it simultaneously.

### Software Timer
Generates **periodic triggers every 3 seconds** for automatic sensor readings.

### Thread Local Storage
Stores **per-task transmission count** to keep track of how many times data has been sent.

---

# Working Flow

1. A **FreeRTOS software timer** generates a trigger every **3 seconds**.
2. The timer releases a **semaphore**.
3. **Sender Task** wakes up and reads temperature and humidity from the DHT11 sensor.
4. Sensor values are sent to a **queue**.
5. **Receiver Task** receives the data from the queue.
6. A **UART mutex** ensures exclusive access to the UART peripheral.
7. Sensor values are printed on the **serial terminal**.
8. When the **user button interrupt** occurs, the system prints the **number of transmissions performed so far**.

---


---

# Key Learning Outcomes

This project helped in understanding:

- **Real-time multitasking using FreeRTOS**
- **Queue-based inter-task communication**
- **Mutex for shared resource protection**
- **Interrupt to task synchronization**
- **Software timers in RTOS**
- **Sensor interfacing with STM32**
- **UART communication for embedded debugging**

---

# Future Improvements

Possible extensions for this project include:

- Adding **WiFi or MQTT connectivity for cloud monitoring**
- Supporting **multiple sensor nodes**
- Implementing **data logging**
- Adding **low power operation**
- Creating a **dashboard for remote monitoring**

---

