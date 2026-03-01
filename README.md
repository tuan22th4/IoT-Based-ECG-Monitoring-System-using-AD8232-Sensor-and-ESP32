# IoT-Based ECG Monitoring System using AD8232 and ESP32

Dự án thiết kế hệ thống giám sát điện tâm đồ (ECG) thời gian thực, tích hợp bộ lọc tín hiệu tương tự và truyền dữ liệu lên nền tảng Cloud qua **ESP32**.

---

## 1. Sơ đồ mạch tổng quát (System Circuit Diagram)

Hệ thống bao gồm khối khuếch đại đo lường sử dụng **AD620AN** và sơ đồ kết nối ngoại vi cho module **AD8232**.

![Sơ đồ mạch tổng quát](IOT_ECG_1.png)

* **Hình 1.1:** Chi tiết thiết kế tầng khuếch đại Instrument Amplifier.
* **Hình 1.2:** Sơ đồ kết nối chân (Pinout) giữa AD8232 và ESP32.

---

## 2. Thiết kế các tầng lọc tín hiệu (Active Filter Design)

Tín hiệu ECG sau khi thu thập được xử lý qua 3 tầng lọc chủ động để loại bỏ nhiễu:

### 2.1. Mạch lọc thông thấp bậc 2 (2nd Order LPF)
Loại bỏ nhiễu tần số cao, sử dụng cấu trúc Sallen-Key với Op-amp OP07.
* **Tần số cắt:** $fc = 159\text{Hz}$
* **Công thức:** $$fc = \frac{1}{2\pi\sqrt{R_1C_1R_2C_2}}$$

![Mạch lọc thông thấp](IOT_ECG_2.png)

### 2.2. Mạch lọc thông cao bậc 2 (2nd Order HPF)
Giúp ổn định đường nền và loại bỏ thành phần DC/nhiễu tần số thấp.
* **Tần số cắt:** $fc = 0.5\text{Hz}$

![Mạch lọc thông cao](IOT_ECG_3.png)

### 2.3. Mạch lọc Notch (Notch Filter)
Triệt tiêu nhiễu điện lưới 50Hz gây ra bởi môi trường xung quanh.
* **Tần số triệt tiêu:** $50\text{Hz}$

![Mạch Notch Filter](IOT_ECG_4.png)

---

## 3. Kết quả hệ thống (System Results)

### 3.1. Dữ liệu lấy mẫu (Sampling Data)
Dữ liệu nhịp tim được chuyển đổi qua bộ ADC của ESP32 và hiển thị giá trị số trên Serial Monitor.

![Kết quả trên Arduino IDE](IOT_ECG_5.png)

### 3.2. Giám sát trên giao diện Blynk (IoT Dashboard)
Kết quả cuối cùng được trực quan hóa trên ứng dụng Blynk, cho phép theo dõi biểu đồ điện tâm đồ mọi lúc mọi nơi.

![Đồ thị ECG trên Blynk](IOT_ECG_6.png)

---

## 4. Thông số kỹ thuật
* **MCU:** ESP32 (Dual-core, Wi-Fi & BT).
* **Sensor:** AD8232 Front-end chip.
* **Lọc nhiễu:** LPF (159Hz), HPF (0.5Hz), Notch (50Hz).
* **Nền tảng Cloud:** Blynk IoT.
