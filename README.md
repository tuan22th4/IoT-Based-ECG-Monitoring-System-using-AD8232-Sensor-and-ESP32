# IoT-Based ECG Monitoring System using AD8232 and ESP32

Hệ thống giám sát điện tâm đồ (ECG) thời gian thực dựa trên nền tảng IoT, sử dụng vi điều khiển **ESP32** và cảm biến **AD8232** để thu thập, xử lý và truyền dữ liệu lên Cloud qua **Blynk**.

---

## 1. Sơ đồ mạch tổng quát (System Circuit Diagram)

Dự án bao gồm việc thiết kế mạch khuếch đại đo lường và cấu hình kết nối phần cứng giữa các module.

* **Hình 1.1:** Chi tiết cấu trúc khuếch đại instrument amplifier AD620AN.
* **Hình 1.2:** Sơ đồ đấu nối thực tế giữa module AD8232 và ESP32.

![Sơ đồ mạch tổng quát](https://github.com/tuan22th4/IoT-Based-ECG-Monitoring-System-using-AD8232-Sensor-and-ESP32/blob/main/IMG/IOT_ECG_1.png?raw=true)

---

## 2. Thiết kế các tầng lọc tín hiệu (Active Filter Design)

Để đảm bảo tín hiệu ECG sạch và không bị nhiễu, hệ thống tích hợp 3 tầng lọc chủ động sử dụng Op-amp OP07:

### 2.1. Mạch lọc thông thấp bậc 2 (2nd Order Low-Pass Filter)
Giúp loại bỏ các nhiễu tần số cao.
* **Tần số cắt:** $f_c = 159\text{ Hz}$
* **Công thức:** $$f_c = \frac{1}{2\pi\sqrt{R_1C_1R_2C_2}}$$

![Mạch lọc thông thấp](https://github.com/tuan22th4/IoT-Based-ECG-Monitoring-System-using-AD8232-Sensor-and-ESP32/blob/main/IMG/IOT_ECG_2.png?raw=true)

### 2.2. Mạch lọc thông cao bậc 2 (2nd Order High-Pass Filter)
Giúp loại bỏ nhiễu trôi nền (baseline wander).
* **Tần số cắt:** $f_c = 0.5\text{ Hz}$

![Mạch lọc thông cao](https://github.com/tuan22th4/IoT-Based-ECG-Monitoring-System-using-AD8232-Sensor-and-ESP32/blob/main/IMG/IOT_ECG_3.png?raw=true)

### 2.3. Mạch lọc Notch (Notch Filter)
Được thiết kế đặc biệt để triệt tiêu nhiễu từ tần số điện lưới 50Hz.
* **Tần số triệt tiêu:** $50\text{ Hz}$

![Mạch Notch Filter](https://github.com/tuan22th4/IoT-Based-ECG-Monitoring-System-using-AD8232-Sensor-and-ESP32/blob/main/IMG/IOT_ECG_4.png?raw=true)

---

## 3. Kết quả thực nghiệm (Implementation Results)

### 3.1. Dữ liệu trên Serial Monitor
Tín hiệu sau khi được lấy mẫu bởi ADC của ESP32 được hiển thị dưới dạng giá trị số trên Arduino IDE.

![Kết quả trên Arduino IDE](https://github.com/tuan22th4/IoT-Based-ECG-Monitoring-System-using-AD8232-Sensor-and-ESP32/blob/main/IMG/IOT_ECG_5.png?raw=true)

### 3.2. Giám sát từ xa qua Blynk
Dữ liệu được đẩy lên Dashboard của Blynk, cho phép theo dõi biểu đồ điện tâm đồ theo thời gian thực.

![Đồ thị ECG trên Blynk](https://github.com/tuan22th4/IoT-Based-ECG-Monitoring-System-using-AD8232-Sensor-and-ESP32/blob/main/IMG/IOT_ECG_6.png?raw=true)

---

## 4. Thành phần linh kiện chính
* **Vi điều khiển:** ESP32 (Tích hợp Wi-Fi/Bluetooth).
* **Cảm biến:** Module AD8232 Heart Rate Monitor.
* **Op-amps:** OP07, AD620AN.
* **Nền tảng IoT:** Blynk Cloud.
