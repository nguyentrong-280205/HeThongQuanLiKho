# 1. Xác định ngữ cảnh (Business Context)

**Doanh nghiệp sản xuất** vận hành hệ thống kho bao gồm kho nguyên liệu và kho thành phẩm để phục vụ quy trình sản xuất và giao hàng. Tuy nhiên, hệ thống hiện tại còn phụ thuộc nhiều vào xử lý thủ công, đặc biệt trong việc quản lý nhập/xuất kho, theo dõi tồn kho, kiểm soát lô hàng, hạn sử dụng và kiểm kê.

Khi quy mô sản xuất và số lượng đơn hàng tăng, hệ thống hiện tại gặp hạn chế về **tự động hóa, truy vết lô hàng, kiểm soát chất lượng nguyên liệu, quản lý tồn kho và khả năng báo cáo thống kê**.

Do đó, doanh nghiệp mong muốn xây dựng **Hệ thống quản lý kho** nhằm tự động hóa quy trình từ **đặt hàng → mua nguyên liệu → kiểm tra chất lượng → nhập kho → lập kế hoạch sản xuất → phân công xưởng → xuất kho nguyên liệu → sản xuất → nhập kho thành phẩm → xuất kho giao hàng → kiểm kê → báo cáo thống kê**, đồng thời hỗ trợ quản lý dữ liệu kho và có khả năng mở rộng trong tương lai.

---

# 2. Business Problem

Hệ thống hiện tại tồn tại các vấn đề chính:

## 2.1. Quản lý nhập/xuất kho thủ công

Việc nhập kho nguyên liệu, thành phẩm, xuất kho cho sản xuất và giao hàng được xử lý thủ công, dễ xảy ra sai sót về số lượng và vị trí lưu trữ.

**Hệ thống cần:** tự động hóa quy trình nhập/xuất kho, tạo phiếu nhập/xuất kho, cập nhật tồn kho và quản lý vị trí lưu trữ.

---

## 2.2. Khó kiểm soát lô hàng và hạn sử dụng

Nguyên liệu và thành phẩm được quản lý theo lô nhưng việc theo dõi hạn sử dụng và áp dụng nguyên tắc FEFO (First Expired, First Out) gặp khó khăn khi xử lý thủ công.

**Hệ thống cần:** quản lý thông tin lô hàng, hạn sử dụng và tự động gợi ý lô xuất kho theo nguyên tắc FEFO.

---

## 2.3. Quy trình mua nguyên liệu chưa tập trung

Việc lập đơn mua, phê duyệt, tiếp nhận nguyên liệu và kiểm tra chất lượng chưa được quản lý thống nhất trên một hệ thống.

**Hệ thống cần:** hỗ trợ toàn bộ quy trình từ lập đơn mua → phê duyệt → nhận nguyên liệu → kiểm tra chất lượng → nhập kho.

---

## 2.4. Kiểm kê và điều chỉnh tồn kho chưa hiệu quả

Việc kiểm kê kho, xử lý chênh lệch và điều chỉnh tồn kho được thực hiện thủ công, mất nhiều thời gian và dễ xảy ra sai sót.

**Hệ thống cần:** hỗ trợ kiểm kê kho, đối chiếu chênh lệch, lập đề nghị điều chỉnh và phê duyệt điều chỉnh tồn kho.

---

## 2.5. Thiếu công cụ báo cáo và cảnh báo kho

Hệ thống hiện tại chưa có công cụ tổng hợp báo cáo tồn kho, nhập/xuất, hiệu suất lưu kho và cảnh báo khi tồn kho thấp, tồn kho cao hoặc hàng sắp hết hạn sử dụng.

**Hệ thống cần:** cung cấp báo cáo thống kê và cảnh báo kho để hỗ trợ ra quyết định.

---

## 2.6. Quản lý kế hoạch sản xuất và phân công xưởng chưa liên kết với kho

Kế hoạch sản xuất và phân công xưởng sản xuất chưa được liên kết chặt chẽ với tình trạng nguyên liệu và năng lực sản xuất trong kho.

**Hệ thống cần:** hỗ trợ lập kế hoạch sản xuất dựa trên tình trạng nguyên liệu, phê duyệt kế hoạch và phân công xưởng sản xuất.

---

## 2.7. Xử lý hàng trả về và hàng lỗi chưa có quy trình rõ ràng

Hàng trả về từ khách hàng và hàng lỗi trong quá trình sản xuất chưa có quy trình kiểm tra, phân loại và xử lý rõ ràng.

**Hệ thống cần:** hỗ trợ kiểm tra hàng trả về, nhập kho hàng trả về đạt chất lượng và xử lý hàng lỗi.

---

# Stakeholders – Hệ thống quản lý kho

| Stakeholder | Vai trò | Mối quan tâm / Mục tiêu |
|---|---|---|
| **Ban giám đốc** | Sponsor / Decision Maker | Phê duyệt kế hoạch sản xuất, đơn mua nguyên liệu, điều chỉnh tồn kho; theo dõi báo cáo thống kê |
| **Khách hàng** | End User | Đặt đơn hàng, nhận thành phẩm đúng thời gian và chất lượng |
| **Nhân viên kho** | Operational User | Nhập/xuất kho nguyên liệu, thành phẩm, hàng trả về; nhận nguyên liệu từ NCC |
| **Bộ phận quản lý kho** | Operational User | Quản lý dữ liệu kho, nguyên liệu, thành phẩm, lô hàng; điều phối nhập/xuất kho; xử lý chênh lệch kiểm kê; xử lý hàng lỗi; tra cứu dữ liệu kho; theo dõi báo cáo |
| **Bộ phận lập kế hoạch sản xuất** | Operational User | Lập kế hoạch sản xuất, phân công xưởng sản xuất |
| **Xưởng sản xuất** | Operational User | Lập phiếu yêu cầu xuất kho nguyên liệu, lập phiếu yêu cầu nhập kho thành phẩm |
| **Bộ phận QC** | Operational User | Kiểm tra chất lượng nguyên liệu, kiểm tra hàng trả về |
| **Bộ phận mua hàng** | Operational User | Lập đơn mua nguyên liệu |
| **Hội đồng kiểm kê** | Operational User | Thực hiện kiểm kê kho |

---

# 3. Business Goals

- **BG1:** Tự động hóa quy trình nhập/xuất kho nguyên liệu và thành phẩm, giảm sai sót thủ công.

- **BG2:** Quản lý lô hàng và hạn sử dụng, hỗ trợ xuất kho theo nguyên tắc FEFO.

- **BG3:** Tập trung hóa quy trình mua nguyên liệu từ lập đơn → phê duyệt → tiếp nhận → kiểm tra chất lượng → nhập kho.

- **BG4:** Liên kết kế hoạch sản xuất với tình trạng nguyên liệu, năng lực sản xuất và phân công xưởng.

- **BG5:** Hỗ trợ kiểm kê kho, xử lý chênh lệch và điều chỉnh tồn kho có phê duyệt.

- **BG6:** Cung cấp báo cáo thống kê và cảnh báo kho để hỗ trợ quản lý và ra quyết định.

- **BG7:** Quản lý dữ liệu kho (nguyên liệu, thành phẩm, lô, vị trí lưu kho) tập trung và nhất quán.

- **BG8:** Hỗ trợ quy trình xử lý hàng trả về và hàng lỗi.

---

# 4. Scope – Phạm vi hệ thống

## 4.1. In Scope

### 1. Đăng nhập hệ thống
- Xác thực tài khoản, xác định vai trò và phân quyền truy cập.

### 2. Đặt đơn hàng
- Khách hàng đặt đơn hàng thành phẩm, tạo căn cứ cho kế hoạch sản xuất.

### 3. Kế hoạch sản xuất
- Lập kế hoạch sản xuất dựa trên đơn hàng, tình trạng nguyên liệu và năng lực sản xuất.
- Phê duyệt kế hoạch sản xuất bởi Ban giám đốc.
- Phân công xưởng sản xuất.

### 4. Mua nguyên liệu
- Lập đơn mua nguyên liệu.
- Phê duyệt đơn mua bởi Ban giám đốc.
- Nhận nguyên liệu từ nhà cung cấp.
- Kiểm tra chất lượng nguyên liệu.

### 5. Nhập kho
- Nhập kho nguyên liệu (sau kiểm tra chất lượng đạt).
- Nhập kho thành phẩm (sau sản xuất hoàn thành).
- Nhập kho hàng trả về (sau kiểm tra đạt chất lượng).

### 6. Xuất kho
- Lập phiếu yêu cầu xuất kho nguyên liệu (từ xưởng sản xuất).
- Xuất kho nguyên liệu (theo FEFO).
- Xuất kho thành phẩm giao hàng (theo FIFO/FEFO).
- Lập phiếu yêu cầu nhập kho thành phẩm (từ xưởng sản xuất).

### 7. Điều phối kho
- Điều phối nhập kho (xác định vị trí lưu trữ).
- Điều phối xuất kho (xác định lô hàng ưu tiên theo FIFO/FEFO).

### 8. Hàng trả về và hàng lỗi
- Kiểm tra hàng trả về.
- Nhập kho hàng trả về đạt chất lượng.
- Xử lý hàng lỗi và hàng trả về không đạt.

### 9. Kiểm kê kho
- Thực hiện kiểm kê kho.
- Xử lý chênh lệch kiểm kê.
- Phê duyệt điều chỉnh tồn kho.

### 10. Quản lý dữ liệu
- Quản lý nguyên liệu (thêm, cập nhật, xóa).
- Quản lý thành phẩm (thêm, cập nhật, xóa).
- Quản lý lô nguyên liệu.
- Quản lý lô thành phẩm.
- Quản lý dữ liệu kho.
- Tra cứu dữ liệu kho.

### 11. Thống kê báo cáo và cảnh báo kho
- Báo cáo tồn kho.
- Báo cáo nhập/xuất kho.
- Báo cáo hiệu suất lưu kho.
- Cảnh báo tồn kho thấp, tồn kho cao, hàng/lô sắp hết hạn sử dụng.

---

## 4.2. Quy trình nghiệp vụ chính

**Quy trình mua nguyên liệu:**
Lập đơn mua nguyên liệu → Duyệt đơn mua → Nhận nguyên liệu từ NCC → Kiểm tra chất lượng → Nhập kho nguyên liệu

**Quy trình sản xuất:**
Đặt đơn hàng → Lập kế hoạch sản xuất → Duyệt kế hoạch → Phân công xưởng → Lập phiếu yêu cầu xuất kho NL → Xuất kho NL → Sản xuất → Lập phiếu yêu cầu nhập kho TP → Nhập kho thành phẩm → Xuất kho giao hàng

**Quy trình hàng trả về:**
Kiểm tra hàng trả về → Đạt: Nhập kho hàng trả về / Không đạt: Xử lý hàng lỗi

**Quy trình kiểm kê:**
Thực hiện kiểm kê → Xử lý chênh lệch → Phê duyệt điều chỉnh tồn kho

---

# 5. Business Requirements

| Mã | Tên Business Requirement | Diễn giải |
|---|---|---|
| **BR01** | Đăng nhập và phân quyền | Hệ thống hỗ trợ người dùng đăng nhập, xác thực tài khoản và phân quyền truy cập theo vai trò. |
| **BR02** | Đặt đơn hàng | Hệ thống hỗ trợ khách hàng đặt đơn hàng thành phẩm với đầy đủ thông tin sản phẩm, số lượng và thông tin nhận hàng. |
| **BR03** | Lập và phê duyệt kế hoạch sản xuất | Hệ thống hỗ trợ lập kế hoạch sản xuất dựa trên đơn hàng, tình trạng nguyên liệu và năng lực sản xuất; Ban giám đốc phê duyệt kế hoạch. |
| **BR04** | Phân công xưởng sản xuất | Hệ thống hỗ trợ phân công xưởng sản xuất cho kế hoạch đã được duyệt dựa trên năng lực và lịch sản xuất. |
| **BR05** | Mua nguyên liệu | Hệ thống hỗ trợ lập đơn mua nguyên liệu, phê duyệt đơn mua, tiếp nhận nguyên liệu từ nhà cung cấp. |
| **BR06** | Kiểm tra chất lượng | Hệ thống hỗ trợ kiểm tra chất lượng nguyên liệu và hàng trả về theo tiêu chuẩn quy định. |
| **BR07** | Nhập/Xuất kho nguyên liệu | Hệ thống hỗ trợ nhập kho nguyên liệu đạt chất lượng, xuất kho nguyên liệu theo FEFO cho sản xuất. |
| **BR08** | Nhập/Xuất kho thành phẩm | Hệ thống hỗ trợ nhập kho thành phẩm sau sản xuất, xuất kho thành phẩm theo FIFO/FEFO cho giao hàng. |
| **BR09** | Điều phối nhập/xuất kho | Hệ thống hỗ trợ xác định vị trí lưu trữ khi nhập kho và lô hàng ưu tiên khi xuất kho. |
| **BR10** | Xử lý hàng trả về và hàng lỗi | Hệ thống hỗ trợ kiểm tra, nhập kho hàng trả về đạt chất lượng và xử lý hàng lỗi. |
| **BR11** | Kiểm kê kho | Hệ thống hỗ trợ kiểm kê kho, xử lý chênh lệch và phê duyệt điều chỉnh tồn kho. |
| **BR12** | Quản lý dữ liệu kho | Hệ thống hỗ trợ quản lý danh mục nguyên liệu, thành phẩm, lô nguyên liệu, lô thành phẩm và dữ liệu kho. |
| **BR13** | Tra cứu dữ liệu kho | Hệ thống hỗ trợ tra cứu dữ liệu kho theo các tiêu chí: mã, tên, lô, kho, vị trí, trạng thái. |
| **BR14** | Thống kê báo cáo và cảnh báo kho | Hệ thống cung cấp báo cáo tồn kho, nhập/xuất kho, hiệu suất lưu kho và cảnh báo tồn kho bất thường, hàng sắp hết hạn. |

