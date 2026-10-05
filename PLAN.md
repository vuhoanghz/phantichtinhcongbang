# Kế hoạch thực hiện: Tiểu luận "Phân tích tính công bằng của các trò chơi cờ bàn và xổ số"

## Định dạng kỹ thuật

Tài liệu được biên soạn bằng **LaTeX (`.tex`)**, biên dịch bằng **pdfLaTeX trên Overleaf**, vì:

-   **Chuẩn học thuật:** LaTeX xử lý tốt các công thức tổ hợp -- xác suất phức tạp ($C_n^k$, $\mathbb{E}[X]$, $\mathrm{Var}(X)$, ma trận chuyển Markov...) với chất lượng in ấn chuyên nghiệp.
-   **Hỗ trợ tiếng Việt đầy đủ:** Gói `babel[vietnamese]` + `fontenc[T5]` + `lmodern` đảm bảo hiển thị đúng dấu tiếng Việt trong cả văn bản lẫn chú thích hình/bảng.
-   **Hình minh họa vector tự vẽ:** Dùng `tikz` + `pgfplots` để dựng sơ đồ Venn, biểu đồ phân phối, sơ đồ Markov, đường cong lý thuyết... trực tiếp bằng mã nguồn -- không phụ thuộc ảnh ngoài, không vướng bản quyền, và luôn khớp bảng màu của tài liệu.
-   **Trình bày trực quan có kiểm soát:** Dùng `tcolorbox` để tạo hai loại hộp cố định xuyên suốt bài -- hộp *"Hiểu theo ngôn ngữ đời thường"* (diễn giải trực giác) và hộp *"Ứng dụng thực tế"* (liên hệ ứng dụng) -- giúp người đọc không chuyên vẫn nắm được ý chính.
-   **Dễ xuất bản:** Overleaf cho phép xuất PDF trực tiếp để nộp bài hoặc chia sẻ, không cần cài đặt môi trường cục bộ.

## Cấu trúc thư mục dự kiến

```text
tieu-luan-cong-bang-tro-choi/
├── docs/
│   ├── 00-de-cuong-tieu-luan.md         # Dàn ý các chương, mục tiêu từng phần
│   └── tai-lieu-tham-khao.md            # Danh mục nguồn tham khảo mở rộng
├── src/
│   └── essay.tex                        # File nguồn LaTeX chính (toàn bộ nội dung)
├── scripts/
│   ├── sicbo_monte_carlo.py             # Script mô phỏng Monte Carlo (trích Listing 1 trong bài)
│   └── verify_probabilities.py          # Đối chiếu số học các công thức tổ hợp đã tính tay
├── outputs/
│   ├── tieu-luan-cong-bang-tro-choi.pdf # Bản PDF biên dịch cuối cùng
│   └── tieu-luan-cong-bang-tro-choi.tex # Bản .tex đã xuất cho người dùng
├── README.md
└── PLAN.md
```

## Quy ước kỹ thuật trong Soạn thảo

-   **Ký hiệu toán học:** Thống nhất dùng $\mathbb{E}[X]$ cho kỳ vọng, $\mathrm{Var}(X)$ cho phương sai, $C_n^k$/$A_n^k$ cho tổ hợp/chỉnh hợp, $P(A)$ cho xác suất -- đồng bộ với sách giáo khoa và các tài liệu xác suất phổ biến.
-   **Hộp giải thích bắt buộc:** Mỗi công thức hoặc định nghĩa cốt lõi (kỳ vọng, House Edge, chuỗi Markov, Kelly Criterion...) phải đi kèm ít nhất một hộp `giaithich` diễn giải bằng ví dụ đời thường, tránh để công thức "trần trụi" không có bối cảnh.
-   **Hộp ứng dụng có chọn lọc:** Chỉ thêm hộp `ungdung` ở những chỗ có liên hệ thực tế rõ ràng (tài chính, bảo hiểm, chọn số vé số, kiểm định RNG...), không lạm dụng để tránh loãng nội dung.
-   **Hình minh họa:** Mọi hình đều vẽ bằng `tikz`/`pgfplots`, dùng đúng bảng màu đã định nghĩa (`sec1color`, `sec2color`, `sec3color`, `thmheadcolor`); mỗi hình có caption giải thích ý nghĩa, không chỉ mô tả hình dạng.
-   **Trích dẫn số liệu ngành:** Các con số không tự suy ra từ công thức trong bài (ví dụ House Edge của Roulette, Keno) phải ghi rõ là "mức trung bình phổ biến trong ngành, có thể thay đổi tùy nhà cái" để tránh gây hiểu nhầm là số liệu tuyệt đối.

## Cài đặt & Môi trường

-   **Yêu cầu hệ thống**: TeX Live 2023+ (khuyến nghị dùng **Overleaf** để tránh thiếu gói cục bộ).
-   **Các gói LaTeX bắt buộc**:
    ```text
    babel (vietnamese), fontenc (T5), lmodern, xcolor, titlesec,
    amsmath, amssymb, amsthm, mathtools, bm,
    tikz, pgfplots (>=1.18), tcolorbox (most),
    graphicx, booktabs, longtable, float, caption,
    listings, listingsutf8, hyperref
    ```
-   **Biên dịch**: Trên Overleaf chọn compiler **pdfLaTeX**, hoặc chạy cục bộ:
    ```bash
    pdflatex essay.tex
    pdflatex essay.tex   # chạy lần 2 để cập nhật mục lục
    ```
-   **Môi trường Python phụ trợ** (cho script mô phỏng trong `scripts/`):
    ```bash
    pip install numpy matplotlib
    python scripts/sicbo_monte_carlo.py
    ```

## Các giai đoạn thực hiện

