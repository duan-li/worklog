---
layout: post
title: PHP jupyter
date: 2018-09-06 09:53 +0000
---

## You need 
* jupyter `pip install jupyter`
* zeroMQ `brew install zeromq`
* php zmq extention [github](https://github.com/mkoppanen/php-zmq)
* Jupyter-PHP's Installer [github](https://github.com/Litipk/Jupyter-PHP)

### Install php-zmq

Install `php-zmq` extention.[^1]
[^1]: [zeromq doc](http://zeromq.org/bindings:php)

```
brew install autoconf
brew install pkg-config
git clone git://github.com/mkoppanen/php-zmq.git
cd php-zmq
phpize && ./configure
make
sudo make install
sudo nano /usr/local/php5/php.d/70-extension-zmq.ini
```

put below into file `/usr/local/php5/php.d/70-extension-zmq.ini`
```
extension=zmq.so
```


### Install 
Download file[^2]
[^2]: [Jupyter-PHP-Installer](https://litipk.github.io/Jupyter-PHP-Installer/)

```
wget https://litipk.github.io/Jupyter-PHP-Installer/dist/jupyter-php-installer.phar
php ./jupyter-php-installer.phar install
```


### run jupyter
```
jupyter notebook
```

## Log
```
501  jupyter notebook
  502  php
  503  php -v
  504  brew install zeromq
  505  cd /etc
  507  php -i
  509  cd cd
  511  cd
  513  cd Downloads/
  515  php ./jupyter-php-installer.signed.phar install
  516  php ./jupyter-php-installer.phar install
  517  php ./jupyter-php-installer.phar install
  518  php ./jupyter-php-installer.phar install -vvv
  519  php -v
  520  cd /usr/local/
  522  cd php5
  524  cd bin
  526  ./php -v
  527  cd ..
  529  cd etc
  531  cd pear.conf
  532  cd pear.conf.default
  535  cd ..
  537  cd php.d
  541  cat 99-liip-developer.ini
  542  history
  543  brew search php-zmq
  544  brew search php7-zmq
  545  brew search zmq
  546  brew
  547  brew update
  548  brew search zmq
  549  phpize
  550  cd
  552  mkdir temp
  553  cd temp
  554  git clone git://github.com/mkoppanen/php-zmq.git
  556  cd php-zmq/
  557  phpize && ./configure
  558  phpize
  559  brew install autoconf
  560  phpize && ./configure
  561  brew install pkg-config
  562  phpize && ./configure
  563  make && make install
  564  make
  565  sudo make install
  566  cd /usr/local/php5
  568  cd bin
  569  ./php -v
  571  cd ..
  573  cd etc
  575  cd locales.conf
  576  cd
  577  cd /usr/local/php5
  579  cd php.d
  582  sudo touch 70-extension-zmq.ini
  583  sudo nano 70-extension-zmq.ini
  584  cd /etc
  586  cd
  587  cd Documents/
  589  cd ..
  590  cd Downloads/
  592  php ./jupyter-php-installer.phar install
  593  history

  ```

---