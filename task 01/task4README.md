# BÁO CÁO
# NGUỒN THAM KHẢO :[tào lao](http://bit.ly/2iryedL)
#NGƯỜI THỰC HIỆN : DƯƠNG XUÂN QUIN
---

>#Chương 6 :CÁC LỆNH ĐIỀU KHIỂN RẺ NHÁNH.
>##MỤC LỤC
>[**I.Một ví dụ về lệnh nhảy.**](#I)

>[**II.Các lệnh nhảy có điều kiện**](#II)

>[**III.Cấu trúc ngôn ngữ bậc cao.**](#III)<ul>
>    <li>[1.Các cấu trúc rẽ nhánh.](#III.1)</li>
>    <li>[2.Các cấu trúc lặp.](#III.2)</li></ul>
---
##I.Một số ví dụ về lệnh nhảy.<a name="I"></a>
**Chương trình PGM6_1.ASM**

```sh
1: TITLE  PGM6_1:Hiển thị các ký tự IBM.
2: .MODEL SMALL
3: .STACK 100H
4: .CODE
5: MAIN PROC
6:       MOV AH,2        ; hàm hiển thị ký tự
7:       MOV  CX,256     ; số ký tự được hiển thị
8:       MOV DL,O        ;DL chứa mã ASCII
9:  PRINT_LOOP:
10:      INT 21h         ; hiển thị một ký tự
11:      INT DL          ; tăng mã ASCII
12:      DEC CX          ; giảm bộ đếm
13:      JNZ PRINT_LOOP  ;lặp lại nếu CX khác 0
14:;trở về DOS
15:      MOV AH,4ch
16:      INT 21H
17:MAIN  ENDP
18:     END MAIN.     
```
**Lưu ý**: PRINT_LOOP là nhân dòng lệnh lần đầu tiên chúng ta sử dụng trong một chương trình. Các nhãn cần thiết khi một lệnh trỏ đến lệnh khác giống như trong trường hợp trên. Nhãn kết thúc bằng dấu hai chấm và để dễ nhận ra, chúng được đặt riêng trong một dòng. Các nhãn tham trỏ tới lệnh ngy sau chúng.
##II.Các lệnh hảy có điều kiện.<a name="II"></a>

JNZ là một ví dụ của lệnh **nhảy có điều kiện**.Cú pháp:
             
             `JNZ          nhãn_đích`

**Phạm vi của lệnh nhảy có điều kiện**
    
    cấu trúc mã máy của lệnh nhảy có điều kiện đòi hỏi nhãn_đích phải đứng trước lệnh nhảy không quá 126 byte hoặc đứng sau không quá 127 byte.

**Bảng 6.1. Các lệnh nhảy có điều kiện.**

**Các lệnh nhảy có dấu.**

```sh
Ký hiệu         Chức năng                                Điều kiện nhảy


JG/JNLE         nhảy nếu lớn hơn                         ZF=0 và SF=OF
                nhảy nếu không nhỏ hơn hay bằng           



GE/JNL          nhảy nếu lớn hơn hay bằng                SF=OF
                nhảy nếu không nhỏ hơn



JL/JNGE         nhảy nếu nhỏ hơn                         SF<>OF
                nhảy nếu không lớn hơn hay bằng



JLE/JNGE        nhảy nếu nhỏ hơn hay bằng                ZF=1 hay SF=OF
                nhảy nếu không lớn hơn

```

**Các lệnh nhảy không dấu.** 
```sh
Ký hiệu     Chức năng                                Điều kiện nhảy


JA/JNBZ         nhảy nếu lớn hơn                         CF=0 VÀ ZF=0
                nhảy nếu không nhỏ hơn hay bằng 


JAE/JNB         nhảy nếu lớn hơn hay bằng                CF=0               
                nhảy nếu không nhỏ hơn


JB/JNAE         nhảy nếu nhỏ hơn                         CF=1
                nhảy nếu không lớn hơn hay bằng     


JBE/JNA         nhảy nếu nhỏ hơn hay bằng                CF=1 hay ZF=1
                nhảy nếu không lớn hơn    
```


**Các lệnh nhảy điều kiện đơn.**

```sh
Ký hiệu          Chức năng                                Điều kiện nhảy


JE/JZ            nhảy nếu bằng                              ZF=1
                 nhảy nếu bằng không  


JNE/JNZ          nhảy nếu không bằng                        ZF=0
                 nhảy nếu khác 0

JC               nhảy nếu có nhớ                            CF=1


JNC              nhảy nếu không nhớ                         CF=0 


JO               nhảy nếu nếu tràn                          OF=1


JNO              nhảy nếu không tràn                        OF=0


JS               nhảy nếu dấu âm                            SF=1



JNS              nhảy nếu dấu dương                         SF=0



JP/JPE           nhảy nếu cờ chẵn                           PF=1



JNP/JPO          nhảy nếu cờ lẻ                             PF=0
```

**Dịch các lệnh có điều kiện.**

Người lập trình không cần thiết phải suy nghĩ nhiềuvề các cờ,bạn có thể chỉ dùng tên của lệnh nhảy để quyết định việc chuyển điều khiển đến nhãn đích.Các lệnh sau:
```sh
                CMP        AX,BX
                JG         BELOW
    Nếu AX lớn hơn BX thì JG sẽ chuyển đến BELOW


               DEC         AX
               JL          THERE
    Nếu nội dung của AX nhỏ hơn 0,điều khiển sẽ được chuyển đến THERE
```
**Làm việc với các ký tự**

**Ví dụ**
    
    Giả sử AX và BX chứa các số có dấu.Hãy viết các lệnh để đưa số lớn nhất 
vào CX

**Trả lời**
```sh
MOV      CX,AX          ; đưa AX vào CX
CMP      BX,CX          ; SX lớn hơn?
JLE      NEXT           ; không, tiếp tục
MOV      CX,BX          ; đúng, đưa BX vào CX
```
##III.Cấu trúc ngôn ngữ bậc cao.<a name="III"></a>
  
  Chúng tôi đã có lần nói rằng cấu trúc nhảy có thể được dùng để thực hiện 
các công việc rẽ nhánh và lặp. Tuy nhiên do các lệnh nhảy quá sơ khai nên râts khó mã hóa một thuật toán nhất là đói với người kới lập trình.

###1.Các cấu trúc rẽ nhánh.<a name="III.1"></a>
  
  Tong các ngôn ngữ bậc cao, các cấu trúc rẽ nhánh của một chương trình để 
chọn ra các đường dẫn khác nhau và phụ thuộc vào các điều kiện.Phần này chúng ta sẽ xem xét ba cấu trúc:

**IF_THEN

```SH
Cấu trúc IF_THEN có thể được khai báo dưới dạng toán tử giả như sau:
      IF điều_kiện
         THEN 
            nhánh_đúng
         END_IF   
Điều kiện AX<0 được kiểm tra bởi lệnh CMP AX,0. Nếu AX không nhỏ hơn 0 ta không phải làm gì cả, JNL được dùng để nhảy qua lệnh NEG AX, nếu điều kiện AX<0 thỏa mãn,chương trình tiếp tục thực hiện lệnh NEG AX.
      IF_THEN_ELSE.
      IF điều_kiện         
    THEN 
         nhánh_đúng
    ELSE
         nhánh_sai
    END_IF          
```

**CASE.**
   
   CASE là một cấu trúc đa nhánh, nó c=kiểm tra các thanh ghi, các biến hay 
các biểu thức với các giá trị riêng rẻ trong miền giá trị. Dạng tổng quát của nó là:
```sh
CASE phát biểu
    giá_trị 1:dòng_lệnh_1
    giá_trị_2:dòng_lệnh_2
    .
    .
    giá_trị n: dòng_lệnh_n
END_CASE    
```

**Các nhánh với điều kiện kép.**
```sh
      Đôi khi điều kiện nhánh của IF hay CASE có dạng:
          điều_kiện_1 AND điều_kiện_2
      hay
          điêu_kiện_1 OR  điều_kiện_2

Ở đây điều_kiện_1 và điều_kiện_2 có thể đúng hoặc sai.Đầu tiên chúng ta hãy xem xét điều kiện ADN (ADN condition), sau đó đến điều kiện OR (OR condition).    

```
###2.Các cấu trúc lặp.<a name="III.2"></a>

**Vòng lặp FOR.**
   
   Đây là một cấu trúc lặp  mà số lần lặp các dọng lệnh đã biết trước (vong 
lặp điều khiển bằng biến đếm ).Dạng mã lệnh giải:
```sh
     FOR số_lần_lặp DO
         các dòng lệnh
     END_FOR  

```

```sh
Ví dụ. Viết một vòng lặp điều khiển bảng biến đếm hiển thị một dòng 80 dấu sao.
Lời giải:
   FOR 80 times DO
       hiển thị'*'
   END_FOR
 Mã lệnh là: 
       MOV     CX,80      ; số các dấu sao được hiển thị
       MOV     AH,2       ; hàm hiển thị ký tự
       MOV     DL,'*'     ; ký tự hiển thị
TOP:
       INT     21h        ; hiển thị một dấu sao
       LOOP    TOP        ; lặp lại 80 lần
       
```
**Vòng lặp WHILE.**

Đây là vòng lặp phụ thuộc vào một điều kiện.Dạng mã lệnh giải:

```sh
    WHILE điều_kiện  DO
      các dong lệnh 
    END_WHILE
```

```sh
Ví dụ. Viết các lệnh để đếm số ký tự trong một dòng.
Lời giải:
   khởi tạo bộ đếm bằng 0,
   đọc một ký tự
   WHILE ký tự <> ký tự để đầu dong DO
      đếm = đếm + 1
      đọc một ký tự
  END_WHILE
Các lệnh là:
      MOV  DX,0              ; DX đếm số ký tự
      MOV  AH,1              ; Chuẩn bị đọc
      INT  21h               ; ký tự trong AL
WHILE_:
       CMP   AL,0Dh          ; CR ?
       JE    END_WHILE       ; đúng, thoát ra
       INC   DX              ; không phải CR, tăng bộ đếm
       INT   21h             ; đọc một ký tự
       JMP   WHILE_          ; lặp lại
END_WHILE
```

**Vòng lặp REPEAT**
    
    Có một vòng lặp có điệu kiện khác đó là vòng lặp REPEAT.dạng mã lệnh 
giải của nó là:

```sh 
     REPEAT 
        các dòng lệnh
     UNTIL điều_kiện   
```

`THE END`
