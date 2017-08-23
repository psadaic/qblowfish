# QBlowfish

QBlowfish is a [Qt](http://qt.nokia.com/) implementation of the [Blowfish](http://www.schneier.com/blowfish.html) encryption algorithm, as described in the original Blowfish [paper](http://www.schneier.com/paper-blowfish-fse.html) by Bruce Schneier.

The Blowfish algorithm requires the input in 8-byte blocks. To simplify usage, QBlowfish can optionally add [PKCS5 padding](http://tools.ietf.org/html/rfc5652#section-6.3) to the input data. (For example, if the input is only 60 bytes long, 4 bytes will be padded to bring the bytecount to a multiple of 8.) When padding is enabled during decryption, QBlowfish will also remove the padded bytes from the output.

You only need to add 3 files (src/*) to your project. You can then use the QBlowfish class to encrypt and decrypt stuff.

    QByteArray secretKey("This is a secret")
    QString clearText("Stuff to encrypt");

    QBlowfish bf(secretKey);
    bf.setPaddingEnabled(true);
    QByteArray encryptedBa = bf.encrypted(clearText.toUtf8());

A more detailed example is included in the repo.

QBlowfish is not optimized for speed. It processes the data in bytes (most other Blowfish implementations seem to work on 4-byte words) and is endianness-agnostic.

### Tests

Unit tests are written using QTestLib. Tests include [the official test vectors](http://www.schneier.com/code/vectors.txt).

QBlowfish is known to work fine with Qt versions 4.8, 5.0 and 5.1, on Windows, Mac and Linux platforms (not all combinations have been tested, though). If you find it's not working in your setup, please [open an issue](https://github.com/roop/qblowfish/issues).

[23/07/2017] - works fine with Qt 5.9.1, on Linux (16.04.3), Windows 10 (version 1703).

### License

QBlowfish is published under the MIT license.
