# gpg-keys

OpenPGP Web Key Directory (WKD) for `@raspberrypi.com` addresses, served from
https://openpgpkey.raspberrypi.com via GitHub Pages.

Clients such as GnuPG, Thunderbird and Mailvelope look up a key for
`someone@raspberrypi.com` at:

    https://openpgpkey.raspberrypi.com/.well-known/openpgpkey/raspberrypi.com/hu/<hash>

where `<hash>` is the z-base-32 SHA-1 of the lower-cased local part of the
address.

## Adding a key

1. Work out the filename for the address:

       gpg-wks-client --print-wkd-hash someone@raspberrypi.com

2. Export the public key in binary form with only that user ID and
   self-signatures, and save it under that name:

       gpg --export-options export-minimal \
           --export-filter 'keep-uid=mbox=someone@raspberrypi.com' \
           --export someone@raspberrypi.com \
           > .well-known/openpgpkey/raspberrypi.com/hu/<hash>

3. Check it:

       gpg --show-keys .well-known/openpgpkey/raspberrypi.com/hu/<hash>

4. Open a pull request.

Keys must be binary, not ASCII-armoured.

## Verifying the live directory

    gpg-wks-client --check someone@raspberrypi.com
