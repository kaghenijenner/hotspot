## Set Member Login as Default

Edit login.html at line 14 to:

```
<body onload="member();">
```

## Auto Lowercase Input for Voucher and Member Mode

Edit login.html from line 120 to 148, change:

```
// set password = username
function setpass(){
  var user = username.value
  password.value = user;
}
username.onkeyup = setpass;
// change to voucher mode
function voucher(){
  username.focus();
  username.onkeyup = setpass;
  username.placeholder = "Kode Voucher";
  username.style = "border-radius:3px;"
  password.type = "hidden";
  infologin.innerHTML  = "Masukkan Kode Voucher kemudian klik login.";
}
// change to member mode
function member(){
  username.focus();
  username.onkeyup = "";
  username.placeholder = "Username";
  username.style = "border-radius:3px 3px 0px 0px;"
  password.type = "password";
  infologin.innerHTML  = "Masukkan Username dan Password kemudian klik login.";
}
//-->


```

to:

```
//set lowercase
function setlower(){
var cekMode = password.type;
if (cekMode === "hidden"){
  var user = username.value
  user = user.toLowerCase();
  username.value = user;
  password.value = user;
} else if (cekMode === "password"){
  var user = username.value
  user = user.toLowerCase();
  username.value = user;
}
}

username.onkeyup = setlower;

// change to voucher mode
function voucher(){
  username.focus();
  username.placeholder = "Voucher Code";
  username.style = "border-radius:3px;"
  password.type = "hidden";
  password.value = username.value;
  infologin.innerHTML  = "Enter your Voucher Code then click login.";
}

// change to member mode
function member(){
  username.focus();
  username.placeholder = "Username";
  username.style = "border-radius:3px 3px 0px 0px;"
  password.type= "password";
  password.value = "";
  infologin.innerHTML  = "Enter your Username and Password then click login.";
}
//-->

```

## QR Code Scanner Feature

To use the QR CODE SCANNER feature, add the following script to MikroTik via Terminal:

```
/ip hotspot walled-garden ip

add action=accept comment="Mikhmon QR Code Scanner" disabled=no dst-host=laksa19.github.io

```

Enable HTTP PAP in the hotspot server profile.
