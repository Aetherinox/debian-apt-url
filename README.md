# apt-url

A debian package to fetch direct download links for .deb packages specified by name. 

This package is used in combination with [LastVersion](https://github.com/dvershinin/lastversion) as part of the system for the [Proteus Apt Repository](https://github.com/Aetherinox/proteus-apt-repo); which is a custom package repository for ZorinOS and Ubuntu. It is used to fetch the direct URL to a package and then is downloaded and added to the repository automatically.

<br />

---

<br />

- [apt-url](#apt-url)
  - [Usage](#usage)
    - [--package](#--package)
    - [--fileOnly](#--fileonly)
    - [--urlOnly](#--urlonly)
    - [--aptOnly](#--aptonly)
    - [--pretty](#--pretty)
    - [--help](#--help)
  - [Install](#install)
  - [Build](#build)

<br />

---

<br />

## Usage

The following are commands you can execute with `apt-url`:

<br />

### --package

This option specifies the package you want to search for.

```shell
$ apt-url --package reprepro

reprepro_5.4.7-1_amd64.deb
https://raw.githubusercontent.com/Aetherinox/proteus-apt-repo/main/pool/main/r/reprepro/reprepro_5.4.7-1_amd64.deb
```

<br />
<br />

Alternatively, if you do not specify any options, and only want to provide a package name, you can do so without `--package` by using:

```shell
$ apt-url reprepro

reprepro_5.4.7-1_amd64.deb
https://raw.githubusercontent.com/Aetherinox/proteus-apt-repo/main/pool/main/r/reprepro/reprepro_5.4.7-1_amd64.deb
```

<br />
<br />

### --fileOnly

This returns only the filename of the package

```shell
$ apt-url --fileOnly --package reprepro
reprepro_5.4.7-1_amd64.deb
```

<br />
<br />

### --urlOnly

This returns only the url of the package

```shell
$ apt-url --urlOnly --package reprepro
https://raw.githubusercontent.com/Aetherinox/proteus-apt-repo/main/pool/main/r/reprepro/reprepro_5.4.7-1_amd64.deb
```

<br />
<br />

### --aptOnly

This option allows you to use `apt-get` to list information about a package, instead of `apt-move / fetch`:

```shell
$ apt-url --aptOnly --urlOnly --package reprepro

https://raw.githubusercontent.com/Aetherinox/proteus-apt-repo/main/pool/main/r/reprepro/reprepro_5.4.7-1_amd64.deb
```

<br />
<br />

### --pretty

This allows you to display the results for a package with color and formatting.

```shell
$ apt-url --pretty --package reprepro

          File         reprepro_5.4.7-1_amd64.deb                          
          URL          https://raw.githubusercontent.com/Aetherinox/proteus-apt-repo/main/pool/main/r/reprepro/reprepro_5.4.7-1_amd64.deb

$ apt-url --pretty --package repbad

        ERROR        💡 Could not find package repbad            
```

<br />
<br />

### --help

Lists all of the available commands for this package; and examples that you can try.

```shell
$ apt-url --help

  apt-url
  A package which allows you to fetch information about a package, including the url of where it is hosted
  last update: 2025-23-05
  apt-url --package package-name 


  Syntax:                                         
        Command                           apt-url [ -option [ arg ] ]
        Options                           apt-url [ -h | --help ]
            -A                            required                                
            -A...                         required; multiple can be specified     
            [ -A ]                        optional                                
            [ -A... ]                     optional; multiple can be specified     
            { -A | -B }                   one or the other; do not use both       
        Arguments                         apt-url [ -p package-name | --package package-name ] arg
        Examples                          apt-url package-name
                                          apt-url --package package-name
                                          apt-url --aptOnly --pretty --package package-name

  Options:                                         
        -p,  --package <string>           package name to search for          
        -a,  --aptOnly                    use apt-get to search for packages instead of apt-fetch
        -f,  --fileOnly                   only return url for package         
        -u,  --urlOnly                    only return filename for package    
        -P,  --pretty                     show results in formatted layout    
        -v,  --version                    current version of this app         
        -x,  --dev                        developer mode; verbose logging     
        -h,  --help                       show this help menu             
```

<br />

---

<br />

## Install

If you do not wish to manually install or build your own copy; you can add it via our [Proteus Apt Repository](https://github.com/Aetherinox/proteus-apt-repo).

Download the GPG key utilized with the repository:

```shell
wget -qO - https://github.com/Aetherinox.gpg | \
  sudo gpg --batch --yes --dearmor -o /usr/share/keyrings/aetherinox-proteus-archive.gpg
```

<br />

Add the Proteus Apt repo to your Linux sources:

```shell
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/aetherinox-proteus-archive.gpg] https://raw.githubusercontent.com/Aetherinox/proteus-apt-repo/main $(lsb_release -cs) main" | \
  sudo tee /etc/apt/sources.list.d/aetherinox-proteus-archive.list
```

<br />

Now update your packages so that the new repo is added:

```shell
sudo apt update
```

<br />

==(Optional)== To test if the correct GPG key was added:

```shell
gpg -n -q --import --import-options import-show \
    /usr/share/keyrings/aetherinox-proteus-archive.gpg | \
    awk -v val=BCA07641EE3FCD7BC5585281488D518ABD3DC629 '/pub/{getline; gsub(/^ +| +$/,"");
    if($0 == val)
        print "("$0") Found match for Proteus Apt Repo."
    else
        print "("$0") No match for Proteus Apt Repo."}'
```

<br />

You can then install `apt-url` with:

```shell
sudo apt install apt-url
```

<br />

==(Optional)== You can test to make sure you are getting the package from the correct source. The URL returned should be the one to the proteus apt repo.

```shell
$ apt-get download --print-uris apt-url

'https://raw.githubusercontent.com/Aetherinox/proteus-apt-repo/main/pool/main/a/apt-url/apt-url_1.0.0-2_all.deb' apt-url_1.0.0-2_all.deb 2310 SHA512:5d04d99e636b897e39c7b7b834e845cd7bc98ed82e5ebb7657fc035819e05d585ddc3c7a8c6e2c9c3c47e56d4529d7b2b185addceb1c2115b6ea32982d6f6de6
```

<br />

---

<br />

## Build

To build, you must have the following structure. In the tree below, the folder `share/lintian` is optional and only contains Lintian overrides.

```
📁 src
    📁 apt-url_1.1.0-1_amd64
        📁 DEBIAN
            📄 control
        📁 usr
            📁 bin
                📄 apt-url
        📁 share
            📁 doc
                📁 apt-url
                    📄 changelog.gz
                    📄 copyright
            📁 lintian
                📁 overrides
                    📄 apt-url

    📁 apt-url_1.1.0-1_arm64
        📁 DEBIAN
            📄 control
        📁 usr
            📁 bin
                📄 apt-url
        📁 share
            📁 doc
                📁 apt-url
                    📄 changelog.gz
                    📄 copyright
            📁 lintian
                📁 overrides
                    📄 apt-url
```

<br />

Compress the changelog:

```shell
cd src
gzip --best -n apt-url_1.1.0-1_amd64/usr/share/doc/apt-url/changelog.Debian
gzip --best -n apt-url_1.1.0-1_arm64/usr/share/doc/apt-url/changelog.Debian
```

<br />

Generate the `.deb` packages:

```shell
cd src
dpkg-deb --root-owner-group --build apt-url_1.1.0-1_amd64
dpkg-deb --root-owner-group --build apt-url_1.1.0-1_arm64
```

<br />

Run Lintian:

```shell
cd src
lintian apt-url_1.1.0-1_amd64.deb --tag-display-limit 0
lintian apt-url_1.1.0-1_arm64.deb --tag-display-limit 0
```