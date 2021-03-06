---
description: Citrix Workspace for Linux
---

# Citrix

## 1. Download Citrix Workspace App 

{% embed url="https://www.citrix.com/ko-kr/downloads/workspace-app/linux/workspace-app-for-linux-latest.html" %}



I downloaded the following deb file, but you do you.

![](.gitbook/assets/image%20%283%29.png)

## 2. Add SSL Certificates

Try to run your ica file.

In my case, I encountered an error like this.

{% hint style="warning" %}
You have not chosen to trust "Entrust.net Certification Authority \(2048\)", the issuer of the server's security certificate \(SSL error 61\)
{% endhint %}

To solve this problem, I followed the guide \#5, \#6, \#9 from the page below.

{% embed url="https://help.ubuntu.com/community/CitrixICAClientHowTo" %}

In short, 

#### \#5. Add more SSL certificates

```text
sudo ln -s /usr/share/ca-certificates/mozilla/* /opt/Citrix/ICAClient/keystore/cacerts/
sudo c_rehash /opt/Citrix/ICAClient/keystore/cacerts/
```

#### \#6. Configure Citrix Receiver

```text
/opt/Citrix/ICAClient/util/configmgr &
```

#### \#9. Configure Chrome/Chromium

To use Citrix Receiver in Chrome and/or Chromium, run:

```text
xdg-mime default wfica.desktop application/x-ica
```



## NOTE

I installed libmotif-dev, but I'm not sure whether it is truely necessary.

```text
sudo apt-get install libmotif-dev
```



## References

{% embed url="https://help.ubuntu.com/community/CitrixXenAppPlugin" %}







