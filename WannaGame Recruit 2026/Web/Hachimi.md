# WannaGame Recruit 2026 - Hachimi

### Category: Web

### Description:
>Author: winky
>
>Maybe you should try this game
## Solution
Bài web này có một unintended solution để lấy flag

Yêu cầu của chúng ta là được cấp quyền truy cập `/admin` bằng tài khoản có username là `admin`

Vì tài khoản admin chưa được tạo nên ta có thể vào `/register` để tạo một tài khoản `admin` được JWT xác thực signature

Sau đó chúng ta có thể vào `/admin`


### Flag
W1{H0rs3s_m4k3_4_l4ndsc4p3_l00k_b34ut1ful_oFA7Rv4L7ppOqipIPSq6QwkV1a22419f54e}