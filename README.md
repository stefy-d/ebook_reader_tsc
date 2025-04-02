## **Manea Ștefania-Delia**
### **Grupa 335CC** 
<br><br>

# **Pașii de implementare**  
- Realizarea schematicului
- Plasarea componentelor pe PCB
- Trasarea circuitelor și optimizarea rutării semnalelor
- Încărcarea modelelor 3D pentru fiecare componentă
- Crearea bateriei și a display-ului
- Inserarea PCB-ului, a bateriei și a display-ului în carcasa 3D
<br><br> 


# **Diagramă bloc**
```` mermaid
graph TD;
    USB_C[USB C Connector & ESD Protection] -->|Power & Data| LDO[LDO Voltage Regulator];
    LDO -->|3.3V Power| ESP32[ESP32 C6];
    LDO -->|3.3V Power| SD[SD Card];
    LDO -->|3.3V Power| RTC[RTC Module DS3231SN];
    LDO -->|3.3V Power| Sensor[Environmental Sensor BME688];
    LDO -->|3.3V Power| Display[EPD Power];
    ESP32 -->|SPI| SD;
    ESP32 -->|I2C| RTC;
    ESP32 -->|I2C| Sensor;
    ESP32 -->|SPI| Display;
    ESP32 -->|GPIO| Button[Voltage Supervisor + Reset & Boot / IO Button];
    ESP32 -->|SPI| Flash[External NOR Flash 64MB];
    ESP32 -->|GPIO| ChargeLevel[Battery Charge Level];
    ESP32 -->|GPIO| Selector[Display Type Selector];
    ChargeController[Li-Po Battery Charging Controller] -->|Power| LDO;
    ChargeController -->|Battery Status| ChargeLevel;

