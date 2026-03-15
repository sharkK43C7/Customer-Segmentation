# Phân Khúc Khách Hàng sử dụng Phân Tích RFM và K-Means Clustering

## Tổng Quan Dự Án

Dự án này thực hiện phân khúc khách hàng trên bộ dữ liệu giao dịch thương mại điện tử bằng cách sử dụng phân tích RFM (Recency, Frequency, Monetary) kết hợp với K-Means clustering. Mục tiêu là xác định các nhóm khách hàng riêng biệt dựa trên hành vi mua hàng của họ, giúp doanh nghiệp điều chỉnh chiến lược marketing và cải thiện quản lý quan hệ khách hàng.

Dự án được phát triển trên Google Colab như một bài tập học tập về khoa học dữ liệu, tập trung vào ứng dụng thực tế của các kỹ thuật machine learning không giám sát cho phân tích khách hàng.

## Mô Tả Dữ Liệu

Dự án sử dụng **Bộ Dữ Liệu Online Retail**, chứa khoảng **540.000 giao dịch** từ một nền tảng thương mại điện tử. Bộ dữ liệu bao gồm các cột sau:

- **InvoiceNo**: Số hóa đơn duy nhất cho mỗi giao dịch
- **StockCode**: Mã sản phẩm
- **Description**: Mô tả sản phẩm
- **Quantity**: Số lượng sản phẩm đã mua
- **InvoiceDate**: Ngày và giờ của giao dịch
- **UnitPrice**: Giá mỗi đơn vị sản phẩm
- **CustomerID**: Mã định danh duy nhất cho mỗi khách hàng
- **Country**: Quốc gia nơi giao dịch diễn ra

## Quy Trình Dự Án

Phân tích tuân theo một pipeline khoa học dữ liệu có cấu trúc:

1. **Tải Dữ Liệu**
   - Nhập bộ dữ liệu vào môi trường phân tích

2. **Làm Sạch Dữ Liệu**
   - Loại bỏ các hàng có giá trị `CustomerID` bị thiếu
   - Loại bỏ các hóa đơn đã hủy (được xác định bởi `InvoiceNo` bắt đầu bằng 'C')
   - Loại bỏ các giao dịch có giá trị `Quantity` âm
   - Loại bỏ các giao dịch có giá trị `UnitPrice` bằng không

3. **Kỹ Thuật Đặc Trưng (Feature Engineering)**
   - Tính toán `TotalPrice` = `Quantity` × `UnitPrice` cho mỗi giao dịch

4. **Phân Tích RFM**
   - **Recency (Độ Mới)**: Tính số ngày kể từ lần mua hàng cuối cùng của mỗi khách hàng
   - **Frequency (Tần Suất)**: Đếm tổng số giao dịch của mỗi khách hàng
   - **Monetary (Giá Trị)**: Tổng số tiền chi tiêu (`TotalPrice`) của mỗi khách hàng

5. **Chuẩn Hóa Đặc Trưng**
   - Áp dụng `StandardScaler` để chuẩn hóa các đặc trưng RFM cho clustering

6. **Lựa Chọn Số Cụm Tối Ưu**
   - Sử dụng Phương Pháp Elbow để xác định số lượng cụm tối ưu

7. **Phân Khúc Khách Hàng**
   - Áp dụng K-Means clustering với k=4 để phân khúc khách hàng

8. **Phân Tích Cụm**
   - Phân tích và giải thích đặc điểm của từng phân khúc khách hàng

9. **Trực Quan Hóa**
   - Sử dụng Phân Tích Thành Phần Chính (PCA) để trực quan hóa các phân khúc khách hàng trong không gian 2D

## Công Nghệ Sử Dụng

- **Python**: Ngôn ngữ lập trình chính
- **Pandas**: Thao tác và phân tích dữ liệu
- **NumPy**: Tính toán số học
- **Scikit-learn**: Thuật toán machine learning (K-Means, StandardScaler, PCA)
- **Matplotlib**: Trực quan hóa dữ liệu
- **Seaborn**: Trực quan hóa dữ liệu thống kê

## Phương Pháp Machine Learning

### Phân Tích RFM
Phân tích RFM là một kỹ thuật phân khúc khách hàng đánh giá:
- **Recency (R - Độ Mới)**: Khách hàng đã mua hàng gần đây như thế nào
- **Frequency (F - Tần Suất)**: Khách hàng mua hàng thường xuyên như thế nào
- **Monetary (M - Giá Trị)**: Khách hàng chi tiêu bao nhiêu tiền

Ba chỉ số này cung cấp cái nhìn toàn diện về giá trị và mức độ tương tác của khách hàng.

### K-Means Clustering
K-Means là một thuật toán machine learning không giám sát phân chia khách hàng thành k cụm dựa trên điểm số RFM của họ. Thuật toán:
- Nhóm các khách hàng có hành vi mua hàng tương tự lại với nhau
- Tối thiểu hóa phương sai trong cụm
- Cho phép xác định các phân khúc khách hàng riêng biệt

