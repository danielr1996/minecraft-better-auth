# minecraft-better-auth

Better authentication for minecraft

## Limits of the official authentication system
- central auth server controlled by mojang
- changing accounts required restart of the game (and launcher)
- multiple accounts require multiple copies of minecraft (at least I think so)
- only a single "character" per account, meaning you can not login with different users (e.g. for creative/survival or starting a new journey a few thousand blocks away while still keeping the old player)

## Goals
### Compatibility
- luckperms
- oauth/oidc
- custom yggdrasil implementations (e.g. unmojang/drasl)
- online-mode=true
- minecraft EULA (https://github.com/unmojang/drasl/issues/106)

### Features
- Allow creating multiple characters on e.g. account
- Allow multiple users per mojang account
- Manage permissions with oauth/oidc, e.g. group membership defines op, allowed gamemodes etc
- Change account/character in game without restarting the client
- Don't require a custom launcher

## Technical Architecture 
### Server plugin
- After a player joined disable all actions
- check if a record for the player exists in the persistent store and if
  - :=true sync the roles from oidc with the permission system
  - :=false prompt the user to sign in and if the sign request
    - := true enable all movement and sync the roles with the permission system
    - := false restart the flow or kick the player

### Client Plugin
