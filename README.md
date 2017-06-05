# Export Kibana dashboard to PDF
How to convert Kibana dashboard to PDF using wkhtmltopdf

## Requirements
```bash
apt-get update
apt-get install libxrender1 libxrender-dev libfontconfig1 libfontconfig1-dev
```

## Download wkhtmltopdf
```bash
cd /opt/
wget "https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz"
tar xvfJ wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
```

## From Kibana
![Imgur](http://i.imgur.com/1NJDHyE.png)

```html
<iframe src="http://10.19.19.1:5601/goto/7fe9584bc879a0b1b54474b7df73169b?embed=true" height="600" width="800"></iframe>
```

## Run wkhtmltopdf
```bash
/root/src/wkhtmltox/bin/wkhtmltopdf -O Landscape --stop-slow-scripts --javascript-delay 10000 "http://10.19.19.1:5601/goto/b4d6701f2d7388fc9acb32da3e4e0f01?embed=true" ./console.pdf
```