### Giai đoạn 0 — Chuẩn bị & định hướng tiểu luận
-   [x] Xác định chủ đề, phạm vi: xổ số, board game, bài, tài chính, AI, tâm lý học hành vi.
-   [x] Thiết lập khung LaTeX: màu sắc, kiểu tiêu đề, môi trường định lý/định nghĩa.
-   [x] Soạn Mở đầu: lịch sử (Pascal-Fermat), định nghĩa trò chơi công bằng, công cụ tổ hợp cốt lõi.

### Giai đoạn 1 — Nội dung xác suất nền tảng (Chương 1)
-   [x] Viết phần Xổ số Mega 6/45, Power 6/55, Keno: tính $|\Omega|$, kỳ vọng, House Edge.
-   [x] Viết phần Sic Bo (Tài Xỉu): phân phối tổng ba xúc xắc, House Edge $\approx 0.93\%$.
-   [x] Viết phần Poker (bảng xác suất 5 lá) và Blackjack (card counting).

### Giai đoạn 2 — Board game, Monte Carlo & Kiểm định (Chương 2-4)
-   [x] Viết phần Catan/Monopoly: phân phối tam giác, chuỗi Markov, ma trận quyết định, cân bằng Nash.
-   [x] Viết mô phỏng Monte Carlo (code Python) + Luật số lớn + kỹ thuật MCMC.
-   [x] Viết chương Kiểm định thống kê: Chi bình phương, khoảng tin cậy, hồi quy tuyến tính.

### Giai đoạn 3 — Ứng dụng tài chính, AI & Tâm lý học (Chương 5-7)
-   [x] Viết chương Tài chính: Black-Scholes, Kelly Criterion, bảo hiểm, danh mục đầu tư.
-   [x] Viết chương Cờ bạc hiện đại: Loot box/Gacha, RNG, AlphaGo/Libratus, Provably Fair.
-   [x] Viết chương Tâm lý học: Gambler's Fallacy, Lý thuyết Triển vọng, đạo đức & pháp luật.
-   [x] Viết Kết luận + mục Tổng hợp so sánh House Edge giữa các trò chơi.

### Giai đoạn 4 — Bổ sung hình minh họa trực quan
-   [x] Vẽ sơ đồ Venn minh họa không gian mẫu $\Omega$ và biến cố $A$.
-   [x] Vẽ minh họa xúc xắc cho ví dụ "Tài" và "Bão" trong Sic Bo.
-   [x] Vẽ sơ đồ mạng Markov đơn giản hóa cho Monopoly.
-   [x] Vẽ đường cong hàm giá trị Lý thuyết Triển vọng.
-   [x] Vẽ biểu đồ xác suất tích lũy Pity System (Gacha).
-   [x] Vẽ biểu đồ so sánh House Edge tổng hợp giữa 5 trò chơi.

### Giai đoạn 5 — Kiểm thử biên dịch & xuất bản
-   [x] Biên dịch thử toàn bộ tài liệu (bản thay thế font tương đương) để xác nhận không lỗi cú pháp TikZ/pgfplots.
-   [ ] Biên dịch chính thức trên Overleaf bằng pdfLaTeX với đầy đủ `babel`/`T5`/`lmodern` để xác nhận khớp 100% với bản gốc.
-   [ ] Rà soát chính tả, ngắt trang và số thứ tự hình/bảng lần cuối.
-   [ ] (Tùy chọn) Tách `scripts/verify_probabilities.py` để đối chiếu số học các công thức đã tính tay trong bài.

## Theo dõi tiến độ từng Chương

| # | Chương / Phần | Trạng thái | Hình minh họa |
|---|---|---|---|
| 0 | Mở đầu: lịch sử, định nghĩa, cơ sở lý thuyết | Hoàn thành | 1 (Sơ đồ Venn) |
| 1 | Chương 1: Giải mã xác suất (xổ số, Sic Bo, Poker, Blackjack) | Hoàn thành | 1 (Xúc xắc Tài/Bão) + 2 bảng |
| 2 | Chương 2: Bản chất cờ bạc (board game, Markov, Nash) | Hoàn thành | 2 (Phân phối 2 xúc xắc, Markov) |
| 3 | Chương 3: Mô phỏng Monte Carlo & thực nghiệm | Hoàn thành | 1 (Đồ thị hội tụ) + 1 code listing |
| 4 | Chương 4: Kiểm định thống kê & phát hiện gian lận | Hoàn thành | - |
| 5 | Chương 5: Ứng dụng tài chính & kinh tế lượng | Hoàn thành | - |
| 6 | Chương 6: Cờ bạc hiện đại, game điện tử & AI | Hoàn thành | 1 (Gacha Pity System) |
| 7 | Chương 7: Tâm lý học hành vi & đạo đức | Hoàn thành | 1 (Đường cong Prospect Theory) |
| 8 | Tổng hợp: So sánh House Edge & Kết luận | Hoàn thành | 1 (Biểu đồ cột so sánh) |
| 9 | Biên dịch chính thức trên Overleaf | Chưa bắt đầu | - |

**Quy trình trạng thái:** `Chưa bắt đầu` → `Đang soạn thảo` → `Đang kiểm tra biên dịch` → `Hoàn thiện`.

## Công cụ hỗ trợ

-   **Overleaf:** Biên dịch trực tuyến, không cần cài đặt, đầy đủ gói `babel-vietnamese`.
-   **TikZ/PGFplots Manual:** Tra cứu cú pháp vẽ sơ đồ, biểu đồ, đường cong.
-   **Python (numpy/matplotlib):** Chạy thử độc lập đoạn mô phỏng Monte Carlo trong `scripts/`.
-   **Git & GitHub:** Quản lý phiên bản file `.tex`, theo dõi lịch sử chỉnh sửa nội dung.




