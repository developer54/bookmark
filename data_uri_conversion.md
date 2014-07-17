### Data URI Conversion

### The the data URI syntax
```
data:[<MIME-type>][;charset=<encoding>][;base64],<data>
```
ere's how an inline, small and encoded SVG image looks like:
```
<img src="data:image/svg+xml;base64,PD94bWwgd..." >
```

and if we deconstruct it:

data - the name of the scheme

image/svg+xml - the content type

base64 - the type of encoding

PD94bWwgd... - the encoded data

data - name of the scheme

### base64 encoding tools

* [b64.io] (http://b64.io/)
* [Data URI Converter] (http://datauriconverter.appspot.com/)
* [AskApache's Base64 encoder/decoder] (http://www.askapache.com/online-tools/base64-image-converter/)
* [Web Coders Tools] ( http://webcodertools.com/imagetobase64converter)
* [Image2Base64] (http://image2base64.wemakesites.net/)
* [duri.me] (http://duri.me/)
* [dataurl.net] (http://dataurl.net/#dataurlmaker)
