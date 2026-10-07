1. Phân tích lỗi
Dòng gây ra lỗi logic là:
heater.power_watt = heater.voltage * heater.current;

Với:
voltage = 220V
current = 35A

nên:
power_watt = 220 × 35 = 7700W

Sau đó chương trình phát hiện:
if (heater.current > 30.0f)

và thực hiện:
heater.is_overloaded = 1;
heater.is_active = 0;

Nhưng không có câu lệnh:
heater.power_watt = 0.0f;

Vì vậy kết quả trở thành:
Trạng thái: TẮT
Công suất: 7700W

=> Sai nghiệp vụ.

2. Bảng Test Cases
Trường hợp kiểm thử	                Dữ liệu đầu vào	                                    Kết quả sai thực tế	                                        Kết quả đúng mong đợi
TC01 - Dòng điện vượt mức an toàn	voltage = 220.0V, current = 35.0A, is_active = 1	Thiết bị chuyển sang TẮT nhưng công suất vẫn là 7700.00W	Thiết bị TẮT, is_overloaded = 1, 
                                                                                                                                                    công suất phải là 0.00W

TC02 - Dòng điện trong mức an toàn	voltage = 220.0V, current = 20.0A, is_active = 1	Không có lỗi, công suất được tính 4400.00W	                Thiết bị BẬT, is_overloaded = 0,
                                                                                                                                                    công suất là 4400.00W