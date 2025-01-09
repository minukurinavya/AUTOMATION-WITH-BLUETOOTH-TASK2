# AUTOMATION-WITH-BLUETOOTH-TASK2

*COMPANY*: CODTECH IT SOLUTIONS
*NAME*: MINUKOORI NAVYA
*INTERN ID*:CT12EHE
*DOMAIN*: EMBEDDED SYSTEMS
*BATCH DURATION*:DECEMBER 17th, 2025 TO FEBURARY 17th, 2025
*MENTOR NAME*:NEELA SANTOSH KUMAR

# DESCRIPTION OF THE TASK

OBJECTIVE:
   The primary objective of this project is to design and implement a Bluetooth-controlled home automation system that allows users to remotely switch household devices on and off using their smartphones or other Bluetooth-enabled devices. This system aims to provide a cost-effective, user-friendly, and energy-efficient solution for managing home appliances, enhancing convenience, and improving the overall quality of life. By leveraging Bluetooth technology, the system ensures reliable short-range communication without requiring internet connectivity, making it an ideal choice for users in areas with limited or no access to Wi-Fi. This project demonstrates how modern technology can be seamlessly integrated into everyday life, offering a practical step toward smarter, automated homes.

INTRODUCTION:
   Home automation has become a cornerstone of modern living, offering convenience, energy efficiency, and improved quality of life. This project focuses on designing a Bluetooth-controlled home automation system that enables users to wirelessly control household devices, such as lights, fans, or appliances, through a smartphone or other Bluetooth-enabled devices. By utilizing Bluetooth technology, this system provides a reliable and secure means of short-range communication without requiring internet connectivity, making it accessible and practical for various environments. The system aims to simplify daily routines, reduce energy consumption, and serve as a stepping stone toward a fully automated and intelligent home ecosystem.

KEY ACTIVITIES:
The main key activities of this Bluetooth-controlled home automation project include:
1.Requirement Analysis and System Design:
Identify the components and features needed for the system, such as Bluetooth modules, microcontrollers, and relays.
Develop a circuit diagram and system architecture for efficient operation.

2.Hardware Development:
Select and assemble the necessary hardware components, including a Bluetooth module (e.g., HC-05 or HC-06), a microcontroller (e.g., Arduino or ESP32), relays, and power supply units.
Build and test the circuit connections to ensure proper hardware functionality.

3.Software Development:
Develop firmware for the microcontroller to interface with the Bluetooth module and control the relays.
Design and implement a mobile application or use existing Bluetooth controller apps to send commands to the system.

4.Integration and Testing:
Integrate the hardware and software components to establish a seamless communication channel.
Conduct thorough testing to verify the system's ability to switch devices on and off reliably.

5.User Interface Design:
Create a simple and intuitive user interface for the mobile application, enabling users to connect, control, and monitor the devices effortlessly.

6.Deployment and Demonstration:
Install the system in a test environment, such as a room or small household setup, to demonstrate its functionality.
Showcase the system's features, such as device control, responsiveness, and energy efficiency benefits.

7.Documentation and Analysis:
Document the project details, including system design, implementation steps, and challenges faced.
Analyze the performance and identify areas for future improvement or scaling the system.

CIRCUIT DIAGRAM OF THE PROJECT:https://github.com/minukurinavya/AUTOMATION-WITH-BLUETOOTH-TASK2/commit/6df9eccc7ed0a16988c5091a8bab9ff86bdfcd64

BLOCK DIAGRAM OF THE PROJECT:https://github.com/minukurinavya/AUTOMATION-WITH-BLUETOOTH-TASK2/commit/5f73f8ff1cc7d0c2c58bbde563fd43601cd2aa28

SOURCE CODE OF THE PROJECT:
#include <LiquidCrystal.h>

LiquidCrystal lcd(8, 9, 10, 11, 12, 13);

#define white 3
#define blue 4
#define green 5

int tx = 1;
int rx = 0;

char inSerial[15];

void setup() {
  Serial.begin(9600);
  pinMode(white, OUTPUT);
  pinMode(blue, OUTPUT);
  pinMode(green, OUTPUT);
  pinMode(tx, OUTPUT);
  pinMode(rx, INPUT);
  digitalWrite(white, HIGH);
  digitalWrite(blue, HIGH);
  digitalWrite(green, HIGH);
  lcd.begin(16, 2);
  lcd.clear();
  lcd.print("MICROCONTROLLERS ");
  lcd.setCursor(0, 1);
  lcd.print(" LAB ");
  delay(2000);
  lcd.clear();
  lcd.print("HOME AUTOMATION ");
  lcd.setCursor(0, 1);
  lcd.print("USING BLUETOOTH");
  delay(2000);
  lcd.clear();
  lcd.print("1. Bulb 1 WHITE");
  lcd.setCursor(0, 1);
  lcd.print("2. Bulb 2 BLUE");
  delay(2000);
  lcd.clear();
  lcd.print("3. Bulb 3 GREEN");
  delay(2000);
  lcd.clear();
  lcd.print("Bulb 1 2 3 ");
  lcd.setCursor(0, 1);
  lcd.print(" OFF OFF OFF");

}

