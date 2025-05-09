# CivitAI REST API Reference

> Source: https://github.com/civitai/civitai/wiki/REST-API-Reference (retrieved May 9, 2025)

---

# Introduction
This article describes how to use the Civitai REST API. We are going to be describing the HTTP method, path, and parameters for every operation. The API will return the response status code, response headers, and a response body.

> This is still in active development and will be updated once more endpoints are made available for the public.

## Civitai API v1

### Authorization
To make authorized requests as a user you must use an API Key. You can generate an API Key from your [User Account Settings](https://civitai.com/user/account).

Once you have an API Key you can authenticate with either an Authorization Header or Query String.

Creators can require that people be logged in to download their resources. That is an option we provide but not something we require – it's entirely up to the resource owner.

Please see [the Guide to Downloading via API](https://education.civitai.com/civitais-guide-to-downloading-via-api/) for more details and open an issue if you are still having trouble downloading.

#### Authorization Header
You can pass the API token as a Bearer token using the `Authorization` header:

```
GET https://civitai.com/api/v1/models
Content-Type: application/json
Authorization: Bearer {api_key}
```

#### Query String
You can pass the API token as a query parameter using the `?token=` parameter:

```
GET https://civitai.com/api/v1/models?token={api_key}
Content-Type: application/json
```

---

# Endpoints

## Creators
### GET /api/v1/creators
- **Endpoint URL:** `https://civitai.com/api/v1/creators`
- **Query Parameters:**
  - `limit` (number, optional): Number of results per page (0-200, default 20, 0 = all)
  - `page` (number, optional): Page number
  - `query` (string, optional): Filter by username
- **Response Fields:**
  - `username` (string)
  - `modelCount` (number)
  - `link` (string)
  - `metadata.totalItems`, `metadata.currentPage`, `metadata.pageSize`, `metadata.totalPages`, `metadata.nextPage`, `metadata.prevPage`
- **Example:**
```json
{
  "items": [
    { "username": "Civitai", "modelCount": 848, "link": "https://civitai.com/api/v1/models?username=Civitai" },
    ...
  ],
  "metadata": {
    "totalItems": 46,
    "currentPage": 1,
    "pageSize": 3,
    "totalPages": 16,
    "nextPage": "https://civitai.com/api/v1/creators?limit=3&page=2"
  }
}
```

## Images
### GET /api/v1/images
- **Endpoint URL:** `https://civitai.com/api/v1/images`
- **Query Parameters:**
  - `limit` (number, optional): Results per page (0-200, default 100)
  - `postId`, `modelId`, `modelVersionId` (number, optional): Filter by post/model/version
  - `username` (string, optional): Filter by user
  - `nsfw` (boolean, optional): Filter by NSFW level
  - `sort` (enum, optional): Most Reactions, Most Comments, Newest
  - `period` (enum, optional): AllTime, Year, Month, Week, Day
  - `page` (number, optional): Page number
- **Response Fields:**
  - `id`, `url`, `hash`, `width`, `height`, `nsfw`, `nsfwLevel`, `createdAt`, `postId`, `stats.*`, `meta`, `username`, `metadata.*`
- **Example:**
```json
{
  "items": [
    { "id": 123, "url": "...", ... }
  ],
  "metadata": {
    "nextCursor": 456,
    "currentPage": 1,
    "pageSize": 1,
    "nextPage": "https://civitai.com/api/v1/images?limit=1&page=2"
  }
}
```

## Models
### GET /api/v1/models
- **Endpoint URL:** `https://civitai.com/api/v1/models`
- **Query Parameters:**
  - `limit` (number, optional): 1-100, default 100
  - `page` (number, optional)
  - `query`, `tag`, `username` (string, optional)
  - `types` (enum[], optional): Checkpoint, TextualInversion, Hypernetwork, etc.
  - `sort` (enum, optional): Highest Rated, Most Downloaded, Newest
  - `period` (enum, optional): AllTime, Year, Month, Week, Day
  - `favorites`, `hidden`, `primaryFileOnly`, `allowNoCredit`, `allowDerivatives`, `allowDifferentLicenses`, `nsfw`, `supportsGeneration` (various, optional)
- **Response Fields:**
  - `id`, `name`, `description`, `type`, `nsfw`, `tags`, `mode`, `creator.*`, `stats.*`, `modelVersions.*`, `metadata.*`
- **Example:**
```json
{
  "items": [
    { "id": 1102, "name": "...", ... }
  ],
  "metadata": {
    "totalItems": 3,
    "currentPage": 1,
    "pageSize": 3,
    "totalPages": 1
  }
}
```

### GET /api/v1/models/:modelId
- **Endpoint URL:** `https://civitai.com/api/v1/models/:modelId`
- **Response Fields:**
  - Same as above, but for a single model
- **Example:**
```json
{
  "id": 1102,
  "name": "...",
  "modelVersions": [ ... ]
}
```

### GET /api/v1/model-versions/:modelVersionId
- **Endpoint URL:** `https://civitai.com/api/v1/model-versions/:id`
- **Response Fields:**
  - `id`, `name`, `description`, `model.*`, `modelId`, `createdAt`, `downloadUrl`, `trainedWords`, `files.*`, `stats.*`, `images.*`
- **Example:**
```json
{
  "id": 1318,
  "name": "...",
  "model": { "name": "..." },
  "downloadUrl": "...",
  "images": [ ... ]
}
```

### GET /api/v1/model-versions/by-hash/:hash
- **Endpoint URL:** `https://civitai.com/api/v1/model-versions/by-hash/:hash`
- **Response Fields:**
  - Same as standard model-versions endpoint

## Tags
### GET /api/v1/tags
- **Endpoint URL:** `https://civitai.com/api/v1/tags`
- **Query Parameters:**
  - `limit` (number, optional): 1-200, default 20, 0 = all
  - `page` (number, optional)
  - `query` (string, optional)
- **Response Fields:**
  - `name`, `modelCount`, `link`, `metadata.*`
- **Example:**
```json
{
  "items": [
    { "name": "Pepe Larraz", "modelCount": 1, "link": "https://civitai.com/api/v1/models?tag=Pepe Larraz" },
    ...
  ],
  "metadata": {
    "totalItems": 200,
    "currentPage": 1,
    "pageSize": 3,
    "totalPages": 67,
    "nextPage": "https://civitai.com/api/v1/tags?limit=3&page=2"
  }
}
```

---

# Notes
- The download url uses a `content-disposition` header to set the filename correctly. Be sure to enable that header when fetching the download.
- If the creator of the asset requires authentication, you will need an API Key to download it.
- Paging and cursor-based pagination are both supported; use `metadata.nextPage` for next page of results.
- See the [official wiki](https://github.com/civitai/civitai/wiki/REST-API-Reference) for the most up-to-date details.

---

# Additional Links
- [REST API Reference](https://github.com/civitai/civitai/wiki/REST-API-Reference)
- [Guide to Downloading via API](https://education.civitai.com/civitais-guide-to-downloading-via-api/)
- [Civitai Home](https://civitai.com/)
