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
