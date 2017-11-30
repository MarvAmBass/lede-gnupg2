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
- libbz2
- libgnutls
- pcscd

## additional useful services / programs

- haveged


### Smartcards

_to enable smartcard reader support enable the `pl2303` kernel module_

* https://www.gnupg.org/howtos/card-howto/en/smartcard-howto-single.html

Also note that the public key is not stored on the smartcard! you need to import the public key first to be able to decrypt the encrypted message with the key stored on the smartcard!
If the public key is not in the gnupg keystore, it will abort with a error that the key cannot be found - but the key will be visible beneath `gnupg --card-status`

If the card isn't detected and you get a message like the following:
```
$ gpg --card-status
gpg: selecting openpgp failed: No such device
gpg: OpenPGP card not available: No such device
```

you might want to try to alter the method which is used to communicate with the card.

By default, scdaemon will try to connect directly to the device. This connection will fail if the reader is being used by another process. For example: the pcscd daemon used by OpenSC. To cope with this situation we should use the same underlying driver as opensc so they can work well together. In order to point scdaemon to use pcscd you should remove `reader-port` from `~/.gnupg/scdaemon.conf`, specify the location to `libpcsclite.so` library and disable ccid so we make sure that we use pcscd: 

I've used the following config `~/.gnupg/scdaemon.conf` and was able to connect succesfully to my SCR335 reader with a OpenPGP Card v.2.1

```
pcsc-driver /usr/lib/libpcsclite.so.1
card-timeout 5
disable-ccid
```
Please check scdaemon's manpages if you do not use OpenSC. 


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
