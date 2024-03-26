create database QL_VeMayBay
go
use QL_VeMayBay

-- T?o b?ng SANBAY
CREATE TABLE SANBAY (
    MaSanBay CHAR(10) PRIMARY KEY,
    TenSanBay VARCHAR(100)
);

-- T?o b?ng MAYBAY
CREATE TABLE MAYBAY (
    MaMayBay CHAR(10) PRIMARY KEY,
    LoaiMayBay VARCHAR(100)
);

-- T?o b?ng TUYENBAY
CREATE TABLE TUYENBAY (
    MaTuyenBay CHAR(10) PRIMARY KEY,
    MaSanBayDi CHAR(10),
    MaSanBayDen CHAR(10),
    FOREIGN KEY (MaSanBayDi) REFERENCES SANBAY(MaSanBay),
    FOREIGN KEY (MaSanBayDen) REFERENCES SANBAY(MaSanBay)
);

-- T?o b?ng CHUYENBAY
CREATE TABLE CHUYENBAY (
    MaChuyenBay CHAR(10) PRIMARY KEY,
    NgayGio DATETIME,
    ThoiGianBay INT,
    SoLuongGheHang1 INT,
    SoLuongGheHang2 INT,
    MaChiTietChuyenBay CHAR(10),
    MaTuyenBay CHAR(10),
    MaMayBay CHAR(10),
    FOREIGN KEY (MaTuyenBay) REFERENCES TUYENBAY(MaTuyenBay),
    FOREIGN KEY (MaMayBay) REFERENCES MAYBAY(MaMayBay)
);

-- T?o b?ng CHITIETCHUYENBAY
CREATE TABLE CHITIETCHUYENBAY (
    MaChiTietChuyenBay CHAR(10) PRIMARY KEY,
    SanBayTrungGian VARCHAR(100),
    ThoiGianDung INT,
    Ghichu TEXT,
    MaChuyenBay CHAR(10),
    FOREIGN KEY (MaChuyenBay) REFERENCES CHUYENBAY(MaChuyenBay)
);

-- T?o b?ng KHACHHANG
CREATE TABLE KHACHHANG (
    CMND CHAR(12) PRIMARY KEY,
    TenKhachHang VARCHAR(100),
    DienThoai VARCHAR(15)
);

-- T?o b?ng NHANVIEN
CREATE TABLE NHANVIEN (
    MaNhanVien CHAR(10) PRIMARY KEY,
    TenNhanVien VARCHAR(100),
    DienThoai VARCHAR(15)
);

-- T?o b?ng HANGVE
CREATE TABLE HANGVE (
    MaHangVe CHAR(10) PRIMARY KEY,
    TenHangVe VARCHAR(100)
);

-- T?o b?ng DONGIA
CREATE TABLE DONGIA (
    MaDonGia CHAR(10) PRIMARY KEY,
    USD DECIMAL(10,2),
    VND DECIMAL(10,2)
);

-- T?o b?ng VECHUYENBAY
CREATE TABLE VECHUYENBAY (
    MaVeChuyenBay CHAR(10) PRIMARY KEY,
    TinhTrangVe VARCHAR(50),
    MaDonGia CHAR(10),
    MaHangVe CHAR(10),
    MaChuyenBay CHAR(10),
    CMND CHAR(12),
    FOREIGN KEY (MaDonGia) REFERENCES DONGIA(MaDonGia),
    FOREIGN KEY (MaHangVe) REFERENCES HANGVE(MaHangVe),
    FOREIGN KEY (MaChuyenBay) REFERENCES CHUYENBAY(MaChuyenBay),
    FOREIGN KEY (CMND) REFERENCES KHACHHANG(CMND)
);

-- T?o b?ng PHIEUDATCHO
CREATE TABLE PHIEUDATCHO (
    MaPhieuDatCho CHAR(10) PRIMARY KEY,
    NgayDat DATE,
    SoGheDat INT,
    CMND CHAR(12),
    MaChuyenBay CHAR(10),
    FOREIGN KEY (CMND) REFERENCES KHACHHANG(CMND),
    FOREIGN KEY (MaChuyenBay) REFERENCES CHUYENBAY(MaChuyenBay)
);

-- T?o b?ng PHIEUDAT_HANGVE
CREATE TABLE PHIEUDAT_HANGVE (
    MaHangVe CHAR(10),
    MaPhieuDatCho CHAR(10),
    PRIMARY KEY (MaHangVe, MaPhieuDatCho),
    FOREIGN KEY (MaHangVe) REFERENCES HANGVE(MaHangVe),
    FOREIGN KEY (MaPhieuDatCho) REFERENCES PHIEUDATCHO(MaPhieuDatCho)
);

-- T?o b?ng HOADON
CREATE TABLE HOADON (
    MaHoaDon CHAR(10) PRIMARY KEY,
    NgayHoaDon DATE,
    ThanhTien DECIMAL(10,2),
    CMND CHAR(12),
    MaNhanVien CHAR(10),
    MaDoanhThuThang CHAR(10),
    FOREIGN KEY (CMND) REFERENCES KHACHHANG(CMND),
    FOREIGN KEY (MaNhanVien) REFERENCES NHANVIEN(MaNhanVien)
);




-- T?o b?ng DOANHTHUTHANG v?i c?t MaHoaDon d? tham chi?u d?n b?ng HOADON
CREATE TABLE DOANHTHUTHANG (
    MaDoanhThuThang CHAR(10) PRIMARY KEY,
    SoLuongVe INT,
    DoanhThu DECIMAL(10,2),
    MaHoaDon CHAR(10),
    FOREIGN KEY (MaHoaDon) REFERENCES HOADON(MaHoaDon)
);
-- T?o b?ng DOANHTHUNAM

CREATE TABLE DOANHTHUNAM (
    MaDoanhThuNam CHAR(10) PRIMARY KEY,
    SoLuongVe INT,
    DoanhThu DECIMAL(10,2),
    MaDoangThuThang CHAR(10),
    FOREIGN KEY (MaDoangThuThang) REFERENCES DOANHTHUTHANG(MaDoanhThuThang)
);
select * from [dbo].[MAYBAY]
select * from[dbo].[SANBAY]
select * from [dbo].[TUYENBAY]
select * from [dbo].[CHUYENBAY]
select * from [dbo].[CHUYENBAY]
select * from [dbo].[CHITIETCHUYENBAY]
select * from [dbo].[KHACHHANG]
select * from[dbo].[NHANVIEN]
select * from[dbo].[HANGVE]
select * from[dbo].[DONGIA]
select * from[dbo].[VECHUYENBAY]
select * from[dbo].[PHIEUDATCHO]
select * from[dbo].[PHIEUDAT_HANGVE]
select * from[dbo].[DOANHTHUTHANG]
select * from[dbo].[DOANHTHUNAM]