---

# 6. Business Process

| Mã | Business Process | Mô tả |
|---|---|---|
| **BP01** | Đăng nhập hệ thống | Người dùng đăng nhập, hệ thống xác thực và phân quyền theo vai trò. |
| **BP02** | Đặt đơn hàng | Khách hàng chọn sản phẩm, nhập thông tin nhận hàng và xác nhận đặt hàng. |
| **BP03** | Lập kế hoạch sản xuất | Bộ phận lập KHSX chọn đơn hàng, nhập thông tin kế hoạch, kiểm tra khả thi và xác nhận. |
| **BP04** | Duyệt kế hoạch sản xuất | Ban giám đốc xem xét và phê duyệt/từ chối/yêu cầu điều chỉnh kế hoạch sản xuất. |
| **BP05** | Phân công xưởng sản xuất | Bộ phận lập KHSX chọn xưởng phù hợp cho kế hoạch đã duyệt. |
| **BP06** | Lập đơn mua nguyên liệu | Bộ phận mua hàng lập đơn mua nguyên liệu với nhà cung cấp. |
| **BP07** | Duyệt đơn mua nguyên liệu | Ban giám đốc xem xét và phê duyệt/từ chối đơn mua. |
| **BP08** | Nhận nguyên liệu từ NCC | Nhân viên kho tiếp nhận nguyên liệu, kiểm tra chứng từ và số lượng. |
| **BP09** | Kiểm tra chất lượng nguyên liệu | Bộ phận QC kiểm tra chất lượng nguyên liệu theo tiêu chuẩn. |
| **BP10** | Nhập kho nguyên liệu | Nhân viên kho nhập kho nguyên liệu đạt chất lượng. |
| **BP11** | Lập phiếu yêu cầu xuất kho NL | Xưởng sản xuất lập phiếu yêu cầu xuất kho nguyên liệu theo lệnh sản xuất. |
| **BP12** | Xuất kho nguyên liệu | Nhân viên kho xuất kho nguyên liệu theo phiếu yêu cầu và FEFO. |
| **BP13** | Lập phiếu yêu cầu nhập kho TP | Xưởng sản xuất lập phiếu yêu cầu nhập kho thành phẩm sau sản xuất. |
| **BP14** | Nhập kho thành phẩm | Nhân viên kho nhập kho thành phẩm và cập nhật tồn kho. |
| **BP15** | Xuất kho thành phẩm giao hàng | Nhân viên kho xuất kho thành phẩm theo đơn hàng và FIFO/FEFO. |
| **BP16** | Điều phối nhập kho | Bộ phận quản lý kho xác định vị trí lưu trữ cho lô hàng nhập kho. |
| **BP17** | Điều phối xuất kho | Bộ phận quản lý kho xác định lô hàng ưu tiên xuất theo FIFO/FEFO. |
| **BP18** | Kiểm tra hàng trả về | Bộ phận QC kiểm tra chất lượng hàng trả về. |
| **BP19** | Nhập kho hàng trả về | Nhân viên kho nhập kho hàng trả về đạt chất lượng. |
| **BP20** | Xử lý hàng lỗi và hàng trả về | Bộ phận quản lý kho phân loại và xử lý hàng lỗi/hàng trả về không đạt. |
| **BP21** | Quản lý dữ liệu kho | Bộ phận quản lý kho thêm, cập nhật, xóa dữ liệu kho. |
| **BP22** | Thực hiện kiểm kê kho | Hội đồng kiểm kê kiểm đếm và đối chiếu với hệ thống. |
| **BP23** | Xử lý chênh lệch kiểm kê | Bộ phận quản lý kho xác định nguyên nhân và lập đề nghị điều chỉnh. |
| **BP24** | Phê duyệt điều chỉnh tồn kho | Ban giám đốc phê duyệt/từ chối đề nghị điều chỉnh tồn kho. |
| **BP25** | Thống kê báo cáo và cảnh báo kho | Hệ thống tổng hợp báo cáo và cảnh báo kho. |

---

# 7. Functional Requirements

## 7.1. Đăng nhập hệ thống – UC01

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR01** | Đăng nhập hệ thống | Cho phép tất cả Actor đăng nhập vào hệ thống bằng tên đăng nhập và mật khẩu hợp lệ. |
| **FR02** | Xác thực tài khoản | Hệ thống xác thực tên đăng nhập và mật khẩu với thông tin trong CSDL. |
| **FR03** | Phân quyền theo vai trò | Hệ thống xác định vai trò người dùng và cấp quyền truy cập chức năng tương ứng. |
| **FR04** | Tạo phiên đăng nhập | Hệ thống tạo phiên đăng nhập cho người dùng sau khi xác thực thành công. |

### Đặc tả Use Case UC01 – Đăng nhập hệ thống

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC01 |
| **Tên** | Đăng nhập hệ thống |
| **Actor chính** | Tất cả các Actor |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép người dùng đăng nhập vào hệ thống, xác thực tài khoản và phân quyền truy cập. |
| **Tiền điều kiện** | Người dùng được cung cấp tài khoản và mật khẩu hợp lệ. Hệ thống đang hoạt động bình thường. |
| **Hậu điều kiện** | Nếu thành công: hệ thống xác thực tài khoản, xác định vai trò và phân quyền truy cập. Nếu thất bại: người dùng không được phép truy cập. |

**Basic Flow:**

| Bước | Người dùng | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng đăng nhập. | |
| 2 | | Hiển thị form đăng nhập gồm: ô Tên đăng nhập, ô Mật khẩu, nút "Đăng nhập". |
| 3 | Nhập tên đăng nhập và mật khẩu. | |
| 4 | Chọn nút "Đăng nhập". | |
| 5 | | Kiểm tra tính đầy đủ của thông tin đăng nhập. |
| 6 | | Xác thực tên đăng nhập và mật khẩu với thông tin tài khoản trong hệ thống. |
| 7 | | Kiểm tra trạng thái hoạt động của tài khoản. |
| 8 | | Xác định vai trò của người dùng và quyền truy cập tương ứng. |
| 9 | | Tạo phiên đăng nhập cho người dùng. |
| 10 | | Kết thúc Use Case. |

**Alternative Flow:**

- **5.1. Người dùng chưa nhập đầy đủ thông tin đăng nhập:**
  1. Hệ thống xác định tên đăng nhập hoặc mật khẩu chưa được nhập.
  2. Hệ thống thông báo yêu cầu nhập đầy đủ thông tin.
  3. Quay lại bước 3 của Basic Flow.

- **6.1. Tên đăng nhập hoặc mật khẩu không chính xác:**
  1. Hệ thống xác định thông tin đăng nhập không chính xác.
  2. Hệ thống thông báo tên đăng nhập hoặc mật khẩu không đúng.
  3. Quay lại bước 3 của Basic Flow.

- **6.2. Tài khoản không tồn tại:**
  1. Hệ thống không tìm thấy tài khoản tương ứng.
  2. Hệ thống thông báo "Tên đăng nhập hoặc mật khẩu không chính xác".
  3. Quay lại bước 3 của Basic Flow.

**Exception Flow:**

- **7.1. Tài khoản không ở trạng thái hoạt động:**
  1. Hệ thống xác định tài khoản đã bị khóa hoặc không còn hoạt động.
  2. Hệ thống thông báo tài khoản không được phép truy cập.
  3. Use Case kết thúc.

- **6.2. Không thể kết nối với cơ sở dữ liệu:**
  1. Hệ thống không thể kết nối với CSDL để xác thực tài khoản.
  2. Hệ thống thông báo hệ thống đang gặp sự cố.
  3. Use Case kết thúc.

- **9.1. Không thể tạo phiên đăng nhập:**
  1. Hệ thống xác thực thành công nhưng không thể tạo phiên đăng nhập.
  2. Hệ thống thông báo "Không thể đăng nhập, vui lòng thử lại sau".
  3. Use Case kết thúc.

---

## 7.2. Lập kế hoạch sản xuất – UC02

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR05** | Lập kế hoạch sản xuất | Cho phép Bộ phận lập KHSX tạo kế hoạch sản xuất dựa trên đơn hàng, nguyên liệu và năng lực sản xuất. |
| **FR06** | Kiểm tra tính khả thi kế hoạch | Hệ thống kiểm tra tính khả thi của kế hoạch dựa trên nguyên vật liệu, thời gian và năng lực sản xuất. |

### Đặc tả Use Case UC02 – Lập kế hoạch sản xuất

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC02 |
| **Tên** | Lập kế hoạch sản xuất |
| **Actor chính** | Bộ phận lập kế hoạch sản xuất |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép lập kế hoạch sản xuất dựa trên đơn hàng, tình trạng nguyên vật liệu và năng lực sản xuất. |
| **Tiền điều kiện** | Đăng nhập thành công và có quyền lập kế hoạch sản xuất. Thông tin đơn hàng, nhu cầu thị trường, năng lực sản xuất và tình trạng nguyên vật liệu đã có trên hệ thống. |
| **Hậu điều kiện** | Kế hoạch sản xuất được lưu vào CSDL với trạng thái "Chờ duyệt". |

**Basic Flow:**

| Bước | Bộ phận lập KHSX | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng lập kế hoạch sản xuất. | |
| 2 | | Hiển thị form lập kế hoạch gồm: danh sách đơn hàng đủ điều kiện, thông tin sản phẩm, số lượng yêu cầu, thời gian cần hoàn thành, tình trạng nguyên vật liệu, năng lực sản xuất. |
| 3 | Chọn đơn hàng cần lập kế hoạch. | |
| 4 | | Hiển thị thông tin chi tiết đơn hàng. |
| 5 | Nhập thông tin kế hoạch: nguyên liệu, số lượng, thời gian dự kiến. | |
| 6 | Chọn xưởng sản xuất và phân công sản phẩm, số lượng cho xưởng. | |
| 7 | Chọn "Kiểm tra". | |
| 8 | | Kiểm tra tính khả thi dựa trên nguyên vật liệu, thời gian và năng lực sản xuất. |
| 9 | | Hiển thị kết quả kiểm tra và cảnh báo nếu có. |
| 10 | Xem xét kết quả và chọn "Xác nhận". | |
| 11 | | Kiểm tra tính đầy đủ và hợp lệ của thông tin. |
| 12 | | Lưu kế hoạch sản xuất với trạng thái "Chờ duyệt". |
| 13 | | Thông báo lập kế hoạch thành công. |

**Alternative Flow:**

- **3.1. Không có đơn hàng phù hợp:** Hệ thống thông báo không có đơn hàng đủ điều kiện. Use Case kết thúc.
- **8.1. Số lượng nguyên vật liệu không đủ:** Hệ thống hiển thị danh sách nguyên liệu còn thiếu. Quay lại bước 5.
- **8.2. Năng lực sản xuất không đủ:** Hệ thống hiển thị thông tin năng lực không đáp ứng. Quay lại bước 5.
- **11.1. Thông tin kế hoạch không đầy đủ hoặc không hợp lệ:** Hệ thống thông báo các thông tin cần bổ sung. Quay lại bước 5.

**Exception Flow:**

- **5.1. Không thể hiển thị thông tin chi tiết đơn hàng:** Hệ thống thông báo lỗi. Quay lại bước 3.
- **6.1. Không thể lấy thông tin nguyên vật liệu hoặc năng lực sản xuất:** Hệ thống thông báo lỗi. Use Case kết thúc.
- **12.1. Không thể lưu kế hoạch sản xuất:** Hệ thống thông báo lỗi. Kế hoạch không được lưu.

---

