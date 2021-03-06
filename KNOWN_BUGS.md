# Vulnerability to password bruteforcing
## Issue affecting keys used in steganography

 An important part of Tomb's security model is to *make it hard for
 attackers to enter in possession of both key and data storage*: once
 that happens, bruteforcing the password can be relatively easy.

 Protection from bruteforcing is provided by the KDF module that can
 be optionally compiled in `extras/kdf-keys` and installed.

 If a key is buried in an image and then the image is stolen, the KDF
 protection does not works because *attackers can bruteforce easily
 using steghide dictionary attacks*: once found the password is the
 same for the steg crypto and the key crypto.

 Users should keep in mind these issues when planning their encryption
 scheme and, when relying on steganography, keep the image always
 mixed in the same folder with many more images since that will be the
 multiplier making it slightly harder to bruteforce their password.

 In most cases consider that *password bruteforce is a feasible attack
 vector on keys*. If there are doubts about a key being compromised is
 a good practice to change it using the `setkey` command on a secure
 machine, possibly while off-line or in single user mode.

# Versioning and stdin key
## 1.5

 Due to distraction tomb version 1.5 displays its version as 1.4.
 Also version 1.5 did not work when using -k - to pipe keys from
 stdin, plus left the encrypted keys laying around in RAM (tmpfs).
 This was a minor vulnerability fixed in 1.5.1.


# Key compatibility broken
## 1.3 and 1.3.1

 Due to an error in the creation and decoding of key files, release
 versions 1.3 and 1.3.1 cannot open older tombs, plus the tombs created
 with them will not be opened with older and newer versions of Tomb.

 This bug was fixed in commit 551a7839f500a9ba4b26cd63774019d91615cb16

 Those who have created tombs with older versions can simply upgrade
 to release 1.4 (and any other following release) to fix this issue
 and be able to operate their tombs normally.

 Those who have used Tomb 1.3 or 1.3.1 to create new tombs should use
 Tomb version 1.3.1 (available from https://files.dyne.org/tomb) to
 open them and then migrate the contents into a new tomb created using
 the latest stable Tomb version.

 This bug was due to a typo in the code which appended a GnuPG status
 string to the content of keys.  All users of Tomb 1.3.* should pay
 particular attention to this issue, however that release series was
 out as latest for less than a month.
