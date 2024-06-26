# Endpoints

Located at `https://gateway.filen.io`

Requests to the API that need authentication carry the API Key (from `/v3/login`) as `Authorization: Bearer <...>`.

Responses from the API look like this:
```typescript
type ApiResponse {
    status: boolean,
    message: string,
    code: string,
    data: any
}
```


## POST `/v3/auth/info`

Request:
```typescript
{
    email: string
}
```

Result `ApiResponse.data`:
```typescript
{
    email: string,
    authVersion: number,
    salt: string,
    id: number
}
```


## POST `/v3/login`

Request:
``` typescript
{
    email: string,
    password: string,
    twoFactorCode: string, // one-time code or recovery code, or 'XXXXXX' if 2FA is disabled
    authVersion: 2
}
```

Result `ApiResponse.data`:
```typescript
{
    apiKey: string,
    masterKeys: string,
    publicKey: string,
    privateKey: string
}
```


## GET `/v3/user/baseFolder`

Response `ApiResponse.data`:
```typescript
{
    uuid: string
}
```


## POST `/v3/dir/content`

Request:
```typescript
{
    uuid: string,
    foldersOnly: boolean | undefined
}
```

Response `ApiResponse.data`:
```typescript
{
    uploads: {
        uuid: string
        metadata: string
        rm: string
        timestamp: number
        chunks: number
        size: number
        bucket: string
        region: string
        parent: string
        version: FileEncryptionVersion
        favorited: 0 | 1
    }[],
    folders: {
        uuid: string
        name: string
        parent: string
        color: DirColors
        timestamp: number
        favorited: 0 | 1
        is_sync: 0 | 1
        is_default: 0 | 1
    }[]
}
```

# Types

```typescript
type FileEncryptionVersion = 1 | 2
```