## 7.3. Duyệt kế hoạch sản xuất – UC03

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR07** | Duyệt kế hoạch sản xuất | Cho phép Ban giám đốc phê duyệt, từ chối hoặc yêu cầu điều chỉnh kế hoạch sản xuất. |

### Đặc tả Use Case UC03 – Duyệt kế hoạch sản xuất

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC03 |
| **Tên** | Duyệt kế hoạch sản xuất |
| **Actor chính** | Ban giám đốc |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép Ban giám đốc phê duyệt hoặc từ chối kế hoạch sản xuất. |
| **Tiền điều kiện** | Đăng nhập thành công. Ban giám đốc có quyền duyệt kế hoạch. Kế hoạch sản xuất đang ở trạng thái "Chờ duyệt". |
| **Hậu điều kiện** | Nếu phê duyệt: trạng thái chuyển thành "Đã duyệt". Nếu từ chối: trạng thái chuyển thành "Từ chối". |

**Basic Flow:**

| Bước | Ban giám đốc | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng duyệt kế hoạch sản xuất. | |
| 2 | | Hiển thị danh sách kế hoạch ở trạng thái "Chờ duyệt". |
| 3 | Chọn kế hoạch cần duyệt. | |
| 4 | | Hiển thị form chi tiết kế hoạch. |
| 5 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 6 | | Hiển thị thông tin phục vụ đánh giá. |
| 7 | Chọn "Phê duyệt". | |
| 8 | | Chuyển trạng thái thành "Đã duyệt". |
| 9 | | Thông báo phê duyệt thành công. |

**Alternative Flow:**

- **7.1. Yêu cầu điều chỉnh:** Ban giám đốc nhập nội dung cần điều chỉnh. Hệ thống chuyển trạng thái thành "Yêu cầu điều chỉnh" và thông báo đến Bộ phận lập KHSX.
- **9.1. Từ chối kế hoạch:** Ban giám đốc nhập lý do từ chối. Hệ thống chuyển trạng thái thành "Từ chối".

**Exception Flow:**

- **2.1. Không có kế hoạch đang chờ duyệt:** Hệ thống thông báo. Use Case kết thúc.
- **4.1. Không thể hiển thị thông tin chi tiết:** Hệ thống thông báo lỗi. Quay lại bước 2.

---

## 7.4. Phân công xưởng sản xuất – UC04

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR08** | Phân công xưởng sản xuất | Cho phép Bộ phận lập KHSX phân công xưởng sản xuất cho kế hoạch đã duyệt. |
| **FR09** | Kiểm tra năng lực xưởng | Hệ thống kiểm tra năng lực và lịch sản xuất của xưởng được chọn. |

### Đặc tả Use Case UC04 – Phân công xưởng sản xuất

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC04 |
| **Tên** | Phân công xưởng sản xuất (Phát sinh lệnh sản xuất) |
| **Actor chính** | Bộ phận lập kế hoạch sản xuất |
| **Actor phụ** | Không |
| **Mục đích** | Phân công xưởng sản xuất cho kế hoạch đã được duyệt. |
| **Tiền điều kiện** | Đăng nhập thành công. Kế hoạch sản xuất đã duyệt và đang ở trạng thái "Chờ phân công". Thông tin xưởng sản xuất đã có trên hệ thống. |
| **Hậu điều kiện** | Thông tin phân công xưởng được lưu. Xưởng sản xuất nhận được thông tin phân công. |

**Basic Flow:**

| Bước | Bộ phận lập KHSX | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Phân công xưởng sản xuất. | |
| 2 | | Hiển thị danh sách kế hoạch ở trạng thái "Chờ phân công". |
| 3 | Chọn kế hoạch cần phân công. | |
| 4 | | Hiển thị thông tin chi tiết kế hoạch. |
| 5 | Chọn "Phân công xưởng". | |
| 6 | | Hiển thị danh sách xưởng sản xuất kèm năng lực và lịch sản xuất. |
| 7 | Chọn xưởng sản xuất phù hợp. | |
| 8 | Chọn "Kiểm tra". | |
| 9 | | Kiểm tra khả năng đáp ứng của xưởng. |
| 10 | | Hiển thị kết quả kiểm tra và cảnh báo nếu có. |
| 11 | Chọn "Xác nhận". | |
| 12 | | Lưu thông tin phân công và cập nhật kế hoạch. |
| 13 | | Gửi thông tin đến xưởng sản xuất. |
| 14 | | Thông báo phân công thành công. |

**Alternative Flow:**

- **9.1. Xưởng không đủ năng lực:** Hệ thống hiển thị thông tin năng lực còn thiếu. Quay lại bước 7.
- **9.2. Lịch sản xuất không phù hợp:** Hệ thống thông báo thời gian phân công không phù hợp. Quay lại bước 7.
- **11.1. Hủy phân công:** Bộ phận lập KHSX xác nhận hủy. Use Case kết thúc.

**Exception Flow:**

- **2.1. Không có kế hoạch chờ phân công:** Hệ thống thông báo. Use Case kết thúc.
- **4.1. Không thể hiển thị thông tin chi tiết:** Hệ thống thông báo lỗi. Quay lại bước 2.
- **6.1. Không thể lấy thông tin xưởng:** Hệ thống thông báo lỗi. Use Case kết thúc.
- **13.1. Không thể lưu thông tin phân công:** Hệ thống thông báo lỗi. Use Case kết thúc.
- **14.1. Không thể gửi thông tin đến xưởng:** Hệ thống thông báo lỗi. Thông tin phân công vẫn được lưu.

---

## 7.5. Thống kê báo cáo & Cảnh báo kho – UC05

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR10** | Báo cáo tồn kho | Hệ thống tổng hợp và hiển thị báo cáo tồn kho theo điều kiện lọc. |
| **FR11** | Báo cáo nhập/xuất kho | Hệ thống tổng hợp dữ liệu nhập/xuất kho theo khoảng thời gian. |
| **FR12** | Báo cáo hiệu suất lưu kho | Hệ thống tổng hợp tình hình sử dụng kho và hiệu suất lưu kho. |
| **FR13** | Cảnh báo kho | Hệ thống cảnh báo tồn kho thấp, tồn kho cao, hàng/lô sắp hết hạn sử dụng. |

### Đặc tả Use Case UC05 – Thống kê báo cáo & Cảnh báo kho

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC05 |
| **Tên** | Thống kê báo cáo và cảnh báo kho |
| **Actor chính** | Bộ phận quản lý kho; Ban giám đốc |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép theo dõi báo cáo tồn kho, nhập/xuất, hiệu suất lưu kho và cảnh báo kho. |
| **Tiền điều kiện** | Đăng nhập thành công. Có quyền truy cập chức năng. Dữ liệu tồn kho, nhập/xuất đã được cập nhật. |
| **Hậu điều kiện** | Người dùng xem được báo cáo và cảnh báo. Không thay đổi dữ liệu kho. |

**Basic Flow:**

| Bước | Người dùng | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng "Thống kê báo cáo và cảnh báo kho". | |
| 2 | | Hiển thị giao diện thống kê gồm: báo cáo tồn kho, nhập/xuất, hiệu suất lưu kho và cảnh báo kho. |
| 3 | Chọn loại báo cáo hoặc cảnh báo. | |
| 4 | Chọn khoảng thời gian và điều kiện lọc. | |
| 5 | | Kiểm tra tính hợp lệ và tổng hợp dữ liệu. |
| 6 | | Hiển thị báo cáo hoặc danh sách cảnh báo. |
| 7 | | Hiển thị thông tin chi tiết liên quan. |
| 8 | Chọn kết thúc. | |
| 9 | | Kết thúc Use Case. |

**Alternative Flow:**

- **3.1. Chọn báo cáo tồn kho:** Hiển thị báo cáo tồn kho các mặt hàng.
- **3.2. Chọn báo cáo nhập/xuất kho:** Hiển thị thông tin nhập/xuất theo khoảng thời gian.
- **3.3. Chọn báo cáo hiệu suất lưu kho:** Hiển thị báo cáo hiệu suất lưu kho.
- **3.4. Chọn cảnh báo kho:** Hiển thị cảnh báo tồn kho thấp, cao hoặc hàng/lô sắp hết hạn.
- **5.1. Thay đổi điều kiện lọc:** Hệ thống cập nhật lại dữ liệu theo điều kiện mới.

**Exception Flow:**

- **6.1. Không có dữ liệu phù hợp:** Hệ thống thông báo không có dữ liệu. Quay lại bước 5.
- **7.1. Không thể tổng hợp hoặc hiển thị báo cáo:** Hệ thống thông báo lỗi. Quay lại bước 5.
- **9.1. Không thể hiển thị thông tin chi tiết:** Hệ thống thông báo lỗi. Quay lại bước 6.

---

## 7.6. Đặt đơn hàng – UC02 (Khách hàng)

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR14** | Đặt đơn hàng | Cho phép khách hàng chọn sản phẩm, nhập thông tin nhận hàng và tạo đơn hàng. |

### Đặc tả Use Case – Đặt đơn hàng

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC-DH |
| **Tên** | Đặt đơn hàng |
| **Actor chính** | Khách hàng |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép khách hàng đặt đơn hàng thành phẩm. |
| **Tiền điều kiện** | Khách hàng đã đăng nhập. Danh mục thành phẩm đã tồn tại. |
| **Hậu điều kiện** | Thành công: Đơn hàng được tạo với trạng thái "Mới / Chờ xử lý". Thất bại: Không có đơn hàng nào được tạo. |

**Basic Flow:**

| Bước | Khách hàng | Hệ thống |
|---|---|---|
| 1 | Chọn "Đặt đơn hàng". | |
| 2 | | Hiển thị danh mục thành phẩm hiện có. |
| 3 | Chọn sản phẩm và nhập số lượng. | |
| 4 | | Kiểm tra sản phẩm đang kinh doanh; hiển thị tạm tính. |
| 5 | Nhập thông tin nhận hàng: địa chỉ, người nhận, SĐT, ngày mong muốn. | |
| 6 | | Kiểm tra định dạng và tính đầy đủ. |
| 7 | Xác nhận đặt hàng. | |
| 8 | | Kiểm tra tính hợp lệ toàn bộ đơn hàng. |
| 9 | | Sinh mã đơn hàng, lưu với trạng thái "Mới / Chờ xử lý". |
| 10 | | Đưa vào danh sách chờ xử lý cho Bộ phận lập KHSX. |
| 11 | | Hiển thị xác nhận thành công kèm mã đơn hàng. |

**Alternative Flow:**

- **7.1. Khách hàng hủy đặt hàng:** Hệ thống không lưu đơn hàng. Use Case kết thúc.

**Exception Flow:**

- **4.1. Sản phẩm không còn kinh doanh:** Hệ thống thông báo lỗi. Quay lại bước 3.
- **8.1. Số lượng đặt bằng 0 hoặc âm:** Hệ thống thông báo lỗi. Quay lại bước 3.
- **8.2. Thông tin nhận hàng thiếu trường bắt buộc:** Hệ thống thông báo lỗi. Quay lại bước 5.

---

## 7.7. Lập đơn mua nguyên liệu – UC06

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR15** | Lập đơn mua nguyên liệu | Cho phép Bộ phận mua hàng lập đơn mua nguyên liệu với nhà cung cấp. |

### Đặc tả Use Case UC06 – Lập đơn mua nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC06 |
| **Tên** | Lập đơn mua nguyên liệu |
| **Actor chính** | Bộ phận mua hàng |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép lập đơn mua nguyên liệu từ nhà cung cấp. |
| **Tiền điều kiện** | Đăng nhập thành công. |
| **Hậu điều kiện** | Đơn mua được lưu vào CSDL với trạng thái "Chờ phê duyệt". |

**Basic Flow:**

| Bước | Bộ phận mua hàng | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng lập đơn mua nguyên liệu. | |
| 2 | | Hiển thị trang lập đơn mua. |
| 3 | Chọn nguyên liệu cần mua. | |
| 4 | | Hiển thị thông tin nguyên liệu và tồn kho hiện tại. |
| 5 | Nhập số lượng cần mua. | |
| 6 | | Kiểm tra số lượng nhập. |
| 7 | Chọn nhà cung cấp. | |
| 8 | | Hiển thị thông tin nhà cung cấp. |
| 9 | Nhập đơn giá dự kiến và thông tin cần thiết. | |
| 10 | | Kiểm tra dữ liệu nhập. |
| 11 | Xác nhận lập đơn mua. | |
| 12 | | Lưu thông tin đơn mua vào CSDL. |
| 13 | | Cập nhật trạng thái "Chờ phê duyệt". |
| 14 | | Thông báo lập đơn mua thành công. |

**Alternative Flow:**

