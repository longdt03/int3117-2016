#Báo cáo bài tập tuần 5

##Mô tả bài toán
* Kiểm tra xem 1 chuỗi có thỏa mãn yêu cầu là 1 tên đăng nhập hay không?
* Tên đăng nhập là chuỗi thỏa mãn:
	* Có độ dài 4-16 kí tự chữ thường, hoa hoặc số
	* Kí tự bắt không được là số
	* Không chứa các kí tự đặc biệt

##Phương thức cần kiểm thử
```java
	public String test(String s){
			
	        int index=1;
	        int start = s.charAt(0);
	        
	        boolean DieuKien1=(s.length()>=4 && s.length()<=16);
	        
	        boolean DieuKien2=((start>=97 && start<=122) || (start>=65 && start<=90));
	        	        
	        if(DieuKien1 && DieuKien2){
	            
	            while(index <= s.length()){
	            	
	                int check = s.charAt(index);
	                
	                if((check>=48 && check<=57) || (check>=97 && check<=122) || (check>=65 && check<=90)); 
	                else{
	                    break;
	                }
	                
	                if(index+1 == s.length()){
	                    return "Ok! Ten dang nhap hop le";
	                }
	                index++;
	            }
        }
        return "Error! Ten dang nhap khong hop le";
    }
```
Biểu thức Branch:
```
(check>=48 && check<=57) || (check>=97 && check<=122) || (check>=65 && check<=90)
```	

##Áp dụng tiêu chuẩn MCDC
* Phân tích: Trong bài toán trên, trước khi đi đến quyết định chuỗi nhập vào là tên đăng nhập hay không, ta sẽ xét qua 2 bộ điều kiện chính:
	* Thỏa mãn cả điều kiện 1(DieuKien1) - tức là độ dài chuỗi và điều kiện 2 (DieuKien2) - kí tự bắt đầu
	* Khi đã thỏa mãn cả 2 điều kiện (DieuKien1 && DieuKien2) ta sẽ tiến đến việc kiểm tra từng kí tự có phải là kí tự đặc biệt hay không?

* Cho cụm điều kiện thứ nhất:

\#       | DieuKien1| DieuKien2| DieuKien1 && DieuKien2
-------|------------|------------|---------------------------|
1.       |T                |T                | T
2.       |T                |F                | F
3.       |F                |T                | F
4.       |F                |F                | F

Từ bảng trên ta có thể xây dựng 3 test cases #2 #3 (#1 và #4 không cần thiết vì cả 2 ĐK đúng (sai) thì tất nhiên kết quả  && cũng sẽ đúng(sai))

* Cho cụm điều kiện thứ hai:
	*(check>=48 && check<=57) cond1 
	*(check>=97 && check<=122) cond2 
	*(check>=65 && check<=90) cond3

\#      | Cond 1 | Cond 2 | Cond 3| Branch
-------|--------|--------|-------|-------|
1.       |T       |T       | T     |T
2.       |T       |F       | F     |T
3.       |T       |T       | F     |T
4.       |T       |F       | T     |T
5.       |F       |F       | F     |F
6.       |F       |T       | T     |T
7.       |F       |F       | T     |T
8.       |F       |T       | F     |T

Từ bảng trên ta xây dựng các test cases ứng với #2 #7 #8 (1 cái đúng, 2 cái sai) và #5 (cả 3 đều sai)

##Unit Test cho các ca kiểm thử
```java
	@Test
	public void test0() {
		String s= "nht";
		String expResult= "Error! Ten dang nhap khong hop le";
		String result = name.test(s);
		assertTrue(expResult==result);
	}
	
	@Test
	public void test1() {
		String s= "1nhtu08051995";
		String expResult= "Error! Ten dang nhap khong hop le";
		String result = name.test(s);
		assertTrue(expResult==result);
	}
	
	@Test
	public void test2() {
		String s= "n123456789";
		String expResult= "Ok! Ten dang nhap hop le";
		String result = name.test(s);
		assertTrue(expResult==result);
	}
	
	@Test
	public void test3() {
		String s= "nGUYENHUUTU";
		String expResult= "Ok! Ten dang nhap hop le";
		String result = name.test(s);
		assertTrue(expResult==result);
	}
	
	@Test
	public void test4() {
		String s= "nguyenhuutu";
		String expResult= "Ok! Ten dang nhap hop le";
		String result = name.test(s);
		assertTrue(expResult==result);
	}
	
	@Test
	public void test5() {
		String s= "n#$%h&&t(";
		String expResult= "Error! Ten dang nhap khong hop le";
		String result = name.test(s);
		assertTrue(expResult==result);
	}
```

##Đo mức dộ bao phủ
![co_incode](https://github.com/ducanhk58uet/int3117-2016/blob/master/NguyenHuuTu/BT2/img/co_incode.PNG?raw=true)
![co_intest](https://github.com/ducanhk58uet/int3117-2016/blob/master/NguyenHuuTu/BT2/img/co_intest.PNG?raw=true)
  