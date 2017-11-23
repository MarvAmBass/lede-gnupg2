# Packages

## from this feeds

- libgpg-error
- libksba
- libassuan
- libgcrypt
- libusb
- npth
- pinentry
- gnupg

## from official feeds

- ccid
- zlib
- libgnutls

## additional useful services / programs

- haveged

# Usage

# Installing

## install this feed

```
echo 'src-git gpg https://github.com/MarvAmBass/lede-gnupg2.git' >> feeds.conf.default
```

## install all packages from this feed

`./scripts/feeds install -a -p gpg`

### install package from specic feed

`./scripts/feeds install -p gpg libgpg-error`

## building

`make -j1 V=s`
