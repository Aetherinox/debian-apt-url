# apt-url
A debian package to fetch direct download links for .deb packages specified by name

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

<br />

---

<br />

## Usage

The following are commands you can execute with `apt-move`:

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