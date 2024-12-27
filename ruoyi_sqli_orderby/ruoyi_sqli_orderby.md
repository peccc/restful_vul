## Ruoyi project sqli injection error messages leak sensitive user information

The ruoyi project is a project on GitHub with 6.6k stars, also open-sourced on gitee, and it has sqli injection in the orderby field, reporting error messages containing sensitive user information

### Version & Reference

ruoyi project 4.8.0

https://gitee.com/y_project/RuoYi

https://github.com/yangzongzhuan/RuoYi

https://ruoyi.vip/

### Vulnerability causes

![1735265076840](.\img\1735265076840.png)

![1735265094094](.\img\1735265094094.png)

The orderby field filters the input, but it is possible to enter non-existent columns and so on, causing errors. The project does not filter the error messages, so sensitive information such as user directories can be leaked.

### Vulnerability reproduce & Impact

![1735264987685](.\img\1735264987685.png)

You can see that the red line portion is the user's local user directory information.

The vulnerability only requires normal user privileges, the harm is information disclosure, and further exploitation requires bypassing its filtering mechanism.