- **5.1. Số lượng không phù hợp:** Hệ thống thông báo và yêu cầu nhập lại. Quay lại bước 5.
- **7.1. Không tìm thấy NCC phù hợp:** Hệ thống thông báo. Quay lại bước 7.
- **10.1. Thông tin không hợp lệ:** Hệ thống thông báo lỗi. Quay lại bước 9.

**Exception Flow:**

- **12.1. Không thể lưu đơn mua:** Hệ thống thông báo lỗi. Use Case kết thúc.

---

## 7.8. Duyệt đơn mua nguyên liệu – UC07

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR16** | Duyệt đơn mua nguyên liệu | Cho phép Ban giám đốc phê duyệt hoặc từ chối đơn mua nguyên liệu. |

### Đặc tả Use Case UC07 – Duyệt đơn mua nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC07 |
| **Tên** | Duyệt đơn mua nguyên liệu |
| **Actor chính** | Ban giám đốc |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép Ban giám đốc phê duyệt hoặc từ chối đơn mua nguyên liệu. |
| **Tiền điều kiện** | Đăng nhập thành công. Có đơn mua ở trạng thái "Chờ phê duyệt". |
| **Hậu điều kiện** | Đơn mua chuyển trạng thái "Đã phê duyệt" hoặc "Từ chối". |

**Basic Flow:**

| Bước | Ban giám đốc | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng duyệt đơn mua. | |
| 2 | | Hiển thị danh sách đơn mua đang chờ phê duyệt. |
| 3 | Chọn đơn mua cần xem xét. | |
| 4 | | Hiển thị thông tin chi tiết đơn mua. |
| 5 | Kiểm tra thông tin nguyên liệu, số lượng và NCC. | |
| 6 | Chọn phê duyệt. | |
| 7 | | Cập nhật trạng thái thành "Đã phê duyệt". |

**Alternative Flow:**

- **6.1. Từ chối đơn mua:** Ban giám đốc nhập lý do từ chối. Hệ thống cập nhật trạng thái thành "Từ chối".
- **3.1. Không có đơn mua cần phê duyệt:** Hệ thống thông báo. Use Case kết thúc.

**Exception Flow:**

- **8.1. Hủy thao tác:** Ban giám đốc chọn hủy. Hệ thống quay lại danh sách đơn mua.

---

## 7.9. Nhận nguyên liệu từ nhà cung cấp – UC08

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR17** | Nhận nguyên liệu từ NCC | Cho phép nhân viên kho tiếp nhận nguyên liệu, kiểm tra chứng từ và ghi nhận số lượng thực nhận. |

### Đặc tả Use Case UC08 – Nhận nguyên liệu từ nhà cung cấp

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC08 |
| **Tên** | Nhận nguyên liệu từ nhà cung cấp |
| **Actor chính** | Nhân viên kho |
| **Actor phụ** | Không |
| **Mục đích** | Tiếp nhận nguyên liệu từ NCC theo đơn mua đã phê duyệt. |
| **Tiền điều kiện** | Đăng nhập thành công. Có đơn mua đã phê duyệt và NCC giao nguyên liệu đến kho. |
| **Hậu điều kiện** | Thông tin thực nhận được lưu. Đơn mua chuyển trạng thái "Đã tiếp nhận". Nguyên liệu chuyển trạng thái "Chờ kiểm tra chất lượng". |

**Basic Flow:**

| Bước | Nhân viên kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Nhận nguyên liệu. | |
| 2 | | Hiển thị danh sách đơn mua đã phê duyệt. |
| 3 | Chọn đơn mua tương ứng. | |
| 4 | | Hiển thị thông tin đơn mua và danh sách nguyên liệu cần nhận. |
| 5 | Kiểm tra chứng từ giao hàng và thông tin NCC. | |
| 6 | | Kiểm tra tính hợp lệ của chứng từ. |
| 7 | Ghi nhận số lượng thực tế nhận được. | |
| 8 | | Kiểm tra số lượng thực tế. |
| 9 | Xác nhận tiếp nhận. | |
| 10 | | Lưu thông tin thực nhận vào CSDL. |
| 11 | | Cập nhật trạng thái đơn mua thành "Đã tiếp nhận". |
| 12 | | Cập nhật trạng thái nguyên liệu thành "Chờ kiểm tra chất lượng". |
| 13 | | Thông báo tiếp nhận thành công. |

**Alternative Flow:**

- **3.1. Không tìm thấy đơn mua:** Hệ thống thông báo. Quay lại bước 3.
- **5.1. Chứng từ không hợp lệ:** Nhân viên kho kiểm tra lại với NCC.
- **8.1. Số lượng thực tế không khớp:** Ghi nhận số lượng thực tế và lý do chênh lệch. Quay lại bước 9.
- **9.1. Từ chối tiếp nhận:** Nhân viên kho nhập lý do. Hệ thống không cập nhật trạng thái.

**Exception Flow:**

- **10.1. Không thể lưu thông tin:** Hệ thống thông báo lỗi. Use Case kết thúc.

---

## 7.10. Kiểm tra chất lượng nguyên liệu – UC09

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR18** | Kiểm tra chất lượng nguyên liệu | Cho phép Bộ phận QC kiểm tra chất lượng nguyên liệu theo tiêu chuẩn quy định. |

### Đặc tả Use Case UC09 – Kiểm tra chất lượng nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC09 |
| **Tên** | Kiểm tra chất lượng nguyên liệu |
| **Actor chính** | Bộ phận QC |
| **Actor phụ** | Không |
| **Mục đích** | Kiểm tra chất lượng nguyên liệu sau tiếp nhận. |
| **Tiền điều kiện** | Đăng nhập thành công. Có nguyên liệu ở trạng thái "Chờ kiểm tra chất lượng". |
| **Hậu điều kiện** | Kết quả kiểm tra được lưu. Nguyên liệu chuyển trạng thái "Đạt chất lượng" hoặc "Không đạt chất lượng". |

**Basic Flow:**

| Bước | Bộ phận QC | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng kiểm tra chất lượng. | |
| 2 | | Hiển thị danh sách lô nguyên liệu chờ kiểm tra. |
| 3 | Chọn lô nguyên liệu cần kiểm tra. | |
| 4 | | Hiển thị thông tin chi tiết lô nguyên liệu. |
| 5 | Thực hiện kiểm tra theo tiêu chuẩn quy định. | |
| 6 | Nhập kết quả kiểm tra. | |
| 7 | | Kiểm tra dữ liệu kết quả. |
| 8 | Xác nhận kết quả kiểm tra. | |
| 9 | | Lưu kết quả vào CSDL. |
| 10 | | Cập nhật trạng thái thành "Đạt chất lượng". |
| 11 | | Thông báo kiểm tra thành công. |
| 12 | | Chuyển lô nguyên liệu đạt sang quy trình nhập kho. |

**Alternative Flow:**

- **8.1. Nguyên liệu không đạt:** Bộ phận QC nhập lý do. Hệ thống cập nhật trạng thái thành "Không đạt chất lượng".
- **6.1. Thiếu thông tin kết quả:** Hệ thống thông báo yêu cầu bổ sung. Quay lại bước 6.

**Exception Flow:**

- **5.1. Không thể thực hiện kiểm tra:** Bộ phận QC ghi nhận nguyên nhân. Hệ thống lưu ở trạng thái "Chờ xử lý".

---

## 7.11. Nhập kho nguyên liệu – UC10

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR19** | Nhập kho nguyên liệu | Cho phép nhân viên kho nhập kho nguyên liệu đã đạt chất lượng, tạo phiếu nhập kho và cập nhật tồn kho. |

### Đặc tả Use Case UC10 – Nhập kho nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC10 |
| **Tên** | Nhập kho nguyên liệu |
| **Actor chính** | Nhân viên kho |
| **Actor phụ** | Không |
| **Mục đích** | Nhập kho nguyên liệu đạt chất lượng, cập nhật tồn kho. |
| **Tiền điều kiện** | Đăng nhập thành công. Thông tin tiếp nhận và kết quả kiểm tra chất lượng đã được ghi nhận. |
| **Hậu điều kiện** | Phiếu nhập kho được tạo. Số lượng tồn kho, lô nguyên liệu và vị trí lưu kho được cập nhật. |

**Basic Flow:**

| Bước | Nhân viên kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng "Nhập kho nguyên liệu". | |
| 2 | | Hiển thị danh sách nguyên liệu đủ điều kiện nhập kho. |
| 3 | Chọn nguyên liệu cần nhập kho. | |
| 4 | | Hiển thị thông tin nguyên liệu và kết quả kiểm tra chất lượng. |
| 5 | Nhập/chọn số lượng, lô nguyên liệu và vị trí lưu kho. | |
| 6 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 7 | Xác nhận nhập kho. | |
| 8 | | Tạo phiếu nhập kho nguyên liệu. |
| 9 | | Cập nhật tồn kho, thông tin lô và vị trí. |
| 10 | | Thông báo nhập kho thành công. |

**Alternative Flow:** Không có.

**Exception Flow:**

- **2.1. Không có nguyên liệu đủ điều kiện:** Hệ thống thông báo. Use Case kết thúc.
- **6.1. Thông tin nhập kho không hợp lệ:** Hệ thống thông báo các thông tin cần bổ sung. Quay lại bước 6.

---

## 7.12. Lập phiếu yêu cầu xuất kho nguyên liệu – UC11

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR20** | Lập phiếu yêu cầu xuất kho NL | Cho phép Xưởng sản xuất lập phiếu yêu cầu xuất kho nguyên liệu theo lệnh sản xuất. |

### Đặc tả Use Case UC11 – Lập phiếu yêu cầu xuất kho nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC11 |
| **Tên** | Lập phiếu yêu cầu xuất kho nguyên liệu |
| **Actor chính** | Xưởng sản xuất |
| **Actor phụ** | Không |
| **Mục đích** | Lập phiếu yêu cầu xuất kho nguyên liệu cho sản xuất. |
| **Tiền điều kiện** | Đăng nhập thành công và có quyền lập phiếu. |
| **Hậu điều kiện** | Phiếu yêu cầu được tạo và chuyển đến nhân viên kho xử lý. |

**Basic Flow:**

| Bước | Xưởng sản xuất | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng lập phiếu yêu cầu xuất kho NL. | |
| 2 | | Hiển thị danh sách lệnh sản xuất đang hoạt động. |
| 3 | Chọn lệnh sản xuất cần cấp nguyên liệu. | |
| 4 | | Hiển thị danh sách nguyên liệu và số lượng cần thiết. |
| 5 | Nhập/xác nhận số lượng nguyên liệu cần xuất. | |
| 6 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 7 | Xác nhận lập phiếu. | |
| 8 | | Tạo phiếu yêu cầu xuất kho nguyên liệu. |
| 9 | | Chuyển phiếu đến nhân viên kho. |
| 10 | | Thông báo lập phiếu thành công. |

**Alternative Flow:**

- **5.1. Điều chỉnh số lượng:** Xưởng sản xuất điều chỉnh số lượng khác với hiển thị. Quay lại bước 6.

**Exception Flow:**

- **2.1. Không có lệnh sản xuất cần cấp nguyên liệu:** Hệ thống thông báo. Use Case kết thúc.
- **6.1. Thông tin phiếu không đầy đủ hoặc không hợp lệ:** Hệ thống thông báo. Quay lại bước 6.

---

## 7.13. Xuất kho nguyên liệu – UC12

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR21** | Xuất kho nguyên liệu | Cho phép nhân viên kho xuất kho nguyên liệu theo phiếu yêu cầu và nguyên tắc FEFO. |

### Đặc tả Use Case UC12 – Xuất kho nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC12 |
| **Tên** | Xuất kho nguyên liệu |
| **Actor chính** | Nhân viên kho |
| **Actor phụ** | Không |
| **Mục đích** | Xuất kho nguyên liệu cho sản xuất theo FEFO. |
| **Tiền điều kiện** | Đăng nhập thành công. Có phiếu yêu cầu xuất kho đang chờ xử lý. |
| **Hậu điều kiện** | Phiếu xuất kho được tạo. Nguyên liệu được xuất kho. Tồn kho và lô nguyên liệu được cập nhật. |

**Basic Flow:**

| Bước | Nhân viên kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng "Xuất kho nguyên liệu". | |
| 2 | | Hiển thị danh sách phiếu yêu cầu đang chờ xử lý. |
| 3 | Chọn phiếu yêu cầu cần xử lý. | |
| 4 | | Hiển thị thông tin nguyên liệu và số lượng cần xuất. |
| 5 | | Kiểm tra tính hợp lệ của phiếu yêu cầu. |
| 6 | | Kiểm tra số lượng tồn kho. |
| 7 | | Hiển thị/gợi ý các lô theo nguyên tắc FEFO. |
| 8 | Chọn lô nguyên liệu để xuất. | |
| 9 | | Kiểm tra số lượng và tính hợp lệ của lô được chọn. |
| 10 | Xác nhận xuất kho. | |
| 11 | | Tạo phiếu xuất kho nguyên liệu. |
| 12 | | Cập nhật tồn kho và số lượng còn lại của từng lô. |
| 13 | | Thông báo xuất kho thành công. |

