---
id: integrity-check
title: Integrity Check for CKB Release
---

All the binaries in [CKB releases](https://github.com/nervosnetwork/ckb/releases) are signed via following PGP keys.

| Version   | Package              | Unique ID                              | OpenPGP Key                                                                          | Fingerprint                                        |
| --------- | -------------------- | -------------------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------- |
| >= 0.13.0 | macOS, Linux, CentOS | Nervos Travis Builder <bot@nervos.org> | [F4631C0A](https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x4F37F694F4631C0A) | 64B7 05B5 6078 1FC5 4047  7B82 4F37 F694 F463 1C0A |
| >= 0.14.0 | Windows              | Nervos Azure Builder <bot@nervos.org>  | [AD748F26](https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x5EBA64ECAD748F26) | 0849 A2D2 4CA7 CFFC FA80  BCD4 5EBA 64EC AD74 8F26 |

You can import the public keys from the keyserver network:

```
gpg --recv-keys 4F37F694F4631C0A 5EBA64ECAD748F26
```

Once you have already imported the public keys, please download both the archive and
the corresponding `.asc` file to verify the signature. For example, to check
the signature of the file `ckb_v0.13.0_x86_64-apple-darwin.zip`

```
gpg --verify ckb_v0.13.0_x86_64-apple-darwin.zip.asc ckb_v0.13.0_x86_64-apple-darwin.zip
```

Note: Please never use a GnuPG version just downloaded to check the integrity of the source — use an existing, trusted GnuPG installation, e.g., the one provided by your distribution.

If the output of the above command is similar to the following, it means that you do not have our public key or the signature was generated by someone else, so you should handle the file suspiciously.

```
gpg: Signature made Wed 05 Jun 2019 10:12:22 PM UTC using RSA key ID F4631C0A
gpg: Can't check signature: No public key
```

If you get this result:

```
gpg: Signature made Wed 05 Jun 2019 10:12:22 PM UTC using RSA key ID F4631C0A
gpg: Good signature from "Nervos Travis Builder <bot@nervos.org>"
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 64B7 05B5 6078 1FC5 4047  7B82 4F37 F694 F463 1C0A
```

then you have a copy of our keys and the signatures are valid, but you have not marked the keys as trusted or the keys are a forgery. In this case, at the very least, you should compare the fingerprints that are shown above.

Ideally, you'll get result like:

```
gpg: Signature made Wed 05 Jun 2019 10:12:22 PM UTC using RSA key ID F4631C0A
gpg: checking the trustdb
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
gpg: next trustdb check due at 2023-06-05
gpg: Good signature from "Nervos Travis Builder <bot@nervos.org>"
```