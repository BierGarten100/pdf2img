# PDF zu IMG Konvertierungs-Service

Dieses Node.js-Projekt bietet eine einfache HTTP-Schnittstelle zur Konvertierung von PDF-Dateien in PNG / JPG / JPEG-Bilder.

---

## 📤 PDF hochladen

Die PDF-Datei kann per `curl` oder Tools wie Postman gesendet werden:

### 🔁 Standardaufruf (1. Seite, Standardgrößen)

```bash
curl -X POST http://[IP / Adresse]:9820/upload -F "pdf=@./pfad/zur/pdf/complete.pdf"
```

- ✅ Es wird **nur die erste Seite** konvertiert
- 📐 Bildgröße: **1200 × 1600 px**
- 🖨️ Qualität (DPI): **200**
- 🖼️ Das Bild wird standardmäßig immer **PNG** sein außer anders angegeben als Parameter

> 💡 Für gute Lesbarkeit wird eine Qualität von **150–200 DPI** empfohlen.

---

## ⚙️ Parameterübersicht

| Parameter | Beschreibung               | Standard | Beispiel     |
|-----------|----------------------------|----------|--------------|
| `s`       | Seitenanzahl (max. 100)    | `1`      | `s=3`        |
| `w`       | Bildbreite in Pixel        | `1200`   | `w=1000`     |
| `h`       | Bildhöhe in Pixel          | `1600`   | `h=1400`     |
| `q`       | Qualität (DPI / Density)   | `200`    | `q=150`      |
| `f`       | Format   (png/jpg/jpeg)    | `png`    | `f=jpg`      |

---

### 📌 Beispiel mit Parametern

```bash
curl -X POST "http://[IP / Adresse]:9820/upload?s=3&w=1000&h=1400&q=150&f=jpg" -F "pdf=@./pfad/zur/pdf/complete.pdf"
```

---

## 📥 Rückgabeformat

```json
{
  "status": "ok",
  "message": "PDF erfolgreich in PNG konvertiert",
  "duration_ms": 12345,
  "format": "jpg",
  "result": {
    "baseUrl": "http://[IP / Adresse]:9820/output/abc123/",
    "files": [
      "abc123.1.jpg",
      "abc123.2.jpg",
      "abc123.3.jpg"
    ],
    "files_url": [
      "http://[IP / Adresse]:9820/output/abc123/abc123.1.jpg",
      "http://[IP / Adresse]:9820/output/abc123/abc123.2.jpg",
      "http://[IP / Adresse]:9820/output/abc123/abc123.3.jpg"
    ]
  }
}
```

---

## 🗑️ Bilder und PDF löschen

Verzeichnisse mit konvertierten Bildern und die dazugehörige PDF in `uploads` können über den folgenden Endpunkt gelöscht werden:

```bash
curl -X DELETE http://[IP / Adresse]:9820/output/abc123
```

Antwort bei Erfolg:

```json
{
  "status": "ok",
  "message": "Ordner und zugehörige PDF erfolgreich gelöscht."
}
```

---

## 🔐 Tipps

- Es werden maximal **100 Seiten** verarbeitet
- `uploads/` und `output/` bleiben dank `.gitkeep` im Repository
- Du kannst optional einen API-Key-Schutz einbauen
