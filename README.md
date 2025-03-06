laptopshop
Môi trường chạy dự án
Node.js v18.17.0
Java v17.0.9
Ứng dụng này được tạo bằng JHipster 8.1.0, bạn có thể tìm tài liệu và trợ giúp tại JHipster Documentation.

Cấu trúc dự án
Node.js là bắt buộc để tạo dự án và được khuyến nghị sử dụng trong quá trình phát triển.
JHipster cũng tạo package.json để hỗ trợ phát triển, bao gồm các công cụ như prettier, commit hooks, scripts, v.v.

Các tệp và thư mục quan trọng:
.yo-rc.json - Tệp cấu hình Yeoman, chứa cấu hình của JHipster.
.yo-resolve (tùy chọn) - Trình giải quyết xung đột của Yeoman.
.jhipster/*.json - Tệp cấu hình cho các entity của JHipster.
npmw - Trình bao bọc giúp sử dụng npm được cài đặt cục bộ.
/src/main/docker - Cấu hình Docker cho ứng dụng và các dịch vụ phụ thuộc.
Phát triển
Trước khi xây dựng dự án, bạn cần cài đặt và cấu hình các công cụ sau trên máy của mình:

Node.js: Dùng để chạy server phát triển và biên dịch dự án.
Sau khi cài đặt Node.js, chạy lệnh sau để cài đặt các công cụ phát triển:

bash
Copy
Edit
npm install
Chạy ứng dụng trong môi trường phát triển
Chạy hai lệnh sau trong hai terminal khác nhau để khởi động ứng dụng với tính năng tự động làm mới khi thay đổi file:

bash
Copy
Edit
./mvnw
npm start
Lệnh npm cũng giúp quản lý các thư viện CSS & JavaScript trong ứng dụng. Bạn có thể cập nhật thư viện bằng cách sửa đổi package.json hoặc chạy lệnh:

bash
Copy
Edit
npm update
npm install
Để xem danh sách các lệnh có sẵn trong dự án, chạy:

bash
Copy
Edit
npm run
Hỗ trợ PWA (Progressive Web App)
JHipster hỗ trợ PWA, nhưng mặc định bị tắt. Để kích hoạt, bỏ dấu comment dòng sau trong src/main/webapp/index.html:

html
Copy
Edit
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('./service-worker.js').then(function () {
      console.log('Service Worker Registered');
    });
  }
</script>
Lưu ý: JHipster sử dụng Workbox để tự động tạo tệp service-worker.js.

Xây dựng sản phẩm
Đóng gói thành JAR
Chạy lệnh sau để tạo tệp JAR tối ưu hóa cho sản phẩm:

bash
Copy
Edit
./mvnw -Pprod clean verify
Sau đó chạy:

bash
Copy
Edit
java -jar target/*.jar
Ứng dụng sẽ chạy tại http://localhost:8080.

Đóng gói thành WAR
Nếu muốn triển khai lên máy chủ ứng dụng, chạy:

bash
Copy
Edit
./mvnw -Pprod,war clean verify
Quản lý & kiểm thử
Kiểm thử Spring Boot
Chạy lệnh sau để kiểm thử ứng dụng:

bash
Copy
Edit
./mvnw verify
Kiểm thử phía client
JHipster sử dụng Jest để kiểm thử JavaScript. Các bài kiểm thử nằm trong src/test/javascript/, chạy bằng lệnh:

bash
Copy
Edit
npm test
Kiểm tra chất lượng mã nguồn với SonarQube
SonarQube giúp phân tích chất lượng mã nguồn. Chạy máy chủ SonarQube bằng Docker:

bash
Copy
Edit
docker compose -f src/main/docker/sonar.yml up -d
Chạy phân tích mã nguồn bằng Maven:

bash
Copy
Edit
./mvnw -Pprod clean verify sonar:sonar -Dsonar.login=admin -Dsonar.password=admin
Nếu cần chạy lại phân tích, chạy:

bash
Copy
Edit
./mvnw initialize sonar:sonar -Dsonar.login=admin -Dsonar.password=admin
Bạn cũng có thể cấu hình thông tin đăng nhập SonarQube trong sonar-project.properties.

Sử dụng Docker để đơn giản hóa phát triển
Bạn có thể sử dụng Docker để chạy các dịch vụ phụ thuộc của JHipster.

Ví dụ, để chạy MySQL trong container:

bash
Copy
Edit
docker compose -f src/main/docker/mysql.yml up -d
Dừng và xóa container:

bash
Copy
Edit
docker compose -f src/main/docker/mysql.yml down
Bạn cũng có thể tạo Docker Image của ứng dụng và chạy cùng các dịch vụ phụ thuộc:

bash
Copy
Edit
npm run java:docker
docker compose -f src/main/docker/app.yml up -d
Nếu đang sử dụng MacOS với chip M1, chạy lệnh sau để tạo ảnh Docker tương thích:

bash
Copy
Edit
npm run java:docker:arm64
Lưu ý: Nếu chạy Docker Desktop trên MacOS Big Sur trở lên, hãy bật Use the new Virtualization framework để cải thiện hiệu suất.

Tích hợp CI/CD
JHipster hỗ trợ thiết lập CI/CD tự động. Để tạo tệp cấu hình CI/CD cho các hệ thống như GitHub Actions, GitLab CI, Jenkins, chạy lệnh:

bash
Copy
Edit
jhipster ci-cd
Xem chi tiết tại Setting up Continuous Integration.

Tham khảo
JHipster Homepage & Docs: https://www.jhipster.tech
Tài liệu JHipster 8.1.0: https://www.jhipster.tech/documentation-archive/v8.1.0
Hướng dẫn phát triển JHipster: Using JHipster in development
Hướng dẫn triển khai JHipster: Using JHipster in production
Sử dụng Docker với JHipster: Using Docker and Docker-Compose