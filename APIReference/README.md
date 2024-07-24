Các hàm điều khiển Leanbot
---

[Arduino tham khảo](https://www.arduino.cc/reference/en/)

[Leanbot](#Leanbot)
- [Leanbot.begin](#Leanbotbegin)
- [LbDelay](#LbDelay)


[Motion ](#Motion)
- [LbMotion.runLR](#LbMotionrunLR)
- [LbMotion.stopAndWait ](#LbMotionstopAndWait)
- [LbMotion.waitDistance ](#LbMotionwaitDistance)
- [LbMotion.waitDistanceMm ](#LbMotionwaitDistanceMm)
- [LbMotion.waitRotation ](#LbMotionwaitRotation)
- [LbMotion.waitRotationDeg ](#LbMotionwaitRotationDeg)
- [LbMotion.getDistance](#LbMotiongetDistance)
- [LbMotion.getDistanceMm](#LbMotiongetDistanceMm)
- [LbMotion.getRotation](#LbMotiongetRotation)
- [LbMotion.getRotationDeg](#LbMotiongetRotationDeg)


[Gripper ](#Gripper)
- [LbGripper.open ](#LbGripperopen)
- [LbGripper.close ](#LbGripperclose)
- [LbGripper.moveTo ](#LbGrippermoveTo)
- [LbGripper.moveToLR ](#LbGrippermoveToLR)
- [LbGripper.readL](#LbGripperreadL)
- [LbGripper.readR](#LbGripperreadR)


[Buzzer ](#Buzzer)
- [Leanbot.tone](#Leanbottone)
- [Leanbot.noTone](#LeanbotnoTone)


[RGB Leds ](#RGB-Leds)
- [LbRGB.show](#LbRGBshow)
- [LbRGB.clear](#LbRGBclear)
- [LbRGB[ ]](#LbRGB[-])
- [LbRGB.fillColor](#LbRGBfillColor)


[Touch Sensors](#Touch-Sensors)
- [LbTouch.read](#LbTouchread)
- [LbTouch.readBits](#LbTouchreadBits)
- [LbTouch.onPress](#LbTouchonPress)


[Ultrasonic Sensor](#Ultrasonic-Sensor)
- [Leanbot.pingCm](#LeanbotpingCm)
- [Leanbot.pingMm](#LeanbotpingMm)


[IR Sensors](#IR-Sensors)
- [LbIRLine.read](#LbIRLineread)
- [LbIRLine.value](#LbIRLinevalue)
- [LbIRLine.print](#LbIRLineprint)
- [LbIRLine.displayOnRGB](#LbIRLinedisplayOnRGB)
- [LbIRLine.isBlackDetected](#LbIRLineisBlackDetected)
- [LbIRLine.doManualCalibration ](#LbIRLinedoManualCalibration)
- [LbIRArray.read](#LbIRArrayread)

<!-- 
[DC Motor ](#DC-Motor)
- [Leanbot.DCMotor.setPower](#LeanbotDCMotorsetPower) -->



# Leanbot

## Leanbot.begin()

### Mô tả
Hàm khởi động Leanbot.

### Cú pháp
```
Leanbot.begin()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ
```
#include <Leanbot.h>

void setup() {
  Leanbot.begin();                // initialize Leanbot
}
```

### Chú ý
Hàm này cần được gọi trong hàm `setup()`.

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbDelay() 

### Mô tả
Hàm này làm cho chương trình chờ cho đến khi hết thời gian trễ được chỉ định, sau đó xử lý dòng lệnh tiếp theo.
Trong khi đó, Leanbot vẫn tiếp tục chạy các hàm khác từ trước, ví dụ như cho Leanbot đi thẳng.

### Cú pháp
```
LbDelay(timeMs)
```

### Tham số
- `timeMs`: Thời gian trễ milli giây (1000 mili giây bằng 1 giây)
  - Đơn vị: ms
  - Khoảng giá trị: [0, 65535]
  - Kiểu dữ liệu: `unsigned int`

### Giá trị trả về
Không có

### Ví dụ
Ví dụ cho Leanbot đi thẳng với vận tốc 400 trong 3 giây, rồi dừng lại
```
LbMotion.runLR(400, 400);    // let Leanbot move forward
LbDelay(3000);               // wait for 3 seconds (Leanbot keeps moving forward)
LbMotion.runLR(0, 0);        // stop Leanbot
```

### Chú ý
Thời gian trễ cao nhất là `65,535` mili giây (≈ 65.5 giây)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

# Motion
![Screenshot](image/Motion.png)

## LbMotion.runLR()

### Mô tả
Hàm này đặt tốc độ và hướng quay cho bánh trái và bánh phải.
Tốc độ càng lớn, bánh xe quay càng nhanh.

### Cú pháp
```
LbMotion.runLR(vL, vR)
```

### Tham số
- `vL`: tốc độ bánh trái
- `vR`: tốc độ bánh phải
  - Đơn vị: bước mỗi giây
  - Phạm vi: [-2000, +2000]
  - Giá trị dương: quay tiến
  - Giá trị âm: quay lùi
  - Các loại dữ liệu cho phép: `int`

### Giá trị trả về
Không có

### Ví dụ
Leanbot di chuyển tiến với tốc độ 400.

```
LbMotion.runLR(400, 400);
```
Xem thêm:
- [runLR.ino](examples/LbMotion/runLR.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)


<!-- ## LbMotion.runLRrpm

### Mô tả
Hàm này đặt tốc độ (vòng quay mỗi phút) và hướng quay cho bánh trái và bánh phải.
Số vòng quay mỗi phút càng lớn, bánh xe quay càng nhanh.

### Cú pháp
```
LbMotion.runLRrpm(rpmL, rpmR)
```


### Tham số
- `rpmL`: tốc độ bánh trái
- `rpmR`: tốc độ bánh phải
  - Đơn vị: RPM - vòng quay mỗi phút
  - Phạm vi: [-60, +60]
  - Giá trị dương: quay tiến
  - Giá trị âm: quay lùi
  - Các loại dữ liệu cho phép: `int`

### Giá trị trả về
Không có

### Ví dụ
Ví dụ này làm cho Leanbot di chuyển tiến với tốc độ 30 vòng mỗi phút
```
LbMotion.runLRrpm(30, 30);
```
Xem thêm:
- [runLRrpm.ino](examples/LbMotion/runLRrpm.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)
 -->
## LbMotion.stopAndWait() 

### Mô tả
Hàm này dừng Leanbot và đợi cho đến khi Leanbot hoàn toàn dừng hẳn.

### Cú pháp
```
LbMotion.stopAndWait()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ

```
LbMotion.stopAndWait();
```

Xem thêm:
- [runLRrpm.ino](examples/LbMotion/runLRrpm.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

<!-- ## LbMotion.stopAndWait 

### Mô tả
Hàm này dừng Leanbot và đợi cho đến khi Leanbot giảm tốc hoàn toàn và dừng hẳn.

### Cú pháp

```
isStop = LbMotion.isStop()
```

### Tham số
Không có

### Giá trị trả về
- `true`: Leanbot has stopped
- `false`: Leanbot is moving
- Data type: `bool`

### Ví dụ
```
bool isStop = LbMotion.isStop();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbMotion.isMoving

### Mô tả
This function checks if Leanbot is moving or not.

### Cú pháp
```
isStop = LbMotion.isMoving()
```

### Tham số
Không có

### Giá trị trả về
- `true`: Leanbot is moving
- `false`: Leanbot has stopped
- Data type: `bool`

### Ví dụ
```
bool isMoving = LbMotion.isMoving();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)
&nbsp; -->
---

## LbMotion.waitDistance() 

### Mô tả

Chương trình sẽ chờ cho đến khi Leanbot đã di chuyển một khoảng cách cho trước rồi thực hiện dòng lệnh tiếp theo.

### Cú pháp
```
LbMotion.waitDistance(distanceStep)
```

### Tham số
- `distanceStep`: Khoảng cách Leanbot di chuyển
  - Đơn vị: bước
  - Các loại dữ liệu cho phép: `long`

### Giá trị trả về
Không có

### Ví dụ

```
LbMotion.runLR(400, 400);       // let Leanbot move forward
LbMotion.waitDistance(1500);    // wait for Leanbot to advance 1500 steps
```
Xem thêm:
- [waitDistance.ino](examples/LbMotion/waitDistance.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)


## LbMotion.waitDistanceMm()

### Mô tả
Chương trình đợi cho đến khi Leanbot di chuyển được khoảng cách (xấp xỉ) tính bằng mm sau đó thực hiện dòng lệnh tiếp theo.

### Cú pháp
```
LbMotion.waitDistanceMm(distanceMm)
```

### Tham số
- `distanceMm`: Khoảng cách Leanbot di chuyển tính bằng mm
  - Đơn vị: mm
  - Các loại dữ liệu cho phép: `int`

### Giá trị trả về
Không có

### Ví dụ

```
LbMotion.runLR(400, 400);       // let Leanbot move forward
LbMotion.delayDistanceMm(150);  // wait for Leanbot to advance 150mm = 15cm
```
Xem thêm:
- [waitDistanceMm.ino](examples/LbMotion/waitDistanceMm.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbMotion.waitRotation() 

### Mô tả

Chương trình sẽ chờ cho đến khi Leanbot đã quay được một góc cho trước rồi thực hiện dòng lệnh tiếp theo

### Cú pháp
```
LbMotion.waitRotation(rotationStep)
```

### Tham số
- `rotationStep`: Góc quay của Leanbot
  - Đơn vị: bước
  - Các loại dữ liệu cho phép: `long`

### Giá trị trả về
Không có

### Ví dụ

```
LbMotion.runLR(+400, -400);      // let Leanbot rotate
LbMotion.waitRotation(1500);     // wait for rotating 1500 steps
```
Xem thêm:
- [waitRotation.ino](examples/LbMotion/waitRotation.ino)

### Chú ý
Cần phải thực nghiệm và điều chỉnh góc quay để tìm ra giá trị bước tương ứng với góc quay mong muốn
- Giá trị bước sẽ khác nhau đối với mỗi Leanbot, tốc độ và bề mặt chuyển động
- Ví dụ: với tốc độ 500 và giá trị bước là 1750, Leanbot sẽ quay một góc khoảng 90°

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbMotion.waitRotationDeg()

### Mô tả

Chương trình đợi cho đến khi Leanbot xoay được (xấp xỉ) góc độ mong muốn sau đó thực hiện dòng lệnh tiếp theo.

### Cú pháp
```
LbMotion.waitRotationDeg(rotationDeg)
```

### Tham số
- `rotationDeg`: góc Leanbot sẽ quay
  - Đơn vị: độ
  - Các loại dữ liệu cho phép: `int`

### Giá trị trả về
Không có

### Ví dụ
```
LbMotion.runLR(+500, -500);        // let Leanbot rotate right
LbMotion.waitRotationDeg(180);     // wait for Leanbot to rotate approximately 180°
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbMotion.getDistance()

### Mô tả
Hàm này trả về giá trị bước mà Leanbot đã di chuyển

### Cú pháp
```
long distance = LbMotion.getDistance()
```

### Tham số
Không có

### Giá trị trả về
Giá trị bước mà Leanbot đã di chuyển
- Đơn vị: bước
- Loại dữ liệu: `long`

### Ví dụ
```
long distance = LbMotion.getDistance();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbMotion.getDistanceMm()

### Mô tả

Hàm này trả về giá trị khoảng cách theo mm mà Leanbot đã di chuyển

### Cú pháp
```
long distance = LbMotion.getDistanceMm()
```

### Tham số
Không có

### Giá trị trả về
Khoảng cách Leanbot đã di chuyển
- Đơn vị: mm
- Loại dữ liệu: `long`

### Ví dụ
```
long distanceMm = LbMotion.getDistanceMm();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbMotion.getRotation()

### Mô tả
Hàm này trả về giá trị góc mà Leanbot đã quay theo đơn vị bước

### Cú pháp
```
long rotation = LbMotion.getRotation()
```

### Tham số
Không có

### Giá trị trả về
Giá trị góc đã quay của Leanbot
- Đơn vị: bước
- Loại giá trị: `long`

### Ví dụ
```
long rotation = LbMotion.getRotation();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbMotion.getRotationDeg()

### Mô tả
Hàm này trả về giá trị góc mà Leanbot đã quay theo đơn vị độ

### Cú pháp
```
long rotationDegree = LbMotion.getRotationDeg()
```

### Tham số
Không có

### Giá trị trả về
Giá trị góc đã quay của Leanbot
- Đơn vị: độ 
- Loại dữ liệu: `long`

### Ví dụ
```
long rotationDegree = LbMotion.getRotationDeg();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

# Gripper
![Screenshot](image/LbGripper.png)

## LbGripper.open() 

### Mô tả
Hàm này di chuyển các cánh tay kẹp đến vị trí mở (cả hai cánh tay ở vị trí 0 độ - vuông góc với bề mặt)

### Cú pháp
```
LbGripper.open()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ
```
LbGripper.open();
```
Xem thêm:
- [GripperOpenClose.ino](examples/LbGripper/GripperOpenClose.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbGripper.close() 

### Mô tả
Hàm này di chuyển cả hai cánh tay kẹp đến vị trí đóng (cả hai cánh tay ở vị trí 90 độ - song song với bề mặt)

### Cú pháp
```
LbGripper.close()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ
```
LbGripper.close();
```
Xem thêm:
- [GripperOpenClose.ino](examples/LbGripper/GripperOpenClose.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbGripper.moveTo() 

### Mô tả
Hàm này di chuyển cả hai cánh tay kẹp đến cùng một góc mong muốn.

### Cú pháp
```
LbGripper.moveTo(toAngle)
```

### Tham số
- `toAngle`: góc cần di chuyển đến
  - Đơn vị: độ (góc)
  - Phạm vi: [-30, +120]
  - Các kiểu dữ liệu cho phép: `int`

### Giá trị trả về
Không có

### Ví dụ
Ví dụ di chuyển cả hai cánh tay kẹp đến vị trí 45°
```
LbGripper.moveTo(45);
```
Xem thêm:
- [GripperMoveTo.ino](examples/LbGripper/GripperMoveTo.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbGripper.moveToLR() 

### Mô tả
Hàm này di chuyển cả hai cánh tay kẹp đến các góc mong muốn cho một khoảng thời gian nhất định.

### Cú pháp
```
LbGripper.moveToLR(toAngleL, toAngleR, timeMs)
```

### Tham số
- `toAngleL`: góc của cánh tay kẹp bên trái cần di chuyển đến
- `toAngleR`: góc của cánh tay kẹp bên phải cần di chuyển đến
  - Đơn vị: độ (góc)
  - Phạm vi: [-30, +120]
  - Các kiểu dữ liệu cho phép: `int`

- `timeMs`: thời gian tính bằng mili giây để di chuyển cả hai cánh tay kẹp đến các góc mục tiêu
  - Các kiểu dữ liệu cho phép: `int`

### Giá trị trả về
Không có

### Ví dụ
Ví dụ di chuyển cánh tay kẹp bên trái đến vị trí 30° và cánh tay kẹp bên phải đến vị trí 60° trong 1.5 giây
```
LbGripper.moveToLR(30, 60, 1500);
```
Xem thêm:
- [GripperMoveToLR.ino](examples/LbGripper/GripperMoveToLR.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbGripper.readL()

### Mô tả
Hàm này trả về góc hiện tại (tính bằng độ) của cánh tay kẹp bên trái.

### Cú pháp
```
LbGripper.readL()
```

### Tham số
Không có

### Giá trị trả về
The current angle (in degrees) of the left gripper arm
- Unit: degree (angle)
- Range: [-30, +120]
- Data type: `int`

### Ví dụ
```
int angleL = LbGripper.readL();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbGripper.readR()

### Mô tả
Hàm này trả về góc hiện tại (tính bằng độ) của cánh tay kẹp bên phải.

### Cú pháp
```
LbGripper.readR()
```

### Tham số
Không có

### Giá trị trả về
Góc hiện tại (tính bằng độ) của cánh tay kẹp bên phải
- Đơn vị: độ (góc)
- Phạm vi: [-30, +120]
- Kiểu dữ liệu: `int`

### Ví dụ
```
int angleR = LbGripper.readR();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

# Buzzer 

## Leanbot.tone()

### Mô tả
Hàm này phát âm thanh với tần số được chỉ định trong một khoảng thời gian.
- Trong khi phát âm thanh, Leanbot tiếp tục xử lý dòng mã tiếp theo
- Âm thanh sẽ tự động dừng lại sau khoảng thời gian, hoặc gọi hàm [Leanbot.noTone](#Leanbot.noTone)

### Cú pháp
```
Leanbot.tone(frequency, duration)
```

### Tham số
- frequency: tần số của âm thanh tính bằng Hertz (Hz)
  - Đơn vị: Hertz (Hz)
  - Kiểu dữ liệu cho phép: `unsigned int`

- duration: (tùy chọn) khoảng thời gian của âm thanh tính bằng mili giây
  - Đơn vị: ms
  - Kiểu dữ liệu cho phép: `unsigned int`

### Giá trị trả về
Không có

### Ví dụ
Phát âm thanh với tần số 1000 Hz trong 1.5 giây
```
Leanbot.tone(1000, 1500);
```
Xem thêm:
- [tone.ino](examples/Buzzer/tone.ino)
- [toneDuration.ino](examples/Buzzer/toneDuration.ino)

### Chú ý
Hàm này là không chặn (non-blocking), nghĩa là ngay cả khi bạn cung cấp tham số thời gian, việc thực thi mã sẽ tiếp tục ngay lập tức ngay cả khi âm thanh chưa phát xong.

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## Leanbot.noTone()

### Mô tả
Hàm này dừng âm thanh được phát bởi [Leanbot.tone](#Leanbot.tone)

### Cú pháp
```
Leanbot.noTone()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ
```
Leanbot.noTone();
```
Xem thêm:
- [noTone.ino](examples/Buzzer/noTone.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

# RGB Leds 
![Screenshot](image/LbRGB.png)
- Leanbot có 7 đèn LED RGB: `ledA`, `ledB`, `ledC`, `ledD`, `ledE`, `ledF` và `ledO`

## Mã màu RGB
Có 3 cú pháp khác nhau để biểu diễn một màu RGB:
1. Tên màu: `CRGB::ColorName`
  - Ví dụ: `CRGB::Red`, `CRGB::Green`, `CRGB::Blue`
  - Xem thêm: [https://github.com/FastLED/FastLED/wiki/Pixel-reference#predefined-colors-list](https://github.com/FastLED/FastLED/wiki/Pixel-reference#predefined-colors-list)

2. Mã thập phân: `CRGB(red, green, blue)`
  - Mỗi tham số (red, green và blue) định nghĩa cường độ của màu với giá trị từ 0 đến 255
  - Ví dụ:
    - `CRGB(255, 0, 0)` là màu đỏ, vì red được đặt ở giá trị cao nhất (255), và hai giá trị còn lại (green và blue) được đặt ở 0
    - `CRGB(0, 255, 0)` là màu xanh lá cây, vì green được đặt ở giá trị cao nhất (255), và hai giá trị còn lại (red và blue) được đặt ở 0
    - Để hiển thị màu đen, đặt tất cả các tham số về 0: `CRGB(0, 0, 0)`
    - Để hiển thị màu trắng, đặt tất cả các tham số về 255: `CRGB(255, 255, 255)`
  - Xem thêm: [https://www.w3schools.com/colors/colors_picker.asp](https://www.w3schools.com/colors/colors_picker.asp)

3. Mã hex: `0xRRGGBB`
  - Nối liền 3 giá trị hex của red, green và blue lại với nhau
  - Ví dụ: `0xFF0000` (đỏ), `0x00FF00` (xanh lá cây), `0x0000FF` (xanh dương)

## LbRGB.show()

### Mô tả
Hàm này hiển thị tất cả các đèn LED.

### Cú pháp
```
LbRGB.show()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ
```
LbRGB.show();
```

### Chú ý
Hàm này phải được gọi sau khi cập nhật màu của các đèn LED.

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbRGB.clear()

### Mô tả
Hàm này xóa tất cả các đèn LED về màu đen.

### Cú pháp
```
LbRGB.clear()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ
```
LbRGB.clear();
LbRGB.show();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbRGB[ ]

### Mô tả
Hàm này đặt một đèn LED đến màu RGB được cho.

### Cú pháp
```
LbRGB[ledX] = color
```

### Tham số
- `ledX`: đèn LED cần được đặt màu
- `color`: mã màu [RGB](#RGB-color-code)

### Giá trị trả về
Không có

### Ví dụ
```
LbRGB[ledA] = CRGB::Red;              // set `ledA` to red
LbRGB[ledO] = CRGB(0, 255, 0);        // set `ledO` to green
LbRGB[ledD] = 0x0000FF;               // set `ledD` to blue
LbRGB.show();                         // show all Leds to diplay
```
Xem thêm:
- [setColor.ino](examples/LbRGB/setColor.ino)

### Chú ý
Hàm này chỉ cập nhật giá trị màu của một đèn LED
- Bạn phải gọi [LbRGB.show](#LbRGB.show) để thực sự hiển thị các màu mới của đèn LED

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbRGB.fillColor()

### Mô tả
Hàm này tô màu (tập hợp các đèn LED) với màu RGB được cho.

### Cú pháp
```
LbRGB.fillColor(color, shape)
```

### Tham số
- `color`: mã màu [RGB](#RGB-color-code)

- `shape`: tập hợp các đèn LED cần đặt màu
  - Các loại dữ liệu được phép: `byte`

### Giá trị trả về
Không có

### Ví dụ
Ví dụ đặt màu xanh lá cây cho 4 đèn LED A, B, C và D (một hình mặt cười)
```
byte LbSmiley = BITMAP(ledA, ledB, ledC, ledD);   // create smiley shape
LbRGB.fillColor(CRGB::Green, LbSmiley);           // fill green color
LbRGB.show();                                     // show all Leds to diplay
```
Xem thêm:
- [fillColor.ino](examples/LbRGB/fillColor.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

# Touch Sensors
![Screenshot](image/LbTouch.png)
- Leanbot has 4 touch sensors: `TB1A`, `TB1B`, `TB2A` and `TB2B`

## LbTouch.read()

### Mô tả
Hàm này đọc trạng thái của cảm biến chạm được chỉ định.

### Cú pháp
```
value = LbTouch.read(tbX)
```

### Tham số
`tbX`: the touch sensor to read. Valid choices are:
- TB1A
- TB1B
- TB2A
- TB2B

### Giá trị trả về
The state the touch sensor
- Value `0`: the sensor is being released
- Value `1`: the sensor is being touched
- Data type: `byte`

### Ví dụ
Ví dụ reads the state of the sensors `TB1A` and `TB2A`
```
byte value1A = LbTouch.read(TB1A);
byte value2A = LbTouch.read(TB2A);
```
Xem thêm:
- [ledControl.ino](examples/LbTouch/ledControl.ino)
- [wheelControl.ino](examples/LbTouch/wheelControl.ino)

### Chú ý
Multiple sensors can be combined and read at once time.
```
LbTouch.read(TB1A | TB1B)
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbTouch.readBits()

### Mô tả
This function reads the state of all 4 touch sensors.

### Cú pháp
```
touchBits = LbTouch.readBits()
```

### Tham số
- Không có

### Giá trị trả về
The binary state of 4 touch sensors
- Value `0`: the sensor is being released
- Value `1`: the sensor is being touched
- Data type: `byte`

### Ví dụ
```
byte touchBits = LbTouch.readBits();
```
Xem thêm:
- [readBits.ino](examples/LbTouch/readBits.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbTouch.onPress()

### Mô tả
This function reads the touching event of the specified touch sensors.

### Cú pháp
```
isOnPress = LbTouch.onPress(tbX)
```

### Tham số
- `tbX`: the touch sensor to read

### Giá trị trả về
The touching event the touch sensor
- Value `true`: the sensor has NOT just been touched, either released or being held
- Value `false`: the sensor has just been touched
- Data type: `bool`

### Ví dụ
Ví dụ reads the touching state of the sensor `TB1A`
```
bool value1A = LbTouch.onPress(TB1A);
```
Xem thêm:
- [onPress.ino](examples/LbTouch/onPress.ino)

### Chú ý
Multiple sensors can be combined and read at once time.
```
LbTouch.onPress(TB1A | TB1B)
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

# Ultrasonic Sensor

### Chú ý
The ultrasonic sensor can be triggered as fast as every 50 ms, or 20 times each second
- You should wait 50 ms before the next ping
- This is to ensure the ultrasonic __beep__ has faded away and will not cause a false echo on the next ranging

## Leanbot.pingCm()

### Mô tả
This function sends a ping and Giá trị trả về the front distance measured in centimeters.

### Cú pháp
```
distanceCm = Leanbot.pingCm()
```

### Tham số
Không có

### Giá trị trả về
The front distance measured in centimeters
- Unit: cm
- Data type: `unsigned int`

### Ví dụ
```
unsigned int distanceCm = Leanbot.pingCm();
```
Xem thêm:
- [pingCm.ino](examples/Ping/pingCm.ino)

### Chú ý
The maximum sensor distance is 300 cm, outside this distance, the function will return 1,000 cm.

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

[[ Ultrasonic Sensor ]](#Ultrasonic-Sensor)
## Leanbot.pingMm()

### Mô tả
This function sends a ping and Giá trị trả về the front distance measured in millimeters.

### Cú pháp
```
distanceMm = Leanbot.pingMm()
```

### Tham số
Không có

### Giá trị trả về
The front distance measured in centimeters
- Unit: mm
- Data type: `unsigned int`

### Ví dụ
```
unsigned int distanceMm = Leanbot.pingMm();
```

### Chú ý
The maximum sensor distance is `3,000 mm`, outside this distance, the function will return `10,000 mm`

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

# IR Sensors

![Screenshot](image/LbIRArray.png)
- Leanbot has 8 IR sensors (order 0 - 7), for different purposes:

| Function             | Sensors                   |
| -------------------- |:-------------------------:|
| Line detection       | ir3R - ir1R - ir0L - ir2L |
| Table edge detection | ir5R - ir4L               |
| Obstacles detection  | ir7R - ir6L               |

## LbIRLine.read()

### Mô tả
This function reads the value of 4 bar sensors. Used to check the position of the black line relative to Leanbot.

### Cú pháp
```
lineState = LbIRLine.read()
```

### Tham số
Không có

### Giá trị trả về
The binary state of 4 bar sensors
- Value `0`: the sensor is on the white surface
- Value `1`: the sensor is on the black line
- Data type: `byte`

### Ví dụ
```
byte lineState = LbIRLine.read();
```
Xem thêm:
- [readLineState.ino](examples/LbIRLine/readLineState.ino)
- [followLine.ino](examples/LbIRLine/followLine.ino)

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbIRLine.value()

### Mô tả
This function Giá trị trả về the value of 4 bar sensors which are read before.

### Cú pháp
```
LbIRLine.value()
```

### Tham số
Không có

### Giá trị trả về
The 4 line sensors value
- Data type: `byte`

### Ví dụ
```
byte lineValue = LbIRLine.value();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbIRLine.print()

### Mô tả
This function sends the value of the 4 bar sensors (which are read before) to the computer.

### Cú pháp
```
LbIRLine.print()
```

### Tham số
Không có

### Giá trị trả về
Không có

### Ví dụ
```
LbIRLine.print();
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbIRLine.displayOnRGB()

### Mô tả
This function displays the 4 bar sensors result on RGB Leds with color.
- If any sensor is on the black line, the corresponding RGB Led will light up

### Cú pháp
```
LbIRLine.displayOnRGB(color)
```

### Tham số
- `color`: the [RGB color code](#RGB-color-code)

### Giá trị trả về
Không có

### Ví dụ
```
LbIRLine.read();                     // update line state
LbIRLine.displayOnRGB(CRGB::Blue);   // display result on Leds
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbIRLine.isBlackDetected()

### Mô tả
This function checks whether one of the 4 bar sensors is on the black line.

### Cú pháp
```
LbIRLine.isBlackDetected()
```

### Tham số
Không có

### Giá trị trả về
- `true` : the bars sensor is on the black line
- `false`: the bars sensor is NOT on the black line
- Data type: `bool`

### Ví dụ
Ví dụ lets Leanbot moving forward until the end of the black line
```
LbMotion.runLR(400, 400);                // move forward
while ( LbIRLine.isBlackDetected() );    // keep moving as long as Leanbot can see the black line
LbMotion.stopAndWait();                  // stop
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbIRLine.doManualCalibration()

### Mô tả
This function does 3-step light level calibration with touch button.

### Cú pháp
```
LbIRLine.doManualCalibration(tbX)
```

### Tham số
- `tbX`: the touch sensor used to perform black/white sampling
  - Leanbot has 4 touch sensors: `TB1A`, `TB1B`, `TB2A` and `TB2A`

### Giá trị trả về
Không có

### Ví dụ
```
LbIRLine.doManualCalibration(TB1A);
```
Xem thêm:
- [lineCalibration.ino](examples/LbIRLine/lineCalibration.ino)
- [calibrationThenFollowLine.ino](examples/LbIRLine/calibrationThenFollowLine.ino)

### Chú ý
It is recommended to perform this step before starting the mission or when there are changes in ambient light or moving surface.

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)

## LbIRArray.read()

### Mô tả
This function reads the value of the specified sensor.
The darker the surface, the higher the sensor value.

### Cú pháp
```
LbIRArray.read(irX)
```

### Tham số
- `irX`: the sensor to read

### Giá trị trả về
The sensor value: 0 - 768
- Data type: `int`

### Ví dụ
Ví dụ reads the value of sensor `ir0L` and sends the result to the computer
```
int value = LbIRArray.read(ir0L);    // read the sensor value
Serial.println(value);               // transfer the results to the computer
```

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot)
<!-- 
# DC Motor 

## Leanbot.DCMotor.setPower

### Mô tả
This function makes the motor rotates at a desired speed in the forward or backward direction.
The greater the power, the faster the motor rotates.

### Cú pháp
```
Leanbot.DCMotor.setPower(power)
```

### Tham số
- `power`: the power level
  - Range: [-255, +255]
  - Positive integer: turn forward
  - Negative integer: turn backward
  - 0: turn off
  - Allowed data types: `int`

### Giá trị trả về
Không có

### Ví dụ
The code makes the motor rotates forward at power level of 250
```
Leanbot.DCMotor.setPower(250);
```
Xem thêm:
- [setPower.ino](examples/DCMotor/setPower.ino)

### Chú ý
Values out of range will be constrained between -255 and +255

[🔼 Trở về đầu trang](#Các-hàm-điều-khiển-Leanbot) -->