**Alternative Flow:**

- **9.1. Một lô không đủ số lượng:** Hệ thống hiển thị lô tiếp theo theo FEFO. Nhân viên kho chọn thêm lô. Quay lại bước 9.

**Exception Flow:**

- **2.1. Không có phiếu yêu cầu đang chờ:** Hệ thống thông báo. Use Case kết thúc.
- **5.1. Phiếu yêu cầu không hợp lệ:** Hệ thống thông báo. Quay lại bước 2.
- **6.1. Không đủ nguyên liệu trong kho:** Hệ thống thông báo. Use Case kết thúc.
- **7.1. Không có lô phù hợp theo FEFO:** Hệ thống thông báo. Use Case kết thúc.

---

## 7.14. Lập phiếu yêu cầu nhập kho thành phẩm – UC13

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR22** | Lập phiếu yêu cầu nhập kho TP | Cho phép Xưởng sản xuất lập phiếu yêu cầu nhập kho thành phẩm sau sản xuất. |

### Đặc tả Use Case UC13 – Lập phiếu yêu cầu nhập kho thành phẩm

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC13 |
| **Tên** | Lập phiếu yêu cầu nhập kho thành phẩm |
| **Actor chính** | Xưởng sản xuất |
| **Actor phụ** | Không |
| **Mục đích** | Lập phiếu yêu cầu nhập kho thành phẩm hoàn thành sản xuất. |
| **Tiền điều kiện** | Đăng nhập thành công. Thông tin lệnh sản xuất đã ghi nhận trên hệ thống. |
| **Hậu điều kiện** | Phiếu yêu cầu được tạo và gửi đến nhân viên kho xử lý. |

**Basic Flow:**

| Bước | Xưởng sản xuất | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng "Lập phiếu yêu cầu nhập kho thành phẩm". | |
| 2 | | Hiển thị danh sách lệnh sản xuất đã hoàn thành. |
| 3 | Chọn lệnh sản xuất cần nhập kho thành phẩm. | |
| 4 | | Hiển thị thông tin lệnh sản xuất và lô sản xuất. |
| 5 | Nhập/xác nhận thông tin thành phẩm và số lượng. | |
| 6 | Nhập ngày sản xuất và hạn sử dụng (nếu có). | |
| 7 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 8 | Xác nhận lập phiếu. | |
| 9 | | Tạo phiếu yêu cầu nhập kho thành phẩm. |
| 10 | | Gửi yêu cầu đến nhân viên kho. |
| 11 | | Thông báo lập phiếu thành công. |

**Alternative Flow:**

- **6.1. Thành phẩm không quản lý hạn sử dụng:** Không cần nhập hạn sử dụng. Quay lại bước 7.

**Exception Flow:**

- **2.1. Không có lệnh sản xuất đã hoàn thành:** Hệ thống thông báo. Use Case kết thúc.
- **7.1. Thông tin chưa đầy đủ hoặc không hợp lệ:** Hệ thống thông báo. Quay lại bước 7.

---

## 7.15. Nhập kho thành phẩm – UC14

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR23** | Nhập kho thành phẩm | Cho phép nhân viên kho nhập kho thành phẩm, tạo phiếu nhập kho và cập nhật tồn kho. |

### Đặc tả Use Case UC14 – Nhập kho thành phẩm

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC14 |
| **Tên** | Nhập kho thành phẩm |
| **Actor chính** | Nhân viên kho |
| **Actor phụ** | Không |
| **Mục đích** | Nhập kho thành phẩm sau sản xuất. |
| **Tiền điều kiện** | Thành phẩm đã hoàn thành sản xuất. Thông tin thành phẩm đã tồn tại trên hệ thống. Nhân viên kho đã đăng nhập. |
| **Hậu điều kiện** | Phiếu nhập kho được tạo. Tồn kho, lô sản xuất và vị trí lưu trữ được cập nhật. |

**Basic Flow:**

| Bước | Nhân viên kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Nhập kho thành phẩm. | |
| 2 | | Hiển thị giao diện nhập kho thành phẩm. |
| 3 | Chọn thành phẩm, nhập số lượng, lô sản xuất, hạn sử dụng (nếu có). | |
| 4 | | Hiển thị thông tin thành phẩm và kiểm tra tính đầy đủ, hợp lệ. |
| 5 | Chọn vị trí lưu trữ phù hợp. | |
| 6 | | Kiểm tra vị trí lưu trữ và khả năng tiếp nhận. |
| 7 | Xác nhận nhập kho. | |
| 8 | | Tạo phiếu nhập kho và cập nhật tồn kho. |
| 9 | | Ghi nhận thông tin lô, vị trí và thông báo thành công. |

**Alternative Flow:** Không có.

**Exception Flow:**

- **3.1. Thông tin sản xuất không hợp lệ:** Hệ thống thông báo. Nhân viên kho liên hệ bộ phận liên quan.
- **3.2. Số lượng nhập kho không hợp lệ:** Hệ thống thông báo lỗi. Nhân viên kho kiểm tra và chỉnh sửa.
- **5.1. Thông tin thành phẩm thiếu hoặc sai:** Hệ thống thông báo cần bổ sung/chỉnh sửa.
- **7.1. Vị trí lưu trữ không phù hợp:** Hệ thống thông báo. Nhân viên kho chọn vị trí khác.
- **8.1. Lỗi khi nhập kho:** Hệ thống thông báo lỗi. Phiếu nhập kho không được tạo.

---

## 7.16. Xuất kho thành phẩm giao hàng – UC15

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR24** | Xuất kho thành phẩm giao hàng | Cho phép nhân viên kho xuất kho thành phẩm theo đơn hàng, gợi ý lô theo FIFO/FEFO. |

### Đặc tả Use Case UC15 – Xuất kho thành phẩm giao hàng

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC15 |
| **Tên** | Xuất kho thành phẩm giao hàng |
| **Actor chính** | Nhân viên kho |
| **Actor phụ** | Không |
| **Mục đích** | Xuất kho thành phẩm giao hàng cho đơn hàng khách hàng. |
| **Tiền điều kiện** | Có đơn hàng hoặc yêu cầu giao hàng hợp lệ. Thành phẩm đã nhập kho đủ số lượng. |
| **Hậu điều kiện** | Thành công: Phiếu xuất kho được lập; tồn kho được trừ; đơn hàng chuyển trạng thái "Đã xuất / Đang giao". Thất bại: Không lập được phiếu xuất kho. |

**Basic Flow:**

| Bước | Nhân viên kho | Hệ thống |
|---|---|---|
| 1 | Tiếp nhận yêu cầu xuất kho thành phẩm gắn với đơn hàng. | |
| 2 | | Kiểm tra yêu cầu hợp lệ (đơn hàng tồn tại, chưa xuất kho). |
| 3 | | Hiển thị thông tin đơn hàng: sản phẩm, số lượng, thông tin nhận hàng. |
| 4 | Kiểm tra tồn kho thành phẩm khả dụng. | |
| 5 | | Hiển thị số lượng tồn theo lô; gợi ý lô ưu tiên theo FIFO/FEFO. |
| 6 | Chọn lô thành phẩm và xác nhận số lượng xuất. | |
| 7 | | Kiểm tra số lượng xuất không vượt quá tồn kho khả dụng. |
| 8 | Lập phiếu xuất kho thành phẩm. | |
| 9 | | Sinh mã phiếu xuất kho, lưu phiếu. |
| 10 | Xác nhận hoàn tất xuất kho. | |
| 11 | | Trừ tồn kho theo lô; cập nhật trạng thái đơn hàng thành "Đã xuất / Đang giao". |
| 12 | | Hiển thị/in phiếu xuất kho. |

**Alternative Flow:**

- **6.1. Chọn lô khác với gợi ý:** Hệ thống kiểm tra lô được chọn còn hạn sử dụng và đủ số lượng. Quay lại bước 7.

**Exception Flow:**

- **2.1. Đơn hàng không tồn tại hoặc đã xuất kho:** Hệ thống từ chối yêu cầu. Use Case kết thúc.
- **4.1. Tồn kho không đủ:** Hệ thống cảnh báo thiếu hàng. Use Case kết thúc.
- **6.2. Lô đã hết hạn sử dụng:** Hệ thống cảnh báo và không cho chọn lô này. Quay lại bước 6.
- **7.1. Số lượng xuất vượt quá tồn kho:** Hệ thống cảnh báo. Quay lại bước 6.

---

## 7.17. Điều phối nhập kho – UC16

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR25** | Điều phối nhập kho | Cho phép Bộ phận quản lý kho xác định vị trí lưu trữ cho lô hàng nhập kho. |

### Đặc tả Use Case UC16 – Điều phối nhập kho

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC16 |
| **Tên** | Điều phối nhập kho |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Xác định kho và vị trí lưu trữ cho lô hàng nhập kho. |
| **Tiền điều kiện** | Có lô hàng đã xác nhận đủ điều kiện nhập kho và đang chờ điều phối. |
| **Hậu điều kiện** | Thành công: Vị trí lưu trữ được xác định; thông tin chuyển cho nhân viên kho lập phiếu nhập. Thất bại: Chưa xác định được vị trí. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn lô hàng cần điều phối từ danh sách chờ. | |
| 2 | | Xác định kho tương ứng với loại hàng; hiển thị thông tin lô hàng. |
| 3 | | Áp dụng quy tắc sắp xếp, hiển thị danh sách khu vực/vị trí còn trống. |
| 4 | Chọn khu vực/vị trí cụ thể. | |
| 5 | | Ghi nhận vị trí điều phối. |
| 6 | Xác nhận điều phối nhập kho. | |
| 7 | | Chuyển thông tin điều phối cho nhân viên kho lập phiếu nhập. |

**Alternative Flow:**

- **3.1. Không có vị trí đủ sức chứa:** Hệ thống cảnh báo. Bộ phận quản lý kho chọn vị trí tạm. Quay lại bước 4.

**Exception Flow:**

- **2.1. Loại hàng không xác định được kho tương ứng:** Hệ thống cảnh báo. Lô hàng được đánh dấu chờ xử lý thủ công. Use Case kết thúc.

---

## 7.18. Kiểm tra hàng trả về – UC17

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR26** | Kiểm tra hàng trả về | Cho phép Bộ phận QC kiểm tra chất lượng hàng trả về từ khách hàng. |

### Đặc tả Use Case UC17 – Kiểm tra hàng trả về

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC17 |
| **Tên** | Kiểm tra hàng trả về |
| **Actor chính** | Bộ phận QC |
| **Actor phụ** | Không |
| **Mục đích** | Kiểm tra tình trạng và chất lượng hàng trả về. |
| **Tiền điều kiện** | Có yêu cầu trả hàng ở trạng thái "Chờ kiểm tra". Hàng đã chuyển đến kho. |
| **Hậu điều kiện** | Thành công: Kết quả kiểm tra (đạt/không đạt) được ghi nhận. Thất bại: Yêu cầu trả hàng vẫn ở trạng thái "Chờ kiểm tra". |

**Basic Flow:**

| Bước | Bộ phận QC | Hệ thống |
|---|---|---|
| 1 | Nhận danh sách yêu cầu trả hàng chờ kiểm tra. | |
| 2 | | Hiển thị thông tin: sản phẩm, số lượng, lý do trả. |
| 3 | Đối chiếu số lượng thực tế. | |
| 4 | | Ghi nhận số lượng thực tế. |
| 5 | Kiểm tra tình trạng và chất lượng hàng. | |
| 6 | | Cho phép ghi nhận kết quả theo từng tiêu chí. |
| 7 | Xác định kết luận: Đạt hoặc Không đạt. | |
| 8 | | Cập nhật trạng thái yêu cầu trả hàng. |
| 9 | | Nếu Đạt: chuyển cho nhân viên kho nhập kho hàng trả về. Nếu Không đạt: chuyển cho Bộ phận quản lý kho xử lý hàng lỗi. |

**Alternative Flow:**

- **3.1. Số lượng thực tế không khớp:** Bộ phận QC ghi nhận sai lệch và đối chiếu lại. Quay lại bước 5.

**Exception Flow:**

- **1.1. Không xác định được nguồn gốc lô/đơn hàng:** Hệ thống cảnh báo yêu cầu xác minh. Use Case kết thúc.

---

## 7.19. Nhập kho hàng trả về – UC18

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR27** | Nhập kho hàng trả về | Cho phép nhân viên kho nhập kho hàng trả về đã đạt chất lượng. |

