

### Lý Thuyết

---

1. Mục tiêu an toàn bảo mật

- **Tính bí mật:** Đảm bảo thông tin không bị truy cập bất hợp pháp
- **Tính toàn vẹn:** Đảm bảo thông tin không bị sửa đổi bất hợp pháp
- **Tính sẵn dùng:** Tài sản luôn sẵn sàng được sử dụng bởi những người có thẩm quyền
- **Tính xác thực:** Đảm bảo dữ liệu nhận được chắc chắn là dữ liệu ban đầu
- **Tính không chối từ:** Đảm bảo người gửi hoặc người nhận không thể chối bỏ tránh nhiệm khi gửi hoặc nhận thông tin



2. Theo luật của Kirchoff thì độ an toàn của hệ mã phụ thuộc vào yếu tố: **Khóa**



3. Tính chiến lược an toàn thông tin:

* **Giới hạn quyền hạn tối thiểu:** Theo nguyên tắc này bất kỳ đối tượng nào cũng chỉ có quyền hạn nhất định với mỗi tài nguyên trên mạng
* **Bảo vệ theo chiều sâu:** Không nên dựa vào một chế độ an toàn dù chúng rất mạnh, mà nên tạo nhiều cơ chế an toàn để hỗ trợ lẫn nhau
* **Nút thắt:** Tạo ra một cửa khẩu hẹp và chỉ cho phép thông tin đi vào hệ thống của mình bằng con đường duy nhất chính là cửa khẩu này
* **Điểm nối yêu nhất:** Chiến lược này dựa trên nguyên tắc: "Một dây xích chỉ chắc tại mắt duy nhất, một bức tường chỉ cứng tại điểm yếu nhất"
* **Tính toàn cực:** Các hệ thống an toàn đòi hỏi phải có tính toàn cục của các hệ thống cục bộ
* **Tính đa dạng bảo vệ:** Cần sử dụng nhiều biện pháp bảo vệ khác nhau cho các hệ thống khác nhau nên không nếu một hệ thống bị tấn công dẫn đến các hệ thống khác dễ dàng bị tấn công theo. 



4. Ứng dụng của mật mã bao gồm: **Bảo mật dữ liệu, xác thực toàn vẹn thông tin, chữ ký số và quản lý khóa**



5. Các cách tăng sự an toàn của bản rõ trong hệ mã: **Nén bản rõ, che giấu mối quan hệ giữa bản rõ và bản mã, tăng sự phụ thuộc giữa bản mã và bản rõ**



6. Các yếu tố không ảnh hưởng đến sự an toàn của một hệ mật mã: **Độ dài bản mã**



7. Lược đồ của một hệ mật mã có: **5 tập khác nhau**



8. SKC: **Hệ mã hóa đối xứng**



9. PKC: **Hệ mã phi đối xứng**



10. Phương pháp chính cho việc mã hóa và giải mã: **Mã hóa đối xứng, công khai và hàm băm**



11. Để che giấu sự dư thừa thông tin bản rõ: **Bản mã có sự lộn xộn và rườm rà**



12. Hệ mã an toàn tuyệt đối nếu: **Khóa có độ dài tối thiểu là tương đương độ dài thông báo**



13. Entropy được hiểu là: **Đo khối lượng thông tin của thông điệp**



14. Nghịch đảo của một số nguyên a trong tập Zn là số: Tồn tại theo điều kiện



> Điều kiện đồng dư 2 số a và b với n: (a - b) chia hết cho n



17. Tập giá trị của Z26 có bao nhiêu phần tử khả nghịch: **12**



### Thực hành

---

| A    | B    | C    | D    | E    | F    | G    | H    | I    | J    | K    | L    | M    | N    | O    | P    | Q    | R    | S    | T    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   | 15   | 16   | 17   | 18   | 19   |



| U | V | Q | X | Y | Z |
| -- | -- | -- | -- | -- | -- |
| 20 | 21 | 22 | 23 | 24 | 25 |

> Khả nghịch Z26 = 1 3 5 7 9 11 15 17 19 21 23 25

1. Affine:

   ```
   𝑒k 𝑥 = ax + b mod 26
   𝑑k 𝑦 = 𝑎−1(y-b) mod 26
   ```

   23. P = KE = { 10, 4 } || a = 1 b = 3 => NH

   A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

​		=> e = 10 x 1 + 3 = 13 % 26 = 13

​				= 4 x 1 + 3 = 7 % 26 = 7





2. Vigenere

   ```
   𝑒k(𝑥1,𝑥2,...,𝑥𝑚)=(𝑥1 +𝑘1, 𝑥2 + 𝑘2,...,𝑥𝑚 +𝑘𝑚) 
   𝑑k(𝑦1,𝑦2,...,𝑦m)=(𝑦1 − 𝑘1,𝑦2 − 𝑘2,...,𝑦m −𝑘m)
   
   ▪ m = 6 và keyword là CIPHER
   ▪ Suy ra, khóa k = (2, 8, 15, 7, 4, 17)
   ▪ Cho bản rõ: thiscr yptosy stemis notsec ure
   Vậy bản mã là: “vpxzgi axivwo ubttmj pwizit wzt”
   ```

   25. P = VANODO, K = MIN

   V + M = 33 % 26 = 7 = H

   A + I = 8 = I

   N + N = 26 % 26 = 0 = A

   O + M = 26 = A

   D + I = 11 = L

   O + N = 27 % 26 = 1 = B
   
   => HIAALB



3. Hill 

   ```
   ```

   