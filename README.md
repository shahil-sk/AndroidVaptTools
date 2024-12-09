# AndroidVaptTools
Android Tools And Installation

## MobSF (Mobile Security Framework)
--------------------------------------------------------------------------

MobSF is an open-source tool for automated security testing of mobile apps (Android, iOS, Windows). It supports **static**, **dynamic**, and **malware analysis**, identifies vulnerabilities, reverse-engineers apps, checks API security, and ensures compliance with standards like OWASP Mobile Top 10. Widely used in penetration testing, it integrates with CI/CD pipelines and provides detailed reports for faster remediation.


> [!IMPORTANT]
> You Need to  Install <a href="https://docs.docker.com/get-started/get-docker/" target="_blank">Docker</a> to Run MobSF

1) Start Docker Engine
2) Run this command

* This command Pulls MobSF Docker Image From Repo
```
docker pull opensecurity/mobile-security-framework-mobsf:latest
```

* Run MobSF in localhost:8000
```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

- Default
	- Username: mobsf 
	- Password : mobsf

> [!NOTE]
> You can enable Wi-Fi debugging or use Genymotion for dynamic analysis with MobSF in Docker. `-e MOBSF_ANALYZER_IDENTIFIER=<remote_device_IP>:<adb_port>`
> 
> **Example:**
> ```docker
> docker run -it --rm --name mobsf -p 8000:8000 -e MOBSF_ANALYZER_IDENTIFIER=192.168.255.101:5555 opensecurity/mobile-security-framework-mobsf
>```

> [!TIP]
> You can bypass or disable the MobSF login feature in Docker by using: `-e MOBSF_DISABLE_AUTHENTICATION=1`

--------------------------------------------------------------------------
## Yaazhini
--------------------------------------------------------------------------

Yaazhini is an open-source **mobile application security testing tool** for Android apps. It automates static, dynamic, and malware analysis to identify vulnerabilities like insecure storage, improper permissions, and weak encryption. Lightweight and user-friendly, Yaazhini is designed for security professionals and developers to ensure app robustness and compliance with security standards.

> [!NOTE]
> You Can Download Yaazhini from [Here](https://www.vegabird.com/yaazhini/#download)

1) Download The Setup From Official Website
2) Install The Application As Normal User
3) DONE!

> [!CAUTION]
> Recommended RAM size is 16GB. You may experience slow performance with Yaazhini due to the low available RAM.

--------------------------------------------------------------------------

## Drozer (on desktop)
--------------------------------------------------------------------------

Dozer is a tool that helps you create real-time **APIs** (ways for applications to talk to each other) from your data. It takes data from places like databases, message queues (like Kafka), or other sources and lets you access it instantly in your application, without delays.

### Pipx Method

```
pipx install drozer
```

### Run and Connect (Pipx)
1. First, forward port 31415 to the phone via ADB: `adb forward tcp:31415 tcp:31415`
2. Ensure that the [drozer agent⁠](https://github.com/WithSecureLabs/drozer-agent/releases/) is running on the target device, and that the embedded server has been started.
3. Then run the drozer command to connect to the phone: 
		`drozer console connect`

### Docker Method

> [!IMPORTANT]
> You Need to  Install <a href="https://docs.docker.com/get-started/get-docker/" target="_blank">Docker</a> to Run Dozer

**Install Drozer:**

```
docker pull withsecurelabs/drozer
```

```
docker build -t withsecurelabs/drozer https://github.com/WithSecureLabs/drozer.git#develop:docker
```


> [!NOTE]
>You need to install Drozer Agent Apk [agent-debug.apk](https://github.com/WithSecureLabs/drozer-agent/releases)

### Run and Connect (Docker)

#### Option 1: connect to the phone via network

If the target phone and PC are on the same network, this tends to be the easiest approach.

1. Ensure that the [drozer agent⁠](https://github.com/WithSecureLabs/drozer-agent/releases/) is running on the target device, and that the embedded server has been started.
2. Then, to run drozer and connect to the phone, run: 
		`docker run --net host -it withsecurelabs/drozer console connect --server <phone IP address>`

If a system shell is required (for example, to inspect and retrieve any files downloaded by drozer), you can:

1. Ensure that the [drozer agent⁠](https://github.com/WithSecureLabs/drozer-agent/releases/) is running on the target device, and that the embedded server has been started.
2. Obtain a shell into the container: 
		`docker run --net host -it --entrypoint sh withsecurelabs/drozer`
1. Then run the drozer command to connect to the phone: 
		`drozer console connect --server <phone IP address>`

#### Option 2: connect to the phone via USB

If network communications is restricted, `adb` port forwarding can be used to forward TCP traffic via USB.

1. First, forward port 31415 to the phone via ADB: `adb forward tcp:31415 tcp:31415`
2. Ensure that the [drozer agent⁠](https://github.com/WithSecureLabs/drozer-agent/releases/) is running on the target device, and that the embedded server has been started.
2. Then, to run drozer and connect to the phone, run: 
		`docker run --net host -it withsecurelabs/drozer console connect --server localhost`

If a system shell is required (for example, to inspect and retrieve any files downloaded by drozer), you can:

1. First, forward port 31415 to the phone via ADB: `adb forward tcp:31415 tcp:31415`
2. Ensure that the [drozer agent⁠](https://github.com/WithSecureLabs/drozer-agent/releases/) is running on the target device, and that the embedded server has been started.
3. Obtain a shell into the container: 
		`docker run --net host -it --entrypoint sh withsecurelabs/drozer`
1. Then run the drozer command to connect to the phone: 
		`drozer console connect --server localhost`
--------------------------------------------------------------------------


## Frida
--------------------------------------------------------------------------

>[!NOTE]
> *Prerequisites*:
> - python
> - Rooted Android device (for advanced functionality; non-rooted devices have limited capabilities).
> - USB debugging enabled on your Android device.
> - Android Debug Bridge (ADB) installed on your computer.
>


**Installation
- `pip install frida-tools`
- `frida --version`

> [!IMPORTANT]
> Download the appropriate frida-server binary from [here](https://github.com/frida/frida/releases) According to your Device CPU Architecture

- **Push the Frida Server to the Device:
	`adb push frida-server-<version>-android-<arch> /data/local/tmp/frida-server`
	
- **Set Permissions:**
	- make frida-server executable
	`adb shell "chmod +x /data/local/tmp/frida-server"`

- **Start the Frida server:
	`adb shell "/data/local/tmp/frida-server &"`

> [!tip]
> - Use `frida-ls-devices` to verify that the device is listed, If the device appears in the list, the setup is complete.

--------------------------------------------------------------------------
## Objection
--------------------------------------------------------------------------

**Objection** is a powerful, open-source tool designed for **mobile application penetration testing**. Built on top of **Frida**, it simplifies the process of runtime app manipulation, security testing, and debugging for Android and iOS applications. It allows security testers to bypass restrictions like SSL pinning, explore app internals, and identify vulnerabilities without needing root or jailbreak access in most cases.

**Installation 
	`pip3 install objection`. 

Upgrade existing Objection tool
	`pip3 install --upgrade objection`.

**Run:
	`objection <command>`

---

## JADX
---

### **JADX** - Dex to Java decompiler

Command line and GUI tools for producing Java source code from Android Dex and Apk files

>[!note]
>You can download the latest version of **JADX from [here](https://github.com/skylot/jadx/releases) and run the setup directly

---
## APKTool
---
A tool for reverse engineering Android apk files. Click Here to [Download](https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.10.0.jar) 

>[!IMPORTANT]
> *Prerequisites*:
> - Minimun JAVA 8 is required [link](https://www.java.com/en/download/)
> - Rename downloaded jar to `apktool.jar`.

Run Command:
	`java -jar apktool.jar <command>`
	
>[!NOTE]
> Make sure you run the command in terminal where the apktool.jar file is stored

---

## APKLeaks
---
**Installation 
	`pip3 install apkleaks`. 
	
**Usage 
	`apkleaks <command>`. 

---
## RMS
---
**Runtime Mobile Security (RMS)**, powered by [FRIDA](https://github.com/frida/frida), is a powerful web interface that helps you to manipulate **Android and iOS Apps** at Runtime. With RMS you can easily dump all loaded classes and relative methods, hook everything on the fly, trace methods args and return value, load custom scripts and many other useful stuff.

>[!IMPORTANT]
> Prerequisites
>1. [NodeJS](https://nodejs.org/en/download/prebuilt-installer) installed on your computer
>2. [FRIDA's CLI tools](https://frida.re/docs/installation/) installed on your computer
>3. **FRIDA server up and running** on the target device
>	- [Android - Official Tutorial](https://frida.re/docs/android/)
>	- [iOS - Official Tutorial](https://frida.re/docs/ios/)

### Installation

1. Open the terminal and run the following command to install the npm package
    - `npm install -g rms-runtime-mobile-security`
2. Make sure frida-server is up and running on the target device.
3. Launch RMS via the following command
    - `rms` (or `RMS-Runtime-Mobile-Security`)
4. Open your browser at `http://127.0.0.1:5491/`

---
## reFlutter
---

### Install

```
pipx install reflutter
```

### Usage

```
reflutter <apkfile.path>
```

---
