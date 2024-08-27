# Tích hợp API mới vào Mina Wallet Adapter

**Mina Wallet Adapter** là một bộ thư viện và thành phần modular được viết bằng TypeScript, giúp tích hợp các ví vào zkApps trên nền tảng Mina Protocol. Hướng dẫn này sẽ đưa bạn qua từng bước để tích hợp một API mới vào Mina Wallet Adapter.

## Source code và tài liệu

- **Mina Wallet Adapter Documentation**: [https://mina-wallet-adapter.github.io/wallet-adapter/docs/intro/](https://mina-wallet-adapter.github.io/wallet-adapter/docs/intro/)

## Hướng dẫn từng bước tích hợp API vào Mina Wallet Adapter

### Bước 1: Xác định chức năng cụ thể của API mới

- **Mục tiêu**: Trước tiên, bạn cần xác định mục tiêu của API. Các chức năng phổ biến có thể bao gồm:

  - **Quản lý giao dịch**: Gửi, nhận, hoặc ký giao dịch.
  - **Truy vấn dữ liệu**: Lấy dữ liệu từ blockchain hoặc từ các dịch vụ khác.
  - **Tính năng tùy chỉnh**: Bất kỳ yêu cầu cụ thể nào mà ứng dụng của bạn cần.

- **Chuẩn bị tài liệu API**: Đảm bảo bạn có tài liệu của API mới, mô tả rõ ràng các endpoint, phương thức HTTP, yêu cầu xác thực, và cách API này tương tác với dữ liệu.

### Bước 2: Thiết lập môi trường phát triển

1. **Clone Mina Wallet Adapter repository**:
   - Clone repository từ GitHub:
   ```bash
   git clone https://github.com/mina-wallet-adapter/wallet-adapter.git
   cd wallet-adapter
   ```
2. **Cài đặt các phụ thuộc**:
   - Cài đặt các package cần thiết bằng Yarn hoặc NPM:
   ```bash
   yarn install
   ```
   or
   ```
   npm install
   ```
3. **Chạy thử nghiệm**:
   - Đảm bảo dự án có thể chạy cục bộ
   ```bash
   yarn dev
   ```

### Bước 3: Tạo Adapter cho API

1.  **Tạo file Adapter mới**:
    - Tạo một file mới trong thư mục packages/wallets/src/adapters/, ví dụ: MyNewAPIAdapter.ts.
    - Trong file này, bạn sẽ hiện thực các phương thức cần thiết như connect, disconnect, signTransaction,... để tương tác với API mới.
2.  **Tạo file Adapter mới**:

    - Kế thừa từ lớp WalletAdapter: Adapter của bạn sẽ kế thừa từ WalletAdapter trong mina-wallet-adapter-core để đảm bảo tính tương thích.
    - Hiện thực các phương thức
      - `connect`: Kết nối API mới với ứng dụng.
      - `disconnect`: Ngắt kết nối khỏi API.
      - `signTransaction`: Thực hiện ký giao dịch.
    - Ví dụ

      ```javascript
      import { WalletAdapter } from "mina-wallet-adapter-core";
      export class MyNewAPIAdapter extends WalletAdapter {
      constructor() {
      super();
      }

           async connect() {
               // Logic kết nối API mới
           }

           async disconnect() {
               // Logic ngắt kết nối API
           }

           async signTransaction(tx) {
               // Logic ký giao dịch
           }
    }
    ```

3.  **Thêm Adapter vào hệ thống**:

- Mở file index.ts trong packages/wallets/src/ và export adapter mới để nó có thể được sử dụng trong ứng dụng zkApp.

```javascript
export * from "./adapters/MyNewAPIAdapter";
```

### Bước 4: Tích hợp UI

1.  **Tạo các thành phần UI mới**:

- Tạo các thành phần UI trong mina-wallet-adapter-ui để người dùng có thể tương tác với API mới. Ví dụ: tạo các nút kết nối, form để gửi giao dịch, hoặc các thành phần hiển thị thông tin.
- Sử dụng các hook có sẵn từ Mina Wallet Adapter như useWallet để quản lý trạng thái ví và các thao tác API.

2.  **Tích hợp UI vào ứng dụng zkApp**:

- Sử dụng các thành phần UI mới trong zkApp để người dùng có thể thực hiện các hành động thông qua API
- Vi dụ

```javascript
import React from "react";
import { useWallet } from "mina-wallet-adapter-ui";

const MyNewAPIButton = () => {
  const { connect, disconnect, connected } = useWallet("MyNewAPIAdapter");

  return (
    <button onClick={connected ? disconnect : connect}>
      {connected ? "Ngắt kết nối API" : "Kết nối API"}
    </button>
  );
};

export default MyNewAPIButton;
```

### 5: Kiểm tra và thử nghiệm

- Thực hiện kiểm thử cục bộ:
  - Kiểm tra toàn bộ các chức năng của adapter mới để đảm bảo chúng hoạt động như mong đợi, bao gồm:
  - Kết nối API: Đảm bảo adapter có thể kết nối thành công với API.
  - Gửi giao dịch: Thực hiện kiểm tra chức năng ký và gửi giao dịch.
  - Truy vấn dữ liệu: Đảm bảo các yêu cầu truy vấn dữ liệu hoạt động tốt.
- Kiểm tra bảo mật:
  - Đảm bảo rằng các kết nối và dữ liệu đều được bảo mật đúng cách.

### 5: Triển khai lên GitHub và ứng dụng thực tế

- Commit các thay đổi:

```sh
git add .
git commit -m "Added MyNewAPIAdapter and integrated UI"
```

- Đẩy mã nguồn lên GitHub:

```sh
git push origin main
```

-Triển khai ứng dụng:
-Sau khi thử nghiệm thành công, triển khai adapter mới và các thành phần UI vào ứng dụng thực tế.

