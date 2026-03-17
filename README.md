# Phân Tích Dữ Liệu Bán Hàng Thương Mại Điện Tử Thời Trang

**Dự án Tốt nghiệp**

---

## Mục tiêu dự án

Dự án này phân tích dữ liệu bán hàng của một thương hiệu thời trang Ấn Độ đang kinh doanh trên nhiều nền tảng thương mại điện tử (Amazon, Flipkart, Myntra và các sàn khác). Phân tích nhằm trả lời 4 câu hỏi kinh doanh cốt lõi:

---

## Nguồn dữ liệu

- **Nguồn:** Kaggle
- **File:** `Master_File.xlsx` — một file Excel chứa 6 sheet dữ liệu

---

## Tổng quan dữ liệu

| Sheet | Mô tả | Số dòng gốc | Số dòng sau cleaning | Cột chính |
|---|---|---|---|---|
| Amazon Sale Report | Đơn hàng nội địa Amazon India (T3–T6/2022) | 128,975 | 107,365 | Order ID, Date, Category, SKU, Qty, Amount, Status, State |
| International Sale Report | Đơn hàng xuất khẩu quốc tế (T6/2021–T5/2022) | 37,432 | 18,635 | DATE, CUSTOMER, SKU, PCS, RATE, GROSS AMT |
| May-2022 (Bảng giá) | Giá MRP trên 8 nền tảng cho 1,330 SKU | 1,330 | 1,330 | SKU, Category, TP (giá vốn), MRP từng platform |
| Sale Report (Tồn kho) | Mức tồn kho hiện tại theo SKU | 9,271 | 9,173 | SKU Code, Category, Stock, Size, Color |
| P&L March 2021 | Tham khảo lịch sử giá | — | Không dùng trực tiếp | — |
| Cloud Warehouse | So sánh chi phí logistics | — | Không dùng trực tiếp | — |

---

## Công cụ và công nghệ sử dụng

| Công cụ | Mục đích sử dụng |
|---|---|
| **Power BI Desktop** | Môi trường phân tích chính: data model, DAX measures, dashboard tương tác |
| **Power Query (M)** | Làm sạch dữ liệu: xử lý null, đổi kiểu dữ liệu, lọc, unpivot cột MRP |
| **DAX** | Tính các chỉ số: Total Revenue, AOV, MoM%, Low Stock SKU Count, Revenue % |
| **Excel** | Kiểm tra nhanh kết quả bằng Pivot Table trước khi đưa vào Power BI |

---

## Các phát hiện quan trọng (Key Insights)

### 1. Rủi ro tập trung doanh thu
- **Set + Kurta chiếm 77.1% tổng doanh thu** (₹53.7M / ₹69.7M)
- Western Dress có AOV cao thứ 2 (₹765) nhưng chỉ chiếm 14.1% doanh thu — tín hiệu cho thấy cầu có nhưng cung (số lượng SKU) đang thiếu
- Tháng 4/2022 là tháng cao điểm với ₹25.7M, sau đó doanh thu giảm liên tiếp -8.6% và -13%

### 2. Giá không nhất quán trên 18.7% SKU
- Mức giá trung bình toàn danh mục khá đồng đều (Amazon ₹2,248 vs Myntra ₹2,233 — chênh lệch chỉ ₹15)
- Nhưng **242 SKU (18.7%)** có mức chênh lệch giá trung bình 9.2%, tối đa lên đến 47.2% giữa các nền tảng
- Điều này tạo ra cơ hội so sánh giá giữa các sàn và xói mòn niềm tin thương hiệu

### 3. Phân bổ tồn kho mất cân đối
- TOP: **45% SKU có nguy cơ hết hàng** (≤3 units) — mức CRITICAL
- DRESS: **44% SKU có nguy cơ hết hàng** — mức CRITICAL
- KURTA: tổng tồn kho cao (114,333 units) nhưng 30% SKU cận hết hàng
- Tồn kho tổng cao ≠ phân bổ tốt: vấn đề nằm ở size và màu sắc cụ thể

### 4. Miền Nam Ấn Độ là thị trường mạnh nhất
- Karnataka + Telangana + Tamil Nadu + Kerala = **36% doanh thu**
- Miền Bắc (UP + Delhi) chỉ chiếm 15%
- Tamil Nadu có lượng đơn hàng cao (9,641) nhưng AOV thấp (₹603 vs trung bình ₹649) — tiềm năng tăng giá trị đơn hàng

---

## Giả thuyết dựa trên phân tích (Hypotheses)

1. **H1:** Tháng 4 là đỉnh doanh thu do mùa lễ hội/cưới hỏi — cần kiểm tra với dữ liệu các năm trước để xác nhận tính lặp lại theo mùa vụ
2. **H2:** 242 SKU có giá không nhất quán đang khiến khách hàng chuyển sang mua ở nền tảng rẻ hơn, làm giảm conversion rate tại các nền tảng có giá cao hơn
3. **H3:** Hết hàng ở danh mục TOP và DRESS trong tháng 4 (peak) đã làm mất doanh thu đáng kể có thể tránh được
4. **H4:** Nhu cầu Western Dress đang cao hơn dữ liệu hiện tại cho thấy — giới hạn đang đến từ nguồn cung SKU, không phải từ cầu thị trường

---

## Khuyến nghị

| # | Khuyến nghị | Hành động cụ thể | Tác động kỳ vọng |
|---|---|---|---|
| R1 | Đa dạng hóa danh mục | Tăng 30–40 SKU Western Dress và Ethnic Dress | Giảm rủi ro tập trung từ 77% xuống <65% trong 2 mùa |
| R2 | Chuẩn hóa giá trên các nền tảng | Kiểm tra và đồng bộ MRP cho 242 SKU sai lệch, sai biệt cho phép ≤2% | Bảo vệ niềm tin thương hiệu, ngăn khách hàng so sánh giá giữa sàn |
| R3 | Bổ sung tồn kho trước mùa cao điểm | Tái cơ cấu TOP và DRESS 8 tuần trước tháng 4 | Tránh hết hàng trong tháng doanh thu cao nhất |
| R4 | Tăng đầu tư marketing tại Miền Nam | Tăng ngân sách digital marketing cho Tamil Nadu và Kerala | Tăng AOV từ ₹603 lên mức trung bình ₹649 — tiềm năng +₹357K/mùa |

---
