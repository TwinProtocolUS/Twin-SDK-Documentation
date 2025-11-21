# File Operations

This document outlines all file-related operations available in the SDK.

## Overview

File operations allow you to upload, download, manage, and track files stored in your buckets. Additionally, you can generate presigned URLs for direct uploads and access files via IPFS/CID.

---

## Upload File

Uploads a file to a specified bucket.

### Method
```javascript
await twinProtocol.uploadFile(formData)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `formData` | FormData | Yes | Form data containing the file and bucket information |

**FormData Properties:**
- `file` (File): The file to upload
- `bucket` (string): Target bucket name

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    success: boolean,
    bucket: string,
    fileKey: string,
    fileName: string,
    fileSize: number,
    url: string,
    etag: string,
    cid: string,
    contentHash: string,
    ipfsUrl: string | null
  }
}
```

### Example

```javascript
try {
  const formData = new FormData();
  formData.append("file", fileInput.files[0]);
  formData.append("bucket", "my-bucket");
  
  const result = await twinProtocol.uploadFile(formData);
  console.log(result);
  // {
  //   success: true,
  //   message: "File uploaded successfully",
  //   data: {
  //     success: true,
  //     bucket: "my-bucket",
  //     fileKey: "uploads/document-abc123.pdf",
  //     fileName: "document.pdf",
  //     fileSize: 2048576,
  //     url: "https://gateway.example.com/my-bucket/uploads/document-abc123.pdf",
  //     etag: "\"abc123def456\"",
  //     cid: "QmXxxx...",
  //     contentHash: "sha256-hash...",
  //     ipfsUrl: "https://ipfs.example.com/QmXxxx..."
  //   }
  // }
} catch (error) {
  console.error("Upload failed:", error);
}
```

### Errors

- `400 Bad Request` - Invalid bucket or file
- `413 Payload Too Large` - File exceeds size limit
- `500 Internal Server Error` - Server error

---

## Download File

Downloads a file from a specified bucket. Returns the file data as base64-encoded string.

### Method
```javascript
await twinProtocol.downloadFile(bucket, url)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucket` | string | Yes | The bucket containing the file |
| `url` | string | Yes | The file URL |

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    bucket: string,
    fileKey: string,
    contentType: string,
    size: number,
    etag: string,
    lastModified: Date,
    metadata: object,
    cid: string | null,
    originalFileName: string,
    buffer: string (base64)
  }
}
```

### Example

```javascript
try {
  const result = await twinProtocol.downloadFile(
    "my-bucket",
    "https://gateway.example.com/my-bucket/uploads/document-abc123.pdf"
  );
  
  console.log(result);
  // {
  //   success: true,
  //   message: "File retrieved successfully",
  //   data: {
  //     bucket: "my-bucket",
  //     fileKey: "uploads/document-abc123.pdf",
  //     contentType: "application/pdf",
  //     size: 2048576,
  //     etag: "\"abc123def456\"",
  //     lastModified: "2024-01-15T10:30:00Z",
  //     metadata: {},
  //     cid: "QmXxxx...",
  //     originalFileName: "document.pdf",
  //     buffer: "JVBERi0xLjQKJeLj..."
  //   }
  // }
} catch (error) {
  console.error("Download failed:", error);
}
```

### Errors

- `400 Bad Request` - Invalid URL or bucket mismatch
- `404 Not Found` - File not found
- `500 Internal Server Error` - Server error

---

## Get File Metadata

Retrieves metadata information for a file without downloading its content.

### Method
```javascript
await twinProtocol.getFileMetadata(bucket, url)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucket` | string | Yes | The bucket containing the file |
| `url` | string | Yes | The file URL |

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    success: boolean,
    bucket: string,
    fileKey: string,
    contentType: string,
    size: number,
    lastModified: Date,
    etag: string,
    cid: string | null,
    ipfsUrl: string | null,
    metadata: object,
    originalFileName: string,
    contentHash: string
  }
}
```

### Example

