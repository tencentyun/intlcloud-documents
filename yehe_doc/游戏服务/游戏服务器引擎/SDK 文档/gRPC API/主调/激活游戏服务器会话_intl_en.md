## API Name
ActivateGameServerSession
<span id="ActivateGameServerSession"></span>

## API Description

This API is used to tell GSE to activate the corresponding `GameServerSession` after the game process receives a callback from GSE through the [OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423) API.

## Request Message

```
message ActivateGameServerSessionRequest{
    string gameServerSessionId = 1;
    int32 maxPlayers = 2;
}
```

## Response Message

```
message GseResponse 
```

## Field Description

##### ActivateGameServerSessionRequest

| Field Name | Type | Description |
| ------------------- | ------ | ------------------------------------------------------------ |
| gameServerSessionId | string | `GameServerSessionId` which uniquely identifies a `GameServerSession` |
| maxPlayers          | int32  | Maximum number of players allowed to join this `GameServerSession`                               |

## Sample

For examples, see the [OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423) API.
