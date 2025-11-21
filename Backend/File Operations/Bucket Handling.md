# Bucket Operations

This document outlines all bucket-related operations available in the SDK.

## Overview

Bucket operations allow you to create, manage, list, and delete storage containers for your files.

---

## Create Bucket

Creates a new storage bucket.

### Method
```javascript
await twinProtocol.createBucket(bucketName)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketName` | string | Yes | The name of the bucket to create |

### Returns

```javascript
{
  success: boolean,
  bucket: string,
  message: string
}
```

### Example

```javascript
try {
  const result = await twinProtocol.createBucket("my-storage-bucket");
  console.log(result);
  // {
  //   success: true,
  //   bucket: "my-storage-bucket",
  //   message: "Bucket created successfully"
  // }
} catch (error) {
  console.error("Failed to create bucket:", error);
}
```

### Errors

- `400 Bad Request` - Invalid bucket name format
- `409 Conflict` - Bucket already exists
- `500 Internal Server Error` - Server error

---

## List Buckets

Retrieves all buckets associated with your account.

### Method
```javascript
await twinProtocol.listBuckets()
```

### Parameters

None

### Returns

```javascript
{
  success: boolean,
  count: number,
  buckets: Array<{
    name: string,
    createdAt: Date
  }>
}
```

### Example

```javascript
try {
  const result = await twinProtocol.listBuckets();
  console.log(result);
  // {
  //   success: true,
  //   count: 3,
  //   buckets: [
  //     {
  //       name: "bucket-1",
  //       createdAt: "2024-01-15T10:30:00Z"
  //     },
  //     {
  //       name: "bucket-2",
  //       createdAt: "2024-01-16T14:45:00Z"
  //     }
  //   ]
  // }
} catch (error) {
  console.error("Failed to list buckets:", error);
}
```

### Errors

- `500 Internal Server Error` - Server error

---

## Delete Bucket

Removes a bucket from your account.

### Method
```javascript
await client.deleteBucket(bucketName)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketName` | string | Yes | The name of the bucket to delete |

### Returns

```javascript
{
  success: boolean,
  bucket: string,
  message: string
}
```

### Example

```javascript
try {
  const result = await client.deleteBucket("old-bucket");
  console.log(result);
  // {
  //   success: true,
  //   bucket: "old-bucket",
  //   message: "Bucket deleted successfully"
  // }
} catch (error) {
  console.error("Failed to delete bucket:", error);
}
```

### Errors

- `400 Bad Request` - Invalid bucket name
- `404 Not Found` - Bucket does not exist
- `500 Internal Server Error` - Server error

---

## Check Bucket Existence

Verifies whether a bucket exists in your account.

### Method
```javascript
await client.bucketExists(bucketName)
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketName` | string | Yes | The name of the bucket to check |

### Returns

```javascript
boolean
```

### Example

```javascript
try {
  const exists = await client.bucketExists("my-storage-bucket");
  
  if (exists) {
    console.log("Bucket exists");
  } else {
    console.log("Bucket does not exist");
  }
} catch (error) {
  console.error("Failed to check bucket:", error);
}
```

### Errors

- `400 Bad Request` - Invalid bucket name
- `500 Internal Server Error` - Server error

---

## Best Practices

- **Bucket Naming**: Use lowercase letters, numbers, and hyphens. Avoid special characters.
- **Error Handling**: Always wrap bucket operations in try-catch blocks.
- **Idempotency**: Creating a bucket that already exists returns success without duplicating.
- **Cleanup**: Remember to delete unused buckets to maintain account hygiene.