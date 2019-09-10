Oke, heyy đây là lần đầu tiên mình viết whiteup cho bản thân và cũng là blog riêng của mình, mong được mọi người ủng hộ =))) Let's go!
## Client side validation is bad! ([Challenge 27](https://ringzer0ctf.com/challenges/27))

Thoạt nhìn qua ta thấy có vẻ như phải đăng nhập mới thấy Flag thì phải =)))) <br/>

![](https://i.imgur.com/Qb5hsO0.jpg)

Oke mình đã đăng nhập thử bằng tài khoản của ringzer0ctf nhưng không được, mình đoán mấy level này chắc view-source là thấy. Dòng 89 có đoạn script submit :v <br/>

![](https://i.imgur.com/qTDr2LX.jpg)

Nói qua thì đây biến `u` là username còn `p` là password xem thêm Jquery tại [đây](https://www.w3schools.com/jquery/html_val.asp)<br/>

Kiểm tra điều kiện bởi `if`, mấy bạn nào theo lập trình vào thiết kế web chắc đã quá rõ rồi :3 mình không nói lại nhiều :v
> var u = 'admin';
>
> var p = String.fromCharCode(74,97,118,97,83,99,114,105,112,116,73,115,83,101,99,117,114,101);

Đoạn `p` kia được lấy từ bằng mã ASCII ta thu được `JavaScriptIsSecure` <br/>

Oke submit thôi :v

## Hashing is more secure ([Challenge 30](https://ringzer0ctf.com/challenges/30))

Oke, ta thấy 1 form submit password, view-source tiếp :&#62; <br/>

![](https://i.imgur.com/Ysk9bMR.jpg)

Oh, hash password bằng SHA1 `Sha1.hash(p)` đây là cách băm dữ liệu 1 chiều :) bẻ khóa thôi :v [link](https://hashkiller.co.uk/Cracker/SHA1) ta thu được password là `adminz` <br/>
Submitinggg!

## Then obfuscation is more secure ([Challenge 31](https://ringzer0ctf.com/challenges/31))

View-source tiếp :v <br/>

![](https://i.imgur.com/ZQOAmpC.jpg)

Oh, Javascript Obfuscate :)) xài Deobfuscator thôi [https://lelinhtinh.github.io/de4js/](https://lelinhtinh.github.io/de4js/) <br/>

![](https://i.imgur.com/2ToJ3Gp.jpg)

Đừng để ý cái tên biến :P kiểm tra điều kiện chỉ là nối chuỗi thôi mà, pass thu được `02l1alk3` <br/>

Submit zooo :v

## Most Secure Crypto Algo ([Challenge 67](https://ringzer0ctf.com/challenges/67))
View-source :3

![](https://i.imgur.com/Oq3SR3D.jpg)

Nhìn khá đáng sợ nhỉ :B <br/>

> \x68\x34\x78\x30\x72

Ta quan tâm cái username `u` trước nhìn khá đơn giản được encrypt bằng HEX ta thu được `h4x0r` <br/>

Tiếp theo là password `p` thú vị nè :D Cách mã hóa sử dụng AES xem thêm ở [Wiki](https://vi.wikipedia.org/wiki/Advanced_Encryption_Standard)
Trang này sử dụng CryptoJS, thư viện này mình khá là thành thạo :P xem thêm tại [đây](https://cryptojs.gitbook.io/docs/#ciphers) <br/>
- Đầu tiên pass được viết bằng hexa `CryptoJS.enc.Hex` ta chuyển qua string `k.toString()` nên chuỗi string sẽ được chia 4 `256 / 4 = 64` :P
- Sau đó ta cắt chuỗi `substring(0,32)` 32 là 1 nửa của 64

```
var encrypted = CryptoJS.AES.encrypt("Message", key, { iv: iv });
```
- Khởi tạo Vector, không truyền thanh số `key`
- Oke code thôi cho nhanh ;)






