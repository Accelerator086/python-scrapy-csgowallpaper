# python-scrapy-csgowallpaper

Python 爬取 http://csgowallpapers.com 全站图片

~~~python
# -*- coding: utf-8 -*-

import os
import urllib
import time

headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:69.0) Gecko/20100101 Firefox/69.0'
}

final_folder = './csgowallpaper/'
os.makedirs(final_folder, exist_ok=True)

proxies_v2ray = {
'http':'http://127.0.0.1:10809',
'https':'https://127.0.0.1:10809'
}

opener = urllib.request.build_opener(urllib.request.ProxyHandler(proxies_v2ray))
urllib.request.install_opener(opener)

for n in range(1,2746):
    url_original='https://csgowallpapers.com/include/download_wallpaper.php?id='+str(n)
    if os.access(final_folder+'%s.png'%str(n), os.F_OK):
        print('Jump to existed picture no.{}'.format(n))
    else:
        urllib.request.urlretrieve(url_original,final_folder+'%s.png'%str(n))
        print('Finish downloading picture no.{}'.format(n))
        time.sleep(0.5)
print('Finish!')

~~~