`````
<br><br>

# **BOM (Bill Of Materials)**

| Componenta      | X      | Y      | Rotatie | Valoare | Package | Link | 
|----------------|--------|--------|----------|------------------------|----------------------------------------|-----------------------------------|  
| BOOT_BUTTON    | 23.90  | 108.41 | 180.00   | BUTTON_CUSYOMV1         | MYBUTTON | https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k |
| C1             | 154.64 | 6.13   | 90.00    | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C10            | 67.34  | 107.83 | 270.00   | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C10_SUPERCAP   | 93.09  | 55.34  | 90.00    | CPH3225A               | CAPCP3225X100N  | https://www.snapeda.com/parts/CPH3225A/Seiko+Instruments/view-part/?ref=eda |
| C1_BAT         | 107.73 | 50.25  | 0.00     | 4.7uF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C1_BAT1        | 109.19 | 37.99  | 0.00     | 4.7uF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C1_BAT2        | 104.58 | 40.47  | 90.00    | 4.7uF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C2             | 153.42 | 6.13   | 90.00    | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C2_BAT         | 120.94 | 51.25  | 90.00    | 4.7uF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C3             | 118.89 | 41.40  | 90.00    | 100uF                  | RCL_CT3528 | https://eu.mouser.com/ProductDetail/KYOCERA-AVX/F910J107MBAAJ6?qs=PqoDHHvF649LraCA%2FjeGXg%3D%3D |
| C4             | 90.95  | 35.19  | 90.00    | 4.7uF/25V              | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C4_USB         | 149.29 | 50.17  | 90.00    | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C5             | 52.21  | 107.71 | 270.00   | 1uF                    | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C5_USB         | 155.40 | 52.97  | 90.00    | 4.7uF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C6             | 27.30  | 107.83 | 270.00   | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C7             | 80.29  | 30.73  | 0.00     | 10uF                   | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C8             | 84.28  | 52.43  | 180.00   | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| C9             | 10.66  | 99.03  | 90.00    | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| CHANGE_BUTTON  | 64.00  | 108.48 | 179.30   | BUTTON_CUSYOMV1         | MYBUTTON | https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k |
| CHG_LED        | 111.34 | 50.15  | 90.00    |                        | ADAFRUIT_CHIP-LED0603                  | https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/view-part/?ref=search&t=LED%200603 |
| C_DELAY        | 51.93  | 101.29 | 269.50   | 100nF                  | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| D1             | 152.58 | 50.47  | 0.00     | USBLC6-2SC6Y            | SOT95P280X145-6N                       | https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=eda |
| D10            | 44.62  | 38.77  | 90.00    | PGB1010603MR            | DIOC1608X36N                           | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda |
| D11            | 42.60  | 38.67  | 90.00    | PGB1010603MR            | DIOC1608X36N                           | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda |
| D12            | 38.38  | 38.87  | 90.00    | PGB1010603MR            | DIOC1608X36N                           | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda |
| D2             | 122.09 | 41.08  | 90.00    | ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0 | ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0 | https://eu.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D |
| D3             | 87.16  | 35.47  | 180.00   | MBR0530                 | SOD3716X135N                           | https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=eda |
| D4             | 87.22  | 31.68  | 0.00     | MBR0530                 | SOD3716X135N                           | https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=eda |
| D5             | 80.26  | 40.58  | 180.00   | MBR0530                 | SOD3716X135N                           | https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=eda |
| D6             | 73.98  | 26.87  | 0.00     | PGB1010603MR            | DIOC1608X36N                           | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda |
| D7             | 83.64  | 68.93  | 0.00     | ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0 | ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0 | https://eu.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D |
| D8             | 14.96  | 98.57  | 0.00     | PGB1010603MR            | DIOC1608X36N                           | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda
| D9             | 33.14  | 47.17  | 270.00   | PGB1010603MR            | DIOC1608X36N                           | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda |
| EPD_C1         | 88.71  | 21.47  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C10        | 76.31  | 21.47  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C11        | 72.05  | 18.89  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C12        | 70.61  | 18.79  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       |   https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C2         | 87.32  | 21.47  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       |   https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C5         | 85.68  | 21.45  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       |   https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C6         | 81.95  | 21.49  | 270.00   | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       |   https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C7         | 80.55  | 21.50  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       |   https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C8         | 79.15  | 21.51  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       |   https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| EPD_C9         | 77.75  | 21.52  | 90.00    | 1uF/50V                | ESP32_WROVER_EAGLE-LTSPICE_C0402       |   https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| IC1            | 48.65  | 101.27 | 0.00     | BD5229G-TR             | SOT95P280X125-5N                       | https://componentsearchengine.com/part-view/BD5229G-TR/ROHM%20Semiconductor |
| IC4            | 113.73 | 40.29  | 0.00     | XC6220A331MR-G         | SOT95P280X120-5N | https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex |
| J1        | 83.10  | 14.17  | 0.00     | FH34SRJ-24S-0.5SH_99_ | FH34SRJ24S05SH99                               | https://componentsearchengine.com/part-view/FH34SRJ-24S-0.5SH(99)/Hirose |
| J2        | 165.53 | 54.30  | 90.00    | SAMACSYS_PARTS_USB4110-GF-A | SAMACSYS_PARTS_USB4110GFA                     | https://componentsearchengine.com/part-view/USB4110-GF-A/GCT%20(GLOBAL%20CONNECTOR%20TECHNOLOGY) |
| J3        | 166.35 | 19.30  | 90.00    | QWIIC_RIGHT_ANGLE | JST04_1MM_RA                                  | https://eu.mouser.com/ProductDetail/Adafruit/4208?qs=PzGy0jfpSMtbScLbr0L5dw%3D%3D |
| J4        | 9.09   | 88.88  | 270.00   | 112A-TAAR-R03_ATTEND | 112ATAARR03ATTEND                             | https://store.comet.srl.ro/Catalogue/Product/43497/ |
| L1        | 80.35  | 35.77  | 270.00   | 68uH            | IND_4828-WE-TPC_WRE                           | https://eu.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D |
| MCP73831  | 116.79 | 49.69  | 90.00    | ESP32_WROVER_SPARKFUN-IC-POWER_MCP73831 | ESP32_WROVER_SPARKFUN-IC-POWER_SOT23-5 | https://eu.mouser.com/ProductDetail/Microchip-Technology/MCP73831T-2ACI-OT?qs=yUQqVecv4qvbBQBGbHx0Mw%3D%3D |
| PFMF.050.1| 151.74 | 43.60  | 0.00     | ESP32C6_VARISTORCN1812 | ESP32C6_VARISTOR_CT/CN1812                    | https://www.mouser.co.uk/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D |
| Q1        | 123.56 | 47.31  | 0.00     | 20V/4.2A/52mΩ/1.4W | ESP32_WROVER_SPARKFUN-DISCRETESEMI_SOT23-3    | https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated |
| Q2        | 76.03  | 31.36  | 270.00   | 20V/4.2A/52mΩ/1.4W | ESP32_WROVER_SPARKFUN-DISCRETESEMI_SOT23-3    | https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated |
| Q3        | 67.19  | 15.28  | 90.00    | SI1308EDL-T1-GE3 | SOT65P210X110-3N                              | https://www.snapeda.com/parts/SI1308EDL-T1-GE3/Vishay+Siliconix/view-part/?ref=eda |
| R1        | 19.35  | 42.13  | 270.00   | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R10       | 12.23  | 99.03  | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R1_BAT    | 111.55 | 48.75  | 0.00     | 200             | ESP32_WROVER_EAGLE-LTSPICE_R0402              |
| R1_PINH   | 156.12 | 6.27   | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R1_PINH1  | 83.56  | 66.94  | 0.00     | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R1_PWRUSB | 106.25 | 40.54  | 90.00    | 100k            | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R2        | 65.73  | 11.51  | 0.00     | 2.2             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R2-PINH   | 157.48 | 6.27   | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R2-USB    | 152.58 | 46.33  | 0.00     | 5k1             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R2-USB1   | 152.56 | 47.77  | 0.00     | 5k1             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R2_BAT    | 115.66 | 46.05  | 90.00    | 2K              | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R2_PINH1  | 89.11  | 63.79  | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R3        | 68.71  | 9.53   | 90.00    | 0.47            | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R4        | 70.49  | 13.91  | 0.00     | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R5        | 31.21  | 47.21  | 270.00   | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R6        | 44.53  | 33.41  | 92.20    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R7        | 42.45  | 33.61  | 270.00   | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R8        | 38.57  | 33.41  | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R9        | 70.89  | 31.31  | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| RESET_BUTTON | 48.90 | 108.49 | 180.40 | BUTTON_CUSYOMV1  | MYBUTTON | https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k |
| R_BOOT    | 20.27  | 107.67  | 270.00   | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R_CAPACITOR | 88.95 | 55.04  | 270.00   | 15              | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R_CHANGE  | 60.62  | 107.78  | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R_CL1     | 72.96  | 31.23  | 90.00    | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| R_RESET   | 45.19  | 107.69  | 269.80   | 10K             | ESP32_WROVER_EAGLE-LTSPICE_R0402              | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| SENSOR2   | 154.46 | 10.42  | 90.00    | ESP32_WROVER_BME680_BME680 | ESP32_WROVER_BME680_PSON80P300X300X100-8N | https://www.snapeda.com/parts/BME680/Bosch/view-part/?welcome=home |
| SJ1       | 65.86  | 9.29   | 0.00     |                 | SJ                                            | https://grabcad.com/library/solder-jumpers-1 |
| TP1       | 10.51  | 67.29  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP10      | 104.28 | 15.51  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP11      | 100.19 | 19.39  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP12      | 99.83  | 15.81  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP13      | 94.86  | 15.83  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP14      | 135.63 | 50.31  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP15      | 78.68  | 70.51  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP16      | 9.43   | 41.31  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP17      | 95.62  | 19.47  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP2       | 14.23  | 67.49  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP3       | 131.25 | 50.56  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP4       | 131.37 | 54.49  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP5       | 135.89 | 54.39  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP6       | 16.11  | 77.59  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP7       | 11.03  | 77.59  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP8       | 5.95   | 77.59  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| TP9       | 104.67 | 19.19  | 0.00     | TPTP20R         | TP20R                                          | CUSTOM
| U1        | 36.89  | 54.16  | 0.00     | W25Q512JVEIQ    | SON127P600X800X80-9N                           | https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/?ref=eda |
| U2        | 16.20  | 54.00  | 90.00    | ESP32-C6-WROOM-1-N8 | XCVR_ESP32-C6-WROOM-1-N8                     | https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif+Systems/view-part/?ref=eda |
| U3        | 79.90  | 59.90  | 270.00   | DS3231SN#       | SOIC127P1032X265-16N                           | https://www.snapeda.com/parts/DS3231SN%23/Analog+Devices/view-part/?ref=eda |
| U4        | 126.58 | 50.72  | 0.00     | MAX17048G+T10   | SON50P200X200X80-9N                            | https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=eda |

<br><br>

# **Pini ESP32-C6**

ESP32-C6 are mai mulți pini utilizați pentru conectarea componentelor din schema bloc. Mai jos este o descriere detaliată a pinilor folosiți și justificarea utilizării lor:

### **1. SD Card (SPI)**
   - **Pini utilizați**:
     - **IO6 (CLK/SCK)** - Semnal de ceas SPI
     - **IO7 (MOSI)** - Linie de date pentru transmitere
     - **IO2 (MISO)** - Linie de date pentru recepție
     - **IO10 (CS)** - Chip Select pentru activarea cardului SD
   - **Motiv**: Protocolul SPI este ideal pentru cardurile SD, deoarece permite viteze mari de transfer cu un număr redus de pini.

### **2. RTC Module DS3231SN (I2C)**
   - **Pini utilizați**:
     - **IO8 (SCL)** - Linie de ceas I2C
     - **IO9 (SDA)** - Linie de date I2C
   - **Motiv**: DS3231SN folosește protocolul I2C pentru comunicație, ceea ce permite partajarea magistralei cu alți senzori.

### **3. Environmental Sensor BME688 (I2C)**
   - **Pini utilizați**:
     - **IO8 (SCL)** - Linie de ceas I2C (partajat cu RTC)
     - **IO9 (SDA)** - Linie de date I2C (partajat cu RTC)
   - **Motiv**: Folosind I2C, senzorul poate comunica eficient cu ESP32 fără a ocupa pini suplimentari.

### **4. EPD Power (SPI)**
   - **Pini utilizați**:
     - **IO6 (CLK/SCK)** - Semnal de ceas SPI
     - **IO7 (MOSI)** - Linie de date pentru transmitere
     - **IO2 (MISO)** - Linie de date pentru recepție
     - **IO5 (CS)** - Chip Select pentru activarea display-ului
   - **Motiv**: Ecranele E-Paper folosesc adesea SPI datorită vitezei mari de transmitere și latenței reduse.

### **5. Voltage Supervisor + Reset & Boot / IO Button (GPIO)**
   - **Pini utilizați**:
     - **IO0** - Buton BOOT
     - **IO3** - Buton Reset
   - **Motiv**: ESP32 folosește aceste pini pentru a intra în mod de programare și resetare rapidă.

### **6. External NOR Flash 64MB (SPI)**
   - **Pini utilizați**:
     - **IO6 (CLK/SCK)** - Semnal de ceas SPI
     - **IO7 (MOSI)** - Linie de date pentru transmitere
     - **IO2 (MISO)** - Linie de date pentru recepție
     - **IO4 (CS)** - Chip Select pentru activarea memoriei Flash
   - **Motiv**: ESP32 poate extinde memoria utilizând SPI pentru a accesa rapid datele stocate.

### **7. Battery Charge Level (GPIO)**
   - **Pini utilizați**:
     - **IO12 (ADC1_CH3)** - Intrare analogică pentru măsurarea tensiunii bateriei
   - **Motiv**: ESP32 dispune de convertoare ADC care permit măsurarea nivelului de încărcare al bateriei.

### **8. Display Type Selector (GPIO)**
   - **Pini utilizați**:
     - **IO14** - Selector de tip ecran (ex. alb-negru vs. color)
   - **Motiv**: Un pin GPIO poate fi folosit pentru a configura sau selecta diferite moduri de operare ale ecranului.

<br><br>

# **Descriere hardware**  


## **1. Microcontrolerul principal – ESP32-C6**  

ESP32-C6 gestionează toate componentele conectate prin diverse protocoale de comunicație, asigurând interfațarea eficientă cu acestea.  

---

## **2. Module și senzori conectați la ESP32-C6: ca mai sus**  

### **2.1. Stocare – Card SD**  
- **Interfață de comunicare**: SPI   

---

### **2.2. Modul RTC DS3231SN**  
- **Interfață de comunicare**: I2C   

---

### **2.3. Senzor BME688** 
- **Interfață de comunicare**: I2C  

---

### **2.4. Ecran E-Paper (SPI)**  
- **Interfață de comunicare**: SPI 

---

### **2.5. Memorie externă NOR Flash 64MB**  
- **Interfață de comunicare**: SPI   

---

### **2.6. Butoane pentru control**   
- **Interfață de comunicare**: GPIO    

---

### **2.7. Monitorizare baterie**  
- **Interfață de comunicare**: GPIO / ADC  

---

### **2.8. Selector de tip ecran**   
- **Interfață de comunicare**: GPIO  

---

### **3. Alimentare și managementul energiei**  

ESP32-C6 și toate componentele funcționează la **3.3V**, alimentarea fiind gestionată de:  

1. **Regulator de tensiune LDO**   

2. **Controler de încărcare baterie Li-Po**  

---

### **4. Rezumat**  

| **Componentă**                        | **Interfață** | **Pini ESP32-C6**      |
|---------------------------------------|--------------|------------------------|
| **Card SD**                           | SPI          | IO6, IO7, IO2, IO10    |
| **RTC DS3231SN**                      | I2C          | IO8, IO9               |
| **Senzor BME688**                     | I2C          | IO8, IO9               |
| **Display E-Paper**                   | SPI          | IO6, IO7, IO2, IO5     |
| **Memorie NOR Flash 64MB**            | SPI          | IO6, IO7, IO2, IO4     |
| **Butoane de control**                | GPIO         | IO0, IO3               |
| **Monitorizare baterie**              | ADC/GPIO     | IO12                   |
| **Selector de tip ecran**             | GPIO         | IO14                   |

