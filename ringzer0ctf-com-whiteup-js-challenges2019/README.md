Oke, heyy đây là lần đầu tiên mình viết whiteup cho bản thân và cũng là blog riêng của mình, mong được mọi người ủng hộ =))) Let's go!
## Client side validation is bad! ([Challenge 27](https://ringzer0ctf.com/challenges/27))

Thoạt nhìn qua ta thấy có vẻ như phải đăng nhập mới thấy Flag thì phải =)))) <br/>

![](https://i.imgur.com/Qb5hsO0.jpg)

Oke mình đã đăng nhập thử bằng tài khoản của ringzer0ctf nhưng không được, mình đoán mấy level này chắc view-source là thấy. Dòng 89 có đoạn script submit :v <br/>

![](https://i.imgur.com/qTDr2LX.jpg)

Nói qua thì đây biến `u` là username còn `p` là password xem thêm Jquery tại [đây](https://www.w3schools.com/jquery/html_val.asp)<br/>

Kiểm tra điều kiện bởi `if`, mấy bạn nào theo lập trình vào thiết kế web chắc đã quá rõ rồi :3 mình không nói lại nhiều :v
> var u = 'admin';
> var p = String.fromCharCode(74,97,118,97,83,99,114,105,112,116,73,115,83,101,99,117,114,101);

Đoạn `p` kia được lấy từ bằng mã ASCII ta thu được `JavaScriptIsSecure` <br/>

Oke submit thôi :v