```javascript
try {
  const metadata = await twinProtocol.getFileMetadata(
    "my-bucket",
    "https://gateway.example.com/my-bucket/uploads/document-abc123.pdf"
  );
  
  console.log(metadata);
  // {
  //   success: true,
  //   message: "File metadata retrieved successfully",
  //   data: {
  //     success: true,
  //     bucket: "my-bucket",
  //     fileKey: "uploads/document-abc123.pdf",
  //     contentType: "application/pdf",
  //     size: 2048576,
  //     etag: "\"abc123def456\"",
  //     cid: "QmXxxx...",
  //     ipfsUrl: "https://ipfs.example.com/QmXxxx...",
  //     metadata: {},
  //     originalFileName: "document.pdf",
  //     contentHash: "sha256-hash..."
  //   }
  // }
} catch (error) {
  console.error("Failed to get metadata:", error);
}
```

### Errors

- `400 Bad Request` - Invalid URL or bucket mismatch
- `404 Not Found` - File not found
- `500 Internal Server Error` - Server error

---

## Check File Existence

Verifies whether a file exists in a bucket.

### Method
```javascript
await twinProtocol.fileExists(bucket, url)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucket` | string | Yes | The bucket to search |
| `url` | string | Yes | The file URL |

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    exists: boolean
  }
}
```

### Example

```javascript
try {
  const result = await twinProtocol.fileExists(
    "my-bucket",
    "https://gateway.example.com/my-bucket/uploads/document-abc123.pdf"
  );
  
  if (result.data.exists) {
    console.log("File exists");
  } else {
    console.log("File does not exist");
  }
} catch (error) {
  console.error("Check failed:", error);
}
```

### Errors

- `400 Bad Request` - Invalid URL or bucket mismatch
- `500 Internal Server Error` - Server error

---

## Delete File

Removes a file from a bucket.

### Method
```javascript
await twinProtocol.deleteFile(bucket, url)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucket` | string | Yes | The bucket containing the file |
| `url` | string | Yes | The file URL |

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    success: boolean,
    bucket: string,
    fileKey: string,
    message: string
  }
}
```

### Example

```javascript
try {
  const result = await twinProtocol.deleteFile(
    "my-bucket",
    "https://gateway.example.com/my-bucket/uploads/document-abc123.pdf"
  );
  
  console.log(result);
  // {
  //   success: true,
  //   message: "File deleted successfully",
  //   data: {
  //     success: true,
  //     bucket: "my-bucket",
  //     fileKey: "uploads/document-abc123.pdf",
  //     message: "File deleted successfully"
  //   }
  // }
} catch (error) {
  console.error("Delete failed:", error);
}
```

### Errors

- `400 Bad Request` - Invalid URL or bucket mismatch
- `404 Not Found` - File not found
- `500 Internal Server Error` - Server error

---

## Generate Presigned Upload URL

Creates a presigned URL for direct file uploads without routing through your server.

### Method
```javascript
await twinProtocol.generatePresignedUploadUrl(bucket, fileMetadata)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucket` | string | Yes | Target bucket name |
| `fileMetadata` | object | Yes | File metadata object |

**fileMetadata Properties:**
- `fileName` (string): Name of the file to upload
- `fileType` (string): MIME type of the file
- `fileSize` (number): Size of the file in bytes

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    url: string,
    filekey: string
  }
}
```

### Example

```javascript
try {
  const metadata = {
    fileName: "report.pdf",
    fileType: "application/pdf",
    fileSize: 2048576
  };
  
  const result = await twinProtocol.generatePresignedUploadUrl("my-bucket", metadata);
  console.log(result);
  // {
  //   success: true,
  //   message: "Presigned URL generated successfully",
  //   data: {
  //     url: "https://gateway.example.com/my-bucket?...",
  //     filekey: "uploads/report-abc123.pdf"
  //   }
  // }
  
  // Now upload directly using the URL
  const response = await fetch(result.data.url, {
    method: "PUT",
    body: fileData,
    headers: { "Content-Type": metadata.fileType }
  });
} catch (error) {
  console.error("Failed to generate presigned URL:", error);
}
```

### Errors

- `400 Bad Request` - Invalid file type or size exceeds 1GB limit
- `500 Internal Server Error` - Server error

### Supported File Types

Documents, images, videos, audio, archives, web files, and data formats including: PDF, Word, Excel, PowerPoint, images (JPEG, PNG, GIF, WebP, SVG, BMP, TIFF), video formats (MP4, WebM, AVI, MOV, MKV), audio formats (MP3, WAV, OGG, M4A), archives (ZIP, RAR, 7Z, TAR, GZIP), web files (HTML, CSS, JS, JSON, XML), and CSV/SQL files.

---

## List All Files

Retrieves a list of all files in a bucket with optional prefix filtering.

### Method
```javascript
await twinProtocol.listAllFiles(bucket, prefix)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucket` | string | Yes | The bucket to list files from |
| `prefix` | string | No | Filter files by key prefix (e.g., "uploads/") |

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    success: boolean,
    bucket: string,
    files: Array<{
      key: string,
      size: number,
      lastModified: Date,
      etag: string,
      url: string
    }>,
    count: number
  }
}
```

