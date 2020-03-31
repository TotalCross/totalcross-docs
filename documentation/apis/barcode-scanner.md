# Scanner

## Overview

Are you thinking in implements a barcode reader in your app? TotalCross have a simple solution. It is easy to make a Scanner application and there is an example ready to use on GitHub!

## Methods

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">readBarcode(String mode)</td>
      <td style="text-align:left">
        <p>The mode can be one of:
          <br />
        </p>
        <p>1D - for one dimension barcodes
          <br />
        </p>
        <p>2D - for QR codes
          <br />
        </p>
        <p>empty string - for both
          <br />
        </p>
        <p>The parameter &amp;msg:</p>
        <p>You can show a message in display</p>
      </td>
    </tr>
  </tbody>
</table>## How to use

There are two ways to make the scanner.

### With Scandit:

 When we do a Scanner.readBarcode and we set on parameter characters "scandit:" with a String contains the scandit key and the camera be call and will capture the image and set on the label result. You will use like this:

 `scan = Scanner.readBarcode("scandit:" + YOUR_SCANDIT_KEY);`

### With ZXing:

In here, we have a little more work because we need find the barcode's mode, if is a 1D or 2D and just after that, we can write Scanner.readBarcode and set the mode and a message telling the user how scanner the barcode.

`scan = Scanner.readBarcode("mode=" + mode + "&msg=" + msg);`

## References

* See more in [Javadoc](https://rs.totalcross.com/doc/totalcross/io/device/scanner/package-summary.html)
* See a project using scanner on [github](https://github.com/TotalCross/ScanditSample)



