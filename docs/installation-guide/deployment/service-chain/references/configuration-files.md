# Tập tin cấu hình

Tài liệu này giải thích các thuộc tính có thể cấu hình của nút. Gói nút Klaytn có các thuộc tính mặc định tốt và yêu cầu rất ít cấu hình. Nếu bạn thay đổi bất kỳ cài đặt nào của nút đang chạy, bạn phải khởi động lại nút để ánh xạ các thay đổi.

## Vị trí tập tin cấu hình SCN <a id="scn-configuration-file-location"></a>

* `kscnd.conf` để định cấu hình Nút đồng thuận chuỗi dịch vụ

Tập tin cấu hình nằm trong thư mục `conf`, có vị trí mặc định phụ thuộc vào việc cài đặt là từ phân bổ lưu trữ \(`tar.gz`\) hay từ phân bổ gói \(RPM\).

* Đối với việc phân bổ lưu trữ, vị trí thư mục cấu hình mặc định là `$INSTALL_PATH/kscn-linux-amd64/conf/`.
* Đối với việc phân bổ lưu trữ, vị trí thư mục cấu hình mặc định là `/etc/kscnd/conf/`.

## Định dạng tập tin cấu hình  <a id="configuration-file-format"></a>

Dưới đây là tập tin cấu hình mẫu cho SCN lưu trữ dữ liệu blockchain ở vị trí mặc định, `~/kscnd_home` với phân bổ lưu trữ, `/var/kscnd/data` với phân bổ gói.

```text
# Tập tin cấu hình kcnd

NETWORK=
# nếu bạn chỉ định NETWORK_ID, một mạng lưới riêng sẽ được tạo.
NETWORK_ID=
PORT=32323
SERVER_TYPE="fasthttp"
SYNCMODE="full"
VERBOSITY=3
MAXCONNECTIONS=100
# LDBCACHESIZE=10240
REWARDBASE="0x0"

...

DATA_DIR=
LOG_DIR=$DATA_DIR/logs
```

Các quy mô bể giao dịch được đề xuất cho SCN như sau.

```text
TXPOOL_EXEC_SLOTS_ALL=16384
TXPOOL_NONEXEC_SLOTS_ALL=16384
TXPOOL_EXEC_SLOTS_ACCOUNT=16384
TXPOOL_NONEXEC_SLOTS_ACCOUNT=16384
```

## Thuộc tính <a id="properties"></a>

Tập tin cấu hình có các thuộc tính có thể định cấu hình sau. Các tập tin cấu hình SCN, SPN và SEN có cùng thuộc tính.

