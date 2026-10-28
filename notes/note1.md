# Note 1

## Role

- BI: Phân tích nghiệp vụ của dự án, cung cấp dữ liệu thô và yêu cầu nghiệp vụ để team Data Engineer làm theo
- Data Model: viết những câu lệnh SQL để join, xử lý dữ liệu thô thành các dữ liệu phù hợp với nghiệp vụ mà BI phân tích
- Data Ops: viết SQL tối ưu hơn so với bên Data Model, thiết kế công cụ và thực hiện xử lý dữ liệu. Dữ liệu được xử lý sẽ đẩy lên Airflow cùng với tình trạng xử lý, nếu xử lý thất bại sẽ thông báo vào Mail.
- Data Infrastructure: cung cấp tài nguyên và môi trường cho Data Model và Data Ops

## Kiến trúc Medallion

- Là một mẫu thiết kế dữ liệu (data design pattern) để tổ chức và cấu trúc dữ liệu trong 1 Data Lake hoặc Data Warehouse. Mục tiêu của kiến trúc này là liên tục cải thiện cấu trúc, chất lượng và độ tinh khiết của dữ liệu khi nó di chuyển qua các tầng khác nhau.
- Các tầng:
  - Bronze - Raw/Landing Layer: dữ liệu thô chưa qua xử lý, thường giữ nguyên định dạng gốc
  - Silver - Enriched/Cleansed Layer: dữ liệu được làm sạch chuẩn hóa, lọc dữ liệu rác, làm giàu để tối ưu hóa cho việc truy vấn, cấu trúc lưu trữ rõ ràng (Delta Lake hoặc Parquet)
  - Gold - Curated / Aggregated / Presentation Layer: dữ liệu tinh khiết nhất, được tổng hợp, tính toán sẵn chỉ số kinh doanh (KPI), số liệu thống kê theo các chiều không gian và tgian

## Ví dụ dữ liệu trong 1 dự án cụ thể

- Raw: dữ liệu thô, hết hạn trong vòng 1 ngày
- Staging: vẫn là dữ liệu thô nhưng lưu trữ được trong vài ngày, cần phải xử lý trong ngày, trong tuần hoặc nếu là đầu tháng thì xử lý hết dữ liệu trong tháng trước
- Sharing: dữ liệu được xử lý từ Staging mà BI có thể xem và truy vấn trong phạm vi phù hợp với nghiệp vụ

## Apache Spark

- Là một framework mã nguồn mở tính toán phân tán (distributed computing framework) cực kỳ nhanh, được thiết kế để xử lý và phân tích dữ liệu lớn (Big Data)
- Hỗ trợ lập trình đa ngôn ngữ như PySpark, Scala hoặc Java
- Có thể xử lý dữ liệu qua việc gọi API hoặc viết SQL. Bản chất quy trình là giống nhau, chỉ khác nhau về giao diện. Spark API thường dùng khi xử lý phức tạp (có thể dùng cache/broadcast), Spark SQL dùng khi xử lý đơn giản và muốn can thiệp sâu
