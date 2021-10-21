# TetCTF 2021 Writeup

Bắt đầu thôi, đây là kì ctf mình thi lần đầu tiên, sau 1 số cuộc thi ctf qua mạng trên ctftime :3 cảm quan qua một chút về giải ctf lần này, mình thấy quy tụ khá là nhiều đội thi mạnh đến từ trong nước và quốc tế, các challenge theo một newbie như mình đánh giá thì rất là hay và chất lượng. Mình tuy chỉ giải được 2 câu web nhưng cx là gọi là "hái lộc đầu năm"😂😂

## 1. Web01 - WYSINWYG

Description: *What you see is not what you get... Do you see the flag? then you don't get the flag.*

```php
<?php
ini_set("display_errors", 0);
include('secret.php');
show_source(__FILE__);
if (isset($_GET['a']) && isset($_GET['b'])) {
    $a = $_GET['a'];
    $b = $_GET['b'];
    if (!empty($a) && !empty($b)) {
        if ($a === $b) {
            if (isset($_GET['a⁡']) && isset($_GET['b⁦'])) {
                $a = $_GET['a⁡'];
                $b = $_GET['b⁦'];
                if ($a !== $b) {
                    die($flag);
                }
            }
        }
    }
}
```

Nhìn qua có vẻ không hợp lí lắm khi ta code kiểm tra 2 lần của 2 bến `$_GET['a']` và `$_GET['b']` nhỉ, nhưng khi dùng IDE hay cụ thể là dùng PHP Storm mình có thể thấy được unicode ở hai biến dòng số 12. Sau đó mình đã urlencode lại để get lấy flag như sau:
POC: `45.77.240.178:8001/?a=1&b=1&a%E2%81%A1=a&b%E2%81%A6=b`