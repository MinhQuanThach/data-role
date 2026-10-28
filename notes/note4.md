# Data Model

## Role

- Nhiệm vụ chính là tổng hợp hoặc phân tách các dữ liệu thành bảng, trường, kiểu phù hợp cho từng loại nghiệp vụ
- Khi có dự án mới, BI sẽ phân tích nghiệp vụ, thu thập dữ liệu và gửi yêu cầu xuống team DE. Yêu cầu có thể gồm: cần những dữ liệu như thế nào để phù hợp với nghiệp vụ; các dữ liệu phải có kiểu/trường/bảng gì, thông số báo cáo như thế nào; có thể đưa ra được insight gì từ những dữ liệu đã được tổng hợp
- Khi BI thu thập yêu cầu nghiệp vụ, họ sẽ tạo ra một tài liệu gọi là Data Mapping Document (hoặc Source-to-Target Mapping - STM). Tài liệu này trả lời các câu hỏi:
  - Trường thông tin A ở bảng nguồn (VD: customer_dob trong MySQL) sẽ được đưa vào trường nào ở bảng đích? (VD: age trong Data Warehouse).
  - Công thức biến đổi/tính toán là gì? (VD: age = CURRENT_YEAR - YEAR(customer_dob)).
  - Quy tắc làm sạch hoặc gom nhóm dữ liệu là gì? (VD: Chuẩn hóa M/F thành Male/Female hoặc định dạng date thành string dạng YYYY/MM/DD).

(Data Mapping là tài liệu mô tả logic cho DE biết phải gom, cắt, ghép, biến đổi dữ liệu nguồn như thế nào để ra được Data Model mong muốn.)

- Data Model làm việc trên dữ liệu được gửi về:
  - Tổng hợp hoặc phân tách những bảng/trường cụ thể tùy thuộc vào nhu cầu sử dụng
  - Convert, chuẩn hóa thành đúng kiểu dữ liệu, đúng trường cần sử dụng
  - Tạo Mapping File gửi cho Data Ops để tạo công cụ tối ưu cách xử lý dữ liệu
  - Đưa dữ liệu về dạng giúp cho team khác (BI, BA) dễ dàng đưa ra insight, quyết định đối với dự án
  - Hỗ trợ với team khác để đưa ra insight dựa trên dữ liệu được xử lý

## Orchestration & Execution

Khi xây dựng một Data Pipeline hay quy trình ETL

- Orchestration: Đây là quá trình lên lịch, quản lý thứ tự, giám sát và điều phối toàn bộ các tác vụ thực thi (Execution)
  - Ví dụ: Ra lệnh: "Chờ đến 2:00 AM mỗi ngày -> Chạy Task A (Tải dữ liệu) -> Khi Task A hoàn thành thành công thì mới chạy Task B (Làm sạch dữ liệu) và Task C (Chạy mô hình ML) song song -> Nếu Task B lỗi thì gửi cảnh báo qua Slack và dừng pipeline".
  - Công cụ phổ biến: Apache Airflow
  - Tập trung trả lời: "Khi nào chạy?", "Chạy cái gì trước, cái gì sau?", "Xử lý thế nào khi có sự cố?"
- Execution: Đây là quá trình chạy thực tế từng tác vụ (Task) đơn lẻ trong Data Pipeline.
  - Ví dụ: Chạy một câu lệnh SQL để biến đổi dữ liệu; Thực thi một đoạn script Python (PySpark) để làm sạch dữ liệu; Gửi một lệnh gọi API để tải file CSV từ bên thứ ba về kho lưu trữ (S3)
  - Tập trung vào: "Làm thế nào để chạy đoạn code/câu lệnh này?" và xử lý logic nghiệp vụ cụ thể của tác vụ đó.