| Tên                            | Mô tả                                                                                                                                                                                                                                                                                                                   |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NETWORK                        | Tên mạng lưới mà nút này sẽ tham gia vào.  Giá trị này được sử dụng khi NETWORK_ID không được xác định.  ("cypress", "baobab")                                                                                                                                                                                          |
| NETWORK_ID                     | ID mạng lưới Klaytn.  Nếu bạn tạo một mạng lưới riêng cục bộ, bạn sẽ chỉ định ID mạng lưới cho mạng lưới riêng của mình.  Các ID sau được dành riêng cho các mạng lưới được định cấu hình trước.  <br>8217 : Cypress (Mạng lưới chính) <br>1000 : Mạng lưới thử Aspen <br>1001 : Mạng lưới thử Baobab |
| PORT                           | Cổng P2P. (Mặc định: "32323")                                                                                                                                                                                                                                                                                           |
| SERVER_TYPE                    | Loại máy chủ JSON RPC.  ("http", "fasthttp")                                                                                                                                                                                                                                                                            |
| SYNCMODE                       | Chế độ đồng bộ blockchain.  ("nhanh", "đầy đủ")                                                                                                                                                                                                                                                                         |
| VERBOSITY                      | Độ chi tiết ghi nhập ký.  (Cấp độ: 0=im lặng, 1=lỗi, 2=cảnh báo, 3=thông tin, 4=gỡ lỗi, 5=chi tiết)                                                                                                                                                                                                                     |
| MAXCONNECTIONS                 | Số lượng tối đa các kết nối thực.  Tất cả các máy ngang hàng đơn kênh có thể có tối đa MAXCONNECTIONS máy ngang hàng.  Tất cả các máy ngang hàng đa kênh có thể có tối đa MAXCONNECTIONS/2 máy ngang hàng.  Kết nối mạng lưới sẽ bị tắt nếu nó được đặt thành 0. (Mặc định: 10)                                         |
| LDBCACHESIZE                   | Kích thước của bộ đệm trong bộ nhớ trong LevelDB (MiB). (Mặc định : 768)                                                                                                                                                                                                                                                |
| REWARDBASE                     | Địa chỉ tài khoản sẽ nhận phần thưởng đồng thuận khối. Thuộc tính này này chỉ áp dụng cho CN.                                                                                                                                                                                                                           |
| TXPOOL_EXEC_SLOTS_ALL        | Số lượng slot giao dịch có thể thực thi tối đa cho tất cả các tài khoản. (Mặc định: 4096)                                                                                                                                                                                                                               |
| TXPOOL_NONEXEC_SLOTS_ALL     | Số lượng slot giao dịch không thể thực thi tối đa cho tất cả các tài khoản. (Mặc định: 1024)                                                                                                                                                                                                                            |
| TXPOOL_EXEC_SLOTS_ACCOUNT    | Số lượng slot giao dịch có thể thực thi được đảm bảo cho mỗi tài khoản. (Mặc định: 16)                                                                                                                                                                                                                                  |
| TXPOOL_NONEXEC_SLOTS_ACCOUNT | Số lượng slot giao dịch không thể thực thi tối đa được đảm bảo cho mỗi tài khoản. (Mặc định: 64)                                                                                                                                                                                                                        |
| TXPOOL_LIFE_TIME             | Khoảng thời gian tối đa các giao dịch không thể thực hiện được xếp hàng chờ. (Mặc định: 30p cho SEN, 5p cho SCN/SPN)                                                                                                                                                                                                    |
| RPC_ENABLE                     | Kích hoạt máy chủ HTTP-RPC nếu nó được đặt thành 1.                                                                                                                                                                                                                                                                     |
| RPC_API                        | Danh sách API phân tách bằng dấu phẩy được cung cấp trên giao diện HTTP-RPC.  (quản trị, gỡ lỗi, klay, thợ đào, mạng, cá nhân, rpc, txpool, web3)                                                                                                                                                                       |
| RPC_PORT                       | Cổng nghe máy chủ HTTP-RPC. (Mặc định: "8551")                                                                                                                                                                                                                                                                          |
| RPC_ADDR                       | Giao diện nghe máy chủ HTTP-RPC. (Mặc định: "localhost")                                                                                                                                                                                                                                                                |
| RPC_CORSDOMAIN                 | Danh sách miền được phân tách bằng dấu phẩy để chấp nhận các yêu cầu từ nhiều nguồn (trình duyệt thực thi)                                                                                                                                                                                                              |
| RPC_VHOSTS                     | Danh sách tên máy chủ ảo được phân tách bằng dấu phẩy để chấp nhận yêu cầu (máy chủ thực thi). Chấp nhận ký tự đại diện '*'. (Mặc định: {"localhost"})                                                                                                                                                                  |
| WS_ENABLE                      | Kích hoạt máy chủ WS-RPC nếu nó được đặt thành 1.                                                                                                                                                                                                                                                                       |
| WS_API                         | API được cung cấp trên giao diện WS-RPC.  (quản trị, gỡ lỗi, klay, thợ đào, mạng, cá nhân, rpc, txpool, web3)                                                                                                                                                                                                           |
| WS_ADDR                        | Giao diện nghe máy chủ WS-RPC.                                                                                                                                                                                                                                                                                          |
| WS_PORT                        | Cổng nghe máy chủ WS-RPC. (Mặc định : "8552")                                                                                                                                                                                                                                                                           |
| WS_ORIGINS                     | Nguồn gốc để chấp nhận yêu cầu Websocket. (Mặc định: "localhost")                                                                                                                                                                                                                                                       |
| SC_MAIN_BRIDGE               | Kích hoạt cầu nối chính nếu nó được đặt thành 1. Sử dụng cho cấu hình chuỗi dịch vụ.                                                                                                                                                                                                                                    |
| SC_MAIN_BRIDGE_PORT          | Cầu nối chính nghe trên cổng này. (Mặc định : "50505")                                                                                                                                                                                                                                                                  |
| SC_MAIN_BRIDGE_INDEXING      | Kích hoạt lưu trữ hàm băm giao dịch của các giao dịch chuỗi con để truy cập nhanh vào dữ liệu chuỗi con nếu đặt nó là 1.                                                                                                                                                                                                |
| METRICS                        | Kích hoạt bộ sưu tập số liệu và báo cáo nếu đặt nó là 1.                                                                                                                                                                                                                                                                |
| PROMETHEUS                     | Kích hoạt prometheus exporter nếu đặt nó là 1.                                                                                                                                                                                                                                                                          |
| DB_NO_PARALLEL_WRITE         | Hủy kích hoạt việc ghi song song dữ liệu khối vào cơ sở dữ liệu liên tục nếu đặt nó là 1.                                                                                                                                                                                                                               |
| MULTICHANNEL                   | Tạo một kênh chuyên dụng để truyền khối nếu đặt nó là 1.                                                                                                                                                                                                                                                                |
| SUBPORT                        | Lắng nghe số cổng phụ nếu kích hoạt tùy chọn Đa kênh. (Mặc định : "32324")                                                                                                                                                                                                                                              |
| NO_DISCOVER                    | Tắt tùy chọn Khám phá nếu đặt nó là 1.                                                                                                                                                                                                                                                                                  |
| BOOTNODE                       | Địa chỉ kni của các nút bootstrap được phân tách bằng dấu phẩy.                                                                                                                                                                                                                                                         |
| ADDITIONAL                     | Cho các tùy chọn dòng lệnh bổ sung. e.g) --txpool.nolocals                                                                                                                                                                                                                                                              |
| DATA_DIR                       | Đường dẫn thư mục dữ liệu blockchain klaytn.                                                                                                                                                                                                                                                                            |
| LOG_DIR                        | Đường dẫn thư mục nhật ký.                                                                                                                                                                                                                                                                                              |


