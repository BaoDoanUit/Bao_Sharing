Link reference: 
https://appsindie.com/tao-kien-truc-phan-mem-tinh-gon-nhat-voi-c4-model/

![[C4_Docs.png]]
Chữ **C** được lấy từ **4** hình vẽ chính trong mô hình này đó là: Context, Container, Component, Code (hay còn được gọi là Class).

-   System **C**ontext: Sơ đồ này mô tả tổng quát về hệ thống theo hướng che đi thành phần bên trong mà chỉ làm nổi bật **thành phần bên ngoài** (blackbox); bao gồm các yếu tố phụ thuộc chính (dependencies) của hệ thống, các giao thức (interfaces) để giao tiếp giữa những hệ thống với nhau và con người (người dùng / theo vai trò / theo phòng ban / v.v). Biểu đồ ngữ cảnh này là tiêu chuẩn trong kỹ thuật phần mềm.
-   **C**ontainer: Sơ đồ này mô tả về hệ thống theo hướng hiển thị thành **phần bên ngoài** cùng với việc phóng to những thành **phần bên trong** của hệ thống (whitebox); do đó hiển thị được các container (building block), mục đích và nhiệm vụ của từng container này, cùng với giao thức giao tiếp giữa những container đó. Sơ đồ này thường được gọi là sơ đồ khối cấp 1 (first level building block). Vậy container cụ thể là cài vẹo gì? Tuỳ theo phạm vi hệ thống các bạn đang làm (có thể là hệ thống, có thể là 1 component, cũng có thể là 1 hệ thống con), container có thể là cái máy tính, vi xử lý, cũng có thể là 1 dịch vụ (service) nào đó gởi email, lưu trữ, APIs…
-   **C**omponent: Sở đồ này phóng to container để mô tả về thành phần bên trong; do đó hiển thị được các components (building block), mục đích và nhiệm vụ, mối quan hệ của từng component cũng như là những giao thức kết nối. Sơ đồ này thường được gọi là sơ đồ khối cấp 2.
-   **C**ode (hay **c**lass): Sơ đồ này mô tả bên trong một component; theo đó hiển thị được các phần hiện thực như là class, package… cùng với mối quan hệ giữa những thành phần này
- 


### Material Architecture
![[Block_Ideas_For_C4_Model.png]]

Notes:
Một số gợi ý để có thể tạo tài liệu C4 model hiệu quả:

-   Hãy nghĩ về tài liệu bổ sung như một cuốn sách hướng dẫn bao gồm bản đồ, điểm ưa thích, điểm tham quan, hành trình, lịch sử, văn hóa, thông tin thực tế,… . Do đó tài liệu này phải thật đơn giản nhưng đầy đủ để có thể đọc được trong 1-2 giờ và cung cấp cho các nhà phát triển phần mềm đầy đủ thông tin để bắt đầu, thúc đẩy quá trình khám phá một hệ thống không quen thuộc với họ.
-   Tài liệu không phải là nhiệm vụ một lần. Thay vào đó, hãy tạo tài liệu và luôn luôn cập nhật và phát triển liên tục. Hãy tự động cập nhật nó bằng cách sử dụng công cụ hoặc bằng cách thêm một mục vào “định nghĩa về việc đã làm” của bạn.
-   Có nhiều tùy chọn dụng cụ; từ Microsoft Word và Atlassian Confluence đến các tập tin Markdown và AsciiDoc được phiên bản cùng với mã nguồn. Giảm trùng lặp và tăng tính nhất quán bằng cách tạo sơ đồ và tài liệu từ một nguồn nếu có thể.
- 

![[visualising-software-architecture.pdf]]

https://www.youtube.com/watch?v=e-JBV2ZsIkk&t=388s
Combine [Arc42](https://arc42.org/overview) vs [C4Model](https://www.ibm.com/garage/method/practices/code/c4-model-for-software-architecture/)
-   Context and Scope => [System Context diagram](https://en.wikipedia.org/wiki/System_context_diagram)  
-   Level 1 Building Block View => [Container diagram](https://www.hava.io/blog/container-diagram-generator)
-   Level 2 Building Block View => [Component diagram](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-component-diagram/)
-   Level 3 Building Block View => [Class diagram](https://en.wikipedia.org/wiki/Class_diagram)