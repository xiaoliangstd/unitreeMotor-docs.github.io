---
sort: 1
---

## 线路连接
&emsp;&emsp;我们使用RS-485作为物理层，所谓的物理层就是指使用什么物理现象来表达和传输信息。实际上可以将RS-485等价与一个半双工的串口（UART)。<br>

&emsp;&emsp;RS-485利用两线之间的电位差来传输数字电平。通常两根线都是等长的双绞线，当外界存在干扰会同时对这对线上产生噪声，差分的电平传到电机内部后，由差分运算放大器对输入差分电平做差还原出原始电平，再传入到串口，这使得通信具有很高的抗干扰能力。 <br>
<center>
<table>
    <tr>
        <td colspan="3">
            RS_485 signal states
        </td>
    </tr>
    <tr>
        <td>
            Signal
        </td>
        <td>
            Mark(logic 1)
        </td>
        <td>
            Space(logic 0)
        </td>
    </tr>
    <tr>
        <td>
            A
        </td>
        <td>
            Low
        </td>
        <td>
            High
        </td>
    </tr>
    <tr>
        <td>
            B
        </td>
        <td>
            High
        </td>
        <td>
            Low
        </td>
    </tr>
</table>
</center>
&emsp;&emsp;因为RS-485数据线只有两根，用来两路差分信号传输一路电平，所以同一时刻线路上只能进行一个方向的通信，这也是RS-485是半双工通信的原因，相对的4根数据线全双工差分传输协议是RS-422，但使用RS-485极大的简化了线缆连接，提高了硬件通信可靠性，降低了成本。<br>
&emsp;&emsp;通常半双工通信需要一个主机（上位机）来控制通信节奏，主机发送的运动控制指令中含有目标电机ID信息，这样每个电机收到运动控制指令都会判断ID信息是否符合，符合的电机会将内部的数据信息发送给主机，这样就完成了一轮通信。<br>
&emsp;&emsp;Go-M8010-6电机最大支持一条总线上15个电机(ID 0~14)，总线上不得有ID相同的电机，否则整条总线通讯都会异常，电机ID的配置请参照6.2。<br>
&emsp;&emsp;为了将运动控制指令发送给宇树科技制造的关节电机，我们需要通过串口将指令下发。电机通过 RS-485 接口与上位机进行通信，固定波特率 (Baud Rate)为：4Mbps。为了方便用户使用，我们会提供 USB 转 RS-485 的转接器。<br>
<center>
<img src="../img/connect.PNG" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">线路连接图</div>
</center>
<br>
&emsp;&emsp;如上图所示。提供给用户的接口使用C（XT30(2+2)线缆），连接至B （XT30(2+2)转接板），并通过D（GH1.25-3线缆）连接到A(485转USB模块)并连接到电脑上。<br>
&emsp;&emsp;在通过自己的电脑控制电机时，为了将指令从上位机发送到电机，需要将RS-485 接口通过USB转 RS-485 转接口连接到上位机。在接通24V直流电源后，电机绿色指示灯开始闪烁，说明电机已开机。 
<center>
<img src="../img/go_start.gif" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">绿灯闪烁，电机开机</div>
</center>
<br>
```warning
请在上电前检查供电电源，请勿让供电电源高于30V ，并检查电源供电能力是否充足。
```
