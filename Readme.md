# **Stored Procedure Demo**

## **I. Create Database**

1. Khách hàng

```
CREATE TABLE KHACHHANG(
    MAKH            char(4) not null,
    HOTEN           varchar(40),
    DCHI            varchar(50),
    SODT            varchar(20),
    NGSINH          smalldatetime,
    NGDK            smalldatetime,
    DOANHSO         money,
    constraint      pk_kh primary key(MAKH)
)
```

2. Nhân viên

```
CREATE TABLE NHANVIEN(
    MANV            char(4) not null,
    HOTEN           varchar(40),
    SODT            varchar(20),
    NGVL            smalldatetime
    constraint      pk_nv primary key(MANV)
)
```

3. Sản phẩm

```
CREATE TABLE SANPHAM(
    MASP            char(4) not null,
    TENSP           varchar(40),
    DVT             varchar(20),
    NUOCSX          varchar(40),
    GIA             money,
    constraint      pk_sp primary key(MASP)
)
```

4. Hóa đơn

```
CREATE TABLE HOADON(
    SOHD            int not null,
    NGHD            smalldatetime,
    MAKH            char(4),
    MANV            char(4),
    TRIGIA          money,
    constraint      pk_hd primary key(SOHD)
)
```

5. CTHD

```
CREATE TABLE CTHD(
    SOHD            int,
    MASP            char(4),
    SL              int,
    constraint      pk_cthd primary key(SOHD,MASP)
)
```

6. Khóa ngoại

```
-- Khoa ngoai cho bang HOADON
ALTER TABLE HOADON ADD CONSTRAINT fk01_HD FOREIGN KEY(MAKH) REFERENCES KHACHHANG(MAKH)
ALTER TABLE HOADON DROP CONSTRAINT FK01_HD
ALTER TABLE HOADON ADD CONSTRAINT fk02_HD FOREIGN KEY(MANV) REFERENCES NHANVIEN(MANV)
ALTER TABLE HOADON DROP CONSTRAINT FK02_HD

-- Khoa ngoai cho bang CTHD
ALTER TABLE CTHD ADD CONSTRAINT fk01_CTHD FOREIGN KEY(SOHD) REFERENCES HOADON(SOHD)
ALTER TABLE CTHD DROP CONSTRAINT FK01_CTHD
ALTER TABLE CTHD ADD CONSTRAINT fk02_CTHD FOREIGN KEY(MASP) REFERENCES SANPHAM(MASP)
ALTER TABLE CTHD DROP CONSTRAINT FK02_CTHD
```

