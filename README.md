# QRCode For Unity

#### 项目介绍
用于在Unity中生成二维码，能够正确的生成任意分辨率二维码，兼容Ios 和 Android

改工具支持两种模式生成二维码，视情况选择使用.

**普通模式 [QRCodeTool.NormalEncodeQRCode(code, codeSize)]** : 使用简单，一句话搞得，但是在低性能设备上生成复杂二维码可能会卡顿。

**一部模式 [QRCodeTool.EncodeQRCode(code, codeSize)]** : 使用相对麻烦，但不会出现卡顿问题。

以下是两种模式的实际使用：

![生成配置](https://images.gitee.com/uploads/images/2018/1012/145142_6323705d_1511066.png "QQ截图20181012142503.png")

![普通模式](https://images.gitee.com/uploads/images/2018/1012/145206_6cb05472_1511066.gif "GIF.gif")

![异步模式](https://images.gitee.com/uploads/images/2018/1012/145218_a04adc69_1511066.gif "GIF2.gif")

#### 使用说明

普通模式：public Texture2D QRCodeTool.NormalEncodeQRCode(string code , Vector2 vector2)

代码示例：

```
rawImage.texture = codeTool.NormalEncodeQRCode(code, codeSize);
```

异步模式: public void EncodeQRCode(string code , Vector2 vector2)

代码示例:


```
 public void AsyncCreate() {
        if (codeTool.isEncodeing() == false) {
            codeTool.EncodeQRCode(code, codeSize);
            StartCoroutine(getQRCode());
        }
    }

    IEnumerator getQRCode() {
        while (true) {
            if (codeTool.GetQRimage() != null) {
                rawImage.texture = codeTool.GetQRimage();
                break;
            }
            yield return 0;
        }
    }
```

