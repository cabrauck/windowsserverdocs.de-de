---
title: Informationen zur dumpverschlüsselung
description: Beschreibt das Verschlüsseln von Dumpdateien und die Problembehandlung bei der Verschlüsselung.
ms.prod: windows-server
manager: dongill
ms.topic: article
author: larsiwer
ms.asset: b78ab493-e7c3-41f5-ab36-29397f086f32
ms.author: kathydav
ms.date: 11/03/2016
ms.openlocfilehash: e1e374a75c11321820393bede83ca9ea225f5424
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392815"
---
# <a name="about-dump-encryption"></a>Informationen zur dumpverschlüsselung
Die dumpverschlüsselung kann verwendet werden, um Absturz Abbilder und Live Abbilder zu verschlüsseln, die für ein System generiert werden. Die Abbilder werden mit einem symmetrischen Verschlüsselungsschlüssel verschlüsselt, der für jedes Abbild generiert wird. Dieser Schlüssel selbst wird dann mit dem öffentlichen Schlüssel verschlüsselt, der vom vertrauenswürdigen Administrator des Hosts angegeben wird (Schutzvorrichtung für Absturz Abbild Verschlüsselung). Dadurch wird sichergestellt, dass nur jemand, der über den entsprechenden privaten Schlüssel verfügt, den Inhalt des Abbilds entschlüsseln und somit darauf zugreifen kann Diese Funktion wird in einem geschützten Fabric genutzt.
Hinweis: Wenn Sie die dumpverschlüsselung konfigurieren, deaktivieren Sie auch Windows-Fehlerberichterstattung. Wer kann verschlüsselte Absturz Abbilder nicht lesen.

# <a name="configuring-dump-encryption"></a>Konfigurieren der dumpverschlüsselung
## <a name="manual-configuration"></a>Manuelle Konfiguration
Um die dumpverschlüsselung mithilfe der Registrierung zu aktivieren, konfigurieren Sie die folgenden Registrierungs Werte unter`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl`

| Wertname | Typ | Wert |
| ---------- | ---- | ----- |
| Dumpverschlüsselungsfähig | DWORD | 1 zum Aktivieren der dumpverschlüsselung, 0 zum Deaktivieren der dumpverschlüsselung |
| Verschlüsselungcertificates\certificate1::P ublickey | Binär | Öffentlicher Schlüssel (RSA, 2048 Bit), der zum Verschlüsseln von Dumps verwendet werden soll. Dies muss als [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)formatiert werden. |
| "Verschlüsselungcertificates\certificate1:: Thumbprint" | Zeichenfolge | Zertifikat Fingerabdruck, um die automatische Suche nach privatem Schlüssel im lokalen Zertifikat Speicher zuzulassen, wenn ein Absturz Abbild entschlüsselt wird. |


## <a name="configuration-using-script"></a>Konfiguration mithilfe eines Skripts
Um die Konfiguration zu vereinfachen, ist ein [Beispielskript](https://github.com/Microsoft/Virtualization-Documentation/tree/live/hyperv-tools/DumpEncryption) verfügbar, das die Verschlüsselung auf der Grundlage eines öffentlichen Schlüssels aus einem Zertifikat ermöglicht.

1. In einer vertrauenswürdigen Umgebung: Erstellen Sie ein Zertifikat mit einem 2048-Bit-RSA-Schlüssel, und exportieren Sie das öffentliche Zertifikat
2. Auf Zielhosts: Importieren des öffentlichen Zertifikats in den lokalen Zertifikat Speicher
3. Ausführen des Beispiel Konfigurations Skripts 
    ```
    .\Set-DumpEncryptionConfiguration.ps1 -Certificate (Cert:\CurrentUser\My\093568AB328DF385544FAFD57EE53D73EFAAF519) -Force
    ```

# <a name="decrypting-encrypted-dumps"></a>Entschlüsseln verschlüsselter Abbilder
Zum Entschlüsseln einer vorhandenen verschlüsselten Dumpdatei müssen Sie die Debugtools für Windows herunterladen und installieren. Diese toolmenge enthält "kerneldumpentschlüsseln. exe", mit dem eine verschlüsselte Dumpdatei entschlüsselt werden kann.
Wenn das Zertifikat mit dem privaten Schlüssel im Zertifikat Speicher des aktuellen Benutzers vorhanden ist, kann die Dumpdatei durch Aufrufen von entschlüsselt werden.

```
    KernelDumpDecrypt.exe memory.dmp memory_decr.dmp
```
Nach der Entschlüsselung können Tools wie WinDBG die entschlüsselte Dumpdatei öffnen.

# <a name="troubleshooting-dump-encryption"></a>Fehlerbehebung
Wenn die dumpverschlüsselung auf einem System aktiviert ist, aber keine Abbilder generiert werden, überprüfen Sie das `System` Ereignisprotokoll des `Kernel-IO` Systems auf das Ereignis 1207. Wenn die dumpverschlüsselung nicht initialisiert werden kann, wird dieses Ereignis erstellt und Abbilder deaktiviert.

| Ausführliche Fehlermeldung | Auszumindern Schritte |
| ---------------------- | ----------------- |
| Der öffentliche Schlüssel oder die Fingerabdruck Registrierung fehlt. | Überprüfen Sie, ob beide Registrierungs Werte am erwarteten Speicherort vorhanden sind. |
| Ungültiger öffentlicher Schlüssel | Stellen Sie sicher, dass der öffentliche Schlüssel, der im Registrierungs Wert PublicKey gespeichert ist, als [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)gespeichert wird. |
| Nicht unterstützte Größe des öffentlichen Schlüssels | Derzeit werden nur 2048-Bit-RSA-Schlüssel unterstützt. Konfigurieren Sie einen Schlüssel, der dieser Anforderung entspricht. |

Überprüfen Sie auch, `GuardedHost` ob `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled` der Wert unter auf einen anderen Wert als 0 festgelegt ist. Dadurch werden Absturz Abbilder vollständig deaktiviert. Wenn dies der Fall ist, legen Sie den Wert auf 0 fest.