7. Thêm dữ liệu demo
```
----------------------------- KHACHHANG ---------------------------------------
insert into khachhang values('KH01','Nguyen Van A','731 Tran Hung Dao, Q5, TpHCM','8823451','22/10/1960','22/07/2006',13060000)
insert into khachhang values('KH02','Tran Ngoc Han','23/5 Nguyen Trai, Q5, TpHCM','908256478','03/04/1974','30/07/2006',280000)
insert into khachhang values('KH03','Tran Ngoc Linh','45 Nguyen Canh Chan, Q1, TpHCM','938776266','12/06/1980','08/05/2006',3860000)
insert into khachhang values('KH04','Tran Minh Long','50/34 Le Dai Hanh, Q10, TpHCM','917325476','09/03/1965','10/02/2006',250000)
insert into khachhang values('KH05','Le Nhat Minh','34 Truong Dinh, Q3, TpHCM','8246108','10/03/1950','28/10/2006',21000)
insert into khachhang values('KH06','Le Hoai Thuong','227 Nguyen Van Cu, Q5, TpHCM','8631738','31/12/1981','24/11/2006',915000)
insert into khachhang values('KH07','Nguyen Van Tam','32/3 Tran Binh Trong, Q5, TpHCM','916783565','06/04/1971','12/01/2006',12500)
insert into khachhang values('KH08','Phan Thi Thanh','45/2 An Duong Vuong, Q5, TpHCM','938435756','10/01/1971','13/12/2006',365000)
insert into khachhang values('KH09','Le Ha Vinh','873 Le Hong Phong, Q5, TpHCM','8654763','03/09/1979','14/01/2007',70000)
insert into khachhang values('KH10','Ha Duy Lap','34/34B Nguyen Trai, Q1, TpHCM','8768904','02/05/1983','16/01/2007',67500)
 
----------------------------- NHANVIEN ---------------------------------------
insert into nhanvien values('NV01','Nguyen Nhu Nhut','927345678','13/04/2006')
insert into nhanvien values('NV02','Le Thi Phi Yen','987567390','21/04/2006')
insert into nhanvien values('NV03','Nguyen Van B','997047382','27/04/2006')
insert into nhanvien values('NV04','Ngo Thanh Tuan','913758498','24/06/2006')
insert into nhanvien values('NV05','Nguyen Thi Truc Thanh','918590387','20/07/2006')
 
----------------------------- SANPHAM ---------------------------------------
insert into sanpham values('BC01','But chi','cay','Singapore',3000)
insert into sanpham values('BC02','But chi','cay','Singapore',5000)
insert into sanpham values('BC03','But chi','cay','Viet Nam',3500)
insert into sanpham values('BC04','But chi','hop','Viet Nam',30000)
insert into sanpham values('BB01','But bi','cay','Viet Nam',5000)
insert into sanpham values('BB02','But bi','cay','Trung Quoc',7000)
insert into sanpham values('BB03','But bi','hop','Thai Lan',100000)
insert into sanpham values('TV01','Tap 100 giay mong','quyen','Trung Quoc',2500)
insert into sanpham values('TV02','Tap 200 giay mong','quyen','Trung Quoc',4500)
insert into sanpham values('TV03','Tap 100 giay tot','quyen','Viet Nam',3000)
insert into sanpham values('TV04','Tap 200 giay tot','quyen','Viet Nam',5500)
insert into sanpham values('TV05','Tap 100 trang','chuc','Viet Nam',23000)
insert into sanpham values('TV06','Tap 200 trang','chuc','Viet Nam',53000)
insert into sanpham values('TV07','Tap 100 trang','chuc','Trung Quoc',34000)
insert into sanpham values('ST01','So tay 500 trang','quyen','Trung Quoc',40000)
insert into sanpham values('ST02','So tay loai 1','quyen','Viet Nam',55000)
insert into sanpham values('ST03','So tay loai 2','quyen','Viet Nam',51000)
insert into sanpham values('ST04','So tay','quyen','Thai Lan',55000)
insert into sanpham values('ST05','So tay mong','quyen','Thai Lan',20000)
insert into sanpham values('ST06','Phan viet bang','hop','Viet Nam',5000)
insert into sanpham values('ST07','Phan khong bui','hop','Viet Nam',7000)
insert into sanpham values('ST08','Bong bang','cai','Viet Nam',1000)
insert into sanpham values('ST09','But long','cay','Viet Nam',5000)
insert into sanpham values('ST10','But long','cay','Trung Quoc',7000)
 
----------------------------- HOADON ---------------------------------------
insert into hoadon values(1001,'23/07/2006','KH01','NV01',320000)
insert into hoadon values(1002,'12/08/2006','KH01','NV02',840000)
insert into hoadon values(1003,'23/08/2006','KH02','NV01',100000)
insert into hoadon values(1004,'01/09/2006','KH02','NV01',180000)
insert into hoadon values(1005,'20/10/2006','KH01','NV02',3800000)
insert into hoadon values(1006,'16/10/2006','KH01','NV03',2430000)
insert into hoadon values(1007,'28/10/2006','KH03','NV03',510000)
insert into hoadon values(1008,'28/10/2006','KH01','NV03',440000)
insert into hoadon values(1009,'28/10/2006','KH03','NV04',200000)
insert into hoadon values(1010,'01/11/2006','KH01','NV01',5200000)
insert into hoadon values(1011,'04/11/2006','KH04','NV03',250000)
insert into hoadon values(1012,'30/11/2006','KH05','NV03',21000)
insert into hoadon values(1013,'12/12/2006','KH06','NV01',5000)
insert into hoadon values(1014,'31/12/2006','KH03','NV02',3150000)
insert into hoadon values(1015,'01/01/2007','KH06','NV01',910000)
insert into hoadon values(1016,'01/01/2007','KH07','NV02',12500)
insert into hoadon values(1017,'02/01/2007','KH08','NV03',35000)
insert into hoadon values(1018,'13/01/2007','KH08','NV03',330000)
insert into hoadon values(1019,'13/01/2007','KH01','NV03',30000)
insert into hoadon values(1020,'14/01/2007','KH09','NV04',70000)
insert into hoadon values(1021,'16/01/2007','KH10','NV03',67500)
insert into hoadon values(1022,'16/01/2007',Null,'NV03',7000)
insert into hoadon values(1023,'17/01/2007',Null,'NV01',330000)
 
----------------------------- CTHD ---------------------------------------
insert into cthd values(1001,'TV02',10)
insert into cthd values(1001,'ST01',5)
insert into cthd values(1001,'BC01',5)
insert into cthd values(1001,'BC02',10)
insert into cthd values(1001,'ST08',10)
insert into cthd values(1002,'BC04',20)
insert into cthd values(1002,'BB01',20)
insert into cthd values(1002,'BB02',20)
insert into cthd values(1003,'BB03',10)
insert into cthd values(1004,'TV01',20)
insert into cthd values(1004,'TV02',10)
insert into cthd values(1004,'TV03',10)
insert into cthd values(1004,'TV04',10)
insert into cthd values(1005,'TV05',50)
insert into cthd values(1005,'TV06',50)
insert into cthd values(1006,'TV07',20)
insert into cthd values(1006,'ST01',30)
insert into cthd values(1006,'ST02',10)
insert into cthd values(1007,'ST03',10)
insert into cthd values(1008,'ST04',8)
insert into cthd values(1009,'ST05',10)
insert into cthd values(1010,'TV07',50)
insert into cthd values(1010,'ST07',50)
insert into cthd values(1010,'ST08',100)
insert into cthd values(1010,'ST04',50)
insert into cthd values(1010,'TV03',100)
insert into cthd values(1011,'ST06',50)
insert into cthd values(1012,'ST07',3)
insert into cthd values(1013,'ST08',5)
insert into cthd values(1014,'BC02',80)
insert into cthd values(1014,'BB02',100)
insert into cthd values(1014,'BC04',60)
insert into cthd values(1014,'BB01',50)
insert into cthd values(1015,'BB02',30)
insert into cthd values(1015,'BB03',7)
insert into cthd values(1016,'TV01',5)
insert into cthd values(1017,'TV02',1)
insert into cthd values(1017,'TV03',1)
insert into cthd values(1017,'TV04',5)
insert into cthd values(1018,'ST04',6)
insert into cthd values(1019,'ST05',1)
insert into cthd values(1019,'ST06',2)
insert into cthd values(1020,'ST07',10)
insert into cthd values(1021,'ST08',5)
insert into cthd values(1021,'TV01',7)
insert into cthd values(1021,'TV02',10)
insert into cthd values(1022,'ST07',1)
insert into cthd values(1023,'ST04',6)
```
Reference: <https://kienthuc24h.com/csdl-bt-thuc-hanh-1-truy-van-sql/>