### Đặc tả Use Case UC18 – Nhập kho hàng trả về

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC18 |
| **Tên** | Nhập kho hàng trả về |
| **Actor chính** | Nhân viên kho |
| **Actor phụ** | Bộ phận QC |
| **Mục đích** | Nhập kho hàng trả về đã đạt chất lượng. |
| **Tiền điều kiện** | Hàng trả về đã kiểm tra và đủ điều kiện nhập lại kho. Nhân viên kho đã đăng nhập. |
| **Hậu điều kiện** | Phiếu nhập kho hàng trả về được tạo. Hàng được ghi nhận vào kho và tồn kho được cập nhật. |

**Basic Flow:**

| Bước | Nhân viên kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Nhập kho hàng trả về. | |
| 2 | | Hiển thị danh sách hàng trả về đủ điều kiện nhập kho. |
| 3 | Chọn hàng cần nhập kho. | |
| 4 | | Hiển thị thông tin sản phẩm, số lượng, lô hàng, kết quả kiểm tra. |
| 5 | Kiểm tra lại số lượng và thông tin. | |
| 6 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 7 | Chọn vị trí lưu trữ và xác nhận nhập kho. | |
| 8 | | Tạo phiếu nhập kho hàng trả về. |
| 9 | | Cập nhật tồn kho và vị trí lưu trữ. |
| 10 | | Thông báo nhập kho thành công. |

**Alternative Flow:**

- **7.1. Không có vị trí phù hợp:** Nhân viên kho chọn vị trí khác. Quay lại bước 7.

**Exception Flow:**

- **6.1. Thông tin hàng trả về thiếu hoặc sai:** Nhân viên kho bổ sung/chỉnh sửa. Quay lại bước 5.
- **8.1. Lỗi khi nhập kho:** Hệ thống thông báo. Phiếu không được tạo. Use Case kết thúc.

---

## 7.20. Xử lý hàng lỗi và hàng trả về – UC19

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR28** | Xử lý hàng lỗi và hàng trả về | Cho phép Bộ phận quản lý kho phân loại và xử lý hàng lỗi/hàng trả về không đạt. |

### Đặc tả Use Case UC19 – Xử lý hàng lỗi và hàng trả về

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC19 |
| **Tên** | Xử lý hàng lỗi và hàng trả về |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Bộ phận QC |
| **Mục đích** | Phân loại và xử lý hàng lỗi/hàng trả về không đủ điều kiện nhập lại kho. |
| **Tiền điều kiện** | Có hàng lỗi hoặc hàng trả về không đạt. Bộ phận quản lý kho đã đăng nhập. |
| **Hậu điều kiện** | Hàng được phân loại. Phương án xử lý được ghi nhận. Trạng thái xử lý được cập nhật. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Xử lý hàng lỗi và hàng trả về. | |
| 2 | | Hiển thị danh sách hàng lỗi/hàng trả về cần xử lý. |
| 3 | Chọn hàng/lô cần xử lý. | |
| 4 | | Hiển thị thông tin hàng, số lượng, lô và tình trạng. |
| 5 | Kiểm tra và phân loại hàng. | |
| 6 | | Ghi nhận thông tin phân loại. |
| 7 | Lựa chọn phương án xử lý phù hợp. | |
| 8 | | Hiển thị phương án và yêu cầu xác nhận. |
| 9 | Xác nhận phương án xử lý. | |
| 10 | | Cập nhật trạng thái hàng và lưu lịch sử xử lý. |
| 11 | | Thông báo xử lý thành công. |

**Alternative Flow:**

- **7.1. Chọn phương án khác:** Người dùng lựa chọn phương án xử lý khác. Quay lại bước 9.

**Exception Flow:**

- **2.1. Không có hàng cần xử lý:** Hệ thống thông báo. Use Case kết thúc.
- **4.1. Không xác định được tình trạng hàng:** Hệ thống thông báo chưa đủ thông tin. Use Case tạm dừng.
- **10.1. Lỗi khi cập nhật:** Hệ thống thông báo. Thông tin xử lý chưa được ghi nhận. Quay về bước 3.

---

## 7.21. Quản lý dữ liệu kho – UC20

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR29** | Quản lý dữ liệu kho | Cho phép Bộ phận quản lý kho thêm, cập nhật, xóa dữ liệu kho (nguyên liệu, thành phẩm, lô, vị trí lưu kho). |

### Đặc tả Use Case UC20 – Quản lý dữ liệu kho

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC20 |
| **Tên** | Quản lý dữ liệu kho |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Quản lý dữ liệu kho: thêm, cập nhật, xóa các nhóm dữ liệu kho. |
| **Tiền điều kiện** | Đăng nhập thành công và có quyền quản lý dữ liệu kho. |
| **Hậu điều kiện** | Dữ liệu kho được cập nhật theo thao tác. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Quản lý dữ liệu kho. | |
| 2 | | Hiển thị các nhóm dữ liệu có thể quản lý. |
| 3 | Chọn nhóm dữ liệu (nguyên liệu, thành phẩm, lô NL, lô TP, vị trí lưu kho). | |
| 4 | | Hiển thị các thao tác Thêm, Cập nhật, Xóa. |
| 5 | Chọn thao tác cần thực hiện. | |
| 6 | | Hiển thị biểu mẫu tương ứng. |
| 7 | Nhập/chỉnh sửa thông tin và xác nhận. | |
| 8 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 9 | Xác nhận lưu/xóa dữ liệu. | |
| 10 | | Thực hiện thêm/cập nhật/xóa dữ liệu. |
| 11 | | Thông báo thao tác thành công. |

**Alternative Flow:**

- **5.1. Thêm dữ liệu mới:** Hiển thị biểu mẫu, nhập thông tin, kiểm tra, lưu dữ liệu.
- **5.2. Cập nhật dữ liệu:** Hiển thị thông tin cần cập nhật, chỉnh sửa, kiểm tra, lưu.
- **5.3. Xóa dữ liệu:** Yêu cầu xác nhận, kiểm tra điều kiện xóa, xóa dữ liệu.

**Exception Flow:**

- **8.1. Dữ liệu thiếu hoặc không hợp lệ:** Hệ thống thông báo. Quay lại bước 7.
- **8.2. Dữ liệu đã tồn tại:** Hệ thống thông báo trùng. Người dùng chỉnh sửa và thực hiện lại.
- **10.1. Không thể xóa dữ liệu:** Dữ liệu đang được sử dụng. Hệ thống thông báo.
- **10.2. Lỗi hệ thống:** Hệ thống thông báo. Dữ liệu không thay đổi. Use Case kết thúc.

---

## 7.22. Tra cứu dữ liệu kho – UC21

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR30** | Tra cứu dữ liệu kho | Cho phép tra cứu dữ liệu kho theo các tiêu chí: mã, tên, lô, kho, vị trí, trạng thái. |

### Đặc tả Use Case UC21 – Tra cứu dữ liệu kho

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC21 |
| **Tên** | Tra cứu dữ liệu kho |
| **Actor chính** | Bộ phận quản lý kho; Nhân viên kho |
| **Actor phụ** | Không |
| **Mục đích** | Cho phép tra cứu thông tin dữ liệu kho theo nhiều tiêu chí. |
| **Tiền điều kiện** | Đăng nhập thành công và có quyền tra cứu. |
| **Hậu điều kiện** | Hiển thị kết quả tra cứu. Không thay đổi dữ liệu kho. |

**Basic Flow:**

| Bước | Người dùng | Hệ thống |
|---|---|---|
| 1 | Chọn "Tra cứu dữ liệu kho". | |
| 2 | | Hiển thị giao diện tra cứu. |
| 3 | Chọn loại dữ liệu cần tra cứu. | |
| 4 | | Hiển thị tiêu chí tra cứu tương ứng. |
| 5 | Nhập thông tin hoặc tiêu chí tra cứu. | |
| 6 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 7 | | Thực hiện tìm kiếm. |
| 8 | | Hiển thị danh sách kết quả. |
| 9 | Chọn dữ liệu cụ thể cần xem chi tiết. | |
| 10 | | Hiển thị thông tin chi tiết. |

**Alternative Flow:**

- **5.1. Không nhập tiêu chí:** Hệ thống thông báo yêu cầu nhập. Quay lại bước 5.
- **6.1. Thông tin tra cứu không hợp lệ:** Hệ thống thông báo. Quay lại bước 5.

**Exception Flow:**

- **7.1. Không tìm thấy dữ liệu:** Hệ thống thông báo. Quay lại bước 5.

---

## 7.23. Thực hiện kiểm kê kho – UC22

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR31** | Thực hiện kiểm kê kho | Cho phép Hội đồng kiểm kê kiểm đếm hàng hóa và đối chiếu với số liệu trên hệ thống. |

### Đặc tả Use Case UC22 – Thực hiện kiểm kê kho

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC22 |
| **Tên** | Thực hiện kiểm kê kho |
| **Actor chính** | Hội đồng kiểm kê |
| **Actor phụ** | Không |
| **Mục đích** | Kiểm đếm hàng hóa thực tế và đối chiếu với số liệu trên hệ thống. |
| **Tiền điều kiện** | Đăng nhập thành công. Có yêu cầu hoặc kế hoạch kiểm kê. |
| **Hậu điều kiện** | Số liệu kiểm kê được ghi nhận và đối chiếu. Kết quả được lưu. Nếu có chênh lệch, hệ thống ghi nhận để chuyển sang xử lý. |

**Basic Flow:**

| Bước | Hội đồng kiểm kê | Hệ thống |
|---|---|---|
| 1 | Chọn "Thực hiện kiểm kê kho". | |
| 2 | Chọn kho cần kiểm kê. | |
| 3 | | Hiển thị danh sách hàng hóa theo kho và lô. |
| 4 | | Cập nhật trạng thái thành "Đang kiểm kê". |
| 5 | Kiểm đếm số lượng thực tế. | |
| 6 | Nhập số lượng thực tế. | |
| 7 | | Kiểm tra tính hợp lệ của số liệu. |
| 8 | | Đối chiếu với số liệu trên hệ thống. |
| 9 | | Hiển thị kết quả đối chiếu. |
| 10 | Kiểm tra kết quả. | |
| 11 | Xác nhận kết quả kiểm kê. | |
| 12 | | Kiểm tra kết quả đối chiếu, xác định có chênh lệch hay không. |
| 13 | | Cập nhật trạng thái thành "Đã kiểm kê". |

**Alternative Flow:**

- **12.1. Không xác nhận kết quả:** Hội đồng kiểm kê chọn kiểm tra lại. Quay lại bước 6.
- **13.1. Số lượng khớp:** Hệ thống ghi nhận không có chênh lệch.
- **13.2. Số lượng không khớp:** Hệ thống ghi nhận thông tin chênh lệch.

**Exception Flow:**

- **8.1. Số lượng kiểm kê không hợp lệ:** Hệ thống thông báo. Quay lại bước 6.
- **14.1. Không thể lưu kết quả:** Hệ thống thông báo lỗi. Use Case kết thúc.

---

## 7.24. Xử lý chênh lệch kiểm kê – UC23

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR32** | Xử lý chênh lệch kiểm kê | Cho phép Bộ phận quản lý kho xác định nguyên nhân chênh lệch và lập đề nghị điều chỉnh tồn kho. |

### Đặc tả Use Case UC23 – Xử lý chênh lệch kiểm kê

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC23 |
| **Tên** | Xử lý chênh lệch kiểm kê |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Xác định nguyên nhân chênh lệch kiểm kê và lập đề nghị điều chỉnh tồn kho nếu cần. |
| **Tiền điều kiện** | Kết quả kiểm kê có chênh lệch và đang ở trạng thái "Chưa xử lý". Đăng nhập thành công. |
| **Hậu điều kiện** | Nguyên nhân chênh lệch được ghi nhận. Nếu cần, đề nghị điều chỉnh tồn kho được lập và chuyển sang "Chờ phê duyệt". |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn "Xử lý chênh lệch kiểm kê". | |
| 2 | | Hiển thị danh sách kết quả kiểm kê có chênh lệch ở trạng thái "Chưa xử lý". |
| 3 | Chọn kết quả kiểm kê cần xử lý. | |
| 4 | | Cập nhật trạng thái thành "Đang xử lý". |
| 5 | Kiểm tra thông tin chênh lệch. | |
| 6 | | Hiển thị thông tin nguyên liệu/thành phẩm, lô hàng, vị trí lưu kho liên quan. |
| 7 | Xác định nguyên nhân chênh lệch. | |
| 8 | Nhập nguyên nhân và thông tin xử lý. | |
| 9 | | Kiểm tra tính đầy đủ và hợp lệ. |
| 10 | Xác nhận kết quả xử lý. | |
| 11 | | Ghi nhận nguyên nhân và kết quả xử lý. |
| 12 | | Cập nhật trạng thái thành "Đã xử lý" và xác định có cần điều chỉnh tồn kho hay không. |

