
### Table of Contents

1. [Overview](#overview)
2. [Installation](#installation)
3. [Setting Up Wallet](#setting-up-wallet)
4. [Using Walrus CLI](#using-walrus-cli)
5. [Storage Prices](#storage-prices)
6. [Reading Blobs](#reading-blobs)
7. [Reclaiming Space via Deletable Blobs](#reclaiming-space-via-deletable-blobs)
8. [Shared Blobs](#shared-blobs)
9. [Blob Objects and Blob ID Utilities](#blob-objects-and-blob-id-utilities)
10. [Blob Attributes](#blob-attributes)
11. [Security Considerations](#security-considerations)
12. [Best Practices](#best-practices)
13. [Troubleshooting](#troubleshooting)
14. [Conclusion](#conclusion)

---

## Overview

Walrus is an open-source blob storage protocol built on top of the Sui blockchain. It allows users to store, share, and manage files as permanent or deletable blobs. The protocol is decentralized, using Sui as the underlying blockchain for metadata storage and transaction processing.

---

## Installation

Walrus supports the following operating systems:

- Ubuntu (x86\_64)
- MacOS (Apple Silicon and Intel)
- Windows (x86\_64)

### Installing via Script (Linux & MacOS)

```sh
curl -sSf https://docs.wal.app/setup/walrus-install.sh | sh
```

### Installing on Windows

```powershell
(New-Object System.Net.WebClient).DownloadFile(
  "https://storage.googleapis.com/mysten-walrus-binaries/walrus-testnet-latest-windows-x86_64.exe",
  "walrus.exe"
)
```

---

## Setting Up Wallet

1. Install Sui CLI.
2. Configure a wallet pointing to the desired network (Mainnet or Testnet).

```sh
sui client envs
```

3. Make sure you have SUI tokens in your wallet.

---

## Using Walrus CLI

### Viewing Available Commands

```sh
walrus --help
```

### Viewing Price Information

```sh
walrus info price --context testnet
```

### Checking Blob Status

```sh
walrus blob-status --blob-id <BLOB_ID> --context testnet
```

### Uploading Files

```sh
walrus store <FILE>
```

---

## Storage Prices

- **1 WAL = 1,000,000,000 FROST**
- **Permanent Blob Storage** is calculated per epoch (\~24 hours)

Encoding Methods:

- **Reed-Solomon**: Cheaper for small blobs
- **RaptorQ**: Cheaper for large blobs

---

## Reading Blobs

```sh
walrus read <BLOB_ID> --out <OUTPUT_FILE>
```

- Outputs blob data to a file or standard output.

---

## Reclaiming Space via Deletable Blobs

### Creating Deletable Blobs

```sh
walrus store <FILE> --deletable
```

### Deleting Blobs

```sh
walrus delete --blob-id <BLOB_ID> --yes
```

---

## Shared Blobs

Shared blobs are publicly accessible and fundable by anyone.

### Creating a Shared Blob

```sh
walrus share --blob-obj-id <BLOB_OBJ_ID>
```

### Funding a Shared Blob

```sh
walrus fund-shared-blob --blob-id <BLOB_ID> --amount <AMOUNT>
```

### Extending a Shared Blob

```sh
walrus extend --blob-id <BLOB_ID> --amount <AMOUNT>
```

---

## Blob Objects and Blob ID Utilities

### Deriving Blob IDs

```sh
walrus blob-id <FILE>
```

### Listing Blobs

```sh
walrus list-blobs --include-expired
```

### Burning Blob Objects

```sh
walrus burn-blobs --object-ids <BLOB_OBJ_IDS>
```

---

## Blob Attributes

Blob attributes are key-value pairs associated with blob objects for metadata.

### Setting Attributes

```sh
walrus set-blob-attribute <BLOB_OBJ_ID> --attr "key1" "value1"
```

### Viewing Attributes

```sh
walrus get-blob-attribute <BLOB_OBJ_ID>
```

### Removing Attributes

```sh
walrus remove-blob-attribute-fields <BLOB_OBJ_ID> --keys "key1,key2"
```

### Removing All Attributes

```sh
walrus remove-blob-attribute <BLOB_OBJ_ID>
```

---

## Security Considerations

- All blobs are public and discoverable.
- Deleting a blob only reclaims space; copies may still exist in caches or other users' storage.
- Shared blobs can be funded by anyone, potentially altering their lifespan.

---

## Best Practices

- Always ensure your `client_config.yaml` is correctly configured.
- Use meaningful attributes for better organization of blobs.
- Regularly burn expired blob objects to reclaim storage.
- Monitor storage costs by checking prices periodically.

---

## Troubleshooting

- Ensure your Sui wallet is properly configured with sufficient SUI for gas fees.
- Check your configuration file path if you encounter errors.
- Ensure your commands target the correct context (Testnet or Mainnet).

---

## Conclusion

This document provides a comprehensive guide to using Walrus, including setting up, storing blobs, managing attributes, and reclaiming space. For more information, consult the official Walrus documentation or use the `--help` option within the CLI.

---

