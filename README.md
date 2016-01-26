# Ruby-Coding-Convention
Source Code Layout

Mọi người đều nghĩ rằng tất cả style trừ của họ đều thật là khó đọc. Bỏ đi ba chữ ‘trừ  của họ’ và họ có lẽ đúng …

Encode các file của project bằng
``
UTF-8
``

- Sử dụng 2 dấu cách (soft tabs) cho mỗi thụt đầu dòng thay vì dùng tab thông thường (hard tabs – 4 spaces)
``
# bad - four spaces
def some_method
    do_something
end

# good
def some_method
  do_something
end
```

- Sử dụng Unix-style
```
 $ git config --global core.autocrlf true
```

- Không sử dụng ; để phân cách các câu lệnh. Mỗi câu lệnh viết thành một dòng không có dấu ;
- Không viết các function một dòng
```
# bad
  def too_much; something; something_else; end
# good
  def some_method
    body
  end
```
- Có dấu cách trước va sau các phép toán, sau dấu , trước và sau { và truớc }. Ngoại trừ toán tử lũy thừa **
```
sum = 1 + 2
a, b = 1, 2
1 == 2 ? true : false; puts 'Hi'
[1, 2, 3].each { |e| puts e }
e = M * c**2
```
- Không có dấu cách sau ( và [ hay trước ], )
```
some(arg).other
[1, 2, 3].size
1
2
some(arg).other
[1, 2, 3].size
```
- Không có dấu cách sau !
```
# good
!something
```
- Trong lệnh when ... case, when cần được thụt dòng ngang với case. Có thể một số người không đồng tình với quan điểm này, nhưng đó cũng là style trong 2 cuốn sách ‘The Ruby Programming Language’ và ‘Programming Ruby’
```
 # bad
  case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration == 120
      puts 'Too long!'
    when Time.now.hour == 21
      puts "It's too late"
    else
      song.play
  end

  # good
  case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration == 120
    puts 'Too long!'
  when Time.now.hour == 21
    puts "It's too late"
  else
    song.play
  end
```

- Khi gán biến theo một câu lệnh if ... else ... end hay case ... when ... else ... end, hãy chú ý để các nhánh được thẳng
```
# bad - pretty convoluted
kind = case year
when 1850..1889 then 'Blues'
when 1890..1909 then 'Ragtime'
when 1910..1929 then 'New Orleans Jazz'
when 1930..1939 then 'Swing'
when 1940..1950 then 'Bebop'
else 'Jazz'
end

result = if some_cond
  calc_something
else
  calc_something_else
end

# good - it's apparent what's going on
kind = case year
       when 1850..1889 then 'Blues'
       when 1890..1909 then 'Ragtime'
       when 1910..1929 then 'New Orleans Jazz'
       when 1930..1939 then 'Swing'
       when 1940..1950 then 'Bebop'
       else 'Jazz'
       end

result = if some_cond
           calc_something
         else
           calc_something_else
         end
```
- Tránh sử dụng kí tự xuống dòng trong Ruby \ nếu không cần thiết, ngoại trừ nối các string
- Khi các hàm được gọi nối tiếp, hãy đặt dấu . ở dòng thứ 2
```
       # bad - K hiểu đc dòng thứ 2
one.two.three.
  four

# good - chúng ta thấy rõ ràng dòng thứ 2 được gọi từ dòng trên
one.two.three
  .four
```
- Đối với những hàm mà tham biến của nó quá nhiều, chúng ta nên xuống dòng từng tham biến theo một trong hai cách sau
```
 # good
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com',
                   from: 'us@example.com',
                   subject: 'Important message',
                   body: source.text)
  end

  # good (normal indent)
  def send_mail(source)
    Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text
    )
  end
```

- Dóng thẳng các phần tử khi khai báo mảng nếu mảng quá nhiều. Ví dụ như sau:
```
# bad - single indent
menu_item = ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
  "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]

# good
menu_item = [
  "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
  "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"
]
```

- Thêm gạch dưới đối với những số lớn để dễ đọc
```
# bad - how many 0s are there?
num = 1000000

# good - much easier to parse for the human brain
num = 1_000_000
```

Mỗi dòng chỉ nên tối đa 80 kí tự
Không sử dụng dấu cách ở cuối dòng lệnh
Không sử dụng kiểu comment cả một block. Kiểu comment này không đặt được dấu cách trước nó và khó nhận ra đó là những comment như bình thường
```
# bad
== begin
comment line
another comment line
== end

# good
# comment line
# another comment line
```