**Alternative Flow:**

- **6.1. Cần kiểm tra lại thông tin:** Hệ thống hiển thị lại thông tin kiểm kê. Quay lại bước 5.
- **13.1. Không cần điều chỉnh tồn kho:** Hệ thống ghi nhận kết quả. Use Case kết thúc.
- **13.2. Cần điều chỉnh tồn kho:** Hệ thống hiển thị thông tin đề nghị điều chỉnh. Bộ phận quản lý kho lập đề nghị. Hệ thống chuyển trạng thái thành "Chờ phê duyệt".

**Exception Flow:**

- **2.1. Không có kết quả kiểm kê có chênh lệch:** Hệ thống thông báo. Use Case kết thúc.
- **3.1. Kết quả kiểm kê đã được xử lý:** Hệ thống thông báo. Quay lại bước 2.
- **10.1. Thông tin xử lý chưa đầy đủ:** Hệ thống thông báo. Quay lại bước 8.
- **13.2.1. Không thể lập đề nghị điều chỉnh:** Hệ thống thông báo lỗi. Kết quả xử lý vẫn được lưu.

---

## 7.25. Phê duyệt điều chỉnh tồn kho – UC24

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR33** | Phê duyệt điều chỉnh tồn kho | Cho phép Ban giám đốc phê duyệt hoặc từ chối đề nghị điều chỉnh tồn kho. |

### Đặc tả Use Case UC24 – Phê duyệt điều chỉnh tồn kho

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC24 |
| **Tên** | Phê duyệt điều chỉnh tồn kho |
| **Actor chính** | Ban giám đốc |
| **Actor phụ** | Không |
| **Mục đích** | Phê duyệt hoặc từ chối đề nghị điều chỉnh tồn kho. |
| **Tiền điều kiện** | Đề nghị điều chỉnh đang ở trạng thái "Chờ phê duyệt". Đăng nhập thành công. |
| **Hậu điều kiện** | Nếu phê duyệt: trạng thái chuyển thành "Đã phê duyệt" và tồn kho được cập nhật. Nếu từ chối: trạng thái chuyển thành "Từ chối" và tồn kho không thay đổi. |

**Basic Flow:**

| Bước | Ban giám đốc | Hệ thống |
|---|---|---|
| 1 | Chọn "Phê duyệt điều chỉnh tồn kho". | |
| 2 | | Hiển thị danh sách đề nghị ở trạng thái "Chờ phê duyệt". |
| 3 | Chọn đề nghị cần xử lý. | |
| 4 | | Hiển thị thông tin đề nghị và kết quả kiểm kê liên quan. |
| 5 | Kiểm tra thông tin đề nghị. | |
| 6 | | Hiển thị số lượng trước điều chỉnh, chênh lệch, sau điều chỉnh, lý do, phương án. |
| 7 | Đánh giá đề nghị. | |
| 8 | Chọn "Phê duyệt" hoặc "Từ chối". | |
| 9 | | Kiểm tra quyền phê duyệt và trạng thái đề nghị. |
| 10 | | Xác định hướng xử lý theo lựa chọn. |

**Alternative Flow:**

- **2.1. Không có đề nghị chờ phê duyệt:** Hệ thống thông báo. Use Case kết thúc.
- **3.1. Đề nghị đã được xử lý:** Hệ thống thông báo. Quay lại bước 2.
- **5.1. Thông tin đề nghị chưa đầy đủ:** Hệ thống thông báo. Quay lại bước 5.
- **10.1. Phê duyệt:** Hệ thống cập nhật tồn kho, chuyển trạng thái thành "Đã phê duyệt", ghi nhận lịch sử.
- **10.2. Từ chối:** Ban giám đốc nhập lý do. Hệ thống chuyển trạng thái thành "Từ chối", không điều chỉnh tồn kho.

**Exception Flow:**

- **9.1. Không có quyền phê duyệt hoặc trạng thái không phù hợp:** Hệ thống thông báo. Use Case kết thúc.
- **10.2.1. Lý do từ chối chưa đầy đủ:** Hệ thống thông báo. Quay lại nhập lý do.
- **10.1.1. Không thể cập nhật tồn kho:** Hệ thống thông báo lỗi. Giữ nguyên trạng thái "Chờ phê duyệt".

---

## 7.26. Điều phối xuất kho – UC26

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR34** | Điều phối xuất kho | Cho phép Bộ phận quản lý kho xác định lô hàng ưu tiên xuất theo FIFO/FEFO. |

### Đặc tả Use Case UC26 – Điều phối xuất kho

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC26 |
| **Tên** | Điều phối xuất kho |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Xác định kho và lô hàng cụ thể cần xuất theo nguyên tắc FIFO/FEFO. |
| **Tiền điều kiện** | Có yêu cầu xuất kho hợp lệ đang chờ điều phối. |
| **Hậu điều kiện** | Thành công: Lô hàng cần xuất được xác định; thông tin chuyển cho nhân viên kho lập phiếu xuất. Thất bại: Chưa xác định được lô hàng phù hợp. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Tiếp nhận yêu cầu xuất kho. | |
| 2 | | Xác định kho chứa loại hàng; hiển thị danh sách lô hàng kèm ngày nhập/hạn sử dụng/số lượng tồn. |
| 3 | | Áp dụng FIFO/FEFO, gợi ý thứ tự lô ưu tiên. |
| 4 | Chọn lô và xác nhận số lượng cần xuất. | |
| 5 | | Kiểm tra tổng số lượng các lô đáp ứng yêu cầu. |
| 6 | Xác nhận điều phối xuất kho. | |
| 7 | | Chuyển thông tin điều phối cho nhân viên kho lập phiếu xuất. |

**Alternative Flow:**

- **3.1. Chọn lô khác với gợi ý:** Hệ thống kiểm tra lô được chọn còn đủ số lượng. Quay lại bước 4.

**Exception Flow:**

- **1.1. Không xác định được kho tương ứng:** Hệ thống cảnh báo. Yêu cầu xuất kho được đánh dấu chờ xử lý thủ công.
- **4.1. Tổng số lượng không đủ:** Hệ thống cảnh báo thiếu hàng. Yêu cầu được đánh dấu chờ bổ sung.

---

## 7.27. Quản lý nguyên liệu – UC27

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR35** | Quản lý nguyên liệu | Cho phép Bộ phận quản lý kho thêm, cập nhật, xóa danh mục nguyên liệu. |

### Đặc tả Use Case UC27 – Quản lý nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC27 |
| **Tên** | Quản lý nguyên liệu |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Quản lý danh mục nguyên liệu: thêm, cập nhật, xóa. |
| **Tiền điều kiện** | Đăng nhập thành công và có quyền quản lý nguyên liệu. |
| **Hậu điều kiện** | Danh mục nguyên liệu được cập nhật theo thao tác. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn "Quản lý nguyên liệu". | |
| 2 | | Hiển thị danh sách nguyên liệu hiện có. |
| 3 | Chọn thao tác: Thêm, Cập nhật, Xóa. | |
| 4 | | Hiển thị giao diện tương ứng. |
| 5 | Chọn nguyên liệu cần xử lý (nếu cập nhật/xóa). | |
| 6 | | Hiển thị thông tin chi tiết. |
| 7 | Nhập/chỉnh sửa thông tin. | |
| 8 | Xác nhận thao tác. | |

**Alternative Flow:**

- **3.1. Thêm nguyên liệu:** Nhập mã, tên, đơn vị tính, quy cách đóng gói, điều kiện bảo quản. Hệ thống kiểm tra và lưu.
- **3.2. Cập nhật nguyên liệu:** Chọn nguyên liệu, chỉnh sửa, kiểm tra, lưu.
- **3.3. Xóa nguyên liệu:** Chọn nguyên liệu, xác nhận xóa, kiểm tra điều kiện, xóa.

**Exception Flow:**

- **2.1. Không có nguyên liệu trong danh mục:** Hệ thống thông báo. Chuyển sang thêm mới.
- **5.1. Không tìm thấy nguyên liệu:** Hệ thống thông báo. Quay lại bước 2.
- **8.1. Thông tin không đầy đủ hoặc không hợp lệ:** Hệ thống thông báo. Quay lại bước 7.
- **8.2. Mã nguyên liệu đã tồn tại:** Hệ thống thông báo. Quay lại bước 7.
- **10.1. Không thể xóa nguyên liệu:** Nguyên liệu đang được sử dụng. Hệ thống thông báo. Use Case kết thúc.
- **10.2. Không thể lưu thông tin:** Hệ thống thông báo lỗi. Use Case kết thúc.

---

## 7.28. Quản lý thành phẩm – UC28

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR36** | Quản lý thành phẩm | Cho phép Bộ phận quản lý kho thêm, cập nhật, xóa danh mục thành phẩm. |

### Đặc tả Use Case UC28 – Quản lý thành phẩm

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC28 |
| **Tên** | Quản lý thành phẩm |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Quản lý danh mục thành phẩm: thêm, cập nhật, xóa. |
| **Tiền điều kiện** | Đăng nhập thành công và có quyền quản lý danh mục thành phẩm. |
| **Hậu điều kiện** | Danh mục thành phẩm được cập nhật theo thao tác. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn "Quản lý thành phẩm". | |
| 2 | | Hiển thị danh sách thành phẩm hiện có và các thao tác Thêm, Cập nhật, Xóa. |
| 3 | Chọn thao tác Thêm. | |
| 4 | | Hiển thị biểu mẫu thêm thành phẩm. |
| 5 | Nhập tên sản phẩm, đơn vị tính, quy cách đóng gói, hạn sử dụng mặc định. | |
| 6 | | Kiểm tra tính đầy đủ, hợp lệ và trùng lặp. |
| 7 | Xác nhận thêm thành phẩm. | |
| 8 | | Lưu thành phẩm mới. |
| 9 | | Thông báo thành công và hiển thị lại danh sách. |

**Alternative Flow:**

- **3.1. Cập nhật thành phẩm:** Chọn thành phẩm, chỉnh sửa, kiểm tra, lưu.
- **3.2. Xóa thành phẩm:** Chọn thành phẩm, xác nhận xóa, kiểm tra điều kiện, xóa.

**Exception Flow:**

- **6.1. Thông tin thiếu hoặc không hợp lệ:** Hệ thống thông báo. Quay lại bước 6.
- **6.2. Thành phẩm đã tồn tại:** Hệ thống thông báo. Quay lại bước 5.
- **3.1.4.1. Thông tin cập nhật không hợp lệ hoặc trùng:** Hệ thống thông báo.
- **3.2.4.1. Thành phẩm không thể xóa:** Thành phẩm đang được sử dụng. Hệ thống thông báo.
- **8.1. Lỗi khi lưu dữ liệu:** Hệ thống thông báo. Use Case kết thúc.

---

## 7.29. Quản lý lô nguyên liệu – UC29

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR37** | Quản lý lô nguyên liệu | Cho phép Bộ phận quản lý kho thêm, cập nhật, xóa thông tin lô nguyên liệu. |

### Đặc tả Use Case UC29 – Quản lý lô nguyên liệu

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC29 |
| **Tên** | Quản lý lô nguyên liệu |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Quản lý thông tin lô nguyên liệu: thêm, cập nhật, xóa. |
| **Tiền điều kiện** | Đăng nhập thành công với vai trò Bộ phận quản lý kho. |
| **Hậu điều kiện** | Thông tin lô nguyên liệu được thêm/cập nhật/xóa thành công. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Quản lý lô nguyên liệu. | |
| 2 | | Hiển thị danh sách lô nguyên liệu. |
| 3 | Chọn Thêm lô nguyên liệu. | |
| 4 | | Hiển thị form nhập thông tin lô. |
| 5 | Nhập mã lô, ngày nhập, hạn sử dụng, số lượng còn lại. | |
| 6 | | Kiểm tra dữ liệu nhập. |
| 7 | Chọn Lưu. | |
| 8 | | Lưu thông tin lô nguyên liệu và thông báo thành công. |

**Alternative Flow:**

- **3.1. Cập nhật lô:** Chọn lô, chỉnh sửa, kiểm tra, lưu.
- **3.2. Xóa lô:** Chọn lô, xác nhận xóa, hệ thống xóa.
- **5.1. Mã lô đã tồn tại:** Hệ thống thông báo. Quay lại bước 5.

**Exception Flow:**

- **5.2. Thiếu hoặc sai thông tin:** Hệ thống thông báo lỗi. Quay lại bước 5.
- **7.1. Hủy thao tác:** Hệ thống quay lại danh sách lô.

---

## 7.30. Quản lý lô thành phẩm – UC30

| Mã | Functional Requirement | Diễn giải |
|---|---|---|
| **FR38** | Quản lý lô thành phẩm | Cho phép Bộ phận quản lý kho thêm, cập nhật, xóa, tìm kiếm lô thành phẩm. |

