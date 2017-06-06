# Export Kibana dashboard to PDF
How to convert Kibana dashboard to PDF using **wkhtmltopdf**, tested on a Docker container Debian GNU/Linux 8 (jessie).

![Imgur](http://i.imgur.com/wj3VNMt.png)

<br>

## Requirements
- A local **webserver** (`apt-get install nginx`)
- **wkhtmltopdf** [https://wkhtmltopdf.org/](https://wkhtmltopdf.org/)

<br>

## Install wkhtmltopdf
```bash
$ # install required packages
$ apt-get update
$ apt-get install libxrender1 libxrender-dev libfontconfig1 libfontconfig1-dev

$ # download wkhtmltopdf
$ cd /opt/
$ wget "https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz"
$ tar xvfJ wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
```

<br>

## From Kibana
![Imgur](http://i.imgur.com/uCvb0Yw.png)

<br>

```html
<iframe src="https://10.19.19.1:5601/app/kibana#/dashboard/..." height="600" width="800"></iframe>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
   <title>Kibana</title>
</head>
<body>

   <!-- PASTE KIBANA IFRAME HERE --> 
   <iframe style="border:none; width:1200px;" src="https://10.19.19.1:5601/app/kibana#/dashboard/..."></iframe>
   <!-- PASTE KIBANA IFRAME HERE -->
   
</body>
</html>
```

## Run wkhtmltopdf
```bash
/opt/wkhtmltox/bin/wkhtmltopdf -O Landscape --stop-slow-scripts --javascript-delay 10000 "http://10.19.19.1:5601/goto/b4d6701f2d7388fc9acb32da3e4e0f01?embed=true" ./console.pdf
```
