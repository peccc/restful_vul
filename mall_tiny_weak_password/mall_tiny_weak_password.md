## The mall-tiny administrator account has a weak password and can be enumerated.

The mall-tiny project is a small e-commerce platform with 1.9k stars on GitHub. Its login interface can be password-enumerated, and weak passwords exist for the default superadmin.

### Version & Reference

1.0.1

https://github.com/macrozheng/mall-tiny

https://www.macrozheng.com/

https://www.macrozheng.com/admin/index.html#/login

### Vulnerability causes

![1734921589015](./img/1734921589015.png)

The project imports users by default and the test user is a super administrator and has a weak password.![1734921638087](./img/1734921638087.png)

And the login interface can try multiple times without a lock, so an attacker can enumerate passwords

### Vulnerability reproduce & Impact

![img](./img/1734919028534.png)

We use burp suite to burst the interface, you can see that the first can be burst successfully.![1734919118166](./img/1734919118166.png)

Use this password to log in and you will see a successful login.![1734919193100](./img/1734919193100.png)

We checked the user's permissions and found that the user is a super administrator.You can see that we are “超级管理员”, which stands for super user.

The vulnerability could lead to information disclosure and elevation of privilege.