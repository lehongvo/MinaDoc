## Đọc về con mina wallet, xem cách implement API vào nó ntn.
1: dùng mina-wallet-adapter để implement API vào mina wallet       
  Source code: https://mina-wallet-adapter.github.io/wallet-adapter/docs/intro/       
  Đùng sẽ update thêm api API của mình thông qua Mina Wallet Adapter để vào implement API Wallet, sau đó hị sẽ merge vào main thì mina wallet sẽ tự động update       
  Mina Wallet Adapter là một bộ thư viện và thành phần modular được viết bằng TypeScript, được thiết kế để giúp tích hợp các ví vào zkApps trên nền tảng Mina Protocol        
2: Step by step   
     + Bước 1: Xác định chức năng cụ thể của API mới, ví dụ như quản lý giao dịch, truy vấn dữ liệu, hoặc nhưng yêu cầu mới    
     + Bước 2: Tạo Adapter cho API        
          Tạo một adapter mới trong Mina Wallet Adapter để quản lý các thao tác API đến API mới    
     + Bước 3: Tích hợp UI       
          Tạo các thành phần UI cần thiết để người dùng tương tác với ví thông qua API mới. Sử dụng các hook và component của Mina Wallet Adapter.       
More detail and run exmaple: https://github.com/lehongvo/MinaDoc/blob/main/README.md   

## Quá trình tạo bằng chứng zk-SNARK (zk-SNARK Proof Generation)
1. Xây dựng mạch zk-SNARK:
    * Mạch zk-SNARK là  Biểu diễn toán học của vấn đề cần chứng minh, Cái này có thể là một hệ thống phương trình hoặc các phép tính mà bạn cần chứng minh không tiết lộ dữ liệu gốc.
    * Cần xác định các quy tắc và logic mà bạn muốn chứng minh bằng zk-SNARK.
2. Tạo bằng chứng:
    * Sau khi xây dựng mạch, bạn sẽ sử dụng các công cụ  o1js để tạo bằng chứng.
    * Trong Mina Protocol, chỉ cần cung cấp các tham số đầu vào (inputs) cho mạch và nó sẽ tạo ra bằng chứng để chứng minh các tính toán là chính xác.
  3. Nullifier và Expiration thêm vào trong Proof
  Nullifier: Giá trị duy nhất để ngăn chặn sử dụng lại giao dịch.
         Expiration: Điều kiện thời gian hết hạn, giới hạn hiệu lực của bằng chứng

Quá trình xác minh bằng chứng zk (zk-SNARK Proof Verification)
   1: Xác minh bằng chứng
     * Sau khi tạo bằng chứng, bạn cần có khóa xác minh (verification key) để xác minh rằng bằng chứng là hợp lệ mà không cần biết các chi tiết bên trong.
     * Trình xác minh sẽ kiểm tra nullifier và expiration để đảm bảo rằng giao dịch hoặc hành động là hợp lệ và chưa được sử dụng lại.
   2: Sử dụng công cụ xác minh:  
     * Sử dụng j1os/snarkjs hoặc các thư viện khác để xác minh bằng chứng đã được tạo.
     * Trong Mina, bạn có thể sử dụng API để gửi bằng chứng lên blockchain và xác minh nó. 
   3: Triển khai trên Mina Protocol
     * Mina Protocol có tích hợp sẵn các công cụ zk-SNARK giúp bạn dễ dàng tạo và xác minh bằng chứng trong ứng dụng zkApp.
     * Sử dụng o1js để tạo các mạch zk-SNARK phức tạp và tích hợp các tính năng như Nullifier và Expiration để đảm bảo bảo mật.

More detail and run exmaple: https://github.com/lehongvo/MinaDoc/blob/main/README-SNARK.md
