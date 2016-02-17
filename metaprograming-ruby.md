# Introduction
- Link book : [Metaprgraming Ruby pdf book](http://www.mediafire.com/view/zkkznnr1sy9n8on/the_ruby_programming_language.pdf)

- Một số thứ có thể làm với **metaprogramming** trong Ruby.
    - Khi viết 1 chương trình Ruby kết nối tới 1 `hệ thống bên ngoài`(có thể là `web service` hoặc 1 `chương trình Java`)
      - có thể viết 1 `wrapper` lấy bất kỳ `method` nào và routes nó đến `hệ thống bên ngoài`
      - nếu `hệ thống bên ngoài` được thêm method sau đó, `Ruby wrapper` của bạn sẽ ko phải thay đổi mà `wrapper` sẽ hỗ trợ các method mới đó ngay vào app của bạn

    - Có thể loại bỏ trùng lặp code mà Java khó có thể làm được `=>` định nghĩa cho các method giống nhau

    - Có thể chỉ dùng **Ruby** để `uốn` cú pháp cho đến khi gần giống 1 ngôn ngữ cụ thể nào đó cho vấn đề của bạn

    - .v.v..

#### *M* Word
Có một số định nghĩa cần nhớ trong **Metaprograming**
##### - `Metaprogramming is writing code that writes code`
  - => dùng code để sinh ra code

##### - Với Ruby `=>` runtime giống như 1 **busy marketplace**
  - `=>` hầu hết các cấu trúc ngôn ngữ vẫn còn sau khi biên dịch xong `job` (không giống như C++)

##### - `Metaprogramming is writing code that manipulates language constructs at runtime`
  - Không viết các `method` `accessor` cho từng thuộc tính của `class`
  - Viết code định nghĩa các `method` trong thời gian chạy cho bất kỳ `class` nào kế thừa `ActiveRecord::Base`
