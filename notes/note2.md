# Note 2

## Monitor quá trình xử lý dữ liệu

- Khi dữ liệu được xử lý bằng logic do Data Ops và Data Model thiết kế, quá trình xử lý sẽ được ghi lại trên Airflow.
- Việc monitor sẽ bao gồm theo dõi các quá trình xử lý các bảng trên Airflow xem cái nào thành công cái nào failed
- Nếu failed thì chạy lại thủ công để tìm nguyên nhân
- Có thể tự sửa lại schema, logic, hoặc ping người phụ trách để giải quyết lỗi.
