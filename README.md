# Origin-Snippets

LabTalk, Python and Origin-C snippets to free you hands.

欢迎为Origin-Snippets提供功能改进、代码修补、bug反馈、使用文档和献计献策，让我们一起把Origin-Snippets做的更好！当然也欢迎你对Origin-Snippets项目进行捐助（可以使用支付宝或微信扫码）。

![](donation.png)

1. [Stack Groups in Worksheet](#stack-groups-in-worksheet)

### Stack Groups in Worksheet
LabTalk
```
int nGroups = 3;
int nFields = 3;
for(int i = 1; i <= nGroups; i++)
{
  for(int j = 1; j <= nFields; j++)
  {
    range src = [Book1]Sheet1!wcol((i-1)*nGroups+j);
    range dst = [Book2]Sheet1!wcol(j);
    copy -a src dst;
  }
}
```
<img src="Screenshots/Stack Columns in Single Worksheet.png">

### Remove Links in Worksheet
LabTalk
```
for(int i = 1; i <= wks.ncols; i++)
{
    range rr = !$(i);
    %A = [%H]%(wks.name$);
    dataset ds = %A!$(i);
    rr = ds;
}
```
