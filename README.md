1. What
 - Spring eureka là một dịch vụ quản lý, đặt tên cho các service, nó cung cấp thông tin của service cho các client muốn tìm kiếm và sử dụng
 

2. Why
 - Khi chúng ta sử dụng microservice mà không sử dụng eureka thì mỗi một service chúng ta sẽ phải code cứng cái địa chỉ IP
 - Điều đó sẽ gặp vấn đề chút vấn đề khi mà service đó thay đổi địa chỉ IP thì khi một người dùng nào đó muốn muốn truy cập tới service đó thì phải vào trong code và thay đổi địa chỉ IP mới. Điều đó khiến cho chúng ta tốn rất nhiều thời gian và nhân lực để xây dựng một ứng dụng microservice
 - Eureka có thể cho ta đăng ký một ứng dụng nào đó theo nhiều phiên bản khác nhau
 - Eureka sẽ tổng hợp tất cả các server đăng ký tạo thành một danh sách và khi một service sử dụng thì có thể truy cập đến các service khác dựa trên danh sách đã đăng ký đó.
 - Điều đó khiến cho một microservice có thể tìm kiếm và kết nối với các service một cách dễ dàng hơn
 - Một service sẽ gửi heartbean cho server trong một khoảng thời gian để thông báo cho server là service đó vẫn còn hoạt động
 - Nếu mà một service không gửi heartbean thì server sẽ xóa thông tin của service đó ra khỏi danh sách đăng ký của server, nếu service đó muốn kết lỗi lại thì server sẽ đăng ký mới cho service đó.
 - Thể hiện một service nào đó có còn hoạt động không thì trên server sẽ đánh dấu là UP nghĩa là service đó vẫn còn hoạt động


3. How
 - Với server chúng ta sẽ add dependencies
 - ![image](https://user-images.githubusercontent.com/103310499/225650091-6a4f9e9d-f058-498a-836c-813c7cfa510a.png)
và cloud
 - ![image](https://user-images.githubusercontent.com/103310499/225650266-a8b50ec1-b165-49ff-b6ef-26f855fe9f5e.png)
 - Chúng ta sẽ sử dụng @EnableEurekaServer để đánh dấu đấy là một server eureka
 - Em sẽ cấu hình eureka server nó như sau:
 - ![image](https://user-images.githubusercontent.com/103310499/225651019-1f144545-2977-4176-ac00-9175c7791d39.png)
 - về phía client chúng ta sẽ add dependencies như sau:
 - ![image](https://user-images.githubusercontent.com/103310499/225651231-9c20f0aa-0602-4e71-afac-608ce624c4cc.png)
và cloud 
 - ![image](https://user-images.githubusercontent.com/103310499/225651365-04506deb-7c4f-4ac5-a3f7-a1bd54bfa72b.png)
 - Về phiên bản cloud mới nhất của spring là 2022.0.1 thì chúng ta sẽ sử dụng @EnableDiscoveryClient để đánh dấu service đó là một Client
 - Cấu hình eureka client như sau 
 - ![image](https://user-images.githubusercontent.com/103310499/225651921-182d8a70-8d7f-4e4e-801a-18247d955da5.png)
 - Để chạy chương trình ta sẽ chạy phía server eureka trước và sau đó tới client
 - Chương trình sau khi được đăng ký với server:
 - ![image](https://user-images.githubusercontent.com/103310499/225652405-4cad970c-4509-41dc-b35d-5222a4a64002.png)
 - Ở đây ta có thể thấy có 2 service được đăng ký bởi em đang cấu hình phía server là eureka.client.service-url:



