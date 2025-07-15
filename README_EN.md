# PDF to IMG Conversion Service

This Node.js project provides a simple HTTP interface to convert PDF files into PNG / JPG / JPEG images.

---

## 📤 Upload PDF

You can upload a PDF file via `curl` or tools like Postman:

### 🔁 Default Call (First Page, Default Sizes)

```bash
curl -X POST http://[IP / Address]:9820/upload -F "pdf=@./path/to/pdf/complete.pdf"
```

- ✅ **Only the first page** will be converted
- 📐 Image size: **1200 × 1600 px**
- 🔠 Quality (DPI): **200**
- 🎼 The image will always be **PNG** by default unless another format is specified via parameter

> 💡 For optimal readability, a quality of **150–200 DPI** is recommended.

---

## ⚙️ Parameter Overview

| Parameter | Description                | Default | Example  |
| --------- | -------------------------- | ------- | -------- |
| `s`       | Number of pages (max. 100) | `1`     | `s=3`    |
| `w`       | Image width in pixels      | `1200`  | `w=1000` |
| `h`       | Image height in pixels     | `1600`  | `h=1400` |
| `q`       | Quality (DPI / Density)    | `200`   | `q=150`  |
| `f`       | Format (png/jpg/jpeg)      | `png`   | `f=jpg`  |

---

### 📌 Example with Parameters

```bash
curl -X POST "http://[IP / Address]:9820/upload?s=3&w=1000&h=1400&q=150&f=jpg" -F "pdf=@./path/to/pdf/complete.pdf"
```

---

## 📥 Response Format

```json
{
  "status": "ok",
  "message": "PDF successfully converted to PNG",
  "duration_ms": 12345,
  "format": "jpg",
  "result": {
    "baseUrl": "http://[IP / Address]:9820/output/abc123/",
    "files": [
      "abc123.1.jpg",
      "abc123.2.jpg",
      "abc123.3.jpg"
    ],
    "files_url": [
      "http://[IP / Address]:9820/output/abc123/abc123.1.jpg",
      "http://[IP / Address]:9820/output/abc123/abc123.2.jpg",
      "http://[IP / Address]:9820/output/abc123/abc123.3.jpg"
    ]
  }
}
```

---

## 🗑️ Delete Images and PDF

Folders with converted images and the corresponding PDF in `uploads` can be deleted via the following endpoint:

```bash
curl -X DELETE http://[IP / Address]:9820/output/abc123
```

Success response:

```json
{
  "status": "ok",
  "message": "Folder and related PDF successfully deleted."
}
```

---

## 🔐 Tips

- A maximum of **100 pages** will be processed
- `uploads/` and `output/` folders are kept in the repository using `.gitkeep`
- You can optionally add API key protection
