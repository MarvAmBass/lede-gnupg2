# LEDE Feeds for GnuPG2

this is my repository for a full gnupg2 installation on a LEDE/OpenWRT device.
Use the official SDK, add this as a feed, install the feeds and compile it for your device.

I created this to have OpenPGP Card / Smartcard functionality on an __Onion Omega2__.

## More infos about the SDK

* https://lede-project.org/docs/guide-developer/compile_packages_for_lede_with_the_sdk

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


### Smartcards

_to enable smartcard reader support enable the `pl2303` kernel module_

* https://www.gnupg.org/howtos/card-howto/en/smartcard-howto-single.html

Also note that the public key is not stored on the smartcard! you need to import the public key first to be able to decrypt the encrypted message with the key stored on the smartcard!
If the public key is not in the gnupg keystore, it will abort with a error that the key cannot be found - but the key will be visible beneath `gnupg --card-status`

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
