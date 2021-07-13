LINK BÀI LAB: https://www.vulnhub.com/entry/tech_supp0rt-1,708/


Tiến hành Scan:

![image](https://user-images.githubusercontent.com/72652376/125455037-800ed3c7-a3c0-4718-9959-95f5f366b33f.png)

![image](https://user-images.githubusercontent.com/72652376/125455166-7331870b-4fd5-402c-b463-bae97236ed8e.png)

/test:

![image](https://user-images.githubusercontent.com/72652376/125455275-68481291-92f7-406d-a7f9-ea76bfb2ef88.png)

/wordpress:

![image](https://user-images.githubusercontent.com/72652376/125455442-fc5a5db2-a6c4-48d1-84ee-79b8375c32e2.png)

Sử dụng enum4linux scan các dịch vụ smb thu được thư mục share trong mạng:

![image](https://user-images.githubusercontent.com/72652376/125455529-e7e85e32-5286-47c7-8da8-49ad71a398c2.png)


![image](https://user-images.githubusercontent.com/72652376/125455787-daf5cfb1-1e97-4faf-8055-96d2b01155dd.png)

Thấy file enter.txt, get về máy xem có thông tin gì không

![image](https://user-images.githubusercontent.com/72652376/125455935-ad769f51-5ae2-4c87-b957-4bc70ea59363.png)

Có thể thấy user và pass được đề cập là được "nấu" với magical. Tiến hành giải mã xem nó có gì

![image](https://user-images.githubusercontent.com/72652376/125456943-b88dd54b-e212-405d-907b-cb6da8639823.png)


Thư này đề cập đến một thư mục ẩn /subrion, thử truy cập nhưng luôn bị chuyển hướng:

![image](https://user-images.githubusercontent.com/72652376/125457269-ef5a642b-85a1-4604-8f5d-3affdc6d3c15.png)


Ở thư có đề cập nếu không thể truy cập thì có thể chỉnh sửa sang panel

![image](https://user-images.githubusercontent.com/72652376/125456374-a75760dd-c28f-4207-a301-469007a822ef.png)

Giao diện đăng nhập có hiện phiên bản Subrion CMS 4.2.1

![image](https://user-images.githubusercontent.com/72652376/125456553-1064e59b-7100-4e9a-9213-64b92c525939.png)

Có thể bypass bằng cách upload file RCE với user là pass thu được ở trên

![image](https://user-images.githubusercontent.com/72652376/125457643-c9130afc-7b87-44cd-8786-b26794253578.png)

Modul yêu cầu url user và pass thể thực hiện upload. 

![image](https://user-images.githubusercontent.com/72652376/125457612-500e7856-31b6-4cb6-8b0a-9676083a1b46.png)

RCE thành công 

![image](https://user-images.githubusercontent.com/72652376/125457912-e8ad9b99-6674-4105-a2ed-4cbe85b06dde.png)

Tìm cách up root từ user www-data:

cat /var/www/html/wordpress/wp-config.php;ls -l

Đọc file lưu trữ database của wps để tìm kiếm password

![image](https://user-images.githubusercontent.com/72652376/125460661-6a4e95b0-d350-467b-8879-f3a742e2d39d.png)

![image](https://user-images.githubusercontent.com/72652376/125461225-e73ff2c3-3f6f-449b-aa6d-8b15c9048199.png)

Có 1 user tìm được. Thử đăng nhập vào user này xem có được không:

![image](https://user-images.githubusercontent.com/72652376/125461529-f043f889-5fb5-4756-974d-1446952465d5.png)

Thành công :v 

Kiểm tra xem có quyền gì đặc biệt không

![image](https://user-images.githubusercontent.com/72652376/125461610-32c055be-c972-4fee-a02e-381b103e3540.png)
