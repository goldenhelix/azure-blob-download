# Azure Blob Storage Download Tasks

This repository contains Golden Helix server tasks for automating file downloads from Azure Blob Storage.

## Prerequisites

- Access to Azure Portal
- Azure Storage Account with appropriate permissions
- Valid SAS URL for the target blob storage container

## Setup Instructions

### 1. Get Azure Blob Storage SAS URL

To get the SAS URL for Azure Blob Storage, follow these steps:

1. Go to the Azure Portal and navigate to your Storage Account
2. Select the container you want to access
3. In the left menu, click on Settings > Shared access tokens
4. Configure the following settings:
   - Signing method: use Account key (default)
   - Signing key: Choose Key 1 or Key 2 as needed
   - Stored access policy: None (unless you have a policy)
   - Permissions: Select at least Read and List (and others as needed)
   - Start and expiry date/time: Set the appropriate window for access
   - Allowed IP addresses: (Optional) Restrict access to specific IPs if desired
   - Allowed protocols: Select HTTPS only for security
5. Click the Generate SAS token and URL button at the bottom
6. Copy the Blob SAS URL that is generated. This will be used as the `sas_url` parameter in the task

Note: The SAS URL provides temporary, restricted access to your blob storage. Make sure to set an appropriate expiration time and permissions for your use case.

## Tasks

The repository contains the following task, which can be run in the Golden Helix server:

### Download Azure Blob Storage Files (`azure_blob_download.task.yaml`)

Downloads files from Azure Blob Storage using rclone.

Parameters:
- `sas_url`: Azure Blob Storage SAS URL (secret)
- `base_path`: Base path in the container (optional, format: "container/folder/subfolder/...")
- `output_directory`: Directory where files will be downloaded
- `dry_run`: List files only without downloading (default: false)

## Notes

- The task uses rclone for efficient file transfers
- The task requires minimal resources (1 CPU core, 1GB memory)
- Make sure the SAS URL has appropriate permissions and hasn't expired
- The base path parameter is optional - if not specified, files will be downloaded from the root of the container
- Use dry run mode to preview which files will be downloaded before actually downloading them