## **II. Tạo Procedure không tham số**

### 1) Tạo Procedure

- **Bước 1:** Tạo bảng **HOADON2** để lưu trữ kết quả

```
SELECT * INTO HOADON2 FROM HOADON WHERE 1 < 0
```

- **Bước 2:** Tạo thủ tục để chuyển toàn bộ dữ liệu từ bảng HOADON sang HOADON2

```
CREATE PROCEDURE Test1
    AS
    BEGIN
    	DELETE FROM HOADON2
    	INSERT INTO HOADON2 SELECT * FROM HOADON
    END
```

- **Bước 3:** Chạy thủ tục

```
Cách 1: Gọi trực tiếp đến thủ tục cần sử dụng

	Test1

Cách 2: (cách 2 chạy khi thủ tục được gọi đến trong 1 thủ tục khác)

	EXEC Test1
```

- **Bước 4:** Kiểm tra kết quả

```
SELECT * FROM HOADON2
```

### 2) Thay đổi/ Sửa đổi Procedure

`Tạo thủ tục và lấy ra hóa đơn đầu tiên của bảng HOADON và lưu vào bảng HOADON2`

```
ALTER PROCEDURE Test1
	AS
	BEGIN
		DELETE FROM HOADON2
		INSERT INTO HOADON2 SELECT TOP 1 * FROM HOADON
	END
```