### Example

```javascript
try {
  // List all files
  const result = await twinProtocol.listAllFiles("my-bucket");
  console.log(result);
  
  // List files with specific prefix
  const filtered = await twinProtocol.listAllFiles("my-bucket", "uploads/");
  console.log(filtered);
  // {
  //   success: true,
  //   message: "Files listed successfully",
  //   data: {
  //     success: true,
  //     bucket: "my-bucket",
  //     count: 2,
  //     files: [
  //       {
  //         key: "uploads/document-abc123.pdf",
  //         size: 2048576,
  //         lastModified: "2024-01-15T10:30:00Z",
  //         etag: "\"abc123def456\"",
  //         url: "https://gateway.example.com/my-bucket/uploads/document-abc123.pdf"
  //       }
  //     ]
  //   }
  // }
} catch (error) {
  console.error("List failed:", error);
}
```

### Errors

- `400 Bad Request` - Invalid bucket
- `500 Internal Server Error` - Server error

---

## Get File by CID

Retrieves a file using its Content Identifier (CID) from IPFS.

### Method
```javascript
await twinProtocol.getFileByCID(bucket, cid)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucket` | string | Yes | The bucket containing the file |
| `cid` | string | Yes | The IPFS Content Identifier |

### Returns

```javascript
Buffer
```

### Example

```javascript
try {
  const fileBuffer = await twinProtocol.getFileByCID("my-bucket", "QmXxxx...");
  
  // Save or process the file
  console.log("File retrieved:", fileBuffer);
} catch (error) {
  console.error("Failed to retrieve file:", error);
}
```

### Errors

- `400 Bad Request` - Missing CID or invalid bucket
- `404 Not Found` - File with CID not found
- `500 Internal Server Error` - Server error

---

## Get CID URL

Generates a gateway URL for accessing a file via its CID.

### Method
```javascript
await twinProtocol.getCIDUrl(cid)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cid` | string | Yes | The IPFS Content Identifier |

### Returns

```javascript
{
  success: boolean,
  message: string,
  data: {
    cid: string,
    url: string
  }
}
```

### Example

```javascript
try {
  const result = await twinProtocol.getCIDUrl("QmXxxx...");
  console.log(result);
  // {
  //   success: true,
  //   message: "CID URL generated successfully",
  //   data: {
  //     cid: "QmXxxx...",
  //     url: "https://ipfs.example.com/QmXxxx..."
  //   }
  // }
  
  // Use the URL to access the file
  window.open(result.data.url);
} catch (error) {
  console.error("Failed to generate CID URL:", error);
}
```

### Errors

- `400 Bad Request` - CID is required
- `500 Internal Server Error` - Server error

---

## Best Practices

- **Error Handling**: Always wrap file operations in try-catch blocks.
- **File Size**: Keep individual files under 1GB for optimal performance.
- **Presigned URLs**: Use presigned URLs for large files to bypass server intermediaries.
- **Metadata**: Leverage file metadata to track file properties and versions.
- **IPFS**: Use CID-based access for distributed and decentralized file retrieval
- **Batch Operations**: When listing files, consider using prefix filtering for large buckets.