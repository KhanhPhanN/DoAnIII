# DoAnIII

File SERVER: server.js
- Tạo server chạy trên local với cổng là 8084
- Xử lý các yêu cầu người dùng
+ Lấy dữ liệu từ elasticsearch
+ Lọc dữ liệu lấy ra các thuộc tính cần sử dụng
+ Nhận yêu cầu tìm kiếm các địa điểm theo category
+ Trả về dữ liệu người dùng yêu cầu (nếu không có dữ liệu trong vùng được chọn sẽ gửi một thông báo cho người dùng




Thư mục views: Lưu trữ các trang giao diện người dùng
- Trang start.js: Giao diện chính của ứng dụng
+ Hiển thị bản đồ
+ Dữ liệu lấy được từ Twitter được hiển thị tại trang này
+ Có một số thành phần khác dành cho category




Thư mục public: Lưu trữ các file về định về css, js hay các file hình ảnh của ứng dụng
- File public/css/main.css     : Định dạng css cho trang start.ejs
- File mục public/js/main.js   : Thêm các mã javascript để gửi, nhận và đổ dữ liệu lên bản đồ
- Thư mục public/image         : Chứa các hình ảnh (cụ thể chứa hình ảnh biểu tượng cho từng category)




Thư mục node_modules: Lưu trữ các module cần thiết có thể được sử dụng trong chương trình



Cơ sở dữ liệu được lưu tại local với cách lấy dữ liệu từ logstash 
File cấu hình của logstash: Dữ liệu hiện tại chỉ được lấy tại nhật bản , các khu vực khác trên thế giới chưa được thực hiện cấu hình để có thể lấy được dữ liệu

input {

    twitter {
    
        consumer_key => "yat6Gf2oCq266HWnLGuIVEX9Y"
        
        consumer_secret => "4K0SGeeW8qZ1sO6ivaujWXfeqK6me0qeWlmNSPNwV7Dd2RHX6E"
        
        oauth_token => "1096331330684502016-LRp9LjblZsthI7ltcINUSkP5TcEMZM"
        
        oauth_token_secret => "JY2HlXgL9BLMsRvO6NCYYB295gx1IBwpI0sDUt6o63id0"
        
        ignore_retweets => true
        
        full_tweet => true
        
        use_samples => false
        
        languages =>["ja"]
        
        locations =>"123,20,154,46"
        
        # locations => "103,8,110,24"
    }
}
output {

    elasticsearch {
    
        hosts => ["localhost:9200"]
        
        index => "locationvn_ls"
        
    }
    stdout {codec => rubydebug}
}

Chạy server elasticsearch bằng cửa sổ cmd dùng 2 câu lệnh trong thư mục bin của thư mục elasticsearch:
1. set JAVA_HOME="link thư mục jre java"
2. elasticsearch

Dữ liệu lấy được sẽ được truy cập thông qua địa chỉ local: localhost:9200/....
 
