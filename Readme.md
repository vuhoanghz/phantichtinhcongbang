# Dự án nghiên cứu: Phân tích tính công bằng của các trò chơi cờ bàn/Xổ số (Ứng dụng Tổ hợp & Xác suất)

## 📌 1. Thông Tin Chung
* **Chủ đề:** Phân tích tính công bằng của Xổ số và Cờ bàn qua lăng kính Tổ hợp & Xác suất.
* **Mục tiêu:** Áp dụng công thức tính kỳ vọng toán học $E(X) = \sum x_i p_i$ để chứng minh ưu thế của nhà cái hoặc đánh giá sự cân bằng trong cơ chế trò chơi.
* **Định dạng đầu ra:** Báo cáo phân tích PDF kèm biểu đồ mô phỏng dữ liệu tỷ lệ thắng thua.

---

## 🗺️ 2. Đề Cương Chi Tiết Dự Án

> **Kim chỉ nam:** "Một trò chơi cá cược hoặc cờ bàn được coi là công bằng tuyệt đối về mặt toán học khi và chỉ khi kỳ vọng lợi nhuận của tất cả người chơi bằng 0. Nếu $E(X) \neq 0$, trò chơi luôn có một bên nắm giữ ưu thế (House Edge)."

### Mở Đầu: Đặt Vấn Đề & Cơ Sở Lý Thuyết
* **Định nghĩa "Tính công bằng":** Khái niệm trò chơi công bằng (Fair game) dưới góc độ Lý thuyết Trò chơi (Game Theory).
* **Công cụ Toán học cốt lõi:**
  * Biến cố và Không gian mẫu ($\Omega$).
  * Phân tích Tổ hợp (Chỉnh hợp, Tổ hợp $C_n^k$, Hoán vị).
  * Công thức Kỳ vọng Toán học: $E(X) = \sum (x_i \cdot p_i) - C$ *(Trong đó $x_i$ là tiền thưởng, $p_i$ là xác suất trúng, $C$ là chi phí tham gia)*.
* **Mục tiêu nghiên cứu:** Đưa xác suất từ những con số trừu tượng thành thước đo rủi ro thực tế trong các trò chơi quen thuộc.

### Phần 1: Giải Mã Xổ Số - Nghệ Thuật Đóng Thuế Tự Nguyện
* **Mô hình nghiên cứu:** Phân tích Xổ số ma trận (Ví dụ: Vietlott Mega 6/45 hoặc Power 6/55) và Xổ số truyền thống.
* **Tính toán không gian mẫu:** Sử dụng Tổ hợp chập $k$ của $n$ phần tử để đếm tổng số trường hợp có thể xảy ra (VD: $C_{45}^6 \approx 8.1$ triệu vé).
* **Phân phối xác suất giải thưởng:** Lập bảng xác suất trúng từng hạng giải (Jackpot, Nhất, Nhì, Ba).
* **Tính Toán Kỳ Vọng $E(X)$ và Ưu thế nhà cái (House Edge):**
  * Chứng minh toán học cho thấy $E(X)$ của một vé số luôn là một số âm (người chơi trung bình luôn lỗ).
  * Phân tích điểm hòa vốn: Khi nào Jackpot tích lũy đủ lớn để $E(X) > 0$? Tại sao ngay cả khi $E(X) > 0$, rủi ro phá sản (Ruin of Gambler) vẫn cực kỳ cao?

### Phần 2: Cơ Chế Cờ Bàn (Board Games) - Sự Ngẫu Nhiên Có Sắp Đặt
* **Động lực học của Xúc xắc:**
  * Khảo sát hàm phân phối xác suất khi tung 2 viên xúc xắc 6 mặt (2D6). 
  * Tại sao tổng bằng 7 có xác suất ra cao nhất (16.67%) và ảnh hưởng của nó đến thiết kế bản đồ cờ.
* **Xác suất có điều kiện và Thẻ Sự kiện:** Tính toán xác suất bốc được thẻ có lợi/hại dựa trên số lượng thẻ còn lại trong xấp bài (Cơ chế không hoàn lại).
* **Mô hình hóa bằng Chuỗi Markov (Markov Chains):**
  * Xây dựng "Ma trận chuyển trạng thái" (Transition Matrix) cho các ô trên bàn cờ (Ví dụ: Bàn cờ Tỷ phú - Monopoly).
  * Phân tích ảnh hưởng của các "Điểm trũng" (Sink nodes) như ô "Vào Tù": Cách luật chơi phá vỡ tính phân phối đều của xác suất di chuyển.

