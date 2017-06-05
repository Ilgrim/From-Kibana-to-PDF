# Export Kibana dashboard to PDF
How to convert Kibana dashboard to PDF using wkhtmltopdf

## Requirements
```bash
$ apt-get update
$ apt-get install libxrender1 libxrender-dev libfontconfig1 libfontconfig1-dev
```

## Download wkhtmltopdf
```bash
$ cd /opt/
$ wget "https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz"
$ tar xvfJ wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
```

## From Kibana
![Imgur](http://i.imgur.com/uCvb0Yw.png)


```html
<iframe src="https://10.19.19.1:5601/app/kibana#/dashboard/4c4e48e0-49fa-11e7-829d-434826ef4a7e?embed=true&_g=(refreshInterval%3A(display%3AOff%2Cpause%3A!f%2Cvalue%3A0)%2Ctime%3A(from%3Anow%2Fd%2Cmode%3Aquick%2Cto%3Anow%2Fd))" height="600" width="800"></iframe>
```

```html
<html>
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="utf-8">
   <meta http-equiv="X-UA-Compatible" content="IE=edge">
   <meta name="viewport" content="width=1024">
   <title>Kibana</title>
</head>
<body>
   <!-- PASTE KIBANA IFRAME HERE --> 
   <iframe style="border:none; width:1200px;" src="https://10.19.19.1:5601/app/kibana#/dashboard/4c4..."></iframe>
   <!-- PASTE KIBANA IFRAME HERE --> 
</body>
</html>
```

## Run wkhtmltopdf
```bash
/root/src/wkhtmltox/bin/wkhtmltopdf -O Landscape --stop-slow-scripts --javascript-delay 10000 "http://10.19.19.1:5601/goto/b4d6701f2d7388fc9acb32da3e4e0f01?embed=true" ./console.pdf
```
