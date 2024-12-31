## Ruoyi system user unique identifiers can be duplicated leading to denial of service attacks

The ruoyi project, a 6.6k star GitHub project also open sourced on gitee, is vulnerable to a denial of service.In ruoyi system, loginName is a non-repeatable user name, users use loginName for system login. Its reset password interface can cause this field to be duplicated, and a duplicated loginName cannot be logged in, so this vulnerability can cause any user to be unable to log in, including the admin user. The system is set up so that no user can modify the admin user's information to ensure that the user is available, but this can lead to a denial of service attack by preventing the admin user from logging in.

### Version & Reference

ruoyi project 4.8.0

https://gitee.com/y_project/RuoYi

https://github.com/yangzongzhuan/RuoYi

https://ruoyi.vip/

### Vulnerability causes

![1735627081484](./img/1735627081484.png)

Other interfaces ensure the uniqueness of the loginName when changing it, such as the user management interface

![1735627160175](./img/1735627160175.png)

However, when resetting the password, it is not checked and the original loginName is overwritten, so it can be duplicated with other loginNames on the system, including the admin user.

### Vulnerability reproduce & Impact

![1735627296110](./img/1735627296110.png)Attackers need to have user administration privileges after logging in. The red line is the loginName, which cannot be duplicated.

![1735627387561](./img/1735627387561.png)

At this point the admin user can log in.

![1735627444135](./img/1735627444135.png)

Sends a password change message and changes the loginName.

![1735627505899](./img/1735627505899.png)

At this point the admin loginName is duplicated.

![1735627564815](./img/1735627564815.png)

logged into admin again and could not log in.

![1735627608883](./img/1735627608883.png)

Originally, a query to the database should only return one result, but 2 are returned, and authentication fails for login.

This vulnerability requires the attacker to have user management privileges, and the impact is that it can cause any user in the system to be unable to log in, including the admin user, resulting in a denial of service attack. The attacker can make the whole system only he can log in.