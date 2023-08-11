<div align="center" >
    <h1>CryptMon - multi-layer Encryption programme</h1>
    <br>
</div>

# 1. introduction

CryptMon is a powerful 3-layer encryption tool that combines the functionalities of GPG, SOPS, and OpenSSL to provide a user-friendly command-line interface for encrypting and decrypting your secrets. It offers an easy-to-use set of options for securing your sensitive data efficiently.

>**DISCLAIMER:** THIS IS AN ALPHA/EXPERIMENTAL VERSION OF THE CRYPTMON ENCRYPTION PROGRAM. USE IT AT YOUR OWN RISK, AS THERE MAY BE BUGS THAT CAN POTENTIALLY CAUSE DATA LOSS OR DAMAGE TO YOUR FILES. BEFORE PERFORMING ANY ENCRYPTION USING CRYPTMON, IT IS STRONGLY RECOMMENDED TO _BACK UP YOUR FILES/DATA AND `AGE`, `GPG`, AND `OPENSSH` KEYS._

# Table of Contents

1. [Introduction](#1-introduction) \
   1.1 [CryptMon - Three-Layer Encryption](#11-cryptmon---three-layer-encryption) 
      - [Layer 1: SOPS Encryption with AGE Key](#layer-1-sops-encryption-with-age-key) 
      - [Layer 2: OpenSSH Encryption with AES-256-CBC Method](#layer-2-openssh-encryption-with-aes-256-cbc-method) 
      - [Layer 3: GPG Encryption with User-Defined Configuration](#layer-3-gpg-encryption-with-user-defined-configuration) \
   1.2 [Quick start](#12-quick-start) \
   1.3 [Commands Usage](#13-commands-usage) \
      1.3.1 [Configure Command (-c) Sub-Option](#131-configure-command--c-sub-option) \
      1.3.2 [Definition of Operator](#132-definition-of-operator) \
      1.3.3 [Conditional Options](#133-conditional-options) \
      1.3.4 [Operator Options](#134-operator-options) \
      1.3.5 [Usage Guidelines](#135-usage-guidelines)
          - [Summary](#summary)

2. [Setup CryptMon](#2-setup-cryptmon) \
   2.1 [Requirements](#21-requirements) \
   2.2 [clone/install](#22-clone) \
   2.3 [Make excutable](#23-make-sctipt-excutable)
3. [Configuration](#3-configuration) \
   3.1 [Manage Configuration](#31-manage-configuration) \
      3.1.1 [Command Chart](#311-command-chart) \
      3.1.2 [About Configuration Directory](#312-about-configuration-directory) \
      3.1.3 [Remove/Reset Configuration](#313-removereset-configuration) \
      3.1.4 [Backup & Restore Keys](#314-backup--restore-keys) \
           3.1.4.1 [Backup/Export Key](#3141-backupexport-key) \
           3.1.4.2 [Import/Restore Key](#3142-importrestore-key) \
      3.1.5 [View Configure File](#315-view-configure-file) \
            - [Viewing All Operator Configurations](#viewing-all-operator-configurations) \
            - [Viewing Specific Operator Configuration](#viewing-specific-operator-configuration) \
            - [summary](#summary)

5. [Encryption & Decryption of an File](#4-encryption--decryption-of-an-file) \
   4.1 [Encrypt an File](#41-encrypt-an-file) \
   4.2 [Decrypt an File](#42-decrypt-an-file) 
   
6. [Tools/Repo](#5-toolsrepo) \
   5.1 [Third-Party](#51-third-party) \
   5.2 [Own/Official](#52-ownofficial) 


## 1.1 CryptMon - multi-Layer Encryption

CryptMon is a powerful encryption tool that provides three layers of security to safeguard your sensitive data. Each layer adds an additional level of protection to ensure the utmost confidentiality. Below is an overview of how CryptMon's three-layer encryption works:

![Alt text](repo_resources/encryption_layer.png?raw=true "3-layer encryption")

#### Layer 1: SOPS Encryption with AGE Key

In the first layer, CryptMon employs the Secure Operation Secret (SOPS) encryption technique using the Asymmetric Encryption tool (AGE) key. AGE is a modern encryption tool designed to be fast, secure, and easy to use. SOPS ensures that your data is securely encrypted using the AGE key, providing the initial layer of protection.

#### Layer 2: OpenSSH Encryption with AES-256-CBC Method

The second layer of encryption involves using OpenSSH encryption with the AES-256-CBC cipher block chaining (CBC) method. In this layer, the user sets a password that acts as the encryption key. The AES-256-CBC method is widely recognized for its strong encryption capabilities and is widely used for data protection.

#### Layer 3: GPG Encryption with User-Defined Configuration

The third and final layer of CryptMon's encryption process utilizes the GNU Privacy Guard (GPG) encryption method. GPG allows users to configure their encryption settings based on their preferences. By providing a user-defined GPG configuration, CryptMon enhances security according to individual needs and requirements.

## 1.2 quick start

*make excutable*
```
chmod +x cryptmon
```
*configure cryptmon*
- step 1. [configure gpg manually ](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
- step 2. configure cryptmon
```
./cryptmon -c  [KEY FILE] [`GPG`USER NAME]
```
>if you have an age key then replace with [KEY FILE] option and add gpg user name that match with gpg configuration 

*encrypt an file*
```
./cryptmon -e [FILE]
```
*decrypt an file*
```
./cryptmon -d [ENCRYPTED FILE]
```

## 1.3 commands usage

| option | long-option | work/meaning | usage |
| ------ | ------ | ------ | ------ |
| -e | --encrypt | encrypt file | ./cryptmon -e [FILE] |
| -d | --decrypt | decrypt file | ./cryptmon -d [FILE] |
| -c | --cfg | configure: `gpg` `age` `sops` | ./cryptmon -c  [KEY FILE] [`GPG`USER NAME] |

> NOTE: Make sure to replace [OPTIONS],[OPERATOR] and [FILE] with the appropriate values when using CryptMon.
> HINTs: [OPERATOR] means : `gpg` `age` `sops`

#### 1.3.1 configure command (-c) SUB-OPTION

| [-c] sub-option | long-option | meaning/work | usage |
| ------ | ------ | ------ | ------ |
| a | --cfg-age | configure `age` | ./cryptmon -ca |
| g | --cfg-gpg | configure `gpg` | ./cryptmon -cg |
| s | --cfg-sops | configure `sops` | ./cryptmon -cs |
| r | --reset | reset/remove configure | ./cryptmon -cr[OPERATOR] |
| e | --export-[OPERATOR] | export/backup configure | ./cryptmon -ce[OPERATOR] |
| i | --import-[OPERATOR] | import/restore configure | ./cryptmon -ci[OPERATOR] |
| v | --cfg-view | view configure | ./cryptmon -cv[OPERATOR] |


### 1.3.2 Definition of Operator:

In CryptMon, an "Operator" refers to a specific encryption method that you can use to secure your files. The available Operators are AGE, SOPS, and GPG.

### 1.3.3 Conditional Options

The following options are considered conditional options, and they come with their respective long-options:

- `r`: Reset the configuration.
- `e`: export a file.
- `i`: Import a specific configuration.
- `v`: Views the configuration. \
    Additionally, there are their respective long-options.

### 1.3.4 Operator Options

On the other hand, the following options are categorized as OPERATOR options, and they also have corresponding long-options:

- `a` : AGE configuration.
- `s` : SOPS configuration.
- `g` : GPG configuration. \
    Similarly, there are their respective long-options.

### 1.3.5 Usage Guidelines:

- Conditional short-options and Operator short-options can only be used in conjunction with the -c option. For example: `./cryptmon -cv`

- Long-options, on the other hand, can be used directly with the ./cryptmon command. For example:`./cryptmon --cfg-view`

- Remember, conditional options cannot be used together, and the same applies to Operator options.

- To set options correctly, use sub-options with the `-c` option without any space in between. here is example:

- correct usage: \
✅ `./cryptmon -ca` \
✅ `./cryptmon --cfg-age` \
✅ `./cryptmon -cai` \
✅ `./cryptmon -cia`

- incorrect usage: \
❌ `./cryptmon -ca --cfg-age` \
❌ `./cryptmon -c -a` \
❌ `./cryptmon -c --cfg-age`

>IMPORTANT NOTE:
>Conditional short-options and OPERATOR short-options only work with the `-c` option. Long-options directly work with `./cryptmon`.
>It is crucial to note that conditional options (e.g., `r`, `e`, `i`, `v`) cannot be used or combined with other conditional options. The same applies to OPERATOR options (e.g., `a`, `s`, `g`) - they should not be mixed with other OPERATOR options.

##### **Summary**

CryptMon provides conditional options for specific operations and OPERATOR options for configuration. Remember that you should not combine multiple conditional or OPERATOR options. Always use sub-options with the `-c` option wthout any space to ensure correct usage.

<!-- 
>`r`,`e`,`i`,`v` and there long-options, are a conditional options.
>`a`,`s`,`g` and there long-options, are a OPERATOR options.
conditional option can not use/work with other conditional option, same with OPERATOR option.
use sub-options with -c option without any space in between.
>_here is example of right use of options :_ 
**correct usage:**
✅ `./cryptmon -ca`
✅ `./cryptmon --cfg-age`
✅ `./cryptmon -cai`
✅ `./cryptmon -cia`
**incorrect usage:**
❌ `./cryptmon -ca --cfg-age`
❌ `./cryptmon -c -a`
❌ `./cryptmon -c --cfg-age` -->

<!--# Setup and Configuration-->

## 2. Setup CryptMon

### 2.1 Requirements

Before using CryptMon, ensure that you have the following prerequisites:

- Linux operating system.
- Required packages: `age`, `sops`, `gpg`, `openssh`.

> CryptMon will automatically fulfill the required packages when you run it.

### 2.2 Clone

To clone the CryptMon repository, execute the following command:

```
git clone https://github.com/rrkroms/cryptmon.git
```

### 2.3 make script excutable
To make CryptMon executable, execute the following command:

```bash
chmod +x cryptmon
```

Alternatively, you can use CryptMon without making it executable by adding `bash` before `./cryptmon` every time you use it:

```bash
bash ./cryptmon
```
## 3. Configuration

Before performing any encryption, it's essential to configure CryptMon based on the configurations of `gpg`, `age`, and `sops`.

- Step 1: Configure GPG Manually

Please follow the instructions in the [GPG documentation](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) to configure GPG manually.

- Step 2: Configure `sops` `age` for CryptMon

Open the CryptMon repository directory and run `./cryptmon` with the `-c` option to configure all [OPERATORs]:

```
./cryptmon -c
```

To configure a specific [OPERATOR], use the `[OPERATOR]` option with the `-c` option:

```
./cryptmon -c[OPERATOR]
```
>For example: To configure the `sops` , use -cs as an option.

If you already have an `AGE` key, you can run the following command:

```
./cryptmon -c [age key file]
```

Alternatively, you can import the `AGE` key using the import command:

```
./cryptmon -cia [age key file]
```

If you have two `GPG` user keys or want to encrypt a file for another user, use the following command:

```
./cryptmon -cg [user name]
```

You can also combine both configurations with the following command:

```
./cryptmon -c [age key file] [gpg user name]
```
Remember to configure CryptMon appropriately to ensure seamless encryption and decryption of your files.

**important notes**
Before running the `SOPS` configuration, first follow the `Age` configure command because the `SOPS` configuration depends on the Age key.
<!-- ### 2. setup cryptmon

#### 2.1 requiments
- linux os/distro
- packages: `age`,`sops`,`gpg`,`openssh`
> requied pckeages automaticly full-fill wthen you run cryptmon

#### 2.2 clone
to clone cryptmon repo run this command:
```
git clone http://repo.git
```

### 2. **Configuration**
_Before  perform any Encryption, configure the cryptmon, configure base on configuration of `gpg` `age` `sops`_

-step 1

[configure gpg manually ](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)

-step 2 open cryptmon repo diractory and run ./cryptmon with -c option configure all [OPERATORs]
```
./crptmon -c
```
to configure specific [OPERATOR] , measn [OPERATOR] option with -c option:
```
./cryptmon -c[OPERATOR]
``` -->

### 3.1 manage configuration

#### 3.1.1 command chart
| option | long-option | work/meaning | usage |
| ------ | ------ | ------ | ------ |
| r | --reset | reset/remove configure | ./cryptmon -cr[OPERATOR] |
| a | --cfg-age-remove | configure `age` | ./cryptmon -ca |
| g | --cfg-gpg-remove | configure `gpg` | ./cryptmon -cg |
| s | --cfg-sops-remove | configure `sops` | ./cryptmon -cs |
>*incaption*: log-option of `gpg` `sops` `age` currnetly not work/add.

### 3.1.2 about configuration directory
CryptMon's configuration directory is located in the `$HOME` directory as `.crypt`, which is a hidden folder. You can view hidden folders using the command `ls -a ~`.

In this configuration directory, your `age` key is stored as a file named `.age.keygen.rom`, while your `gpg` user name is stored in the `.config` file.

Additionally, CryptMon uses a clever trick by creating a symbolic link between `~./.crypt/keygen.rom` and `./config/sops/age/keys.txt`. This link ensures that if you remove or reset the age configuration, the keys stored in `./config/sops/age/keys.txt` become automatically useless.

>_*Please exercise caution when managing your configuration files and keys, as they are critical for the security of your encrypted data.*_

#### 3.1.3 remove/reset configuration
To remove/reset the configuration for [OPERATORs], simply add the r sub-option after -c, or use the long-option --reset to reset all [OPERATORS] configurations.

To reset or remove a specific [OPERATOR], place the [OPERATOR] before or after the r sub-option.

*reset/remove all [OPERATORs] command*:
shot-opyion:
```
./cryptmon -cr
```
or 
long-option
```
./cryptmon --reset
```

*reset/remove specific [OPERATOR] command*
```
./cryptmon -c[OPERATOR]r
```
or 
```
./cryptmon -cr[OPERATOR]
```

For example:

To reset the age configuration, use -cra or -car as an option.
To reset all [OPERATORS] configurations, use -cr or --reset as an option.

#### 3.1.4 backup & restore keys

cryptmon provides a simple function `export` & `import` that allows you to backup and import secret keys. The script facilitates the management of cryptographic keys in a secure and efficient manner. Below, you will find instructions on how to use the function/script for backing up and restoring secret keys.
*import/export options/commands*
| [-c]sub-option | log-option | meaning/work | usage |
| ------ | ------ | ------ | ------ |
| e | --export-[OPERATOR] | export/backup configure | ./cryptmon -ce[OPERATOR] |
| i | --import-[OPERATOR] | import/restore configure | ./cryptmon -ci[OPERATOR] |

##### 3.1.4.1 backup/export key

- To backup or export a secret key, follow these steps:

Run the `./cryptmon` script with the `-ce[OPERATOR] [DIR]` or `-c[OPERATOR]e [DIR]` option:
```
./cryptmon -cea ~/backup.secret.key
```
> The [DIR] parameter is optional. If you provide a directory, the exported key will be stored there. *If no directory is provided*,
> the backup/export *key* will be *saved in the working directory*.

##### 3.1.4.2 Import/Restore Key

- To import or restore a secret key, follow these steps:

> Ensure you have the exported secret key file available on your machine.

Run the ./cryptmon script with the `-ci[OPERATOR] [DIR]` or `-c[OPERATOR]i [DIR]` option:
```
./cryptmon -cia [DIR]
```
> The [DIR] parameter is optional. If you provide a directory, the backup key will be restored from there. If no directory is provided,
> the script will prompt you to provide the location of the backup/exported secret key file.
> After providing the file location, the script will import and restore the secret key for your use.

>*_Please remember to keep your secret key files secure and backed up regularly to prevent data loss and unauthorized access._*

**Note: It's essential to follow security best practices when dealing with cryptographic keys. Make sure to protect the exported secret keys with strong encryption and store them in a secure location. Do not share or store the keys in public repositories. Use a password manager or other secure methods to handle passwords and passphrase information related to the keys.**

#### 3.1.5 view configure file
CryptMon provides a simple and convenient way to view configurations for different operators. You can view all operator configurations or specify a particular operator to view its configuration. Please follow the instructions below to access the configuration viewing feature.

###### **Viewing All Operator Configurations**

*Short Option*:
To view all operator configurations, use the following short option:
```
./cryptmon -cv
```

*Long Option*:
Alternatively, you can use the long option to achieve the same result:

```
./cryptmon --cfg-view
```

###### **Viewing Specific Operator Configuration**

To view the configuration of a specific operator, add the operator's option before or after the v sub-option with the -c option.
```
./cryptmon -c[OPERATOR]v
```
or
```
./cryptmon -cv[OPERATOR]
```
**Examples**:
To view the AGE configuration, use any of the following options:`./cryptmon -cva` or `./cryptmon -cav`

To view the configuration of other operators, simply replace [OPERATOR] with the desired operator's option. For example, to view the GPG configuration: `./cryptmon -cvg` or `./cryptmon -cgv`

##### **Summary**:
To view all operators' configurations: `./cryptmon -cv` or `./cryptmon --cfg-view`.
To view a specific operator's configuration: `./cryptmon -cv[OPERATOR]` or `./cryptmon -c[OPERATOR]v`.


## 4. ENCRYPTION & DECRYPTION of an FILE

<!-- To utilize CryptMon's three-layer encryption, follow these simple steps: -->
<!-- 
1. Install CryptMon: Ensure you have CryptMon installed on your system. You can download and install it from the official website [link to CryptMon website]. -->
<!--  -->
### 4.1 Encrypt an File
To encrypt a file, use the following command:
```
./cryptmon -e [FILE]
```
> Replace [FILE] with the path to the file you want to encrypt. For example, if you have a file named my_secret_file.txt located in the current directory, you can encrypt it using: `./cryptmon -e my_secret_file.txt`

After executing the command, cryptmon will encrypt the specified file and *store the encrypted version securely in current working directory* and delete origial none-encrypted file*.

### 4.2 Decrypt an File
To decrypt a file, use the following command:
```
./cryptmon -d [FILE]
```
replace [FILE] with the path to the file you want to decrypt. For example, if you have a file named my_encrypted_file.txt located in the current directory, you can decrypt it using: `./cs -d my_encrypted_file.txt`

cryptmon will then use the appropriate decryption method to retrieve the original contents of the file and make it available for you to access.

>_note: [FILE] is a placeholder in the commands provided above. When using CryptScript, you should replace [file] >with the actual file path or filename that you wish to encrypt or decrypt._

**Important Note**
<!-- >*Make sure to handle sensitive files with care and keep your encryption keys secure. Always make backups of your important data to avoid data loss.* -->

CryptMon's three-layer encryption system provides robust protection for your data. However, it is crucial to remember and securely store the passwords and keys used in each layer. Losing or forgetting these credentials may result in permanent data loss, as decryption becomes impossible without the appropriate keys.

<!-- ## Further Assistance

For more information or any queries regarding CryptMon, refer to the official documentation [link to documentation] or contact our support team [support email/contact form link].

We hope you find CryptMon's three-layer encryption to be a reliable and efficient solution for securing your valuable data! -->

<!-- ##### 3.2 how to work?
_cryptmon currently base on 3 layer encryption._
*Layer1* : _`sops` encryption with `age` key._
*Layer2* : _`openssh` encryption with `aes-256-cbc` method that password set by user._
*Layer3* : _`GPG` encryption with GPG configure method by user._ -->
<!-- ![Alt text](repo_resource/encryption_layer.png?raw=true "Title") -->

##### 5. tools/repo

###### 5.1 third-party
- [GPG](https://gnupg.org)
- [SOPS](https://github.com/getsops/sops.git)
- [AGE](https://github.com/FiloSottile/age.git)
- [OPENSSH](https://www.openssh.com/)

###### 5.2 own/official
- ROM-ui(private repo)
- ROM-bash-addon(private repo)
