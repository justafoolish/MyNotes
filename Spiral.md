



Các bước thực hiện thuật toán



1. Tạo một chương trình có thể xoay một điểm khi biết tọa độ một điểm nhất định

2. Sửa đổi chương trình để thực hiện quay cũng như co với một tỉ lệ r nhất định

3. Thực hiện quay cũng như co với với một tâm quay nhất định

   => Xây dựng được thuật toán tối ưu hóa xoắn ốc



Pseudo code:

```
INPUT:
	m >= 2 # số điểm
	theta # góc quay (0 <= theta <= 2pi)
	r # bán kính xoắn ốc
	k_max # số lần lặp lại tối đa

PROCESS:
	1. Khởi tạo m điểm Xi ngẫu nhiên
	
	2. Đặt điều kiện ban đầu: k = 0; (Chưa thực hiện vòng lặp nào)
	
	3. Tìm điểm Xmin thỏa mãn min(f(Xi))
	
	4. Thực hiện xoay và co tất cả các điểm Xi với Xmin làm tâm quay vừa tìm được ở bước trước và tăng k lên 1 đơn vị
	
	5. Lặp lại quy trình 3 và 4 cho đến khi k = k_max (số lần lặp tối đa)
	
	OUTPUT:
		điểm cực tiểu Xmin
```



#### Code in R

```R
library(magrittr) 
library(dplyr)

soa = function(N, # Số điểm
               x1_d, # Cận trên x1
               x1_u, # Cận dưới x1
               x2_d, # Cận trên x2
               x2_u, # Cận dưới x2
             	 rot, # Số vòng quay
               k_max, # Số lần lặp tối đa
               r # Tốc độ co lại của xoăn ốc
              ) {
  
  x1 = runif(N, x1_d, x1_u)
  x2 = runif(N, x2_d, x2_u)
  
  # Tính góc quay theta
  theta = 2 * pi / rot
  
  # Định ngĩa ma trận xoay
 	A = matrix(c(cos(theta), -sin(theta), sin(theta), cos(theta)), ncol = 2, byrow = T)
  
  
  # Tạo frame dữ liệu
  temp = data.frame(x1, x2) %>% mutate(f = f(x1,x2))
  
  # Quy trình lặp lại
  for(i in 1:k_max){
    # Tìm điểm x thỏa mãn min(f)
    f_min = 
    	temp %>%
    	filter(f == min(f))
    center = c(f_min$x1, f_min$x2)
    
    for(j in 1:N){
      
      x0 = c(temp$x1[j], temp$x2[j])
      
      xk = A %*% (x0-center)
      	xk = center + (r * xk)
      
      temp$x1[j] = xk[1]
      temp$x2[j] = xk[2]
      
    }
    
    # Tính toán lại giá trị x1 và x2
    temp = temp %>% mutate(f = f(x1, x2))
  }
  
  # Kết quả
  output = temp %>% filter(f == min(f))
  return(output)
}

#Run code

N = 50
a = -4
b = 4
k_max = 70
r = .75
rot = 30
f = function(x1, x2){
  ((x1^4 - 16 * x1^2 + 5 * x1) / 2) + ((x2^4 - 16 * x2 ^ 2 + 5 * x2)/2)
}

soa(N,a,b,a,b,rot,k_max,r)
```

