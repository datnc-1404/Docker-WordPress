# Docker-WordPress



I. Install Docker
- Gỡ cài đặt các phiên bản cũ:

      sudo apt-get remove docker docker-engine docker.io containerd runc
      
- Cập nhật chỉ mục gói và cài đặt các gói để cho phép sử dụng kho lưu trữ qua HTTPS:

       sudo apt-get update 
       sudo apt-get install \
       ca-certificates \
       curl \
       gnupg \
       lsb-release

- Thêm khóa GPG chính thức của Docker:

       curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
       
- Sử dụng lệnh sau để thiết lập kho lưu trữ ổn định . Để thêm kho lưu trữ hàng đêm hoặc thử nghiệm , hãy thêm từ nightlyhoặc test(hoặc cả hai) vào sau từ stabletrong các lệnh bên dưới:

        echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

- Cài đặt Docker Engine:

        sudo apt-get update
        sudo apt-get install docker-ce docker-ce-cli containerd.io
        
- Để cài đặt một phiên bản cụ thể của Docker Engine, hãy liệt kê các phiên bản có sẵn trong repo, sau đó chọn và cài đặt:
Một. Liệt kê các phiên bản có sẵn trong repo:

        apt-cache madison docker-ce
        sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
II. Cài đặt WordPress

- Kiểm tra Docker Compose Installation:

        docker-compose --version
        
- Tạo thư mục WordPress:

        mkdir ~/wordpress/
        cd ~/wordpress/
        
- Tạo file docker-compose.yml và điền thông số cần thiết:

        version: '3.3'
        services:
           db:
             image: mysql:5.7
             volumes:
               - db_data:/var/lib/mysql
             restart: always
             environment:
               MYSQL_ROOT_PASSWORD: somewordpress
               MYSQL_DATABASE: wordpress
               MYSQL_USER: wordpress
               MYSQL_PASSWORD: wordpress
           wordpress:
             depends_on:
               - db
             image: wordpress:latest
             ports:
               - "8000:80"
             restart: always
             environment:
               WORDPRESS_DB_HOST: db:3306
               WORDPRESS_DB_USER: wordpress
               WORDPRESS_DB_PASSWORD: wordpress
               WORDPRESS_DB_NAME: wordpress
        volumes:
            db_data: {}
- Tạo Container:

        docker-compose up -d

III. Kết quả 

![image](https://user-images.githubusercontent.com/74607192/162566626-6778cbeb-6af3-41c4-8283-6eb1f2664b5f.png)
