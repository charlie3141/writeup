# WannaGame Recruit 2026 - Hachimi fixed

### Category: Web

### Description:
>Author: winky
>
>Maybe you should try this game
## Solution
Em giải bài này dùng unintended solution, sau đó đã báo BTC để fix lại và được giữ solve ạ

Yêu cầu bài là chúng ta phải truy cập vào `/admin` bằng tài khoản có username là `admin` và được xác thực bằng JWT signature

Vì đây là bản fixed của `Hachimi`, nên em đoán người ra đề chỉ sửa lại bug tự tạo tài khoản `admin` để hoàn thành challenge trước, vậy nên có một khả năng rằng `secret` của JWT vẫn được giữ nguyên

Để kiểm chứng điều đó, em tạo tài khoản `admin` từ bài `Hachimi`, sau đó lấy JWT được xác thực username `admin` và dán vào cookie auth của bài hiện tại và vào `/admin` thành công

### Flag
>to be updated