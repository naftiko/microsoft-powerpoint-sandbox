# Microsoft PowerPoint Sandbox
This is sandbox for the Microsoft PowerPoint Sandbox API, using an OpenAPI specification with examples, Microcks and Bruno as the sandbox interface, and this GitHub repository as the vehicle for delivering as a localized sandbox, or also enabling the working directly with production APIs.

## APIs.json Index
There is an APIs.yml file in the root of this repository, providing an index of all the artifacts used as part of this capability, providing a machine-readable way to read, manage, and execute the resources available here.

## OpenAPI
This capability uses OpenAPI as the definition, providing a complete definition of all available paths for the Microsoft PowerPoint Sandbox. The OpenAPI for this capability uses examples and Microcks extensions to mock the requests and responses for each API operation, something we will iterate and expand upon with richer examples as the capability evolves.

## Microcks
This capability uses Microcks to deliver the mock API. [You just install Microcks, with the Docker extension being the easiest](https://microcks.io/documentation/guides/installation/docker-desktop-extension/), [import the OpenAPI as a service](openapi/notion-openapi.yml), and you have a mocked API for all APIs, available via REST and MCP APIs--providing a multi-protocol sandbox.

## Bruno
This capability [uses Bruno as the client](https://www.usebruno.com/), leveraging Bruno Collections pre-generated from the OpenAPI and Bruno environments that uses the localhost and port of Microcks to work with the mocked API. You just have to install Microcks, then open the collection provided in this repository, select the available environments, and begin calling the Microsoft PowerPoint Sandbox via the sandbox or production.


## OpenAPIs
These are the OpenAPIs available for the Microsoft PowerPoint Sandbox, which are made available via this sandbox API, which can be imported into Microcks and deployed as a sandbox using their mock feature.

  - [Microsoft Powerpoint Openapi.yaml](openapi/microsoft-powerpoint-openapi.yaml)

## Agent Skills
These are the agent skills available for the Microsoft PowerPoint Sandbox, providing a discrete list of capabilities that AI agents can use when working with Microsoft PowerPoint files via OneDrive and SharePoint. Each skill maps directly to an OpenAPI operation, making it easy for agents to discover and invoke the right capability for a given task.

### Uploads
  - [Upload PowerPoint File](skills/upload-file/SKILL.md) (`uploadFile`) — Upload or replace a PowerPoint presentation in OneDrive using a simple PUT request for files smaller than 4 MB.
  - [Create Upload Session](skills/create-upload-session/SKILL.md) (`createUploadSession`) — Initiate a resumable upload session for large PowerPoint files (greater than 4 MB) to enable reliable chunked byte-range transfers.
  - [Create File or Folder Entry](skills/create-child-item/SKILL.md) (`createChildItem`) — Create a new empty file placeholder or folder as a child item under a specified OneDrive parent folder.

### Content
  - [Download File Content](skills/get-file-content/SKILL.md) (`getFileContent`) — Download the binary content of a PowerPoint presentation, with optional server-side conversion to PDF, HTML, JPG, or PNG.

### Metadata
  - [Get File Metadata](skills/get-drive-item/SKILL.md) (`getDriveItem`) — Retrieve metadata for a specific PowerPoint file or folder by its OneDrive item ID, including name, size, timestamps, author, and download URL.
  - [Update File Metadata](skills/update-drive-item/SKILL.md) (`updateDriveItem`) — Update writable properties on a PowerPoint file such as its name, description, or parent folder location for moving.
  - [Delete File](skills/delete-drive-item/SKILL.md) (`deleteDriveItem`) — Soft-delete a PowerPoint file or folder by moving it to the OneDrive recycle bin, where it can be restored within the retention period.

### Permissions
  - [List File Permissions](skills/list-item-permissions/SKILL.md) (`listItemPermissions`) — Retrieve all sharing permissions currently applied to a PowerPoint file or folder, including roles for users, groups, and links.
  - [Get Specific Permission](skills/get-item-permission/SKILL.md) (`getItemPermission`) — Retrieve details for a single sharing permission on a PowerPoint file by its permission ID.
  - [Update Permission Role](skills/update-item-permission/SKILL.md) (`updateItemPermission`) — Change the role of an existing sharing permission, such as downgrading a collaborator from write to read access.
  - [Remove Permission](skills/delete-item-permission/SKILL.md) (`deleteItemPermission`) — Revoke a specific sharing permission from a PowerPoint file or folder by its permission ID.
  - [Share via Invitation](skills/invite-item-recipients/SKILL.md) (`inviteItemRecipients`) — Grant permissions and optionally send an email sharing invitation to specified recipients with configurable roles and sign-in requirements.
  - [Create Sharing Link](skills/create-sharing-link/SKILL.md) (`createSharingLink`) — Generate an anonymous or organizational sharing link for a PowerPoint file with configurable type, scope, optional password, and expiration date.

### Document Locks
  - [Check Out File](skills/checkout-item/SKILL.md) (`checkoutItem`) — Lock a PowerPoint presentation for exclusive editing by the current user, making it read-only for others until checked back in.
  - [Check In File](skills/checkin-item/SKILL.md) (`checkinItem`) — Release the exclusive lock on a checked-out PowerPoint file and optionally publish a new version with a descriptive comment.

### Search
  - [Search OneDrive](skills/search-drive-items/SKILL.md) (`searchDriveItems`) — Search file names, metadata, and indexed content within the signed-in user's OneDrive to find PowerPoint presentations.
  - [Search via Microsoft Search](skills/microsoft-search-query/SKILL.md) (`microsoftSearchQuery`) — Use the Microsoft Search API with KQL syntax to find PowerPoint files across OneDrive and all SharePoint sites the user has access to.

## Support
Please provide any questions or feedback via GitHub issues, or just email kinlane@naftiko.io with feedback. The goal is to keep iterating upon this sandboxes using existing OpenAPI, Microcks, and Bruno features, offering value out of the box via this forkable capability.

