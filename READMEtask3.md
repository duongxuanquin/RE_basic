# BÁO CÁO
# NGUỒN THAM KHẢO :[tào lao](http://bit.ly/2iryedL)
#NGƯỜI THỰC HIỆN : DƯƠNG XUÂN QUIN
---

#Chương 5 :TRẠNG THÁI CỦA BỘ XỬ LÝ VÀ THANH GHI CỜ.
##MỤC LỤC
>[**I.Thanh ghi cờ**](#I)<ul> 
> <li>[1.Các cờ trạnh thái](#I.1)</li>
> <li>[2.Cờ nhớ(Cary Flag-CF)](#I.2)]</li>
> <li>[3.Cờ chẵn lẻ(Parity Flag-PF)](#I.3)</li>
> <li>[4.Cờ nhớ phụ(Auxiliary-AF)](#I.4)</li>
> <li>[5.Cờ Zero(Zero Flag-ZF)](#I.5)</li>
> <li>[6. Cờ dấu(Sign Flag-SF)](#I.6)</li>
> <li>[7.Cờ tràn(Overflow Flag-OF)](#I.7)</li></ul>
>[**II.Hiện tượng tràn**](#II) <ul>
> <li>[1.Các ví dụ về hiện tượng tràn](#II.1)</li>
> <li>[2.CPU đã chỉ ra có hiện tượng tràn như thế nào?](#II.2)</li>
> <li>[3.Làm cách nào CPU biết được có hiện tượng tràn xảy ra ?(Xét về phép công và phép trừ)](#II.3)</li></ul>

>[**III.Sự ảnh hưởng của các lệnh đến các cờ**](#III)
>----
##**I.Thanh ghi cờ**<a name="I"></a>

**1.Các cờ trạng thái**<a name="I.1"></a>
- Bộ xử lý sử dụng cờ này để phản ánh kết quả của một phép tính.
  
- **Chẳng hạn** :Lệnh **SUB AX,AX** được thực hiện cờ ZF sẽ được thiết lập 1 nhờ vậy nó chỉ ra kết quả bằng 0 đã được tạo ra.
  
**2. Cờ nhớ (Carry Flag - CF)**<a name="I.2"></a>

- Được thiết lập 1 khi có từ nhớ từ bit msb trong phép cộng hay có vay vào bít msb trong phép trừ. Ngược lại nó bằng 0.

- Cờ CF cũng bị ảnh hưởng bởi các lệnh quay và dịch .

**3. Cờ chẵn lẻ (Parity Flag-PF)**<a name="I.3"></a>

- Cờ PF được thiết lập 1 nếu byte thấp của kết quả có số chẵn các bit 1 (parity chẵn). Nó bằng 0 neeys byte thấp có số lẻ bit 1 (parity lẻ)

- Ví dụ: kết quả của một phép cộng các word là FFFEh, như vậy byte thấp có 7 bite do đó PF=0.

**4. Cờ nhớ phụ (Auxiliary Flag-AF)**<a name="I.4"></a>

- Được thiết lập 1 neeys có nhớ từ bit 3 trong phép cộng or có vay vào bit 3 trong phép trừ .

- Cờ AF được sd trong các thao tác với số thập phân mã hóa nhị phân số (số BCD) .

**5. Cờ Zero (Zero Flag-ZF).**<a name="I.5"></a>

- Cờ ZF được thiết lập 1 khi kết quả bằng 0 và ngược lại .

**6. Cờ dấu (Sign Flag - SF)**<a name="I.6"></a>

- Được thiết lập 1 khi bit msb của kết quả bằng 1 có nghĩa là kết quả là âm nếu bạn làm việc với số có dấu . Ngược lại **SF** =0 nếu bit msb của kết quả bằng 0 .

**7. Cờ tràn (Overflow Flag - OF)**<a name="I.7"></a>

- Được thiết lập 1 khi xảy ra tràn ngược lại nó bằng 0 , khái niệm tràn sẽ được giải thích sau .

                         CỜ TRẠNG THÁI
                                  
                  Bit       Tên gọi             Ký hiệu
                        
                           0            cờ nhớ                     CF
                         
                           2           cờ chẵn lẻ              PF
                         
                           4           Cờ nhớ phụ              AF
                         
                           6            Cờ Zero                    ZF
                         
                           7             Cờ dấu                    SF
                         

                                      CỜ ĐIỀU KHIỂN
                                  
                           Bit            Tên gọi             Ký hiệu
                         
                            8              Cờ bẫy                   TF
                          
                            9              Cờ ngắt                  IF
                          
                            10                Cờ định hướng             DF
                          
##**II. Hiện tượng tràn.**<a name="II"></a>

>- Là hiện tượng phạm vi của các số biểu diễn trong máy tính có giới hạn ( Một word 16 bit là từ -32768 đến 32767 , với một byte 8 bit thì phạm vi là từ -128 đến 127; đối với số không dấu là từ 0 đến 255 cho một byte ).
>- Hiện tượng tràn sẽ xảy ra khi kết quả phép tính nằm ngoài phạm vi giới hạn và kết quả nhận được bị cắt bớt sẽ không phải là kết quả đúng .

**1. CÁC VÍ DỤ VỀ HIỆN TƯỢNG TRÀN .**<a name="II.1"></a> 

>   Khi chương trình thực hiện thao tác số học như cộng hay trừ, có 4 khả năng xảy ra : (1)không tràn, (2) chỉ tràn có dấu, (3) chỉ tràn không dấu, (4) tràn có dấu và không dấu đồng thời .

**Ví dụ về hiện tượng tràn không dấu nhưng không tràn có dấu .**

+ Giả sử AX chứa FFFh, BX chứa 0001h và lệnh ADD AX,DX được thực hiện. Kết quả nhị phân như sau:

                                  1111  1111    1111    1111
                                  
                        +     0000   0000   0000    0000
                                
                              ---------------------------- 
                            
                                1  0000  0000   0000    0000
                                
+ Xét với các sô không dấu, kết quả đúng phải là 100000h = 65536 nhưng kết quả lại nằm ngoài phạm vi biểu diễn của một word nên còn lại trong thanh ghi AX là 0h như vậy hiện tượng tràn không dấu đã xảy ra.

+ Xét ngược lại với các số có dấu thì kết quả nhận được lại đúng : FFFh= -1 , 0001h =1 vậy tổng chúng bằng 0 . Như vậy rõ rang hiện tương tràn dấu không xảy ra.

**Ví dụ về hiện tương tràn có dấu nhưng lại không tràn không dấu : Giả sử AX và BX cùng chứa 7FFFh, thực hiện cộng ADD AX,BX .**

                                        0111    1111    1111    1111
                                    
                                        0111    1111    1111    1111
                                    
                                        --------------------------------
                          
                                        1111    1111    1111    1110
                                    
+ Trong 2 dạng có và không có dấu 7FFFh đều bằng 32767, bởi vậy trong cả 2 phép cộng đều có kết quả là 65534. Giá trị này nằm ngoài phạm vi của số có dấu , kết quả nhận được là FFFEh = -2, vậy hiện tượng tràn có dấu xảy ra. Tuy nhiên FFFEh = 65534 ở dạng không dấu do vậy không xảy ra hiện tượng tràn không dấu .
  
**2. CPU ĐÃ CHỈ RA CÓ HIỆN TƯỢNG TRÀN NHƯ THẾ NÀO ?**<a name="II.2"></a> 

>-  Bộ xử lý lập cờ OF =1 để báo có hiện tượng tràn dấu và CF =1 để báo có hiện tượng tràn không dấu . Mục đích là để tiến hành những hành động thích hợp, nếu như không có hành động nào xảy ra ngay lập tức thì kết quả của lệnh sau có thể xóa cờ báo tràn .

>-  Bộ xử lý sử dụng kết qả vào cả 2 cách hiểu có dấu và không có dấu cho mỗi thao tác đồng thời thiết lập các cờ CF và OF báo tràn có dấy hay không có dấu một cách tương ứng .

>-  Người lập trình sẽ quy ước kết quả . Nếu làm việc với số có dấu thì chỉ có cờ OF đáng quan tâm trong khi cờ CF bỏ qua, ngược lại với số không dấu thì cờ quan trọng là CF .

**3. LÀM CÁCH NÀO CPU BIẾT ĐƯỢC CÓ HIỆN TƯỢNG TRÀN XẢY RA ? (XÉT VỀ PHÉP CỘNG VÀ PHÉP TRỪ)**<a name="II.3"></a> 

• Hiện tượng tràn không dấu : 

>+  Khi thực hiện phép cộng nó xảy ra khi có nhớ từ bit msb (kq đúng của phép tính lớn hơn số không dấu lớn nhất có thể biểu diễn, đó là FFFh cho một word và FFh cho một byte ).

>+ Đối với phép trừ xảy ra khi có sự vay vào bit msb (kết quả đúng nhỏ hơn 0).

•   Hiện tượng tràn có dấu :

>+ Xét phép công các số cùng dấu, xảy ra khi tổng có dấu khác với dấu của 2 số hạng (Ví dụ khi cộng 7FFFh lại nhận được kết quả là số âm FFFEh ).

>+ Xét phép trừ các số khác dấu cũng như phép cộng các số cùng dấu ; **Ví dụ : A-(-B) = A+B và –A-(+B) = -A + -B.** Tràn xảy ra khi kết quả có dấu khác với dấu chúng ta chờ đợi .

>+ Xét phép công 2 số khác dấu hiện tượng tràn là không thể xảy ra vì** A + (-B) = A-B** và bởi vì A và B là 2 số đủ nhỏ để chứa trong toán hạng đích thì hiệu của chúng tất nhiên không thể vượt qua phạm vi của nó được

>+ Bộ xử lý đã sử dụng phương pháp sau để thiếp lập cờ **OF** : có nhờ vào msb nhưng không có nhớ ra từ nó , hay có nhớ ra từ nó mà không có nhớ vào thì hiện tượng tràn có dấu xuất hiện và **OF** được thiếp lập 1 .

##**III.  SỬ ẢNH HƯỞNG CỦA CÁC LỆNH ĐẾN CÁC CỜ .**<a name="III"></a>

     Chỉ thị                              Các cờ bị ảnh hưởng
   
    MOV / XCHG                          Không cờ nào
  
    ADD /SUB                              Tất cả các cờ
  
    INC / DEC                         Tất cả các cờ trừ cờ CF
  
    NEC                 Tất cả các cờ (CF = 1 trừ khi kết quả là 0 , OF =1 nếu toán hạng word là 8000h
                            hay toán hạng byte là 80h)

**Ví dụ : Thực hiện phép cộng AX, BX trong đó  AX và BX đều chứa FFFFh**

                                            FFFh
                                          + FFFh
                            ----------------------
                                           1FFFh
                                          
>Kết quả thu được chứa trong AX là FFFEh = 1111 1111    1111    1110

>SF =1 vì msb =1

>PF = 0 vì có 7 bit 1(lẻ các bit 1) trong byte thấp của kết quả .

>ZF =0 vì kết quả thu được khác 0

>CF = 1 vì có nhớ từ bit msb trong phép cộng .

>OF =0 vì dấu của tổng nhận được giống như dấu của các số hạng tham gia phép cộng .

**Ví dụ :Thực hiện phép cộng AL , BL trong đó AL và BL cùng chứa 80h .**

                                                80
                                            80
                                             ------ 
                                                100
 
>Kết quả nhận được trong AL bằng 0

>SF =0 vì msb =0

>PF = 1 vì tổng các bit của tổng bằng 0 
.
>ZF =1 vì kết quả thu bằng 0

>CF = 1 vì có nhớ từ bit msb trong phép cộng .

>OF =1 vì các sô hạng tham gia phép cộng đều là các số âm nhưng kết quả nhận được là một số dương .

**Ví dụ : Thực hiện phép trừ AX, BX trong đó AX chứa 8000h còn BX chứa 0001h.**

                                            8000
                                                0001
                                  -           -------  
                                                7FFF
                                              
>Kết quả nhận được trong AX là 7FFFh = 0111 1111    1111    1111

>SF =0 vì msb =0

>PF = 1 vì có 8 bit 1(chẵn các bit 1) trong byte thấp của kết quả .

>ZF =0 vì kết quả thu được khác 0

>CF = 0 vì số không dấu nhỏ hơn bị trừ từ số lớn hơn.

>Về cờ OF, xét về phương diện các số có dấu, chúng ta đã trừ một số dương từ một số âm, cũng giống như cộng 2 số âm. Tuy nhiên kết quả nhận được lại là số dương (sai dấu) do đó OF =1 .

**Ví dụ: Tăng AL lên 1 khi AL chứa FFh .**

                                                FF
                                                 1
                                         --------------
                                               100
                                             
>Kết quả nhận được trong AX là 00h

>SF =0 vì msb =0

>PF = 1 vì tất cả có bit bằng 0 .

>ZF =1 vì kết quả thu được bằng 0

>CF = 0 vì hai số hạng có dấu khác nhau.

**Ví dụ: Chuyển -5 vào AX**

>Kết quả nhận được trong **AX** là **-5 = FFFBh**, không có cờ nào bị ảnh hưởng bởi lệnh **MOV**.

**Ví dụ: Nghịch đảo AX, trong đó AX chứa 8000h .**


                       8000h        1000    0000    0000    0000
               Số bù 1 của 8000h                0111    1111    1111    1111
                                                  +1                                                            
                   ---------------------------------------------------------           
               Số bù 2 của 8000h                1000    0000    0000    0000
               
>Kết quả nhận được trong AX là 1000 0000    0000    0000 = 8000h

>SF =1 vì msb =1

>PF = 1 vì tất cả có bit bằng 0 .

>ZF =0 vì kết quả thu được khác 0

>CF = 1 vì trong lệnh NEG, CF ln bằng 1 trừ khi kết quả bằng 0.

>OF =1 vì kết quả là 8000h, khi lấy nghịch đảo của một số kết quả nhận được phải có dấu ngược lại nhưng ở đây số bù 2 của 8000h lại chính bằng nó tức là dấu không thay đổi .



                            THE END.