### Phần 3: Thực Nghiệm Cờ Tỷ Phú (Monopoly) Bằng Monte Carlo
* **Thiết lập mô phỏng:** 
  * Lập trình một đoạn mã Python (hoặc sử dụng phần mềm) chạy mô phỏng (Monte Carlo Simulation) 10.000 đến 100.000 lượt tung xúc xắc và di chuyển.
  * Giả lập các luật lệ phức tạp: Tung 3 lần đôi bị vào tù, ra tù bằng thẻ/tung đôi,...
* **Phân tích Dữ liệu đầu ra (Heatmap):** 
  * Xây dựng "Bản đồ nhiệt" (Heatmap) thể hiện tần suất người chơi dừng chân tại mỗi ô đất.
  * **Kết quả dự kiến:** Chứng minh bằng số liệu tại sao nhóm đất màu Cam (Orange Properties) thường mang lại lợi thế chiến thắng cao nhất (Do nằm ngay sau lộ trình ra Tù với khoảng cách là 6, 8, 9 bước).
* **Chiến thuật tối ưu:** Từ số liệu xác suất, đề xuất chiến lược mua bán/đầu tư đất trong trò chơi để tối đa hóa tỷ lệ thắng (Win rate).

### Kết Luận: Xác Suất Và Tâm Lý Học Điểm Mù
* **Ngụy biện của con bạc (Gambler's Fallacy):** Sai lầm tâm lý khi cho rằng "Đã thua nhiều lần thì lần sau xác suất thắng sẽ cao hơn" (Hiểu lầm về các biến cố độc lập).
* **Tổng kết:** Đánh giá lại tính công bằng. Trò chơi cờ bàn thường cân bằng nhờ kỹ năng (kết hợp với may rủi), trong khi xổ số là sự bất đối xứng thông tin và tỷ lệ hoàn toàn nghiêng về nhà phát hành.
* **Giá trị cốt lõi:** Việc hiểu và áp dụng tư duy xác suất giúp con người đưa ra quyết định lý trí hơn trước những lựa chọn mang tính rủi ro trong cuộc sống.

---

## 📈 3. Kế Hoạch & Tiến Độ Thực Hiện

- [ ] **Ngày 1-3:** Thu thập luật chơi và định nghĩa các không gian mẫu xác suất, hoàn thiện khung lý thuyết cơ sở.
- [ ] **Ngày 4-7:** Tính toán kỳ vọng Xổ số và lập ma trận xác suất (chuỗi Markov) cho Cờ bàn.
- [ ] **Ngày 8-10:** Viết mã Python chạy thuật toán mô phỏng tần suất tung xúc xắc và vẽ biểu đồ phân phối.
- [ ] **Ngày 11-12:** Hoàn thiện báo cáo, viết Mở đầu, Kết luận và tổng hợp tài liệu tham khảo.
- [ ] **Ngày 13-14:** Rà soát lỗi logic, kiểm tra tính trực quan của các hình vẽ minh họa và đóng gói sản phẩm hoàn chỉnh.

---

## 📚 4. Tài Liệu Tham Khảo (Dự Kiến)
1. Sách giáo trình Xác suất Thống kê cơ bản tại các trường Đại học.
2. Các nghiên cứu chuyên sâu về lý thuyết chuỗi Markov ứng dụng trong trò chơi Cờ tỷ phú.
3. Dữ liệu cơ cấu giải thưởng chính thức được công bố từ các công ty Xổ số.

---

## 🛠️ 5. Cấu Trúc Kho Lưu Trữ
* `/docs`: Bản thảo nội dung phân tích chi tiết dạng `.md` và `.pdf`.
* `/images`: Biểu đồ phân phối xác suất và các ma trận trạng thái.
* `/scripts`: Các script Python mô phỏng Monte Carlo.
* `/data`: Dữ liệu thô thu thập từ mô phỏng hoặc tỷ lệ thưởng xổ số.