### Đặc tả Use Case UC30 – Quản lý lô thành phẩm

| Thuộc tính | Mô tả |
|---|---|
| **ID** | UC30 |
| **Tên** | Quản lý lô thành phẩm |
| **Actor chính** | Bộ phận quản lý kho |
| **Actor phụ** | Không |
| **Mục đích** | Quản lý thông tin lô thành phẩm: thêm, cập nhật, xóa, tìm kiếm. |
| **Tiền điều kiện** | Đăng nhập thành công. Có quyền quản lý lô thành phẩm. Thông tin thành phẩm đã tồn tại. |
| **Hậu điều kiện** | Thông tin lô thành phẩm được cập nhật. Dữ liệu mã lô, ngày sản xuất, hạn sử dụng (nếu có), số lượng còn lại được lưu chính xác. Hỗ trợ truy vết và FEFO. |

**Basic Flow:**

| Bước | Bộ phận quản lý kho | Hệ thống |
|---|---|---|
| 1 | Chọn chức năng Quản lý lô thành phẩm. | |
| 2 | | Hiển thị danh sách lô thành phẩm và các chức năng Thêm, Cập nhật, Xóa, Tìm kiếm. |
| 3 | Chọn thao tác cần thực hiện. | |
| 4 | | Hiển thị giao diện tương ứng. |
| 5 | Nhập/chỉnh sửa mã lô, thành phẩm, ngày sản xuất, hạn sử dụng (nếu có), số lượng. | |
| 6 | | Kiểm tra tính đầy đủ, hợp lệ và tính duy nhất mã lô. |
| 7 | Kiểm tra lại thông tin và xác nhận. | |
| 8 | | Lưu/cập nhật/xóa thông tin lô thành phẩm. |
| 9 | | Thông báo thành công và cập nhật danh sách. |

**Alternative Flow:**

- **2.1. Tìm kiếm lô thành phẩm:** Nhập mã lô hoặc thông tin thành phẩm, hệ thống hiển thị kết quả.
- **3.1. Cập nhật lô thành phẩm:** Chọn lô, chỉnh sửa, kiểm tra, lưu.
- **3.2. Xóa lô thành phẩm:** Chọn lô, xác nhận xóa, kiểm tra giao dịch liên quan, xóa nếu chưa phát sinh giao dịch.

**Exception Flow:**

- **5.1. Thông tin thiếu hoặc không hợp lệ:** Hệ thống thông báo. Quay lại bước 5.
- **5.2. Mã lô đã tồn tại:** Hệ thống thông báo trùng. Nhập lại mã lô khác.
- **5.3. Số lượng còn lại không hợp lệ:** Hệ thống thông báo lỗi. Quay lại bước 5.
- **7.1. Hủy thao tác:** Hệ thống không lưu. Quay về danh sách.
- **8.1. Lỗi khi lưu dữ liệu:** Hệ thống thông báo lỗi. Use Case kết thúc.

---

# 8. Danh sách Actors

| STT | Actor | Mô tả |
|---|---|---|
| 1 | Tất cả các Actor | Đăng nhập hệ thống |
| 2 | Bộ phận lập kế hoạch sản xuất | Lập kế hoạch sản xuất, phân công xưởng sản xuất |
| 3 | Ban giám đốc | Duyệt kế hoạch sản xuất, duyệt đơn mua nguyên liệu, phê duyệt điều chỉnh tồn kho, theo dõi báo cáo |
| 4 | Khách hàng | Đặt đơn hàng |
| 5 | Nhân viên kho | Nhập kho nguyên liệu, xuất kho nguyên liệu, nhập kho thành phẩm, xuất kho thành phẩm, nhận nguyên liệu từ NCC, nhập kho hàng trả về |
| 6 | Bộ phận quản lý kho | Quản lý dữ liệu kho, nguyên liệu, thành phẩm, lô; điều phối nhập/xuất kho; xử lý chênh lệch kiểm kê; xử lý hàng lỗi; tra cứu dữ liệu kho; theo dõi báo cáo |
| 7 | Xưởng sản xuất | Lập phiếu yêu cầu xuất kho nguyên liệu, lập phiếu yêu cầu nhập kho thành phẩm |
| 8 | Bộ phận QC | Kiểm tra chất lượng nguyên liệu, kiểm tra hàng trả về |
| 9 | Hội đồng kiểm kê | Thực hiện kiểm kê kho |
| 10 | Bộ phận mua hàng | Lập đơn mua nguyên liệu |

---

# 9. Danh sách Use Cases

| STT | Mã UC | Tên Use Case | Actor chính |
|---|---|---|---|
| 1 | UC01 | Đăng nhập hệ thống | Tất cả các Actor |
| 2 | UC02 | Lập kế hoạch sản xuất | Bộ phận lập kế hoạch sản xuất |
| 3 | UC03 | Duyệt kế hoạch sản xuất | Ban giám đốc |
| 4 | UC04 | Phân công xưởng sản xuất | Bộ phận lập kế hoạch sản xuất |
| 5 | UC05 | Thống kê báo cáo & Cảnh báo kho | Bộ phận quản lý kho; Ban giám đốc |
| 6 | UC-DH | Đặt đơn hàng | Khách hàng |
| 7 | UC06 | Lập đơn mua nguyên liệu | Bộ phận mua hàng |
| 8 | UC07 | Duyệt đơn mua nguyên liệu | Ban giám đốc |
| 9 | UC08 | Nhận nguyên liệu từ nhà cung cấp | Nhân viên kho |
| 10 | UC09 | Kiểm tra chất lượng nguyên liệu | Bộ phận QC |
| 11 | UC10 | Nhập kho nguyên liệu | Nhân viên kho |
| 12 | UC11 | Lập phiếu yêu cầu xuất kho nguyên liệu | Xưởng sản xuất |
| 13 | UC12 | Xuất kho nguyên liệu | Nhân viên kho |
| 14 | UC13 | Lập phiếu yêu cầu nhập kho thành phẩm | Xưởng sản xuất |
| 15 | UC14 | Nhập kho thành phẩm | Nhân viên kho |
| 16 | UC15 | Xuất kho thành phẩm giao hàng | Nhân viên kho |
| 17 | UC16 | Điều phối nhập kho | Bộ phận quản lý kho |
| 18 | UC17 | Kiểm tra hàng trả về | Bộ phận QC |
| 19 | UC18 | Nhập kho hàng trả về | Nhân viên kho |
| 20 | UC19 | Xử lý hàng lỗi và hàng trả về | Bộ phận quản lý kho |
| 21 | UC20 | Quản lý dữ liệu kho | Bộ phận quản lý kho |
| 22 | UC21 | Tra cứu dữ liệu kho | Bộ phận quản lý kho; Nhân viên kho |
| 23 | UC22 | Thực hiện kiểm kê kho | Hội đồng kiểm kê |
| 24 | UC23 | Xử lý chênh lệch kiểm kê | Bộ phận quản lý kho |
| 25 | UC24 | Phê duyệt điều chỉnh tồn kho | Ban giám đốc |
| 26 | UC26 | Điều phối xuất kho | Bộ phận quản lý kho |
| 27 | UC27 | Quản lý nguyên liệu | Bộ phận quản lý kho |
| 28 | UC28 | Quản lý thành phẩm | Bộ phận quản lý kho |
| 29 | UC29 | Quản lý lô nguyên liệu | Bộ phận quản lý kho |
| 30 | UC30 | Quản lý lô thành phẩm | Bộ phận quản lý kho |

---

# 10. Tổng hợp Functional Requirements

| Mã FR | Tên FR | UC liên quan |
|---|---|---|
| FR01 | Đăng nhập hệ thống | UC01 |
| FR02 | Xác thực tài khoản | UC01 |
| FR03 | Phân quyền theo vai trò | UC01 |
| FR04 | Tạo phiên đăng nhập | UC01 |
| FR05 | Lập kế hoạch sản xuất | UC02 |
| FR06 | Kiểm tra tính khả thi kế hoạch | UC02 |
| FR07 | Duyệt kế hoạch sản xuất | UC03 |
| FR08 | Phân công xưởng sản xuất | UC04 |
| FR09 | Kiểm tra năng lực xưởng | UC04 |
| FR10 | Báo cáo tồn kho | UC05 |
| FR11 | Báo cáo nhập/xuất kho | UC05 |
| FR12 | Báo cáo hiệu suất lưu kho | UC05 |
| FR13 | Cảnh báo kho | UC05 |
| FR14 | Đặt đơn hàng | UC-DH |
| FR15 | Lập đơn mua nguyên liệu | UC06 |
| FR16 | Duyệt đơn mua nguyên liệu | UC07 |
| FR17 | Nhận nguyên liệu từ NCC | UC08 |
| FR18 | Kiểm tra chất lượng nguyên liệu | UC09 |
| FR19 | Nhập kho nguyên liệu | UC10 |
| FR20 | Lập phiếu yêu cầu xuất kho NL | UC11 |
| FR21 | Xuất kho nguyên liệu | UC12 |
| FR22 | Lập phiếu yêu cầu nhập kho TP | UC13 |
| FR23 | Nhập kho thành phẩm | UC14 |
| FR24 | Xuất kho thành phẩm giao hàng | UC15 |
| FR25 | Điều phối nhập kho | UC16 |
| FR26 | Kiểm tra hàng trả về | UC17 |
| FR27 | Nhập kho hàng trả về | UC18 |
| FR28 | Xử lý hàng lỗi và hàng trả về | UC19 |
| FR29 | Quản lý dữ liệu kho | UC20 |
| FR30 | Tra cứu dữ liệu kho | UC21 |
| FR31 | Thực hiện kiểm kê kho | UC22 |
| FR32 | Xử lý chênh lệch kiểm kê | UC23 |
| FR33 | Phê duyệt điều chỉnh tồn kho | UC24 |
| FR34 | Điều phối xuất kho | UC26 |
| FR35 | Quản lý nguyên liệu | UC27 |
| FR36 | Quản lý thành phẩm | UC28 |
| FR37 | Quản lý lô nguyên liệu | UC29 |
| FR38 | Quản lý lô thành phẩm | UC30 |

---

# 11. Business Rules

| Mã | Business Rule | Diễn giải |
|---|---|---|
| **BRL01** | Nguyên tắc FEFO | Khi xuất kho nguyên liệu, hệ thống ưu tiên xuất các lô có hạn sử dụng gần nhất trước (First Expired, First Out). |
| **BRL02** | Nguyên tắc FIFO/FEFO cho thành phẩm | Khi xuất kho thành phẩm giao hàng, hệ thống gợi ý lô ưu tiên theo FIFO/FEFO đối với sản phẩm có hạn sử dụng. |
| **BRL03** | Kế hoạch sản xuất phải được duyệt | Kế hoạch sản xuất phải được Ban giám đốc phê duyệt trước khi phân công xưởng sản xuất. |
| **BRL04** | Đơn mua phải được duyệt | Đơn mua nguyên liệu phải được Ban giám đốc phê duyệt trước khi thực hiện mua hàng. |
| **BRL05** | Nguyên liệu phải qua kiểm tra chất lượng | Nguyên liệu phải được Bộ phận QC kiểm tra và xác nhận đạt chất lượng trước khi nhập kho. |
| **BRL06** | Hàng trả về phải qua kiểm tra | Hàng trả về phải được kiểm tra chất lượng. Nếu đạt thì nhập kho, nếu không đạt thì chuyển sang xử lý hàng lỗi. |
| **BRL07** | Điều chỉnh tồn kho phải được phê duyệt | Đề nghị điều chỉnh tồn kho sau kiểm kê phải được Ban giám đốc phê duyệt trước khi cập nhật vào hệ thống. |
| **BRL08** | Phiếu nhập/xuất kho | Mọi thao tác nhập kho và xuất kho đều phải có phiếu nhập/xuất kho tương ứng. |
| **BRL09** | Xuất kho theo phiếu yêu cầu | Xuất kho nguyên liệu cho sản xuất phải dựa trên phiếu yêu cầu xuất kho từ xưởng sản xuất. |
| **BRL10** | Nhập kho thành phẩm theo phiếu yêu cầu | Nhập kho thành phẩm phải dựa trên phiếu yêu cầu nhập kho từ xưởng sản xuất. |
| **BRL11** | Không cho xuất lô đã hết hạn | Hệ thống không cho phép chọn lô thành phẩm đã hết hạn sử dụng khi xuất kho. |
| **BRL12** | Không xóa dữ liệu đang được sử dụng | Hệ thống không cho phép xóa nguyên liệu, thành phẩm hoặc lô hàng đang được sử dụng trong các nghiệp vụ liên quan. |
| **BRL13** | Mã lô phải duy nhất | Mã lô nguyên liệu và mã lô thành phẩm phải là duy nhất trong hệ thống. |