Số lượng cụm tối ưu (k=4) được xác định bằng Phương Pháp Elbow, đánh giá tổng bình phương trong cụm (WCSS) cho các giá trị k khác nhau.

## Kết Quả

Thuật toán K-Means clustering đã xác định thành công **4 phân khúc khách hàng riêng biệt** dựa trên đặc điểm RFM:

1. **Champions (Khách Hàng Vàng)**: Recency, frequency và monetary value cao - khách hàng có giá trị nhất
2. **Loyal Customers (Khách Hàng Trung Thành)**: Người mua thường xuyên với frequency và monetary value tốt
3. **At Risk (Khách Hàng Có Nguy Cơ)**: Khách hàng có recency giảm dần, có thể cần tái tương tác
4. **Lost Customers (Khách Hàng Đã Mất)**: Recency, frequency và monetary value thấp - khách hàng không hoạt động

Mỗi phân khúc thể hiện các mẫu hành vi riêng biệt có thể thông báo các chiến lược marketing có mục tiêu:
- Champions có thể hưởng lợi từ chương trình khách hàng thân thiết và các ưu đãi cao cấp
- Khách hàng At Risk có thể cần các chiến dịch win-back
- Khách hàng Lost có thể cần các chiến lược kích hoạt lại

## Trực Quan Hóa

Dự án bao gồm các biểu đồ trực quan để hiểu rõ hơn về các phân khúc khách hàng:

- **Biểu Đồ Elbow Method**: Hiển thị số lượng cụm tối ưu bằng cách vẽ WCSS so với các giá trị k
- **Trực Quan Hóa PCA**: Biểu đồ scatter 2D của các phân khúc khách hàng sử dụng Phân Tích Thành Phần Chính, cho thấy cách các phân khúc khác nhau được phân bố trong không gian giảm chiều
- **Biểu Đồ Phân Phối RFM**: Histogram và box plot hiển thị phân phối của các giá trị Recency, Frequency và Monetary trên các phân khúc

## Cách Chạy Dự Án

### Yêu Cầu
- Tài khoản Google Colab (hoặc môi trường Jupyter Notebook)
- Python 3.x
- Các thư viện cần thiết: pandas, numpy, scikit-learn, matplotlib, seaborn

### Các Bước

1. **Mở notebook trong Google Colab**
   ```python
   # Tải lên file notebook vào Google Colab
   ```

2. **Tải lên bộ dữ liệu**
   - Đảm bảo Bộ Dữ Liệu Online Retail có sẵn trong môi trường Colab của bạn
   - Cập nhật đường dẫn file trong phần tải dữ liệu nếu cần

3. **Cài đặt các thư viện cần thiết** (nếu chưa được cài đặt)
   ```python
   !pip install pandas numpy scikit-learn matplotlib seaborn
   ```

4. **Chạy tất cả các cell tuần tự**
   - Thực thi các cell theo thứ tự từ trên xuống dưới
   - Notebook sẽ thực hiện làm sạch dữ liệu, phân tích RFM, clustering và trực quan hóa

5. **Xem xét kết quả**
   - Kiểm tra kết quả phân tích cụm
   - Xem xét các biểu đồ trực quan để hiểu các phân khúc khách hàng

### Lưu Ý
Đảm bảo điều chỉnh đường dẫn file và các tham số theo vị trí bộ dữ liệu và yêu cầu cụ thể của bạn.

## Cải Tiến Trong Tương Lai

Các cải tiến tiềm năng cho dự án này bao gồm:

- **Lựa Chọn Cụm Động**: Triển khai các phương pháp tự động (ví dụ: Silhouette Score) để lựa chọn cụm tối ưu
- **Thuật Toán Clustering Nâng Cao**: Thử nghiệm với DBSCAN, Hierarchical Clustering hoặc Gaussian Mixture Models
- **Kỹ Thuật Đặc Trưng**: Kết hợp các đặc trưng bổ sung như danh mục sản phẩm, tính thời vụ hoặc nhân khẩu học khách hàng
- **Phân Tích Dựa Trên Thời Gian**: Thực hiện phân tích thời gian để theo dõi cách các phân khúc khách hàng phát triển theo thời gian
- **Khuyến Nghị Kinh Doanh**: Phát triển các chiến lược marketing có thể hành động cho mỗi phân khúc được xác định
- **Đánh Giá Mô Hình**: Thêm các chỉ số định lượng để đánh giá chất lượng clustering
- **Bảng Điều Khiển Tương Tác**: Tạo các biểu đồ trực quan tương tác bằng Plotly hoặc Tableau
- **Triển Khai**: Chuyển đổi phân tích thành một pipeline sẵn sàng sản xuất để phân khúc khách hàng theo thời gian thực

