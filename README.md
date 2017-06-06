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
Select your Kibana dashboard and click on *Share* -> *Copy* embedded iframe
![Imgur](http://i.imgur.com/uCvb0Yw.png)

<br>

In your clipboard you'll have the iframe syntax, something like this:
```html
<iframe src="https://10.19.19.1:5601/app/kibana#/dashboard/..." height="600" width="800"></iframe>
```
<br>

Now, we need to create an HTML page in which include the Kibana iframe, and then parse it with wkhtmltopdf. Is important to edit the iframe syntax including a static with, a static height and removing the iframe border. For example:
`<iframe style="border:none; width:1200px; height:800px;" ...`. Go to your webserver root directory and create a `kibana.html` that contains:
```bash
$ cd /var/www/html
$ nano -w kibana.html
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
   <title>Kibana</title>
</head>
<body>

   <!-- PASTE KIBANA IFRAME HERE --> 
   <iframe style="border:none; width:1200px; height:800px;" src="https://10.19.19.1:5601/app/kibana#/dashboard/..."></iframe>
   <!-- PASTE KIBANA IFRAME HERE -->
   
</body>
</html>
```
<br>

## Run wkhtmltopdf
```bash
$ cd /var/www/html
$ /opt/wkhtmltox/bin/wkhtmltopdf -O Landscape --stop-slow-scripts --javascript-delay 10000 "http://127.0.0.1/kibana.html" ./kibana_dashboard.pdf
```

Now you can download your PDF from `http://127.0.0.1/kibana_dashboard.pdf`

<br>

## Hope this can help :bowtie:
> theMiddle<br>https://secthemall.com