void loop() {
  int i = 0;
  int m = 0;
  delay(500);
  if (Serial.available() > 0) {
    while (Serial.available() > 0) {
      inSerial[i] = Serial.read();
      i++;
    }
    inSerial[i] = '\0';
    Check_Protocol(inSerial);
  }
}



void Check_Protocol(char inStr[]) {
  int i = 0;
  int m = 0;
  Serial.println(inStr);

  if (!strcmp(inStr, "all on")) {
    digitalWrite(white, LOW);
    digitalWrite(blue, LOW);
    digitalWrite(green, LOW);
    Serial.println("ALL ON");
    lcd.setCursor(4, 1);
    lcd.print("ON ");
    lcd.setCursor(8, 1);
    lcd.print("ON ");
    lcd.setCursor(12, 1);
    lcd.print("ON ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }

  if (!strcmp(inStr, "all off")) {
    digitalWrite(white, HIGH);
    digitalWrite(blue, HIGH);
    digitalWrite(green, HIGH);
    Serial.println("ALL OFF");
    lcd.setCursor(4, 1);
    lcd.print("OFF ");
    lcd.setCursor(8, 1);
    lcd.print("OFF ");
    lcd.setCursor(12, 1);
    lcd.print("OFF ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }

  if (!strcmp(inStr, "white on")) {
    digitalWrite(white, LOW);
    Serial.println("White ON");
    lcd.setCursor(4, 1);
    lcd.print("ON ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }

  if (!strcmp(inStr, "white off")) {
    digitalWrite(white, HIGH);
    Serial.println("White OFF");
    lcd.setCursor(4, 1);
    lcd.print("OFF ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }

  if (!strcmp(inStr, "blue on")) {

    digitalWrite(blue, LOW);
    Serial.println("Blue ON");
    lcd.setCursor(8, 1);
    lcd.print("ON ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }

  if (!strcmp(inStr, "blue off")) {

    digitalWrite(blue, HIGH);
    Serial.println("Blue OFF");
    lcd.setCursor(8, 1);
    lcd.print("OFF ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }
  if (!strcmp(inStr, "green on")) {

    digitalWrite(green, LOW);
    Serial.println("Green ON");
    lcd.setCursor(12, 1);
    lcd.print("ON ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }

  if (!strcmp(inStr, "green off")) {

    digitalWrite(green, HIGH);
    Serial.println("Green OFF");
    lcd.setCursor(12, 1);
    lcd.print("OFF ");
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;
  }

  else {
    for (m = 0; m < 11; m++) {
      inStr[m] = 0;
    }
    i = 0;

  }
}

WORKING:
  The Bluetooth-controlled home automation system operates by establishing a wireless connection between a user's smartphone or Bluetooth-enabled device and a microcontroller-based control unit. The user sends commands through a mobile application or Bluetooth controller app, which are transmitted to the control unit via the Bluetooth module (e.g., HC-05 or HC-06). The microcontroller processes these commands and activates or deactivates the corresponding relays connected to household devices, such as lights, fans, or appliances. Each relay acts as a switch, toggling the power supply to the connected device based on the received instructions. This setup enables seamless, real-time control of devices without the need for internet connectivity. The system ensures secure, low-latency communication within the Bluetooth range, providing an efficient and user-friendly solution for managing home appliances.

CONCLUSION:
  In conclusion, the Bluetooth-controlled home automation system effectively demonstrates how modern technology can enhance convenience, efficiency, and control in managing household devices. By utilizing Bluetooth technology, the system provides a cost-effective and user-friendly solution for wirelessly switching devices on and off, eliminating the need for complex installations or internet connectivity. This project serves as a practical and scalable step toward creating smart homes, making everyday tasks easier while promoting energy conservation. The successful implementation of this system highlights the potential of integrating technology into daily life to improve comfort and quality, paving the way for more advanced home automation innovations in the future.

OUTPUT OF THE PROJECT:https://github.com/minukurinavya/AUTOMATION-WITH-BLUETOOTH-TASK2/commit/7705fe476d084b0919418c19024ff3ca3ed08cd0
