# QR Code Generator

## Overview

QR codes are a popular type of two-dimensional barcode.They can store up to 4,296 alphanumeric characters of arbitrary text. This text **can be numerical, alphanumerical or binary**, for example ****URL, contact information, a telephone number. 

QR codes can be read by an optical device with the appropriate software like a totalcross application or even your phone's camera. To see how to make a qrcode reader click [here](https://totalcross.gitbook.io/playbook/apis/barcode-scanner).

## Usage

To generate the QR Code just instantiate a QRCode Image and call the method **`generate(ecc,str)`** passing as parameters the ECC, which is the quality of the generated code \(better in the next topic\) and the text of QRCode. 

See the example below:

{% code title="QRCode\_Sample" %}
```java
import totalcross.qrcode.QRCode;
import totalcross.sys.Settings;
import totalcross.ui.Container;
import totalcross.ui.Control;
import totalcross.ui.ImageControl;
import totalcross.ui.Label;
import totalcross.ui.ScrollContainer;
import totalcross.ui.image.Image;
import totalcross.ui.image.ImageException;
import totalcross.util.UnitsConverter;

public class SampleQRCodeView extends ScrollContainer{
	private String text;
	public void initUI(){
		text = new String ("I am a QRCode :)");					
		QRCode.DEBUG = true;									
		addCard(this, text);									
	}
	
	private Image getImage (String text, int size){
		Image image = new QRCode().generate(QRCode.ECC_QUARTILE, text);
		
		try{
			image = image.getScaledInstance(size, size);		
		}catch(ImageException e){
			e.printStackTrace();
		}
		
		return image;													
	}
	
	private void addCard (Container container, String text){
		int size = (int)(Math.min(Settings.screenWidth, Settings.screenHeight) * 0.8);	
		Image image = getImage(text, size);								
		
		Label label = new Label(text);									
		label.autoSplit = true;
		container.add(label, CENTER, TOP, Control.PARENTSIZE, Control.PREFERRED);		
		container.add(new ImageControl(image), Control.CENTER, Control.AFTER + UnitsConverter.toPixels(Control.DP + 30), size, size);
	}
}

```
{% endcode %}

It is noteworthy that, depending on the type and complexity of the text entered, the version of QRCode generated changes. The choice of the appropriate version for the past text happens internally. To see which version was chosen, simply pass true in the QRCode Debug attribute\(`QRCode.DEBUG = true;`\),as in line 16 of the code above.

### Error Correction Level

The ECC, as commented above, ECC corresponds to Error Correction Level and they are:

| Error Correction Level | Description |
| :--- | :--- |
|  `ECC_LOW` | Allows recovery of up to 7% data loss |
|  `ECC_MEDIUM` | Allows recovery of up to 15% data loss |
|  `ECC_QUARTILE` | Allows recovery of up to 25% data loss |
|  `ECC_HIGH` | Allows recovery of up to 30% data loss |

{% hint style="info" %}
By default, totalcross uses `ECC_QUARTILE`
{% endhint %}

## References

* See more in [https://www.qrcode.com/en](https://www.qrcode.com/en)
* Download the full QRCode generator example [here](https://github.com/TotalCross/QRCode_Sample/)



