# UML
Series về học UML/ Demo các lược đồ thực tế<br/>
Mỗi nhánh trong Repo sẽ là 1 ví dụ/ giải pháp/ project mẫu trong UML

# Tools sử dụng
- DrawIO online trên https://app.diagrams.net/
- PlantUML online trên https://plantuml.com/
- PlantUML được cài đặt ở Local & tích hợp vào Visual Studio Code/ Intellij IDEA

# Folder liên quan trên Windows
```
D:\Projects\UML
```

==============================================================

# Ví dụ [03.SequenceDiagram]
==============================================================

(Tìm hiều về Sequence Diagram)

## Tham khảo
- https://codelearn.io/sharing/sequence-diagram-trong-uml
- https://viblo.asia/p/thiet-ke-sequence-diagram-su-dung-plantuml-924lJB9YlPM

## Ví dụ về Sequence Diagram về việc rút tiền tại cây ATM
```shell
@startuml 
actor User as user 
boundary "Cây ATM" as atm_machine 
database "Server Ngân Hàng" as bank_server 
 
user -> atm_machine: Nhập thẻ 
activate user 
activate atm_machine 
atm_machine -->> user: Yêu cầu mã PIN 
user -> atm_machine: Nhập mã PIN 
atm_machine -> bank_server: Kiểm tra mã PIN 
activate bank_server 
bank_server -->> atm_machine: Xác nhận mã PIN 
deactivate bank_server 
atm_machine -->> user: Hiển thị danh sách lựa chọn 
user -> atm_machine: Nhập lựa chọn 
 
alt Lựa chọn Kiểm tra số dư 
  atm_machine ->  bank_server: Lấy số dư 
  activate bank_server 
  bank_server -->> atm_machine: Trả về số dư 
  deactivate bank_server 
  atm_machine -->> user: Hiển thị số dư 
else Lựa chọn rút tiền 
  atm_machine -->> user: Yêu cầu nhập số tiền 
  user -> atm_machine: Nhập số tiền 
  atm_machine -> bank_server: Kiểm tra số dư 
  activate bank_server 
  bank_server -->> atm_machine: Trả về số dư 
  deactivate bank_server 
  alt Số dư > Số tiền muốn rút 
    atm_machine -> bank_server: Cập nhật số dư 
    activate bank_server 
    bank_server -->> atm_machine: Số dư đã được cập nhật 
    deactivate bank_server 
    atm_machine -->> user: Thông báo "Hãy nhận tiền" 
    user ->  atm_machine: Nhận tiền 
  else Số dư < Số tiền muốn rút 
    atm_machine -->> user: Thông báo "Số dư không đủ để giao dịch" 
  end 
else Hủy 
  atm_machine -->> user: Thông báo "Giao dịch đã bị hủy" 
end 
 
atm_machine -->> user: In hóa đơn 
atm_machine -->> user: Trả thẻ 
user -> atm_machine: Nhận lại thẻ 
atm_machine -->> user: Hiển thị cảm ơn 
destroy atm_machine 
destroy user 
 
deactivate user 
deactivate atm_machine 
 
@enduml
```
![CashFromATM Sequence Diagram](./sequence-diagram/resources/CashFromATM-1.png "CashFromATM")
