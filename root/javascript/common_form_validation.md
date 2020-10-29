```ts
const checkMap = {
  tel: /^(\(\d{3,4}\)|\d{3,4}-|\s)?\d{7,14}$/,
  phone: /^1[3456789]\d{9}$/,
  smsCode: /^\d{6}$/,
  goodPass: /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,20}$/,
  integerNum: /^-?\d+$/,
  carNo: /^[京津沪渝冀豫云辽黑湘皖鲁新苏浙赣鄂桂甘晋蒙陕吉闽贵粤青藏川宁琼使领A-Z]{1}[A-Z]{1}[A-Z0-9]{4}[A-Z0-9挂学警港澳]{1}$/,
  email: /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/,
  url: /^(https?|ftp|file):\/\//,
};
```

<iframe data-src="https://liaojunjun.github.io/nice/root/javascript/common_form_validation_demo.html" width="100%" height="400"></iframe>
