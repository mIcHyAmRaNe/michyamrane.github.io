---
title: "OKadminFinder: Easy way to find admin panel of site"
date: 2021-05-14T15:34:30-04:00
categories:
  - tools
tags:
  - OKadminfinder
---

*OKadminFinder is an Apache2 Licensed utility, rewritten in **Python 3.x**, for admins/pentesters who want to find admin panel of a website. There are many other tools but not as effective and secure. Yeah, Okadminfinder has the the ability to use tor and hide your identity*

* ## Requirements
    ![PyPI](https://img.shields.io/pypi/v/argparse.svg?label=argparse)
    ![PyPI](https://img.shields.io/pypi/v/colorama.svg?label=colorama)
    ![PyPI](https://img.shields.io/pypi/v/PySocks.svg?label=PySocks)
    ![PyPI](https://img.shields.io/pypi/v/tqdm.svg?label=tqdm)
    ![PyPI](https://img.shields.io/pypi/v/requests.svg?label=requests)
    * #### Linux
       ```bash
       sudo apt install tor
       sudo apt install python3-socks  (optional)
       pip3 install --user -r requirements.txt
       ```

    * #### Windows
       download [tor expert bundle]
       ```bash
       pip3 install -r requirements.txt
       ```

* ## Usage
    * #### Preview
       [![asciicast](https://asciinema.org/a/209959.png)](https://asciinema.org/a/209959)

    * #### Linux
       ```bash
       git clone https://github.com/mIcHyAmRaNe/okadminfinder3.git
       cd okadminfinder3
       chmod +x okadminfinder.py
       python3 okadminfinder.py
       ```

    * #### Windows
       download & extract [zip]
       ```bash
       cd okadminfinder3
       py -3 okadminfinder.py
       ```

## Features
- [x] More than 500 potential admin panels
- [x] Tor & Proxy
- [x] Random-Proxy
- [x] Random-Agents
- [x] Console work with params, like: `okadminfinder.py -u example.com --proxy 127.0.0.1:8080`
- [ ] Multithreading, for faster work
- [ ] Adding more potential admin panel pages  

[Github Repository]{: .btn .btn--info .btn--larg}{:target="_blank"}

[tor expert bundle]: https://dist.torproject.org/torbrowser/10.0.15/tor-win64-0.4.5.7.zip
[zip]: https://github.com/mIcHyAmRaNe/okadminfinder3/archive/master.zip
[admin panel links]: https://github.com/mIcHyAmRaNe/okadminfinder3/blob/master/LinkFile/adminpanellinks.txt
[Github Repository]: https://github.com/mIcHyAmRaNe/okadminfinder3