### 3) Xóa Procedure

```
DROP PROCEDURE Test1
```

## **III. Tạo Procedure có tham số đầu vào**

### 1) Truyền 1 tham số đầu vào

`Tạo thủ tục để lấy ra các thông tin hóa đơn trong năm 2006`

```
CREATE PROCEDURE Test2(@Year INT)
	AS
	BEGIN
		DELETE FROM HOADON2
		INSERT INTO HOADON2 SELECT * FROM HOADON
		WHERE YEAR(NGHD) = @Year
	END
```

`Thực thi và kiểm tra thủ tục`

```
EXEC Test2 2006

SELECT * FROM HOADON2
```

### 2) Truyền nhiều tham số đầu vào (mỗi tham số cách nhau bởi dấu phẩy)

`Tạo thủ tục để lấy ra các thông tin hóa đơn trong tháng 10 năm 2006`

```
CREATE PROCEDURE Test3(@Year INT,@Month INT)
	AS
	BEGIN
		DELETE FROM HOADON2
		INSERT INTO HOADON2 SELECT * FROM HOADON
		WHERE YEAR(NGHD) = @Year AND MONTH(NGHD) = @Month
	END
```

`Thực thi và kiểm tra thủ tục`

```
EXEC Test3 2006,10

SELECT * FROM HOADON2
```

## **IV. Tạo Procedure có tham số đầu ra**

`Tạo thủ tục đếm số lượng hóa đơn có trong @YEAR và @MONTH, truyền giá trị của thủ tục đó vào biến @Number và in kết quả ra màn hình`

```
CREATE PROCEDURE test4(@Year INT,@Month INT, @Count INT OUTPUT)
	AS
	BEGIN
		SELECT @Count = count(*) FROM HOADON
		WHERE YEAR(NGHD) = @Year AND MONTH(NGHD) = @MONTH
	END
```
`Thực thi và kiểm tra`
```
DECLARE @Number INT

EXEC Test4 2006,10, @Number OUTPUT

SELECT @number
```

## **V. Một số lưu ý**
`Mệnh đề return có nghĩa là trả về giá trị của Procedure nhưng mà là giá trị int, mặc định là 0`
```
Ví dụ: Tạo thủ tục tính tổng 2 số float

CREATE PROCEDURE test5 ( @Var1 FLOAT, @Var2 FLOAT)
	AS 
	BEGIN
		DECLARE @Sum FLOAT
		SET @Sum = @Var1 + @Var2
		RETURN @Sum -- nếu bỏ đi dòng return @Sum này, kết quả trả về của procedure sẽ mặc định là 0.
	END

	DECLARE @Tong FLOAT
	EXEC @Tong = Test5 1.4,6.2
	SELECT @Tong
```
