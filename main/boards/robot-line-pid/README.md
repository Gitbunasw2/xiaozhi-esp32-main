# RB Do Line PID (ESP32-S3)

Board rieng cho robot do line. Chan co dinh trong `config.h`.
Menuconfig: Xiaozhi Assistant -> Board Type -> **RB Do Line PID**. Ban co Bluetooth AT-09: **RB Do Line PID + AT09** (`robot-line-pid-at09`).

| Thiet bi | Chan |
|---|---|
| Man ST7789 2.8" 320x240 | SDA 10, SCL 9, DC 8, CS 14, RES 18, BL 13 |
| Mic INMP441 | WS 4, SCK 5, DIN 6 |
| Loa MAX98357 | DOUT 7, BCLK 15, LRCK 16 |
| Nut | BOOT 0, Vol+ 40, Vol- 39 |
| TB6612 motor phai | AIN1 21, AIN2 47, PWMA 12 |
| TB6612 motor trai | BIN1 20, BIN2 19, PWMB 11 |
| TB6612 | STBY noi 3.3V, VCC 3.3V, VM nguon motor, GND chung |
| Cam bien line S0..S5 (S0 = trai nhat) | 1, 41, 2, 48, 42, 3 |
| LED | 17 |

## Cam bien
- S0 (GPIO1), S2 (GPIO2), S5 (GPIO3) co ADC -> doc analog.
- S1 (GPIO41), S3 (GPIO48), S4 (GPIO42) KHONG co ADC tren ESP32-S3 -> doc digital 0/1
  (tin hieu analog cua module duoc so voi nguong ~1.6V). Van chay duoc, nhung muon muot nhat thi
  dua ca 6 kenh ve GPIO1-10.

## Dung
1. Dat robot len vach, noi "hieu chinh cam bien" (hoac GIU LAU Vol-). Robot quay trai phai ~3 giay
   va luu ket qua (giu sau khi tat nguon).
2. Noi "do line" (hoac GIU LAU Vol+). Noi "dung" / "dung do line" hoac giu Vol+ de dung.
3. Mat vach qua 2 giay robot tu dung.

Lenh khac: "do line nhanh len / cham lai", "chinh PID kp 0.05 kd 0.2", "doc cam bien line",
tien / lui / re trai / re phai / dung, bat / tat den.

## Chinh
- Banh quay nguoc: doi `MOTOR_INVERT_LEFT` / `MOTOR_INVERT_RIGHT`.
- Vach trang tren nen den: `LINE_WHITE_ON_BLACK true`.
- PID mac dinh: Kp 0.04, Ki 0, Kd 0.1, toc do 50%. Lac nhieu -> giam Kp hoac tang Kd. Cua khong kip -> tang Kp.
- Doi driver: `MOTOR_DRIVER` (L298n, L293d, Drv8833, L9110s, Mx1508, Bts7960, Generic4).

## Luu y
- GPIO19/20 la chan USB D-/D+ (BIN2/BIN1): mat cong USB native, nap / xem log qua cong UART.
- GPIO43/44 (TX/RX) khong dung tren board nay.
