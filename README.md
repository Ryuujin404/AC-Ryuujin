# 🛡️ AC-Ryuujin Anti-Cheat

**Language / Bahasa:**  
[🇮🇩 Indonesia](#indonesia) | [🇬🇧 English](#english)

---

<a id="indonesia"></a>

## 🇮🇩 Indonesia

### 📦 Pemasangan

1. Masukkan file `AC-Ryuujin.amx` ke dalam folder `filterscripts`.
2. Buka file `server.cfg`, lalu di bagian `filterscripts` tambahkan `AC-Ryuujin` di paling akhir (setelah semua filterscript lainnya).
   ```
   filterscripts file1 file2 AC-Ryuujin
   ```
3. Periksa kembali apakah penulisannya sudah benar.
4. Jalankan server, lalu cek file `server_log.txt` untuk memastikan anti-cheat sudah ter-load dengan benar.
5. Cek juga di dalam game untuk memastikan anti-cheat aktif.

---

### ⚙️ Konfigurasi

**[1] Jetpack**

Agar staff server tidak terdeteksi saat menggunakan jetpack, tambahkan code berikut **SEBELUM** memberikan jetpack kepada player:

```pawn
SetPVarInt(playerid, "Ryuujin-Jetpack", 1);
```

**[2] CMD Admin**

Agar staff server tidak terdeteksi cheat saat menggunakan cmd, seperti `/goto`, `/gotodoor`, dll, tambahkan code berikut ke cmd admin:

```pawn
SetPVarInt(playerid, "Ryuujin-CmdAdmin", 1);
```

---

### 📝 Contoh Pemasangan Jetpack

```pawn
CMD:jetpack(playerid, params[])
{
    // Cek apakah player adalah admin (sesuaikan dengan sistem admin kamu)
    if(!IsPlayerAdmin(playerid))
        return SendClientMessage(playerid, 0xFF0000FF, "[ERROR] Kamu tidak memiliki izin untuk menggunakan command ini.");

    // Set PVar bypass SEBELUM memberikan jetpack
    SetPVarInt(playerid, "Ryuujin-Jetpack", 1);

    // Berikan jetpack ke player
    SetPlayerSpecialAction(playerid, SPECIAL_ACTION_USEJETPACK);

    SendClientMessage(playerid, 0x00FF00FF, "[INFO] Jetpack diaktifkan.");
    return 1;
}
```

> ⚠️ **CATATAN PENTING:** `SetPVarInt "Ryuujin-Jetpack"` WAJIB dipasang sebelum `SetPlayerSpecialAction` jetpack diberikan.

---

### 📝 Contoh Pemasangan CMD Admin

```pawn
CMD:goto(playerid, params[])
{
    if (AccountData[playerid][pAdmin] < 1 && !AccountData[playerid][pSteward])
        return PermissionError(playerid);

    new otherid;
    if (sscanf(params, "d", otherid))
        return SUM(playerid, "/goto [playerid]");

    if (!IsPlayerConnected(otherid))
        return ShowTDN(playerid, NOTIFICATION_ERROR, "Pemain tersebut tidak terkoneksi ke server!");

    SetPVarInt(playerid, "Ryuujin-CmdAdmin", 1);

    static string[144];
    SendPlayerToPlayer(playerid, otherid);
    format(string, sizeof(string), "AdmCmd: %s teleported to your position.", AccountData[playerid][pAdminname]);
    SendClientMessage(otherid, Y_LIGHTRED, string);

    return 1;
}
```

> ⚠️ **CATATAN PENTING:** `SetPVarInt(playerid, "Ryuujin-CmdAdmin", 1);` WAJIB dipasang sebelum player teleport ke tempat tersebut.

---

### 📌 Catatan

- Jika ada request fitur anti-cheat baru, silakan PM **Ryuujin**. Permintaan akan dimasukkan ke dalam daftar antrian pengembangan.
- **Feedback WAJIB diberikan.** Tanpa feedback, bantuan tidak akan diberikan.

---

<a id="english"></a>

## 🇬🇧 English

### 📦 Installation

1. Place the `AC-Ryuujin.amx` file inside the `filterscripts` folder.
2. Open `server.cfg` and in the `filterscripts` line, add `AC-Ryuujin` at the very end (after all other filterscripts).
   ```
   filterscripts file1 file2 AC-Ryuujin
   ```
3. Double-check that the entry is written correctly.
4. Start the server and check `server_log.txt` to verify the anti-cheat has loaded successfully.
5. Also verify in-game that the anti-cheat is active.

---

### ⚙️ Configuration

**[1] Anti Jetpack**

To prevent staff from being flagged while using a jetpack, add the following line **BEFORE** giving the jetpack to the player:

```pawn
SetPVarInt(playerid, "Ryuujin-Jetpack", 1);
```

**[2] CMD Admin**

To prevent staff from being flagged while using admin commands such as `/goto`, `/gotodoor`, etc., add the following line inside the admin command:

```pawn
SetPVarInt(playerid, "Ryuujin-CmdAdmin", 1);
```

**[3] Anti Fake Spawn**

To prevent fake spawns, add the following line inside your player login dialog or spawn script, right **AFTER** the player successfully spawns:

```pawn
SetPVarInt(playerid, "Ryuujin-Spawned", 1);
```

---

### 📝 Usage Example — Jetpack

```pawn
CMD:jetpack(playerid, params[])
{
    // Check if the player is an admin (adjust to your admin system)
    if(!IsPlayerAdmin(playerid))
        return SendClientMessage(playerid, 0xFF0000FF, "[ERROR] You do not have permission to use this command.");

    // Set the bypass PVar BEFORE giving the jetpack
    SetPVarInt(playerid, "Ryuujin-Jetpack", 1);

    // Give the player a jetpack
    SetPlayerSpecialAction(playerid, SPECIAL_ACTION_USEJETPACK);

    SendClientMessage(playerid, 0x00FF00FF, "[INFO] Jetpack activated.");
    return 1;
}
```

> ⚠️ **IMPORTANT:** `SetPVarInt "Ryuujin-Jetpack"` MUST be set before `SetPlayerSpecialAction` jetpack is called.

---

### 📝 Usage Example — CMD Admin

```pawn
CMD:goto(playerid, params[])
{
    if (AccountData[playerid][pAdmin] < 1 && !AccountData[playerid][pSteward])
        return PermissionError(playerid);

    new otherid;
    if (sscanf(params, "d", otherid))
        return SUM(playerid, "/goto [playerid]");

    if (!IsPlayerConnected(otherid))
        return ShowTDN(playerid, NOTIFICATION_ERROR, "That player is not connected to the server!");

    SetPVarInt(playerid, "Ryuujin-CmdAdmin", 1);

    static string[144];
    SendPlayerToPlayer(playerid, otherid);
    format(string, sizeof(string), "AdmCmd: %s teleported to your position.", AccountData[playerid][pAdminname]);
    SendClientMessage(otherid, Y_LIGHTRED, string);

    return 1;
}
```

> ⚠️ **IMPORTANT:** `SetPVarInt(playerid, "Ryuujin-CmdAdmin", 1);` MUST be set before the player is teleported to the destination.

---

### 📌 Notes

- If you have a feature request for the anti-cheat, please PM **Ryuujin**. Requests will be added to the development queue.
- **Feedback is MANDATORY.** Without feedback, support will not be provided.
